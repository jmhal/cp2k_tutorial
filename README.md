# Instalação do CP2K

O objetivo deste guia é estabelecer passo-a-passo a instalação do _software_ [CP2K](https://www.cp2k.org/). É um pacote de simulação da química, mas sua função não importa. O que estamos atrás é de familiarizar o leitor com o processo de compilação de programas científicos em C/C++/Fortran com suporte ao MPI e bibliotecas auxiliares.

## Ambiente

Vamos considerar que qualquer distribuição Linux com um compilador GCC presente seja capaz de servir como base para para os passos aqui descritos. Entretanto, irei testar inicialmente no Ubuntu 16.04.

Onde for lido */home/usuario*, considere o diretório do usuário. Neste diretório, crie um subdiretório chamado *cp2k_tutorial* e dentro dele os diretórios *install* e *sources*. Em *install* vamos instalar os programas e bibliotecas, geralmente indicando através do parâmetro *--prefix*. Já em *sources* vamos baixar os códigos fonte e fazer as compilações.

Dentro do diretório *cp2k_tutorial*, o arquivo a ser criado *environment.sh* conterá os comandos para atualizar as variáveis de ambiente a medida que os pacotes forem instalados. Basicamente, as variáveis atualizadas são _PATH_ e *LD_LIBRARY_PATH*. A primeira variável indica onde o *bash* deve procurar por executáveis. A segunda indica onde o *ld* deve procurar bibliotecas para ligação.

## Etapas

As seguintes etapas são necessárias: 

1. [Compilação e instalação do GCC 5.3.0](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/01_gcc)

   O objetivo é ter uma versão fixa do GCC, nem tão nova e nem tão velha. A idade mediana garante a maior compatibilidade. A versão padrão do Ubuntu seria suficiente, mas vamos aproveitar o tutorial para aprender a compilar uma versão do GCC.

2. [Compilação e instalação do OpenMPI 1.10.1](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/02_openmpi)

   Novamente, poderíamos usar a versão da distribuição, mas vamos praticar a configuração do MPI também.

3. [Biblioteca LAPACK](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/03_lapack)

   É uma biblioteca de rotinas matemáticas bastante utilizada. Inclue a BLAS, sendo que nesta etapa também vamos compilar a SCALAPACK para permitir o uso do MPI.

4. [Biblioteca FFTW](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/04_fftw)
  
   É uma biblioteca de rotinas matemáticas para a transformada de _fourier_.

5. [Biblioteca Libxc](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/05_libxc)

   Já neste caso, é uma biblioteca utilizada pelo CP2K que não é muito comum em outros pacotes.

6. [Biblioteca Libint](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/06_libint)
   
   Mesmo cenário da Libxc.

7. [CP2k](https://github.com/jmhal/cp2k_tutorial/tree/master/doc/07_cp2k)
   
   Passo final, a compilação do programa em si.

