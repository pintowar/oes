# Applying Genetic Improvement to MiniSAT
Esta seção tem como objetivo avaliar o artigo [Applying Genetic Improvement to MiniSAT](minisat.pdf) por
*Justyna Petke, William B. Langdon, Mark Harman* -
**CREST Centre, University College London, Gower Street, London, WC1E 6BT, United Kingdom**

## Resumo

A programação genética (GP) vem sendo aplicada em vários problemas da SBSE. Recentemente tem havido muito interesse em usar GP e suas variações para automaticamente melhorar programas de acordo com uma ou mais funções fitness.

Este artigo investiga a aplicação de um melhoramento genético em um sistema bem conhecido e estudado, um solver open-source (em C++) de satisfatibilidade booleana chamado MiniSAT. Muitos programadores já tentaram tornar este solver ainda mais rápido e até mesmo uma competição foi criada para tentar facilitar este objetivo. Portanto melhorar geneticamante o MiniSAT se mostra um grande desafio. Além disso, devido a uma vasta gama de aplicações de tecnologias de solução de SAT, qualquer melhoria pode representar um grande impacto.

O objetivo da melhoria genética é encontrar uma nova versão do MiniSAT que esteja correto, ou seja que possa dizer se uma instância é contentável ou não, e que seja mais rápida que a solução original. Para validar o objetivo foram usados os casos de teste de competições SAT. O solver foi modificado no seu código fonte, para isso foi utilizado uma gramática BNF que assegurasse que o código evoluído estivesse sintaticamente correto. Assim os indivíduos tinham chance de compilar e executar. Um timeout foi utilizado para assegurar que a execução de um novo indivíduo não fosse significamente maior que o tempo de execução do MiniSAT original.

A evolução do programa se deu por uma evolução de uma lista de instruções de mudanças (copias, substituições e exclusões de linhas de código). Para cada geração metade da população era selecionada para o processo de mutação (adicionando uma instrução a mais) e crossover (fazendo o merge de duas soluções) com propabilidades de 50%. A função fitness então era avaliada de modo que se um indivíduo estivesse correto, receberia 2 pontos, se fosse mais rápido receberia mais um ponto. Apenas invivíduos com 10 ou mais pontos eram considerados para a seleção.

Os resultados iniciais, usando a abordagem multi objetivo de melhoramento genético, GISMOE (Genetic Improvement of Software for Multiple Objectives), mostram que há espaço para melhorias simplemente eliminando assertions e declarações relacionadas a dados estatísticos da execução. Além disso a remoção de algumas otimizações menores levaram a execuções mais rápidas em algumas instancias SAT. Entretanto uma versão significamente mais eficiente do MiniSAT ainda está para ser descoberta.

## Avaliação

### Originalidade

O trabalho faz parte de um ramo da SBSE que o uso de GP é voltada para o desenvolvimento (evolução de código) e não fonte de apoio de tomada de decisão. Este trabalho adaptou uma aobrdagem anterior (Langdon e Harman) que procurava otimizar o MiniSAT.

### Qualidade

O autor abordou um problema desafiador e embora não tenha encontrado uma nova versão significamente mais eficiente, conseguiu de uma forma direta representar os possíveis ganhos desta abordagem.

### Relevância

Trabalho reforça a importância de pesquisas na área de melhoramento genético mostrando que mesmo em situações extremas, no sentido de que o caso escolhido para o estudo é algo que já vem sendo melhorado durante anos por uma série de pessoas diferentes, ainda teria espaço para melhorias no código. Por sua vez dá base a uma série de novos trabalhos neste ramo da SBSE.

### Apresentação

Artigo muito curto, faltou um cuidado maior em exibir os resultados finais e algumas descrições sobre a abordagem não ficaram muito claras, mas no geral conseguiu expressar de maneira satisfatória os principais conceitos utilizados na solução do problema.

### Pontos Positivos

* Problema desafiador.
* Abordagem criativa na representação do problema.

### Pontos Negativos

* Explicação da função fitness não ficou tão clara.
* Ausência gráfico ao invés de tabelas ajudariam mais na vizualização dos resultados.
