# Compilar Libxc

Sem muito drama.

```
$ source cp2k_tutorial/environment.sh
$ cd cp2k_tutorial/sources
$ wget http://www.tddft.org/programs/octopus/down.php?file=libxc/libxc-2.2.2.tar.gz (aqui você pode ter que renomear o arquivo)
$ tar -xzvf libxc-2.2.2.tar.gz 
$ cd libxc-2.2.2/
$ mkdir /home/usuario/cp2k_tutorial/install/libxc-2.2.2
$ ./configure --prefix=/home/usuario/cp2k_tutorial/install/libxc-2.2.2
$ make
$ make install
```
