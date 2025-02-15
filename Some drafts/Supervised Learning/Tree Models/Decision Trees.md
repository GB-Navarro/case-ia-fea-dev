
As **Decision Trees** (Árvores de Decisão) são estruturas amplamente utilizadas em machine learning, tanto para tarefas de classificação quanto de regressão. Elas funcionam como modelos hierárquicos, onde cada nó representa uma decisão baseada em uma condição lógica, e os dados são direcionados por essas condições ao longo das ramificações da árvore. Ao final, os resultados são representados nas folhas, que fornecem a classe ou o valor predito.

### Estrutura de uma Árvore de Decisão

- **Raiz (Root)**: 

		É o ponto inicial da árvore, onde os dados começam a ser processados. Representa o nó principal e a condição inicial de divisão.
		
 - **Nós Internos (Internal Nodes)**: 
 
		São os pontos intermediários onde os dados são divididos com base em condições específicas, como "a variável x é maior que um certo valor?".

- **Folhas (Leaves)**: 

		São os nós finais da árvore, que contêm a saída do modelo. No caso de uma **Classification Tree**, cada folha corresponde a uma classe. Já em uma **Regression Tree**, as folhas contêm valores numéricos.

As árvores de decisão geralmente são binárias, ou seja, cada nó interno divide os dados em dois grupos: um correspondente à condição verdadeira e outro à condição falsa. Isso facilita a navegação e a interpretação do modelo.


### Combinação de Variáveis

Um aspecto interessante das árvores de decisão é sua capacidade de lidar simultaneamente com variáveis numéricas e categóricas. Por exemplo, uma ramificação pode dividir os dados com base em uma variável numérica $(x>10)$, enquanto outra ramificação pode depender de uma variável categórica $(y∈ \{A,B\})$. Isso possibilita um modelo adaptado a conjuntos de dados heterogêneos.

### Um modelo simples

As **árvores de decisão** são consideradas simples de entender e modelos altamente explicáveis devido às seguintes características:

###### **Representação Gráfica Intuitiva**

Árvores de decisão são apresentadas de forma hierárquica, com cada nó representando uma decisão ou condição lógica. Essa estrutura é fácil de visualizar e acompanhar, mesmo para quem não tem formação técnica. Além disso,  o processo de tomada de decisão é semelhante ao raciocínio humano: "Se a condição $X$ é verdadeira, siga este caminho; caso contrário, siga aquele caminho."
###### **Transparência no Processo de Decisão** 

As regras geradas pela árvore podem ser inspecionadas diretamente. Isso significa que é possível entender claramente quais variáveis influenciam cada decisão e como essas variáveis interagem. Por exemplo, em uma árvore construída para prever o preço de imóveis, pode-se identificar que "o número de quartos" ou "a localização" são os fatores mais importantes para a previsão.

###### **Explicação Simples para Usuários Não Técnicos**
	
As árvores de decisão permitem explicar previsões a um público leigo de maneira acessível. Um gerente, por exemplo, pode entender facilmente que "clientes com idade acima de 30 anos e renda maior que R$ 5.000 têm maior probabilidade de comprar o produto."

 ###### **Interpretação Clara das Folhas**

As folhas da árvore mostram claramente o resultado final de cada caminho. Isso elimina a necessidade de compreender cálculos matemáticos complexos ou transformações internas que ocorrem em modelos mais sofisticados, como redes neurais.

###### **Detecção Automática de Importância de Variáveis**
		
Durante o treinamento, a árvore seleciona as variáveis mais relevantes para as decisões. Isso ajuda a identificar quais fatores têm mais impacto no problema em questão, trazendo mais insights sobre os dados.

###### `​`

Essas propriedades tornam as árvores de decisão ferramentas valiosas, especialmente em cenários onde a transparência e a confiança no modelo são essenciais, como em diagnósticos médicos, análises financeiras e tomada de decisões estratégicas.

### O impacto limitado dos outliers em Árvores de Decisão

Em **árvores de decisão**, podemos dizer que o impacto dos outliers é limitado, isso refere-se ao fato de que, embora esses valores extremos possam afetar as divisões em alguns casos, o impacto geral sobre o modelo não é tão forte quanto em outros tipos de modelos, como regressões lineares. Isso ocorre por algumas razões:

-  **Divisão em binários**: As árvores de decisão tomam decisões com base em condições simples (por exemplo, "X > 10?"). Mesmo que um dado valor seja muito alto ou muito baixo (um outlier), ele pode ser tratado isoladamente em uma ramificação específica sem que isso afete significativamente a estrutura global da árvore. O modelo pode simplesmente separar esse outlier em uma folha própria ou em uma ramificação muito específica, o que ajuda a limitar seu impacto no modelo como um todo.
    
-  **Resistência a outliers**: Diferente de modelos que ajustam uma equação para todos os pontos de dados, as árvores de decisão dividem os dados em subconjuntos baseados nas características mais importantes. Isso significa que, se um outlier não altera as divisões principais da árvore (por exemplo, se ele estiver em uma região onde os dados são homogêneos), ele terá um impacto limitado na forma da árvore e na capacidade de previsão do modelo.
    
-  **Robustez**: Como as árvores de decisão se concentram em divisões sequenciais baseadas em características, um outlier pode ser simplesmente classificado de maneira separada, sem impactar o comportamento de outros dados. Em comparação com modelos lineares, onde um único outlier pode distorcer completamente a linha de ajuste, as árvores de decisão são mais robustas porque não tentam "encaixar" todos os dados em uma única linha ou função contínua.
    

Apesar disso, **outliers extremos** podem levar a uma maior **complexidade** na árvore (por exemplo, aumentando a profundidade ou criando divisões desnecessárias), o que pode resultar em **overfitting**. Por isso, técnicas como **poda**, **limitação de profundidade** e **ajuste de parâmetros** podem ser usadas para garantir que a árvore de decisão continue generalizando bem, sem ser excessivamente influenciada por esses valores atípicos.

### O problema do Overfitting 

Um dos principais desafios ao construir árvores de decisão é o **overfitting** (sobreajuste). Isso ocorre quando o modelo é tão complexo que começa a se ajustar demais aos dados de treinamento, capturando até mesmo o "ruído" ou as variações aleatórias nos dados, em vez de padrões gerais. Como resultado, a árvore de decisão pode ter um desempenho muito bom nos dados de treinamento, mas falhar ao generalizar para novos dados.

Em uma árvore de decisão, o overfitting pode ocorrer quando a árvore é construída com profundidade excessiva, ou seja, quando ela continua dividindo os dados até o ponto em que cada folha contém apenas uma instância de dados ou poucas instâncias. Isso leva a um modelo que é extremamente sensível a pequenas variações nos dados de entrada e pode não ser robusto o suficiente para fazer previsões precisas em dados não vistos.

#### Como Evitar o Overfitting?

Existem várias técnicas para evitar o overfitting em árvores de decisão:

- **Poda (Pruning)**: A poda é um processo no qual removemos alguns nós da árvore após ela ter sido construída. Isso é feito para simplificar a árvore e reduzir sua complexidade. Existem duas abordagens principais para poda:
    
	    Poda Prévia (Pre-pruning): Durante o processo de construção da árvore, podemos limitar a profundidade máxima da árvore ou o número mínimo de instâncias em um nó, impedindo que a árvore cresça demais.
	    
	    Poda Pós-Construção (Post-pruning): Depois que a árvore é construída, podemos revisar seus nós e remover aqueles que não contribuem significativamente para a precisão do modelo, ou seja, que não melhoram a generalização do modelo.
    
-  **Limitação da Profundidade da Árvore**: Limitar a profundidade da árvore significa restringir o número máximo de divisões que ela pode realizar. Árvores muito profundas têm mais chances de se ajustar excessivamente aos dados de treinamento, capturando padrões específicos e ruídos. Controlando a profundidade, garantimos que a árvore seja mais simples e mais capaz de generalizar.
-  **Número Mínimo de Instâncias por Nó**: Estabelecer um número mínimo de instâncias que devem estar presentes em cada nó antes de permitir uma divisão também ajuda a evitar o overfitting. Se o número de instâncias for muito pequeno em alguns nós, isso pode indicar que a árvore está se ajustando demais a detalhes específicos dos dados de treinamento.
    
-  **Limitação do Número de Ramos**: Limitar o número máximo de ramificações em cada nó pode impedir que a árvore cresça de forma descontrolada. Isso pode ser feito estabelecendo um limite para o número máximo de valores distintos que uma feature pode ter para ser considerada para uma divisão.
    
-  **Uso de Conjuntos de Dados de Validação**: Utilizar conjuntos de dados de validação durante o treinamento ajuda a monitorar o desempenho do modelo em dados não vistos, permitindo interromper o treinamento antes que o overfitting ocorra.
    

Essas técnicas ajudam a garantir que a árvore de decisão seja capaz de generalizar bem, ou seja, fazer previsões precisas não apenas nos dados com os quais foi treinada, mas também em novos dados. Ao controlar o crescimento excessivo da árvore e evitar a captura de padrões irrelevantes, conseguimos um modelo mais robusto e eficiente.
### Classificação e Regressão

Quando as **Decision Trees** classificam dados em categorias, elas são chamadas de **Classification Trees**. Por exemplo, ela pode decidir se um cliente é ou não elegível para um cartão de crédito. Por outro lado, quando o objetivo é prever valores numéricos, como o preço de uma casa, as árvores são chamadas de **Regression Trees**.

### Ensemble Learning e Decision Trees

As **decision trees** são amplamente utilizadas em técnicas de Ensemble Learning devido às suas características únicas que as tornam ideais como modelos base. Por serem modelos simples, capazes de capturar relações complexas nos dados, mas também altamente sensíveis a variações no conjunto de treinamento, elas se beneficiam significativamente ao serem combinadas em um ensemble. Dois dos métodos de ensemble mais conhecidos que utilizam decision trees são o Bagging e o Boosting, cada um com abordagens distintas para melhorar o desempenho.

### Bagging e Random Forest

O **bagging** (Bootstrap Aggregating) busca reduzir a **variância** combinando várias árvores independentes, cada uma treinada em diferentes subconjuntos de dados gerados por **amostragem com reposição**. Ao combinar as previsões dessas árvores, seja por votação (em problemas de classificação) ou média (em regressão), o modelo final se torna mais robusto e menos suscetível a overfitting.

O Random Forest é uma variação poderosa do bagging aplicada especificamente às decision trees. Além da amostragem dos dados, ele introduz uma camada adicional de aleatoriedade: em cada nó da árvore, apenas um subconjunto aleatório de atributos é considerado para encontrar a melhor divisão. Isso torna as árvores do ensemble mais diversificadas, reduzindo ainda mais a correlação entre elas e melhorando a precisão do modelo.

### Boosting e AdaBoost

Já o **boosting** tem como objetivo reduzir o **viés** do modelo. Nesse método, as árvores são treinadas sequencialmente, e cada novo modelo corrige os erros cometidos pelos anteriores. Uma das implementações mais conhecidas é o AdaBoost (Adaptive Boosting)**, que combina decision trees simples, geralmente **stumps** (árvores com apenas um nível), em um modelo final mais forte. Após cada iteração, AdaBoost ajusta os pesos das amostras, aumentando a influência das que foram mal classificadas. Assim, as próximas árvores focam nas áreas mais difíceis dos dados.
