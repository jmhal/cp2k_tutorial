# Compilar CP2K

Vamos agora para a parte principal, compilar o CP2K com as dependências já configuradas.

```
$ source cp2k_tutorial/environment.sh
$ cd cp2k_tutorial/sources
$ git clone https://github.com/cp2k/cp2k.git
$ cd cp2k/cp2k/
$ cd arch
$ cp Linux-x86-64-gfortran.popt cp2k_tutorial.popt
```

Na pasta *arch*, temos vários arquivos de configuração para a compilação. Nós vamos usar o arquivo *Linux-x86-64-gfortran.popt* e adaptá-lo para nossa instalação. Ele é baseado em um sistema Linux 64 _bits_ com o compilador *gfortran*, que é o compilador Fortran que acompanha o gcc. A extensão *popt* significa que vamos construir uma versão paralela com suporte ao MPI. A versão serial seria *sopt*.

O conteúdo de *cp2k_tutorial.popt* deve ficar assim:

```
# Tested with: GFortran 6.4, MPICH 3.2, LAPACK 3.5.0, ScaLAPACK 2.0.2
CC         = gcc
CPP        =
FC         = mpif90
LD         = mpif90
AR         = ar -r
FFTW_INC   = /home/usuario/cp2k_tutorial/install/fftw-3.3.6/include/ 
FFTW_LIB   = /home/usuario/cp2k_tutorial/install/fftw-3.3.6/lib
LIBINT_INC = /home/usuario/cp2k_tutorial/install/libint-1.1.4/include/
LIBINT_LIB = /home/usuario/cp2k_tutorial/install/libint-1.1.4/lib/
LIBXC_INC  = /home/usuario/cp2k_tutorial/install/libxc-2.2.2/include/
LIBXC_LIB  = /home/usuario/cp2k_tutorial/install/libxc-2.2.2/lib
DFLAGS     = -D__FFTW3 -D__LIBINT -D__LIBXC -D__MPI_VERSION=3\
             -D__LIBINT_MAX_AM=7 -D__LIBDERIV_MAX_AM1=6 -D__MAX_CONTR=4\
             -D__parallel -D__SCALAPACK
CPPFLAGS   =
FCFLAGS    = $(DFLAGS) -O2 -ffast-math -ffree-form -ffree-line-length-none\
             -ftree-vectorize -funroll-loops\
             -mtune=native\
             -I$(FFTW_INC) -I$(LIBINT_INC) -I$(LIBXC_INC)
LDFLAGS    = $(FCFLAGS)
LIBS       = /home/usuario/cp2k_tutorial/install/scalapack/libscalapack.a\
             /home/usuario/cp2k_tutorial/install/lapack/liblapack-gnu.a\
             /home/usuario/cp2k_tutorial/install/lapack/libblas-gnu.a\
             /home/usuario/cp2k_tutorial/install/fftw-3.3.6/lib/libfftw3.a\
             /home/usuario/cp2k_tutorial/install/libxc-2.2.2/lib/libxcf90.a\
             /home/usuario/cp2k_tutorial/install/libxc-2.2.2/lib/libxc.a\
             /home/usuario/cp2k_tutorial/install/libint-1.1.4/lib/libderiv.a\
             /home/usuario/cp2k_tutorial/install/libint-1.1.4/lib/libint.a
```

Veja que o que fizemos foi simplesmente atualizar as variáveis com a localização das bibliotecas estáticas. Também incluimos os caminhos para os cabeçalhos, que são os diretórios *include* de cada biblioteca.Para finalizar, devemos continuar atuando no diretório *makefiles*: 


```
$ cd /home/usuario/cp2k_install/sources/cp2k/cp2k/makefiles
$ make ARCH=cp2k_tutorial VERSION=popt
```

Após um longo processo de compilação, teremos na pasta *cp2k_tutorial/sources/cp2k/cp2k/exe/cp2k_tutorial* os binários do cp2k. Podemos agora movê-los para uma pasta adequada:

```
$ mkdir cp2k_tutorial/install/cp2k
$ cp cp2k_tutorial/sources/cp2k/cp2k/exe/cp2k_tutorial/* cp2k_tutorial/install/cp2k/
```

Podemos adicionar o diretório no *.bashrc* do usuário ou continuar adicionar a atualização das variáveis de ambiente no arquivo *cp2k_tutorial/environment.sh*:

```
# CP2K
export PATH=/home/usuario/cp2k_tutorial/install/cp2k:$PATH
```

Vamos validar a instalação executando uma simulação:

```
$ wget https://www.cp2k.org/_media/static_calculation.tgz
$ tar -xzvf static_calculation.tgz 
$ cd static_calculation/sample_output_with_smearing/
$ rm Si_bulk8.out Si_bulk8-RESTART.wfn 
$ mpirun -n 2 cp2k.popt -o Si_bulk8.out Si_bulk8.inp
```

Se não surgir nenhuma mensagem de erro e o arquivo *Si_bulk8.out* for gerado novamente, então a configuração está correta.
