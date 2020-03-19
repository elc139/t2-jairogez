[Programação Paralela](https://github.com/AndreaInfUFSM/elc139-2020a) > Trabalhos

# T2: Programação Paralela Multithread 

Este trabalho tem o objetivo de familiarizá-los sobre etapas de [projeto de programas paralelos](https://docs.google.com/presentation/d/1Ev5CROjugPpZm5hT4a387dLEQTmxnZAtKUqXItVeHOc?usp=sharing), passando pela realização de experimentos para cálculo de métricas de desempenho.

O roteiro abaixo assume familiaridade com Linux e linguagem C, com compilador GCC. É possível usar outras combinações de SO e compilador, por sua conta e risco :-) 

## Entrega

No seu repositório, você deverá entregar:

1. Um documento `Entrega.md`, contendo:
   - Identificação: seu nome e nome da disciplina;
   - Duas seções separadas contendo respostas para questões sobre Pthreads e OpenMP, incluindo gráficos, links para programas, screenshots, tabelas, etc.
   - Referências.
 
2. Todos os arquivos citados no documento Entrega.md, incluindo:

   - Um arquivo `specs.txt`, com especificações da plataforma utilizada (processador, memória, SO). Cuidado aqui se estiver usando máquina virtual.
   - Um arquivo `results.csv`, preenchido com dados de execuções dos programas, conforme o roteiro abaixo. Você deve usar uma formatação padronizada para esse arquivo, disponível [aqui](results.csv). Para converter esse arquivo para Markdown e incluí-lo na sua página de entrega, use scripts ou serviços como esse [aqui](https://donatstudios.com/CsvToMarkdownTable).


## Parte I: Pthreads

1. Escolha um computador com mais de um núcleo de processamento. Verifique suas características (processador, memória).

3. Você vai trabalhar com 2 programas que usam POSIX threads para cálculo de um produto escalar: [pthreads_dotprod.c](pthreads_dotprod/pthreads_dotprod.c) e [pthreads_dotprod2.c](pthreads_dotprod/pthreads_dotprod2.c).

4. Compile esses programas:

   ```
   make
   ```
5. Execute o programa pthreads_dotprod usando 1 thread, para vetor de 1000000 de elementos, com 2000 repetições:

   ```
    ./pthreads_dotprod 1 1000000 2000
   ```
   
6. Execute o mesmo programa usando 2 threads, com 500000 elementos para cada thread, 2000 repetições:

   ```
    ./pthreads_dotprod 2 500000 2000
   ```
    O resultado deve ser o mesmo do caso anterior, mas o tempo de processamento deve ser diferente.

7. Estude o código-fonte do programa, verificando as funções que implementam o paralelismo.

8. Observe que o programa [pthreads_dotprod2.c](pthreads_dotprod/pthreads_dotprod2.c) é semelhante a [pthreads_dotprod.c](pthreads_dotprod/pthreads_dotprod.c), mas tem **2 linhas a menos**.
    
    
### Questões Pthreads


1. Explique como se encontram implementadas as 4 etapas de projeto: particionamento, comunicação, aglomeração, mapeamento (use trechos de código para ilustrar a explicação).

2. Considerando o tempo (em microssegundos) mostrado na saída do programa, qual foi a aceleração (speedup) com o uso de threads?

3. A aceleração  se sustenta para outros tamanhos de vetores, números de threads e repetições? Para responder a essa questão, você terá que realizar diversas execuções, variando o tamanho do problema (tamanho dos vetores e número de repetições) e o número de threads (1, 2, 4, 8..., dependendo do número de núcleos). Cada caso deve ser executado várias vezes, para depois calcular-se um tempo de processamento médio para cada caso. Atenção aos fatores que podem interferir na confiabilidade da medição: uso compartilhado do computador, tempos muito pequenos, etc.

4. Elabore um gráfico/tabela de aceleração a partir dos dados obtidos no exercício anterior.

5. Explique as diferenças entre [pthreads_dotprod.c](pthreads_dotprod/pthreads_dotprod.c) e [pthreads_dotprod2.c](pthreads_dotprod/pthreads_dotprod2.c). Com as linhas removidas, o programa está correto? 
    
    
## Parte II: OpenMP


1. Nesta parte você vai trabalhar com um programa muito simples que usa OpenMP: [ompsimple.c](openmp/ompsimple.c).

2. Compile o programa usando a flag `-fopenmp`, que habilita OpenMP:

   ```
   gcc -fopenmp -o ompsimple ompsimple.c
   ```
   
3. Execute o programa com 8 threads:

   ```
   OMP_NUM_THREADS=8 ./ompsimple
   ```

### Implementação OpenMP

1. Implemente um programa equivalente a [pthreads_dotprod.c](pthreads_dotprod/pthreads_dotprod.c) usando OpenMP. 

2. Avalie o desempenho do programa em OpenMP, usando os mesmos dados/argumentos do programa com threads POSIX. 


## Material de apoio

- [POSIX Threads Programming](http://www.llnl.gov/computing/tutorials/pthreads/)  
  Tutorial do Lawrence Livermore National Laboratory (LLNL) sobre Pthreads.

- [Tutorial OpenMP](https://computing.llnl.gov/tutorials/openMP/)  
  Tutorial do Lawrence Livermore National Laboratory (LLNL) sobre OpenMP. 

