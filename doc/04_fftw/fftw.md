# Compilar FFTW

Como é um *software* recente, a compilação do FFTW é bem simples, basta seguir os passos abaixo.

```
$ source cp2k_tutorial/environment.sh
$ cd cp2k_tutorial/sources
$ wget http://www.fftw.org/fftw-3.3.6-pl2.tar.gz
$ tar -xzvf fftw-3.3.6-pl2.tar.gz 
$ cd fftw-3.3.6-pl2/
$ mkdir /home/usuario/cp2k_tutorial/install/fftw-3.3.6
$ ./configure --prefix=/home/usuario/cp2k_tutorial/install/fftw-3.3.6
$ make
$ make install
```

Assim como no caso da LAPACK/SCALAPACK, não atualizamos a variável LD_LIBRARY_PATH mesmo a *fftw* sendo uma biblioteca que possibilite ligação dinâmica. Para simplificar, na compilação do *cp2k* vamos informar a localização das bibliotecas estáticas no arquivo de configuração.
