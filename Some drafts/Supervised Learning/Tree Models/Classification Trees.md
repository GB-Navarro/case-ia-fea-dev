As **árvores de classificação** são um tipo de árvore de decisão projetada para categorizar dados em diferentes classes. Elas funcionam dividindo os dados em subconjuntos baseados em condições específicas, representadas por regras de "se-então". O objetivo final é determinar a classe mais provável de um dado, com base nos valores de suas características. As folhas da árvore representam as classes finais, enquanto os nós internos contêm condições que guiam o processo de decisão.

Por exemplo, em um modelo para classificar e-mails como "spam" ou "não spam", os nós internos podem verificar condições como "o e-mail contém a palavra 'promoção'?" ou "há mais de 3 links?". Esses critérios ajudam a separar os e-mails em grupos homogêneos, até que uma decisão final seja tomada em cada folha.

## O conceito de impureza

A **impureza** em uma árvore de decisão é uma medida da heterogeneidade ou mistura das classes em um conjunto de dados em um determinado nó da árvore. Ela quantifica o grau de incerteza associado à distribuição das classes no nó, ou seja, o quão "confuso" ele é em termos de pertencer predominantemente a uma única classe. Quanto menor a impureza, mais homogêneo é o nó e mais confiante o modelo pode estar ao classificar uma instância que atinge aquele nó.

**Por que a impureza é importante ?**

A impureza é usada durante o treinamento para determinar as condições de divisão nos nós. O objetivo de uma árvore de classificação é criar nós que sejam os mais homogêneos possíveis em relação às classes. Isso significa que, após cada divisão, os subconjuntos resultantes devem ter impureza reduzida em comparação com o nó original. Essa redução na impureza é conhecida como **ganho de informação** ou **redução de Gini**, dependendo do critério escolhido.

#### Quantificando a impureza de um nó

##### **Índice de Gini**

O **Índice de Gini** mede a probabilidade de escolher uma instância aleatória de um nó e classificá-la incorretamente, caso a classificação fosse feita com base na distribuição das classes no nó. Ele varia de 0 (nó completamente puro, com apenas uma classe) a um valor máximo que depende da distribuição das classes.

###### Calculando o Índice de Gini para valores categóricos

**Fórmula para calcular o Índice de Gini de um nó**:

$$
	G = 1 - \sum\limits_{i = i}^{k} p_{i}^{2}
$$
Onde:
- $p_{i}:$ *proporção de instâncias na classe* $i$.
- $k:$ número total de classes.

*Obs: Uma instância de classe é, em termos simples, um item que é classificado dentro de uma certa categoria.*

**Interpretação**:

- Quando todas as instâncias no nó pertencem a uma única classe, $p_{i} = 1$ para essa classe, e o índice de Gini é $0$ (máxima pureza).
- Quando as classes estão uniformemente distribuídas, o índice de Gini é maior, refletindo maior impureza.

**Exemplo**: Se um nó contém 60% de instâncias da classe $A$ e 40% da classe $B$:

$$
	G = 1 - (0,6^{2} + 0,4^{2}) = 1 - (0,36 + 0,16) = 0,48
$$
Caso o nó possua ramificações, o seu **Índice de Gini** será dado pela média ponderada dos Índices de Gini de seus dois nós filhos, ou seja:

$$
G_{total} = (\dfrac{n_{a}}{n_{a}+n_{b}}) \cdot G_{A} + (\dfrac{n_{b}}{n_{a}+n_{b}}) \cdot G_{B}
$$
Onde:
- $G_{A}$ é o Índice de Gini do nó filho $A$
- $G_{B}$ é o Índice de Gini do nó filho $B$ 
- $(\dfrac{n_{a}}{n_{a}+n_{b}})$  e  $(\dfrac{n_{b}}{n_{a}+n_{b}})$ são as proporções de instâncias nas folhas $A$ e $B$, respectivamente.

**Interpretação:**

- Se as duas folhas tiverem uma grande diferença no número de instâncias, a folha com mais instâncias terá um peso maior no índice de Gini final da ramificação.
- Quanto mais homogêneo for um nó filho (ou seja, quanto mais as instâncias de uma única classe estiverem concentradas nesse nó), menor será o índice de Gini desse nó. Isso implica que a impureza do nó filho será reduzida. Como resultado, se ambos os nós filhos forem homogêneos, a ramificação como um todo terá uma impureza menor, o que, por sua vez, reduz a impureza do nó pai e melhora a qualidade da divisão.

###### Calculando o Índice de Gini para valores numéricos
##### Entropia

##### Ganho de informação

## O treinamento de uma árvore de decisão

Durante o treinamento, a árvore de decisão analisa todas as possíveis divisões dos dados e escolhe a condição que resulta na maior redução de impureza. Isso garante que os nós sucessivos sejam cada vez mais homogêneos, ajudando o modelo a separar melhor as classes e melhorar sua capacidade preditiva.

A construção de uma árvore de decisão segue um processo iterativo de divisão dos dados em subconjuntos baseados nas features do conjunto de dados, com o objetivo de minimizar a impureza (ou incerteza) nos nós. Como vimos, uma das maneiras de medir a impureza é o **índice de Gini**, que é utilizado para selecionar as melhores condições de divisão, como "peso > 150g".

##### Passo 1: A Seleção da Raiz

O processo de construção da árvore começa com o conjunto completo de dados, representado por um nó raiz. O objetivo inicial é dividir esse conjunto de dados em dois ou mais subconjuntos que sejam mais homogêneos, ou seja, que contenham instâncias da mesma classe. A seleção de qual feature será usada para essa divisão é feita com base em um critério de **impureza**, como o **Índice de Gini**.

Durante a construção da árvore, calculamos o para cada possível condição de divisão em uma feature *(Como assim para cada possível condição de divisão ? Elas não podem ser infinitas ? - Ver o livro Intr. to Statistical Learning)*, e a condição que resultar no menor índice de Gini será escolhida para dividir o nó.

###### Exemplo:

Suponha que estamos tentando classificar frutas em **maçãs** e **laranjas**, e temos duas features: **$peso$** e **$cor$**. Para calcular o índice de Gini para a feature **$peso$**, testamos várias condições possíveis, como $peso > 150g$, $peso > 100g$, $peso > 200g$, etc. Para cada uma dessas condições, dividimos os dados e calculamos o índice de Gini de cada subconjunto gerado.

- Se a condição $peso > 150g$ gerar um índice de Gini menor (ou seja, um subconjunto mais puro) do que qualquer outra condição de divisão por exemplo, $peso > 100g$, então $peso > 150g$ será a condição que ficará no nó raiz da árvore.

##### Passo 2: Divisão dos Dados nos Nós Filhos

Depois de selecionar a condição que será usada para dividir os dados no nó raiz, por exemplo, $peso > 150g$, o conjunto de dados é dividido em dois subconjuntos: um grupo de instâncias com **$peso > 150g$** e outro com **$peso <= 150g$**. Esses subconjuntos são passados para os **nós filhos** da árvore.

Para cada nó filho, o processo de cálculo do índice de Gini é repetido para as **features restantes**. Para cada feature, diferentes condições são testadas, como "cor = vermelha", "cor = verde", etc., e a condição que resultar no menor índice de Gini será escolhida para dividir o nó. Esse processo é repetido recursivamente para cada novo nó da árvore.

###### Exemplo:

Se o nó à esquerda (com **peso <= 150g**) tiver tanto **maçãs vermelhas** quanto **maçãs verdes**, vamos calcular o índice de Gini para a feature **cor**. Se, por exemplo, a condição "cor = vermelha" resultar em um subconjunto mais homogêneo (ou seja, mais maçãs vermelhas do que verdes), então essa será a condição escolhida para dividir ainda mais esse nó.

A árvore de decisão continuará a se expandir dessa forma, com novas divisões sendo feitas para cada nó, com base na feature que gera a maior pureza nos subconjuntos.

##### Passo 3: Divisão Recursiva dos Nós Filhos

O processo de divisão recursiva continua até que:

- Os subconjuntos nos nós filhos sejam puros (ou seja, todas as instâncias em um nó pertençam à mesma classe).
- Ou até que um critério de parada seja atingido, como o número mínimo de instâncias por nó ou a profundidade máxima da árvore.

Durante esse processo, a árvore continua a calcular o índice de Gini para as condições de divisão em cada nó. Se uma nova divisão gerar uma maior pureza (menor índice de Gini), ela será escolhida. Caso contrário, a árvore de decisão pode parar a divisão, e aquele nó se tornará uma folha.

##### Passo 4: Construção Completa da Árvore

O processo continua até que todos os nós atendam a um critério de pureza ou a árvore alcance um critério de parada, como a profundidade máxima ou o número mínimo de instâncias em um nó. A árvore gerada terá um conjunto de **nós internos**, cada um representando uma divisão dos dados com base em uma feature e uma condição, e **folhas** (nós terminais) que contêm a classe final ou valor para as instâncias que atingiram aquele nó.