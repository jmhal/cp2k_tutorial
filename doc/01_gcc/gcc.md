# Compilação e instalação do GCC 5.3.0

Primeiro vamos baixar os fontes. Você pode tentar usar versões mais recentes da bibliotecas, mas com estas garanto funcionar.

```
$ cd cp2k_tutorial/sources
$ wget ftp://gcc.gnu.org/pub/gcc/releases/gcc-4.9.4/gcc-4.9.4.tar.bz2
$ wget ftp://gcc.gnu.org/pub/gcc/infrastructure/gmp-6.1.0.tar.bz2
$ wget ftp://gcc.gnu.org/pub/gcc/infrastructure/mpfr-3.1.4.tar.bz2
$ wget ftp://gcc.gnu.org/pub/gcc/infrastructure/mpc-1.0.3.tar.gz
$ wget ftp://gcc.gnu.org/pub/gcc/infrastructure/isl-0.18.tar.bz2
```

## Compilando a biblioteca GMP

Execute os seguintes passos para compilar:

```
$ cd cp2k_tutorial/sources
$ mkdir ../install/gmp-6.1.0
$ tar -xjvf gmp-6.1.0.tar.bz2
$ cd gmp-6.1.0
$ ./configure --prefix=/home/usuario/cp2k_tutorial/install/gmp-6.1.0 (adapte o caminho de acordo seu usuário)
$ make
$ make install
```

Adicione as seguintes linhas ao arquivo *cp2k_tutorial/environment.sh*:

```
# GMP
export LD_LIBRARY_PATH=/home/usuario/cp2k_tutorial/install/gmp-6.1.0/lib:$LD_LIBRARY_PATH
```

## Compilando a biblioteca MPFR

Execute os seguintes passos para compilar:

```
$ cd cp2k_tutorial/sources
$ mkdir ../install/mpfr-3.1.4
$ tar -xjvf mpfr-3.1.4.tar.bz2 
$ cd mpfr-3.1.4/
$ ./configure --with-gmp=/home/usuario/cp2k_tutorial/install/gmp-6.1.0 --prefix=/home/usuario/cp2k_tutorial/install/mpfr-3.1.4
$ make
$ make install
```

Adicione as seguintes linhas ao arquivo *cp2k_tutorial/environment.sh*:

```
# MPFR 
export LD_LIBRARY_PATH=/home/usuario/cp2k_tutorial/install/mpfr-3.1.4/lib:$LD_LIBRARY_PATH
```

## Compilando a biblioteca MPC

Execute os seguintes passos para compilar:

```
$ cd cp2k_tutorial/sources
$ mkdir ../install/mpc-1.0.3
$ tar -xzvf mpc-1.0.3.tar.gz 
$ cd mpc-1.0.3/
$ ./configure --with-mpfr=/home/usuario/cp2k_tutorial/install/mpfr-3.1.4 --with-gmp=/home/usuario/cp2k_tutorial/install/gmp-6.1.0 --prefix=/home/usuario/cp2k_tutorial/install/mpc-1.0.3 --enable-languages=c,c++,fortran --disable-multilib
$ make
$ make install
```

Adicione as seguintes linhas ao arquivo *cp2k_tutorial/environment.sh*:

```
# MPC
export LD_LIBRARY_PATH=/home/usuario/cp2k_tutorial/install/mpc-1.0.3/lib:$LD_LIBRARY_PATH
```

## Compilando o GCC:

Execute os seguintes passos para compilar:

```
$ cd cp2k_tutorial/sources
$ tar -xjvf gcc-5.3.0.tar.bz2 
$ mkdir gcc_build
$ mkdir ../install/gcc-5.3.0
$ cd gcc_build/
$ ../gcc-4.9.4/configure --prefix=/home/usuario/cp2k_tutorial/install/gcc \
--with-gmp=/home/usuario/cp2k_tutorialinstall/gmp-6.1.0 \
--with-mpfr=/home/usuario/cp2k_tutorial/install/mpfr-3.1.4 \
--with-mpc=/home/usuario/cp2k_tutorial/install/mpc-1.0.3 \
--enable-languages=c,c++,fortran \
--disable-multilib
$ make (demora um bom tempo)
$ make install
```

Adicione as seguintes linhas ao arquivo *cp2k_tutorial/environment.sh*:

```
# GCC 5.3.0
export GNU_PATH=/home/usuario/cp2k_tutorial/install/gcc-5.3.0/
export PATH=$GNU_PATH/bin:$PATH
export LD_LIBRARY_PATH=$GNU_PATH/lib:$GNU_PATH/lib64:$LD_LIBRARY_PATH
export MANPATH=$GNU_PATH/share/man:$MANPATH
```

## Validando a Instalação

Primeiro, devemos carregar as variáveis de ambiente. Para isso, executamos `source /home/usuario/cp2k_tutorial/environment.sh`.Para validar, vamos executar o comando `gcc --version`. Se aparecer a versão como 5.3.0, a compilação foi bem sucedida. O próximo passo é o OpenMPI.
