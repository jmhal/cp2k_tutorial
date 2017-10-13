# OpenMPI

O OpenMPI é a biblioteca de comunicação entre processos usada em computação paralela. Não vamos explicar como configurar um _cluster_, apenas como compilar a biblioteca e ferramentas para construção de programas. Em outras palavras, todos os processos vão executar localmente.

```
$ cd cp2k_install/sources
$ source ../environment.sh 
$ wget https://www.open-mpi.org//software/ompi/v1.10/downloads/openmpi-1.10.1.tar.bz2
$ mkdir ../install/openmpi-1.10.1
$ tar -xjvf openmpi-1.10.1.tar.bz2 
$ cd openmpi-1.10.1/
$ ./configure --prefix=/home/usuario/cp2k_tutorial/install/openmpi-1.10.1
$ make
$ make install
```

No passo da execução do _script configure_, informamos apenas o local da instalação através do parâmetro *--prefix*. Entretanto, instalações mais complexas podem existir mais informações. Por exemplo, caso o OpenMPI for interagir com o gerenciador SLURM, precisamos informar também o parâmetro *--with-slurm*. Mais opções pode ser vistas executando o _script_ informando apenas o parâmetro *--help*.

Adicione as seguintes linhas ao arquivo *cp2k_tutorial/environment.sh*:

```
# OpenMPI
MPI_HOME=/home/usuario/cp2k_tutorial/install/openmpi-1.10.1
export PATH=$MPI_HOME/bin:$PATH
export LD_LIBRARY_PATH=$MPI_HOME/lib:$LD_LIBRARY_PATH
export MANPATH=$MPI_HOME/share/man/:$MANPATH

export OMPI_MCA_btl_vader_single_copy_mechanism=none
export OMPI_MCA_btl_sm_use_knem=0

```

Para verificar se a instalação está correta, abra um novo terminal e execute `source cp2k_tutorial/environment.sh`. Em seguida, execute `mpicc --version`. Deve aparecer a versão 5.3.0 do GCC.
