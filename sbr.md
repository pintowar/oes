# Search-Based Refactoring (SBR)
Esta seção tem como objetivo avaliar o artigo [Search-Based Refactoring: an empirical study](sbr.pdf) por
*Mark O’Keeffe, Mel Ó Cinnéide* -
**School of Computer Science & Informatics, University College Dublin, Ireland**

## Resumo

Sistemas orientados a objetos que recebem incrementos de funcionalidade e acabam tendo perda de qualidade no seu design. Para atenuar o problema é preciso passar por uma custosa fase de refatoração a ser feita no código do sistema. O artigo se refere a área da SBSE sobre a automação da refatoração de código baseado no conceito de tratar o design orientado a objeto como um problema de otimização combinatorial, onde a representação da solução é o programa em sí, em sua forma de Árvore Sintática Abstrata (AST), as operações de mudança da solução são mudanças de código (mudança hierárquica e mudança na definição de segurança de campos e métodos, substituir herança por delegação, etc) e a função fitness define a qualidade do design do código, que é construída por uma soma ponderada de métricas orientadas a objeto. Esta abordagem teve como fonte de inspiração outras abordagens da SBSE como agrupamento de subsistemas e geração de dados de teste.

Por ser uma abordagem nova ainda será preciso estabelecer que técnicas de busca são mais adequadas para esta tarefa.
Neste artigo são reportados os resultados de uma comparação empírica entre *simulated annealing* (SA), *genetic algorithms* (GA), *multiple ascent hill-climbing* (HCM), e *steepest ascent hill-climbing* (HCS) para a refatoração baseada em busca. Este último embora não seja muito adequado devido ao longo tempo de execução e incapacidade de sair de um local optima, será usado como ponto de referência.

Para validação das estratégias foram selecionados 5 programas escritos em Java, onde foram considerados o número de classes, o número de linhas de código e número de heranças. Além dos métodos citados também foi utilizado uma ferramenta de refatoração automática, capaz de fazer mudanças significativas no código sem alterar o seu comportamento.

O tempo de processamento médio por solução examinada foi de menos de um segundo, incluindo construção de modelo, extração de métricas, avaliação de qualidade, descoberta de refatoração e refatoração do AST. O tempo total de execução variou entre 6 minutos e 18 horas, dependendo da tecnica utilizada, número de refatorações possíveis e número de refatorações aplicadas. Os experimentos tiveram como objetivo descobrir os parâmetros adequados por cada uma das abordagens propostas.

Foi selecionado o maior ganho de qualidade médio (para qualquer conjunto de parâmetros) de cada par programa/método de busca. Valores estes que foram normalizados pelo *steepest ascent hill-climbing*.

Entre as execuções pode-se observar que:

* O GA foi o método mais lento em muitas execuções, e sua performance foi relativamente fraca em termos de ganho de qualidade quando não era lento.
* O tempo de execução do SA, efetivamente configurado, teve uma grande variação, mas uma longa execução não necessariamente equivale a um grande ganho de qualidade.
* O tempo de execução do HCM variou consideravelmente, mas quando foi longo, um grande ganho de qualidade foi encontrado.

Os resultados mostraram que o *multiple ascent hill-climbing* (HCM) obteve um resultado melhor que os outros métodos discutidos.

## Avaliação

### Originalidade

Embora o autor já tivesse um trabalho anterior sugerindo algumas das abordagens utilizadas neste artigo, este artigo é uma expansão natural do trabalho anterior, pois fez uso de um maior conjunto de entrada de dados (programas), experiências mais diversificadas (mais parâmetros) e uma discussão mais detalhada sobre os resultados e a conclusão.

### Qualidade

O autor fez um comparativo empírico entre 3 abordagens para solucionar o problema de refatoração baseada em busca. Descorreu bem sobre o problema a ser resolvido e fez uso de ferramentas estatísticas para executar e comparar os resultados em cada uma delas usando uma quarta abordagem como modelo de comparação.

### Relevância

Trabalho reforça todo um conhecimento na área de refatoração baseada em busca de uma forma mais detalhada e dá base a uma série de novos trabalhos neste ramo da SBSE.

### Apresentação

Excelente apresentação, o autor conseguiu expressar bem o problema proposto, a formatação e apresentação dos resultados seguiu uma linha compreensível e coerente. Além do uso de recursos gráficos para expressar os resultados, ele ainda descreveu os pontos fortes e fracos de cada abordagem.

### Pontos Positivos

* Comparativo usando gráfico que auxiliaram no entendimento da interpretação dos resultados.

### Pontos Negativos
