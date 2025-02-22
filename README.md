# Multiplicação de Matrizes com Paralelismo em OpenMP (C++)

Este repositório contém a implementação de um algoritmo de multiplicação de matrizes em C++, utilizando tanto a abordagem sequencial quanto a paralelizada com a biblioteca **OpenMP**. O objetivo é analisar o ganho de desempenho (aceleração) ao explorar o paralelismo em um problema computacional, conforme especificado na atividade da disciplina de Programação Paralela.

## Descrição do Algoritmo

O algoritmo realiza a multiplicação de duas matrizes (`A` e `B`) para gerar uma matriz resultante (`C`), onde:
- A dimensão de `A` é `linhaA × colunaA`.
- A dimensão de `B` é `linhaB × colunaB`.
- A dimensão de `C` é `linhaA × colunaB`.
- Pré-requisito: `colunaA` deve ser igual a `linhaB` para que a multiplicação seja válida.

Foram implementadas duas versões:
1. **Sequencial**: Realiza a multiplicação de forma tradicional, sem paralelismo.
2. **Paralelizada**: Utiliza a diretiva `#pragma omp parallel for` do OpenMP para distribuir as iterações do laço externo entre múltiplas threads (configurado para 4 threads).

O tempo de execução de ambas as versões é medido com a função `omp_get_wtime()`, e a aceleração é calculada como `tempoSequencial / tempoParalelizado`.

## Detalhamento do Computador Utilizado

- **Hardware**:
  - Processador: [Insira o modelo do seu processador, ex.: Intel Core i5-12400]
  - Memória RAM: [Insira a quantidade, ex.: 16 GB DDR4]
  - Sistema Operacional: Windows 10 64-bit
- **Software**:
  - Compilador: g++ versão 14.2.0
  - IDE: Visual Studio Code
  - Biblioteca OpenMP: Incluída no compilador g++ (ativada com a flag `-fopenmp`)

## Linguagem e Bibliotecas Utilizadas

- **Linguagem**: C++
- **Bibliotecas**:
  - `<iostream>`: Para entrada e saída de dados.
  - `<time.h>`: Para inicialização da semente randômica.
  - `<stdlib.h>`: Para geração de números aleatórios.
  - `<omp.h>`: Para suporte ao paralelismo com OpenMP.
  - `<iomanip>`: Para formatação da saída (ex.: precisão de casas decimais).

A biblioteca **OpenMP** foi utilizada para implementar o paralelismo, especificamente a diretiva `#pragma omp parallel for` para dividir as iterações do laço entre as threads.

## Visão Geral das Implementações

### Estrutura do Código
- `criarMatrizDinamica()`: Aloca dinamicamente uma matriz na memória.
- `deletaMatrizDinamica()`: Libera a memória alocada.
- `inserirDados()`: Preenche a matriz com valores aleatórios entre 0 e 998.
- `printMatriz()`: Exibe a matriz (não utilizada na versão final, mas disponível para debug).
- `iniciarZerada()`: Inicializa a matriz resultante com zeros.
- `multiplicacaoMatrizSequencial()`: Implementação sequencial da multiplicação.
- `multiplicacaoMatrizParallel()`: Implementação paralelizada com OpenMP.
- `main()`: Controla a entrada de dados, execução e exibição dos resultados.

### Segmentos Paralelizados
O segmento paralelizado está na função `multiplicacaoMatrizParallel()`, onde o laço externo (`for (int i = 0; i < linhaA; i++)`) é distribuído entre as threads usando a diretiva:
```cpp
#pragma omp parallel for

Isso permite que cada thread processe um subconjunto das linhas da matriz resultante C, reduzindo o tempo total de execução em sistemas multi-core.
Análise do Desempenho e Aceleração Obtida
Os tempos de execução são medidos em segundos e exibidos em minutos, segundos e milissegundos. A aceleração é calculada como:

Aceleração = Tempo Sequencial / Tempo Paralelizado

Exemplo de Resultado
Para matrizes de tamanho 1000 × 1000 (testadas localmente, ajuste conforme seus testes):

    Tempo Sequencial: 2.2919 segundos
    Tempo Paralelizado: 0.862 segundos
    Aceleração: ~3.38x

O ganho de desempenho depende do número de threads (definido como 4 via omp_set_num_threads(4)), da arquitetura do processador e do tamanho das matrizes.
Como Executar

    Pré-requisitos:
        Compilador C++ com suporte a OpenMP.
        Sistema operacional compatível (Windows, Linux, macOS).
    
    -Passos para Compilação e Execução-
    1. Compilação: Compile o código usando o compilador g++ com suporte a OpenMP. Execute o seguinte comando no terminal:
    ```bash
    g++ -fopenmp main.cpp -o matriz_multiplication

    2. Execução: Após compilar, execute o programa gerado:
    No Linux/macOS:
    ```bash
    ./matriz_multiplication

    No Windows, você pode executar diretamente:
    matriz_multiplication.exe

        Insira as dimensões das matrizes A e B quando solicitado.
        O programa exibirá os tempos de execução e a aceleração obtida.

Contribuições
Este projeto foi desenvolvido como parte de uma atividade acadêmica. Sugestões de melhorias são bem-vindas, mas o foco principal é a análise de desempenho com OpenMP.
Autores

    Felipe Apio de Souza
    Guilherme Da Silva Schveitzer
    Leandro Rodrigues Marques 
    Pedro Tsalikis De Melo