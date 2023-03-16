# Encriptação

## Introdução

Este projeto é uma introdução a Segurança de Informações, disciplina
muito relevante no contexto de Sistemas de Programação. Para entender
corretamente o que deve ser feito deve-se entender quais os princípios e
processos utilizados para proteger arquivos num computador, que serão
será aprofundados na disciplina "Segurança da Informação".

## Base de Segurança

É muito importante que haja maneiras de proteger os arquivos e
mensagens de uma máquina para que não possam ser vistos por pessoa
indesejadas quando acessarem essa máquina ou captarem a mensagem sendo
transmitida pela rede. Existem diversas formas e técnicas para garantir
uma comunicação segura entre as partes com maiores e menores
complexidades e garantias de segurança e outras características.

Para realizar todo tipo de cifração, são precisas chaves criptográficas,
que permitem variabilidade entre as cifrações feitas por diferentes
pessoas. Quando há uma única chave no processo, ambas as partes da
comunicação devem conhecê-la e a cifração é chamada simétrica. Quando há
duas chaves, uma delas é conhecida por todos na rede, chamada chave
pública, e a outra apenas pelo transmissor, chamada chave privada, e a
cifração é chamada assimétrica.

Uma cifra simétrica muito simples é a *RC4*, que considera uma chave
vetorial com alguns elementos. Para implementá-la, primeiro é
inicializado um vetor pseudo-aleatório $S$ com um tamanho padrão de
elementos, que será o tamanho de mensagem que será cifrada por vez. Para
tal, define-se $S$ como um vetor identidade (ou seja $[1,2,3,\cdots]$) e
uma variável $j=0$ e, em seguida, para cada índice $i$ de $S$
redefine-se $j=(j+S[i]+chave[i\%len(chave)])\%len(S)$ e troca-se o valor
de $S[i]$ com $S[j]$. Para realizar a cifração, segmenta-se a mensagem a
ser cifrada, $M$, em pedaços de tamanho igual a $S$ e, para cada índice
$k$ de segmentos de $M$, realiza-se novamente a operação sobre $j$
assumindo $i=k$ e o segmento de mensagem cifrado $M'_k=M_k \oplus S$. A
decifração pode ser feita pelo mesmo processo, já que a operação de ou
exclusivo é auto-inversa.

## O que será fornecido

Para a execução do trabalho, é necessário que hajam funções de operações
lógicas sobre os bits de números armazenados. Por isso é fornecido na
própria implementação da MVN um método de realizar esse tipo de cálculo
utilizando a função `OS`. O tipo de operação é determinado pelo valor do
acumulador: `0x0` para operação NOT, `0x1` para AND, `0x2` para OR e `0x3`
para XOR. A menos da operação NOT, que recebe 1 argumento, todas estas
operações recebem dois argumentos e o resultado é colocado no acumulador.
Com essas funções, todos os métodos de criptografia podem ser implementados.

## O trabalho

O trabalho consiste na implementação de um encriptador de arquivos de
forma a aumentar a segurança dos arquivos armazenados e enviados por
rede.

Deve ser codificado um algoritmo que leia dados de um arquivo de
entrada, chamado `file.txt`, e gere um arquivo de saída, chamado
`file_enc.txt`, com o resultado da aplicação de uma cifra simétrica
(não necessariamente a RC4 que foi mostrada). Seu código deve ser capaz
de realizar tanto encriptação do arquivo quanto decriptação dele, então
escolher uma cifra que faça as duas coisas por um mesmo processo pode
ser mais fácil.

O trabalho pode ser feito em duplas ou individualmente. Definir escopo
de uso do encriptador, mensagens de erro coerentes, eventuais limitações
e funcionalidades não comentadas acima fazem parte do trabalho.

### Desafio

Quando falamos de dumpers e loaders, utilizávamos o _checksum_
para verificar se os blocos lidos estão completos. O _checksum_, porém, é
uma alternativa fraca para essa finalidade, a melhor escolha para esse
fim são os algoritmos de _hashing_, como os da família SHA. Você deve
incluir uma informação de validação ao fim do arquivo gerado
correspondendo ao _hash_ do arquivo encriptado.

## Perguntas

Seguem algumas perguntas a serem respondidas depois da codificação:

1.  Os algoritmos propostos podem ser mais eficientes? Como? Se sim, por
    que a forma menos eficiente foi escolhida?

2.  Os códigos escritos podem ser mais eficientes? Como? Se sim, por que
    a forma menos eficiente foi escolhida?

3.  Qual foi a maior dificuldade em implementar as rotinas?

4.  O que teria que ser mudado no seu código para que a chave de
    encriptação fosse alterada a cada execução do algoritmo?

5.  O que aconteceria com a execução do seu código se o arquivo de
    entrada fosse menor que o tamanho que você definiu para $S$?

## Entrega

Dois ou mais arquivos devem ser entregues:

1.  **Encriptador:** um arquivo em ASM chamado `encripta.asm` contendo a
    rotina que encripta o arquivo de entrada e gera o arquivo de saída.

2.  **Relatório:** um arquivo chamado `relatorio_<NUSP1>_<NUSP2>.pdf` para
    trabalhos realizados em dupla, ou `relatorio_<NUSP>.pdf` para individuais
    contendo uma descrição resumida do problema e dos conceitos e uma descrição
    detalhada das etapas de resolução, da estratégia utilizada em cada módulo
    e outras informações que julgarem úteis. O relatório pode conter imagens
    das execuções de teste;

3.  Outros arquivos que julgar necessário.
