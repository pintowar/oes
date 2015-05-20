# Project Planning
Esta seção tem como objetivo avaliar o artigo [Search–Based Techniques Applied to Optimization of Project Planning for a
Massive Maintenance Project](planning.pdf) por
*Giulio Antoniol, Massimiliano Di Penta e Mark Harman* -
**RCOST - Research Centre on Software Technology University of Sannio, Department of Engineering Palazzo ex Poste, Via Traiano 82100 Benevento, Italy.**
**Department of Computer Science, King’s College London, Strand, London WC2R 2LS, UK**

## Resumo

Este artigo avalia o uso de três abordagens de busca diferentes, são elas genetic algorithms, hill climbing e simulated annealing, em duas representações diferentes para o problema (*pigeon hole* e *ordering*) para o planejamento de alocação de recursos em projetos de manutenção de grande porte. A representação *pigeon hole* descreve a solução como um array de tamanho N, que é o número de WP (pacotes de trabalho), e cada valor do array representa um time que será alocado para trabalhar naquele pacote. A sua função fitness é simplesmente o tempo total do projeto. Já na representação *ordering* cada elemento do array representa a ordem do WP para a fila de entrada, o seu fitness é calculado usando um simulador de filas para computar o seu prazo. Ou seja uma abordagem baseada em busca objetiva encontrar a ordem ótima, ou próxima de ótima, de alocação de pacotes de trabalho para times de desenvolvedores, procurando minimizar a duração do projeto.

A abordagem é validada por dois estudos empíricos. O primeiro estudo compara as duas representações do problema e as três técnicas entre sí e com uma busca randômica (como teste de sanidade). Já o segundo analisa a variação da estimativa de tempo de conclusão com o número de pessoas disponíveis (times de tamanhos diferentes).

Os resultados mostram que uma ordenação, baseada na representação *ordering*, e algoritmos genéticos apresentam a solução mais robusta, embora a abordagem do Hill Climbing também tenha tido uma boa performance. A melhor técnica de busca reduziu a duração do projeto em até 50%. O artigo também reporta os resultados de experimentos que alteram o tamanho dos times do projeto. Enquanto que em times pequenos dobrar o tamanho do time nã melhora a performance, em times ainda maiores os efeitos podem ser dramáticos.

## Avaliação

### Originalidade

O artigo evoluiu a ideia de alocação de recursos para a área de planejamento de projeto de software e a comparação do uso de 3 meta heuristicas diferentes para a resolução do problema.

### Qualidade

O autor fez um comparativo empírico entre 3 abordagens para solucionar e 2 representações do problema de alocação de recursos. Descorreu bem sobre o problema a ser resolvido e fez uso de resultados experimentais para comparar os resultados de dois estudos empíricos diferentes.

### Relevância

Trabalho pioneiro na área de alocação de recursos em projetos de software, iniciou uma provocação no assunto e deu base a uma série de novos trabalhos neste ramo da SBSE.

### Apresentação

Artigo muito bem estruturado, objetivos claros desde o início do artigo. Seções bem definidas, a formatação e apresentação dos resultados seguiu uma linha compreensível e coerente. E bom uso de recursos gráficos para expressar a diferença entre os resultados.

### Pontos Positivos

* Comparativo usando gráfico que auxiliaram no entendimento da interpretação dos resultados.
* Provocação sobre o assunto e abrir horizontes sobre essa área da SBSE.

### Pontos Negativos

* Falta de um melhor esclarecimento sobre o uso de sistemas de filas para calcular o fitness.
