# The Multi-Objective Next Release Problem (MONRP)
Esta seção tem como objetivo avaliar o artigo [The Multi-Objective Next Release Problem](the_multi_next_release_problem.pdf) por
*Yuanyuan Zhang, Mark Harman, S. Afshin Mansouri* -
**King’s College London Strand, London, WC2R 2LS, UK.**

## Resumo

### O Problema

Assim como o [NRP (Next Release Problem)](nrp.html), a motivação deste trabalho veio da demanda de empresas de desenvolvimento de software em determinar as funcionalidades a serem adicionadas no próxima release de um software em desenvolvimento.

Satisfazer cada um dos requisitos demanda um **custo** operacional, ao passo que a entrega de um requisito, implica em agregar **valor** para a empresa de desenvolvimento. O problema então é selecionar os requisitos para a próxima release de modo que maximize o valor agregado e minimize o custo operacional. Estes objetivos são conflitantes entre si, o que os tornam inapropriados a serem combinados em uma única função fitness. Portanto uma formulação multi objetivo se torna mais apropriada.

Diferentemente do [NRP](nrp.html), onde dado um conjunto de clientes com uma série de requisitos (demanda de novas funcionalidades) cada, deve-se selecionar quais clientes são atendidos, o MONRP, procura selecionar quais requisitos devem ser satisfeitos na próxima release.

Um Problema de Otimização Multi Objetivo (Multi-Objective Optimization Problem, ou MOOP), pode ser descrito matematicamente como:

    $Max \{f_1(\vec{x}), f_2(\vec{x}), ..., f_m(\vec{x})\}$
    $s.t.$
    $g_j(\vec{x}) \geq 0; j = 1, 2,..., J$
    $h_k(\vec{x}) = 0; k = 1, 2,..., K$

Para o modelo proposto, seja `$C = \{c_1, ..., c_m\}$`, o conjunto de clientes e `$R = \{r_1, ..., r_n\}$`, o conjunto de requisitos. Assumindo que cada requisito é independente, para satisfazer cada um deles, alguns recursos precisam ser alocados. A alocação de recurso para cada requisito pode ser representada em termos de custo por `$Cost = \{cost_1, ..., cost_n\}$`.

Cada cliente possui um nível de importancia estratégica para a empresa, que pode ser refletida um valor, ou peso definido por `$W = \{w_1, ..., w_m\}$`. O valor agregado de um requisito para um determinado cliente, é expresso por `$value(r_i, c_j)$`. Portanto o valor agregado de um requisito para a empresa que o desenvolve seria a soma dos seus valores por cliente, multiplicado pelo peso do cliente, definido por: `$score_i = \sum_{j=1}^{m} w_j value(r_i, c_j)$`. O vetor de decisão `$\vec{x} = \{x_1, x_2, ..., x_n\} \in \{0,1\}$` determina se o requisito será selecionado para a próxima release ou não.

Para a formulação final, dois objetivos foram levados em consideração, maximizar a satisfação dos clientes e minimizar o custo necessário. Portanto o custo é tratado como objetivo, ao invés de ser tratado como uma restrição. O motivo desta abordagem é explorar os valores ótimos da frente de Pareto, que é uma ótima fonte de informações para a tomada de decisão, dado a natureza conflitante dos objetivos. A formulação final, pode ser dada por:

    $Max \sum_{i=1}^{n} score_i x_i$
    $Max -\sum_{i=1}^{n} cost_i x_i$
    $x_i \in \{0,1\}$

### Estratégia(s) proposta(s)

Este artigo aplica meta heuristicas para encontrar a frente de Pareto para o MONRP. Isto permite ao responsável pela tomada de decisão selecionar a solução preferida de acordo com as suas prioridades. A frente de Pareto pode prover insights valiosos, pois ele (o responsável) pode capturar os trade-offs entre os objetivos conflitantes.

Quatro abordagens foram selecionadas do NRP Multi-Objetivo, elas são:

* Random Search
* Single-Objective (Weighted) Genetic Algorithm
* Pareto GA and Non-dominated Sorting
* Genetic Algorithm II (NSGA-II)

#### Random Search

O uso do Random Search serviu meramente como uma checagem de sanidade. Todas as outras abordagens devem ser capaz de ter um desempenho melhor.

#### Single-Objective GA

Para aplicar o Single-Objective GA, foi usado um método ponderado que combina as duas funções objetivas em uma única função. Usando o fator `$\omega$`, as funções objetivas são convertidas na segunte função fitness:

    $F(\vec{x}) = (1 - \omega) f_1(\vec{x}) + \omega f_2(\vec{x})$

Ao modificar o valor de `$\omega \in [0, 1]$`, é possivel explorar várias regiões da frente de Pareto. Esta abordagem é aplicada para comparar o Single-Objective GA com outras técnicas Multi Objetivas.

#### Pareto GA

O Pareto GA usado nesta pesquisa é uma variação de uma algoritmo genético (GA) simples. Um GA simples mantém as populações de soluções que são evoluidas de acordo com um valor fitness. Em um MONRP há pelo menos dois valores fitness para cada solução que são usados em uma seleção de torneio. O algoritmo usa relações de dominação de Pareto entre as soluções para selecionar os candidatos para a fase de reprodução. Uma nova população é gerada recombinando as soluções selecionadas por operadores de cruzamento e mutação.

#### NSGA-II

O Non-dominated Sorting Genetic Algorithm-II (NSGA-II) é uma extensão do NSGA, ele incorpora o elitismo para manter as melhores soluções encontradas. O rank de cada indivíduo é baseado no nível de não-dominação.

A população é ordenada usando relações de não-dominação em várias frontes. Cada solução é associada a um valor fitness de acordo com o seu valor de não-dominação. Desta maneira, soluções com melhores frentes tem um maior valor de fitness. O NSGA-II usa um nível de distância de multidão, que estima a densidade das soluçãos pertencentes ao mesmo front. Soluções com uma maior distância de multidão são associadas a um melhor fitness.

Assumindo que cada indivíduo $i$ da população tem atributos de rank não-dominador e distancia de multidão, pode-se dizer que entre soluções de diferentes "rank não-dominador", as melhores soluções tem um baixo valor. Caso contrario as melhores soluções possuem a menor distância de multidão.

### Validação

Para validar o problema foram criadas amostras aleatórias de valor e custo. Onde os valores de custo variam entre 1 e 9 e os valores variam entre 0 e 5. Este cenário simula situações o cliente define as prioridades dos requisitos e os custos são estimados em muito baixo, baixo, médio, alto e muito alto. Cada algoritmo foi executado 5 vezes para cada amostra.

As abordagens em dois conjuntos de teste para dois casos de estudos empiricos (ES1 e ES2). No ES1 foram reportados resultados com respeito a performance dos algoritmos em casos consideredos *típicos*, com número de clientes variando entre 15 e 100 e o número de requisitos entre 40 e 140.
Já no ES2 o interesse é o limite inferior do problema, determinar com que tamanho do problema, a busca não é apropriada. Ou seja o objetivo do ES2 é encontrar que ponto cada meta heuristica é capaz de trazer um resultado melhor que o Random Search.

A população inicial foi de 200 soluções binárias simples, onde o tamanho do cromossomo (ou solução) é o tamanho de requisitos do problema. O critério de parada foi atingir a 50a. geração populacional. As abordagens genéticas usaram a seleção de torneio (com tamanho 5), cruzamento de ponto único (p = 0.8) e mutação bitwise (p = 1/n, onde n é o tamanho da solução).

### Resultados

#### Resultados ES1

Foram selecionados 3 amostras (S1, S2 e S3) com os seguintes valores:

<table>
  <thead>
    <th>
      <td>Clientes</td><td>Requisitos</td>
    </th>
  </thead>
  <tbody>
    <tr>
      <td>S1</td><td>15</td><td>40</td>
    </tr>
    <tr>
      <td>S2</td><td>50</td><td>80</td>
    </tr>
    <tr>
      <td>S3</td><td>100</td><td>140</td>
    </tr>
  </tbody>
</table>

Foram examinadas 5 execuções de cada abordagem. O Single-Objective GA foi executado 9 vezes, variando o peso $\omega$ entre 0.1 e 0.9.

Após a analise dos resultados, as conclusões foram:

* O NSGA-II obteve o melhor resultado nas três amostras. Claramente encontrou uma melhor diversidade na distribuição de soluções e também convergiu em resultados melhores que os outros algoritmos, pois seu fronte de resultados domina os demais. Este resultado produz uma evidencia empirica de que o NSGA-II é eficaz na solução do MONRP.

* Soluções usando Single-Objective GA ponderado, onde o $\omega$ foi proximo de 0 ou 1 levou a busca para os extremos da frente de Pareto. Estas partes extremas não foram exploradas pelo NSGA-II. Portanto embora o Single-Objective GA não tenha encontrado uma diversidade grande de soluções próximo a frente de Pareto, ele conseguiu complementar as soluções encontradas pelo NSGA-II.

#### Resultados ES2

A intenção deste estudo é explorar os limites do MONRP, ou seja, obter a "massa critica" de clientes e requisitos. Quando a massa critica exceder um determinado valor crítico, o problema se torna apto a usar uma meta heuristica na sua resolução, abaixo deste ponto o problema é trivial o suficiente para poder se aplicar o Random Search.

Foram consideradas duas situações. Uma primeira, onde foram considerados muitos clientes e poucos requisitos e uma segunda onde foram considerados poucos clientes e muitos requisitos.

Para a primeira situação pode-se encontrar que 20 requisitos seria o número crítico. Já para a segunda situação qualquer número de clientes já é apto ao uso de meta heurisicas.

## Avaliação

### Originalidade

O artigo é uma evolução natural do tópico iniciado no [The next release problem](nrp.html), levando a encarar o problema com uma formulação multi objetiva. Esta formulação é importante pois, na pratica, um engenheiro de software tem muitos objetivos conflitantes para atender quando está determinando o conjunto de requisitos a serem atendidos para a próxima entrega (release).

### Qualidade

O autor utilizou algumas estratégias multi objetivas na resolução do problema e conseguiu descrever bem os principais detalhes em cada uma das abordagens utilizadas. Além disso procurou mostrar resultados em dois casos de estudos empiricos, que pode mostrar o quão rica esta abordagem pode ser.

### Relevância

Embora tenha se utilizado de muitas ideias elaboradas no [The next release problem](nrp.html), ele foi pioneiro ao generalizar o NRP com uma abordagem multi objetiva, abrindo espaço para futuras abordagens com esta formulação.

### Apresentação

O autor conseguiu expressar bem o problema e a abordagem sugerida. A formatação e apresentação dos resultados seguiu uma linha compreensível de modo que foram apresentados dois estudos empiricos (performance das diferentes abordagens multi objetivas e determinar o tamanho do problema onde o MONRP se torna não trivial) de maneira que os resultados foram fáceis de analizar. O uso de recursos gráficos também foi providencial para a interpretação dos resultados, pois tornou os argumentos sobre a frente de Pareto mais claros.

### Pontos Positivos

* Abordagem encarando situações mais praticas, onde mais de um objetivo é levado em consideração.
* Comparativo usando gráfico que auxiliaram no entendimento da interpretação dos resultados.

### Pontos Negativos

* Falta de um melhor comparativo de tempo de execução das estratégias.
* Falta de uma maior diversidade nas amostras analisadas.

