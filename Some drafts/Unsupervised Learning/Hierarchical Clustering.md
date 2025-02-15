Clusters hierárquicos são uma técnica de clusterização que organiza os dados em uma estrutura de árvore, conhecida como **dendrograma**. Diferentemente de métodos como o K-means, que requerem um número fixo de clusters ($k$) previamente definido, a clusterização hierárquica permite explorar os dados em múltiplos níveis, agrupando elementos semelhantes em etapas sucessivas até que todos os elementos estejam conectados em um único grupo.

O agrupamento é guiado por uma métrica de similaridade ou distância, que quantifica o quão próximos ou diferentes os elementos estão uns dos outros. Métricas comuns incluem a **distância euclidiana**, usada para medir a proximidade em termos de espaço geométrico, e a **distância de Manhattan**, que considera a soma das diferenças absolutas entre as coordenadas dos elementos. Também é possível usar medidas baseadas em estatísticas, como a **correlação**, que avalia o alinhamento entre os padrões dos dados.

Essa técnica pode ser realizada de duas maneiras principais: **aglomeração** e **divisão**. No método **aglomerativo** (ou bottom-up), cada elemento começa como um cluster individual. A cada etapa, os dois clusters mais semelhantes, com base na métrica de similaridade escolhida, são combinados até que todo o conjunto de dados forme um único cluster. Já no método **divisivo** (ou top-down), o processo é invertido: todos os elementos começam em um único cluster e, a cada etapa, este é dividido em dois, com base nas maiores diferenças entre seus elementos.

### Dendogramas

Um elemento essencial da clusterização hierárquica é o **dendrograma**, uma representação gráfica que organiza a hierarquia dos clusters. Ele se assemelha a uma árvore invertida, onde as folhas na base representam os elementos individuais do conjunto de dados, enquanto os ramos mostram como os clusters foram formados, conectando elementos ou grupos em níveis superiores. A altura dos ramos indica a distância ou dissimilaridade entre os clusters combinados: ramos mais baixos representam elementos mais semelhantes, enquanto ramos mais altos indicam maior diferença. Essa visualização é especialmente útil para decidir o número de clusters, permitindo "cortar" o dendrograma em diferentes níveis e testar agrupamentos sem a necessidade de uma definição inicial.

### Clusters hierárquicos e mapas de calor

Clusters hierárquicos também são frequentemente associados a **heatmaps**, uma combinação poderosa para analisar grandes conjuntos de dados. Enquanto o heatmap exibe os valores dos dados em uma matriz colorida, destacando padrões visuais, a clusterização hierárquica organiza as linhas e colunas dessa matriz com base na similaridade, tornando os padrões ainda mais evidentes.

### Como um cluster hierárquico é criado ?

1. Escolha de uma métrica de similaridade ou distância

		O primeiro passo é determinar como a similaridade entre dois elementos será medida. Algumas métricas comuns incluem:

		1. Distância Euclidiana: Mede a distância linear entre dois pontos.
			
		2. Distância de Manhattan: Soma das diferenças absolutas entre as coordenadas dos pontos.
			
		3. Correlação: Mede a similaridade baseada na relação estatística entre variáveis.

2. Escolha do critério de aglomeração *(linkage method)*

		Depois de calcular a similaridade entre pares de pontos, precisamos decidir como combinar os clusters. Métodos comuns de "linkagem" incluem:

		1. "Linkagem" simples (single linkage): Usa a menor distância entre dois elementos, um de cada cluster.

		2. "Linkagem" completa (complete linkage): Usa a maior distância entre dois elementos, um de cada cluster.

		3. "Linkagem" média (average linkage): Usa a média das distâncias entre todos os pares de elementos de dois clusters (isto é, usa o centroides de cada um dos clusters).

		4. Ward’s Method: Minimiza a soma dos quadrados das distâncias dentro dos clusters.

3. Iniciar os clusters

		Inicialmente, cada ponto do conjunto de dados é tratado como um cluster individual (no caso de clusters aglomerativos). Portanto, se há $n$ pontos, começam como $n$ clusters.

4. Agrupamento iterativo

		O algoritmo repete os seguintes passos até que todos os pontos sejam agrupados em um único cluster (no caso de clusters aglomerativos):

		1. Identificar os dois clusters mais semelhantes: Isso é feito com base na métrica de distância e no critério de aglomeração escolhido.

		2. Combinar esses clusters em um único grupo: Eles se tornam um novo cluster no nível superior da hierarquia.

		3. Atualizar as distâncias: Recalcula as distâncias entre o novo cluster e os clusters restantes.

5. Construção do dendrograma

		À medida que os clusters são combinados, os dendrogramas são criados.