# Instalação do CP2K

O objetivo deste guia é estabelecer passo-a-passo a instalação do _software_ [CP2K](https://www.cp2k.org/). É um pacote de simulação da química, mas sua função não importa. O que estamos atrás é de familiarizar o leitor com o processo de compilação de programas científicos em C/C++/Fortran com suporte ao MPI e bibliotecas auxiliares.

## Ambiente

Vamos considerar que qualquer distribuição Linux com um compilador GCC presente seja capaz de servir como base para para os passos aqui descritos. Entretanto, irei testar inicialmente no Ubuntu 16.04.

## Etapas

As seguintes etapas são necessárias: 

1. Compilação e instalação do GCC 5.3.0

   O objetivo é ter uma versão fixa do GCC, nem tão nova e nem tão velha. A idade mediana garante a maior compatibilidade. A versão padrão do Ubuntu seria suficiente, mas vamos aproveitar o tutorial para aprender a compilar uma versão do GCC.

2. Compilação e instalação do OpenMPI 1.10.1

   Novamente, poderíamos usar a versão da distribuição, mas vamos praticar a configuração do MPI também.

3. Biblioteca LAPACK

   É uma biblioteca de rotinas matemáticas bastante utilizada. Inclue a BLAS, sendo que nesta etapa também vamos compilar a SCALAPACK para permitir o uso do MPI.

4. Biblioteca FFTW
  
   É uma biblioteca de rotinas matemáticas para a transformada de _fourier_.

5. Biblioteca Libxc

   Já neste caso, é uma biblioteca utilizada pelo CP2K que não é muito comum em outros pacotes.

6. Biblioteca Libint
   
   Mesmo cenário da Libxc.

7. CP2k
   
   Passo final, a compilação do programa em si.

Para este tutorial, dentro do diretório principal *cp2k_tutorial* na pasta do usuário (ou qualquer outro lugar que desejar), crio um diretório _install_ e outro _sources_. No primeiro vão ficar os binários, enquando no segundo vamos fazer a compilação.  Dentro da pasta de cada etapa, existem os passos necessários para o requisito.

