# Compilar Libint

Bem simples também.

```
$ source cp2k_tutorial/environment.sh
$ cd cp2k_tutorial/sources
$ wget --no-check-certificate https://downloads.sourceforge.net/project/libint/v1-releases/libint-1.1.4.tar.gz?r=&ts=1507680819&use_mirror=ufpr (talvez precise renomear o arquivo)
$ tar -xzvf libint-1.1.4.tar.gz 
$ cd libint-1.1.4/
$ mkdir /home/usuario/cp2k_tutorial/install/libint-1.1.4
$ ./configure --prefix=/home/usuario/cp2k_tutorial/install/libint-1.1.4
$ make
$ make install
```

