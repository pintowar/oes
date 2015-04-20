# The Next Release Problem (NRP)
Esta seção tem como objetivo avaliar o artigo [The next release problem](the_next_release_problem.pdf) por
*A.J. Bagnall, V.J. Rayward-Smith, I.M. Whittley* -
**Computer Science Sector, School of Information Systems, University of East Anglia, Norwich NR4 7TJ, UK.**

## Resumo

### O Problema

A motivação deste trabalho veio da demanda de empresas de desenvolvimento de software em determinar as funcionalidades a serem adicionadas no próxima release de um software em desenvolvimento.

O desafio proposto é selecionar um conjunto de clientes a serem atendidos na próxima entrega de funcionalidades (next release), onde são levado em consideração a importância estratégica (peso) que cada cliente possui, o custo do conjunto de funcionalidades exigidas por cada cliente e o orçamento préviamente estipulado pela própria empresa para custear o desenvolvimento das funcionalidades.

O custo do conjunto de funcionalidades de um determinado cliente `cost(R)` seria a soma do custo individual de cada funcionalidade exigida por cliente `cost(r)`. Portanto o custo de funcionalidades de um cliente pode ser descrita como `cost(R) = sum(cost(r) | r in R)`. É válido mencionar que algumas funcionalidades dependem de outras funcionalidades e portanto o seu custo é a soma do seu custo e do custo de seus dependentes.

Em uma formulação simples (com funcionalidades independentes), pode-se descrever o problema da seguinte maneira:

$$Max \sum_{i=1}^{n} w_i x_i$$
$$s.t. \sum_{i=1}^{n} c_i x_i \leq B$$

Onde $w_i$ é o peso e $c_i$ é o custo de um cliente i e se faz necessário encontrar uma variável binária, $x_i \in$ {0, 1}. Se $x_i = 1$, então o cliente i será selecionado e terá suas funcionalidades satisfeitas, caso contrario $x_i = 0$.

### Estratégia(s) proposta(s)

Três abordagens foram desenvolvidas para resolver o problema do próximo release (NRP).

* A primeira utiliza técnicas exatas para resolver uma relaxação de programação linear, permitindo que limites superiores sejam encontrados.
* A segunda utiliza um conjunto simples de algoritmos gulosos permitindo uma geração rápida de limites inferiores, o melhor destes algoritmos é então melhorado com linhas GRASP para melhorar os valores obtidos.
* A terceira utiliza uma série de buscas locais tradicionais, com o propósito de encontrar soluções próximas da ótima, evitando um excessivo tempo computacional.

#### Programação Inteira (técnica exata)

Sendo $x_1$, $x_2$, ... $x_m$ e $y_1$, $y_2$, ... $y_n$ variaveis 0/1 representando respectivamente o conjunto de funcionalidades e de clientes. E $w_i$ e $c_i$ representando os seus significados originais, a formulação final seria:

$$Max \sum_{i=1}^{m} w_i y_i$$
$$s.t. \sum_{i=1}^{n} c_i x_i \leq B$$
$$x_i \\geq x_j \forall (r_i, r_j) \in E$$
$$0 \leq x_i \leq 1 \forall 1 \leq i \leq m$$
$$0 \leq y_i \leq 1 \forall 1 \leq j \leq n$$

Onde $E$ seria a relação de dependencia entre $(r_i, r_j)$, mais precisamente: $(r_i, r_j) \in E$ iff $r_i$ for pré requisito de $r_j$.

#### Algoritmos Gulosos

Estes algoritimos iniciam-se com um conjunto vazio de de clientes e a cada iteração um cliente é adicionado até que mais nenhuma adição possa ser feita sem exceder o orçamento estabelecido. A escolha que cada cliente selecionado por cada iteração é feita por um conjunto de metricas simples.

A primeira métrica utilizada simplesmente seleciona o cliente com o maior prioridade estratégica, sem que ele ultrapasse o orçamento, caso algum cliente ultrapasse o orçamento, o cliente seguinte é considerado.

A segunda métrica é semelhante a primeira, entretanto a prioridade são os clientes que requerem o mínimo de recursos para atenderem as suas funcionalidades.

A terceira métrica é uma combinação das duas métricas anteriores, usando como métrica a taxa da prioridade estratégica pelos recursos que cada cliente demanda. Aquele que possuir a maior taxa ganhará a prioridade na seleção de clientes, mas sempre respeitanto o orçamento estabelecido.

Em um esforço de melhorar os resultados obtidos foram utilizados ideias da literatura GRASP. Ao invés de sempre selecionar o melhor cliente para agregar a solução em cada iteração, o algoritmo foi adaptado para selecionar randomicamente os top k clientes da lista de candidatos. A utilização da abordagem GRASP melhorou a qualidade dos resultados, mas com um acrescimo no tempo computacional.

#### Hill climbing (busca local)

O algoritmo Hill climbing funciona movendo de uma solução inicial até encontrar uma local ótima, utilizando somente movimentos que melhorem a solução. Três abordagens de Hill climbing foram utilizadas:

* steepest ascent
* first found
* sampling

#### Simulated annealing (busca local)

O algoritmo Simulated Annealing (SA) é baseado no modelo de resfriamento de materiais em banho quente, um processo conhecido como Annealing. A sua simplicidade combinada com seus resultados empiricos e teóricos o levaram a ser largamente aceito na comunidade de Otimização. O algoritmo funciona permitindo movimentos que não melhoram a solução, mas feitos de uma maneira controlada. A cada movimento ela é avaliada e associada a uma probabilidade de aceitação. Esta probabilidade depende do custo benefício do movimento e também do estado atual da busca, modelado por um parametro chamado "temperatura". De inicio a temperatura é alta e a busca aceita movimentos de baixa qualidade. A medida que a busca progride a "temperatura" esfria e a probabilidade cai até que a fase final só aceite bons movimentos.

É necessário a especificação de um calendário de resfriamento. Dois foram usados:

* Geométrico: $t_{i+1} = \alpha t_i$

* Lundy and Mees: $t_{i+1} = t_i/(1 + \beta t_i)$

Onde $\alpha$ e $\beta$ são parâmetros de controle. Ambos requerem que uma "temperatura inicial" seja especificada. O SA Geométrico requer um parâmetro especificando quanto permanecer a cada estágio de "temperatura". Para o Lundy and Mees a "temperatura" cai após cada movimento.

### Validação

Para validar o problema foi selecionado um conjunto de 5 proplemas randomicamente gerados.
O menor problema (NRP1) tem 100 clientes e 140 funcionalidades, enquanto o maior (NRP5) tem 500 clientes e 3250 funcionalidades.
Para cada problema, o orçamento total para satisfazer todos os clientes foi calculado e experimentos foram executados com 30, 50 e 70% do seu total.

Com o conjunto de problemas gerado, foi executado cada uma das estratégias propostas nos 5 problemas (NRP1 a NRP5) com os 3 cenários de orçamento possíveis (30, 50 e 70% do total). Após as execuções os resultados foram comparados com o resultado ótimo esperado.

### Resultados

A técnica Simulated Annealing (SA) aproximou-se em até 1.5% da solução ótima em todos os casos testados, portanto pode-se espera uma performance semelhante em problemas que não se conhece o resultado ótimo.

Em problemas pequenos, técnicas exatas se mostraram suficiente, enquanto que nas outras a técnica Simulated annealing encontrou as melhores soluções (não necessariamente ótimas) em um tempo computacional aceitável.

Além dos resultados pode-se há áreas para futuros desenvolvimento nas áreas exatas e heuristicas. Do lado heuristico fica em aberto a utilização de outras tecnicas como Busca Tabu e Otimização de Colônia de Formigas. Já as tecnicas exatas, ainda há muito o que se aproveitar da estrutura especial do problema, e também de incorporar alguns dos muitos avanços que mostraram sucesso na resolução do problema da mochila.

## Avaliação

### Originalidade

Uma adaptação do problema da mochila para o mundo da Engenharia de Software. A adaptação consistiu especialmente com a preocupação em satisfazer a restrição de funcionalidades com dependências.
Seu embasamento teórico veio basicamente outras abordagens de otimização, mas serviu para início de uma provocação na área de Engenharia de Software.

### Qualidade

O artigo utilizou de várias estratégias para solucionar o problema e embora não tenha entrado em detalhes muito profundos sobre como cada estratégia funcione, ele consegue descreve-las de maneira que se faça entender os maiores desafios encontrados nessas abordagens. E além disso conseguiu obter resultados bem claros, que despertam uma maior curiosidade sobre o tópico.

### Relevância

Embora o problema proposto seja ainda muito simples se comparado aos problemas de Engenharia de Software do mundo real, o autor conseguiu iniciar uma provocação bem fundamentada tanto na área de Engenharia de Software como na Área de Otimização.

### Apresentação

O autor conseguiu ser claro em suas ideias, apresentou o problema de forma clara e conseguiu descrever as estratégias de solução de uma forma direta, embora sem entrar em muito detalhes sobre o funcionamento de cada uma delas. Entretanto uma seção dedicada somente a interpretação dos resultados teria sido um grande acréscimo. Com esta seção dedicada poderia ter sido utilizado algum recurso gráfico para auxiliar na interpretação dos resultados e até mesmo ter focado mais no tempo requerido para executar cada uma das estratégias propostas.

### Pontos Positivos

* Criatividade na adaptação do problema da mochila.
* Provocação sobre o assunto e abrir horizontes sobre essa área da SBSE.

### Pontos Negativos

* Falta de um melhor comparativo de tempo de execução das estratégias.
* Comparativo usando gráfico ao invés de tabelas ajudariam mais na vizualização dos resultados.
