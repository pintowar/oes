# Release Planning (RP)
Esta seção tem como objetivo avaliar o artigo [The Art and Science of Software Release Planning](release_planning.pdf) por
*Günther Ruhe, Moshood Omolade Saliu* -
**Laboratory for Software Engineering Decision Support, University of Calgary, CA**

## Resumo

### O Problema

O planejamento de releases refere-se a decisões relacionadas a seleção e alocação de funcionalidades em uma sequência consecutiva de releases de produtos que satisfaçam restrições de risco, técnicas, orçamento e recursos. Um planejamento ruim pode levar a clientes insatisfeitos, atrasos, baixa qualidade de entregas e um valor agregado ruim para a empresa de desenvolvimento.

O objetivo deste artigo é discutir a 'Arte e Ciência' do planejamento de releases de software. A "Arte do planejamento de releases" é a parte referente a intuição humana, comunicação e a capacidade de negociar entre restrições e objetivos conflitantes. Já "Ciência do planejamento de releases" refere-se a formulação do problema e a aplicação de algoritmos computacionais que buscam as melhores soluções.

De acordo com a definição de Pfleeger, sobre definição de boas decisões em Engenharia de Software, foi assumido que o planejamento deve prover o maior valor de negocio possível alocando as funcionalidades na sequência correta, satisfazer os stakeholders mais importantes, ser factível em termos de recursos disponíveis e deve refletir as dependências entre funcionalidades.

Para determinar um bom planejamento de release, é necessário identificar os objetivos e restrições do problema, assim como os principais stakeholders, suas importâncias e preferências (de funcionalidades). A natureza dessas informações são incertas e estão mudando dinamicamente, o que torna o planejamento de release um problema de grande dificuldade.

De acordo com o CMMI, o planejamento de um projeto consiste em estabelecer e manter planos que definem as atividades do projeto. Para este processo de planejamento existem certos padrões a serem seguidos, entretanto pouco se sabe como realmente agir de uma maneira eficaz e eficiente. Tais padrões não oferecem respostas adequadas sobre como alocar funcionalidades à releases para garantir o máximo valor de negocio.

### Estratégia(s) proposta(s)

A proposta usa uma abordagem de planejamento híbrido que faz uso da inteligência computacional (A Ciência do planejamento de Release) e do conhecimento e experiência de especialistas humanos (A Arte do planejamento de Release).

#### A Arte do Planejamento de Release

A arte do planejamento de release foca na intuição humana, comunicação e capacidades humanas de decidir que funcionalidade será selecionada para cada release. Uma justificação para esta abordagem é a crença que o planejamento de release seja um problema mal definido, ou seja, não é claro qual é exatamente o problema, tampouco a sua solução. Um outro motivo para tratar o planejamento de release como uma arte é a falta de ênfase no processo, que pode ser intencional ou pela falta de maturidade no processo.

Até mesmo em ambientes maduros (em termos de planejamento), o planejamento de release é feito de forma informal. As decisões de release são feitas tentando balancear os recursos disponíveis com os interesses dos stakeholders. Entretanto o crescimento do número de release, funcionalidades e de stakeholders torna o planejamento manual uma tarefa cada vez mais complexa.

#### A Ciência do Planejamento de Release

A ciência do planejamento de release é baseada na premissa que o problema pode ser (pelo menos aproximadamente) formalizado.
A formalização leva em consideração os seguintes pontos:

* **Variáveis de decisão**: Um conjunto de funcionalidades pode estar relacionado a novos incrementos, correção de defeitos, ajuste de requisito dos clientes. O objetivo é alocar as funcionalidades a um número K de opções de releases.
* **Dependência de funcionalidades**: Há uma variedade de dependências entre funcionalidades, entretanto a formulação levará em conta dependências de acoplamento (duas funcionalidades dependem uma da outra) e relação de precedência.
* **Restrição de recursos**: As restrições estão relacionadas a diferentes tipos de recursos, seja orçamento ou esforço a ser consumido. Tais restrições acabam limitando as capacidades de cada tipo de recurso.
* **Stakeholders**: É a importancia estratégica de cada stakeholder, possui um peso diferente para a ordem de prioridade de cada um deles.
* **Priorização de funcionalidades**: Na formulação proposta, a priorização de funcionalidades pode ser exposta em relação a valor e urgência.
* **Função objetivo**: Tipicamente, o objetivo é uma mistura de diferentes aspectos como valor, urgência, risco, satisfação ou retorno do investimento. Para o modelo foi proposto a soma da média ponderada de satisfação dos prioridades dos stakeholders por todas as funcionalidades alocadas ao release k.

De acordo com a proposta o objetivo é a maximização da função `$F(x)$`, que é dada por:

    $F(x) = \sum_{k=1}^{K} \sum_{i=1}^{x(i)=k} WAS(i,k)$
    $WAS(i,k) = \xi(k) [\sum_{p=1}^{q} \lambda(p) value(p,i) urgency(p,i,k)]$

Sujeito a

    $\sum_{i=1}^{x(i)=k} r(i,t) \leq Cap(k,t)$

Para todas releases `$k$` e recursos tipo `$t$`.

A formulação dada constitui em um problema de Programação Linear Inteira, todos os objetivos e restrições são lineares e as variáveis são inteiras. Este tipo de problema é da classe dos mais difíceis problemas computacionais.

Entretanto a estrutura do problema é especializada e permite a aplicação de técnicas mais eficientes. A solução adotada é baseada na solução de uma sequência de problemas de programação linear sem condições inteiras. Estes problemas *relaxados* podem ser solucionados de maneira eficiente. Esta abordagem é combinada com heurísticas para acelerar o processo e gerar um conjunto de de soluções boas o suficiente.

#### A Arte e Ciência do Planejamento de Release

As duas abordagens não são contraditórias e sim complementares. Enquanto a Arte encontra grandes dificuldades a medida que os fatores considerados aumentam, a parte da Ciência lida melhor com a complexidade, mas não tem capacidade de codificar o problema como uma mente de um tomador de decisões humano.

A proposta então é um processo contínuo de planejamento e replanejamento, ao invés de apenas um plano para o problema, uma sequencia de problemas é resolvido, gerando um conjunto de soluções 'suficientemente boas'. Estas soluções são apresentadas a um tomador de decisões humano que avalia as alternativas baseados na experiência e familiaridade com o contexto do problema. As três fases do processo de planejamento são:

* **Modelagem (Fase 1)**: Foca na formalização do problema, transforma um problema dinâmico do mundo real e o torna adequado para soluções baseadas em inteligência computacional.
* **Exploração (Fase 2)**: É o plano de geração da solução, baseada na formulação da fase de modelagem. Para o problema foi proposto um algoritmo especializado de programação inteira para explorar o espaço de soluções e gerar soluções alternativas.
* **Consolidação (Fase 3)**: As soluções computacionalmente geradas são apresentadas para um tomador de decisão para avaliação. O tomador de decisão deve ser capaz de analisar as soluções propostas e tomar decisões que contribuirão com o entendimento do problema e podem resultar em modificações de algumas partes do modelo proposto. Tais decisões diminuem a complexidade do problema para a próxima iteração e assim por diante.

### Validação

Um projeto de amostra foi proposto com as seguintes caracteristicas:

* 15 funcionalidades
* 2 releases (e suas importâncias)
* 2 stakeholders (e suas importâncias)
* atribuções de peso e valor das funcionalidades peloes stakeholders
* 4 tipo de recursos envolvidos
* 8 restrições (3 de acoplamento e 5 de dependência)

### Resultados

Assumindo que o plano determinado está entre os 95% e os 100% do total da melhor função objetivo possível, pode-se observar que o planejamento das duas releases são estruturalmente diferentes, o que dá mais flexibilidade para um tomador de decisão agir.

## Avaliação

### Originalidade

Embora não tenha utilizado uma formulação original, a formulação para o problema foi extendida de modo que possa haver uma maior flexibilidade no número de releases futuras a serem planejadas, além de manter a iteração humana durante o processo de otimização, aliando embasamento técnico a experiência de um tomador de decisão.

### Qualidade

O autor usou de definições bem embasadas, para justificar a importância e complexidade inerente do problema do planejamento de releases e conseguiu expressar bem a dificuldade do problema e a extensão sugerida na sua formulação. Embora tenha uma validação e apresentação de resultados muito fracos.

### Relevância

Em termos de formulação, houve um incremento da formulação original no que diz respeito ao número de releases.

### Apresentação

Segue uma progressão de ideia razoável, mas não formula nem separa de forma clara as principais seções do artigo. Ainda possui uma fraca validação e descrição de resultados.

### Pontos Positivos

* Apresentação de um problema difícil com muitas restrições envolvidas.
* Apresentar o fator humano como um diferencial.

### Pontos Negativos

* Baixo foco na resolução do problema.
* Falta de uma melhor validação de resultados.
