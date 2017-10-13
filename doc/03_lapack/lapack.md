# LAPACK

A LAPACK e sua versão paralela (SCALAPACK) são muito utilizadas em vários programas científicos. Aqui, nós vamos compilá-las com o GCC 5.3.0 e o OpenMPI 1.10.1 das seções anteriores. No LAPACK, está inclusa tammbém a biblioteca BLAS.

## Compilar LAPACK:

```
$ source cp2k_tutorial/environment.sh
$ cd cp2k_tutorial/sources
$ git clone https://github.com/reference-lapack/lapack
$ cd lapack
$ cp make.inc.example make.inc
$ make
$ mkdir /home/usuario/cp2k_tutorial/install/lapack
$ cp *.a /home/usuario/cp2k_tutorial/install/lapack/
```

## Compilar SCALAPACK

```
$ source cp2k_tutorial/environment.sh
$ cd cp2k_tutorial/sources
$ wget http://www.netlib.org/scalapack/scalapack-2.0.2.tgz
$ tar -xzvf scalapack-2.0.2.tgz
$ cd scalapack-2.0.2/
$ cp SLmake.inc.example SLmake.inc
```

Neste ponto, devemos fazer uma atualização no arquivo _SLmake.inc_ para apontar as bibliotecas LAPACK/BLAS. No lugar de:

```
BLASLIB       = -lblas
LAPACKLIB     = -llapack
LIBS          = $(LAPACKLIB) $(BLASLIB)

```

Coloque:

```
BLASLIB       = /home/usuario/cp2k_tutorial/install/lapack/librefblas.a
LAPACKLIB     = /home/usuario/cp2k_tutorial/install/lapack/liblapack.a
LIBS          = $(LAPACKLIB) $(BLASLIB)

```

Podemos continuar agora:

```
$ make
$ mkdir /home/usuario/cp2k_tutorial/install/scalapack
$ cp libscalapack.a /home/usuario/cp2k_tutorial/install/scalapack
```

Com isso terminamos a compilação dessas bibliotecas para ligação estática (arquivo *.a*). Seria possivel criá-las para ligação dinâmica (arquivos *.so*), mas como são muito usadas e de tamanho pequeno, optamos pela opção estática.
