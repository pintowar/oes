# Test Data Generation
Esta seção tem como objetivo avaliar o artigo [A Multi–Objective Approach To Search–Based Test Data
Generation](testgen.pdf) por
*Mark Harman, Kiran Lakhotia e Phil McMinn* -
**King’s College, CREST Strand, London WC2R 2LS, UK**
**University of Sheffield 211 Portobello St, Sheffield S1 4DP, UK**

## Resumo

Gerar dados manualmente é um processo tedioso, caro e propenso a erros. Entretanto para muitas organizações esta atividade não pode ser evitada pois níveis adequados de teste são constantemente requeridos ou recomendados por padrões de aceitação internacionais para controle de qualidade e segurança. Esta combinação de dificuldade e importância tornou a automação de geração de dados de teste um campo amplamente estudado.
Há um considerável trabalho na área de geração de dados de testes baseado em buscas. Entretanto não havia trabalhos usando uma abordagem multi objetiva. Em muitos casos uma abordagem mono objetiva não se mostra bem realista. Há situações onde, por exemplo, testadores podem desejar encontrar dados que satisfaçam vários objetivos simultaneamente objetivando maximizar o valor obtido do processo de execução de casos de testes e examinando os resultados produzidos.

Este artigo apresenta resultados da execução de experimentos em 5 casos de estudo (2 casos reais de código C e 3 programas sinteticos) usando uma implementação de de busca randômica, implementação de GA ponderado e uma implementação de GA multi objetivo, que tem como objetivos  maximizar o *branch coverage* e maximizar a alocação de memória dinâmica de programas reais e sintéticos.

Embora o GA ponderado tenha mostrado um melhor resultado, não é possível afirmar que um método é melhor que o outro, já que de pendendo do caso um tem um melhor resultado do que o outro. O mais aconselhável seria uma abordagem híbrida, onde um GA ponderado poderia ser usado para cobrir *branches* que o GA multi objetivo. Esta abordagem também resolveria o problema de não ser capaz de avaliar a performance de um GA ponderado para um objetivo sem ótimo definido.

Sendo assim os GAs multi objetivos são adequados para este problema e ilustra como a busca de Pareto pode levantar valiosos insights sobre os trade-offs entre os objetivos concorrentes.

## Avaliação

### Originalidade

Primeiro artigo a considerar uma abordagem multi objetiva para o problema de geração de dados de teste.

### Qualidade

O autor detalhou bem a fundamentação teórica e fez experimentos em 5 casos de estudo (2 casos reais de código C e 3 programas sinteticos). Com resultados relevantes que mostram como uma solução multi objetivo pode levantar valiosos insights sobre os trade-offs entre os objetivos.

### Relevância

Artigo muito relevante (84 citações segundo o google scholar), especialmente em termos de estratégia de resolução. Trabalho pioneiro na utilização de uma abordagem multi objetiva na geração de dados de teste, iniciou uma provocação no assunto e deu base a uma série de novos trabalhos neste ramo da SBSE.

### Apresentação

Artigo muito bem estruturado, com objetivos claros e seções bem definidas. A formatação e apresentação dos resultados seguiu uma linha compreensível e coerente. Possui uma excelente descrição dos casos de estudo e fez bom uso de recursos gráficos para expressar a diferença entre os resultados.

### Pontos Positivos

* Abordagem multi objetiva
* Descrições detalhadas de casos de estudo

### Pontos Negativos
