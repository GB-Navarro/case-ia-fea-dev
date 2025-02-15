O K-means é uma técnica de clusterização, ou seja, uma técnica de aprendizado não supervisionado que visa dividir um conjunto de dados em grupos (clusters) baseados em suas similaridades. O objetivo principal do K-means é minimizar a variação dentro dos clusters (a soma dos quadrados das distâncias entre cada ponto e o centro do cluster) enquanto maximiza a diferença entre clusters.
## Como funciona o K-means ?
    
1.  **Definição do número de clusters ($k$):**  
    
	    Começamos escolhendo o número de clusters que queremos identificar nos dados. Esse é o parâmetro k, que dá nome ao método. A escolha de k pode ser feita empiricamente ou por meio de métodos como o "cotovelo" (explicado mais adiante).
2. **Inicialização dos centróides:**  
    
	    Selecionamos k pontos iniciais (centróides) aleatoriamente no espaço dos dados. Esses pontos serão usados como as sementes para formar os clusters iniciais.
    
3. **Atribuição de pontos aos clusters:**  
    
	    Para cada ponto do conjunto de dados, calculamos sua distância para cada centróide (geralmente usando a distância euclidiana). O ponto é atribuído ao cluster cujo centróide estiver mais próximo.
    
4. **Recalcular os centróides:**  
    
	    Depois que todos os pontos forem atribuídos a clusters, recalculamos os centróides. Isso é feito tirando a média das coordenadas de todos os pontos pertencentes a um cluster.
    
5. **Iteração:**  
    
	    Repetimos os passos 3 e 4 até que os centróides se estabilizem (ou seja, não mudem significativamente entre as iterações) ou até atingir um número máximo de iterações definido previamente.

## **Como sabemos o melhor número de clusters?**

Um dos métodos mais populares para determinar o valor ideal do parâmetro $k$ é o **método do cotovelo**. Entretanto, existem outras abordagens igualmente eficazes, como o **coeficiente de silhueta**, a **gap statistic** e o **índice de Davies-Bouldin (DBI)**, cada uma oferecendo diferentes perspectivas para avaliar a qualidade dos clusters formados. Por enquanto, vamos nos concentrar no primeiro método citado.

**Método do Cotovelo (Elbow Method):**
    
	1. Calculamos e plotamos a evolução da soma das variâncias dentro dos clusters para diferentes valores de k (essa soma geralmente diminui à medida que aumentamos k, pois mais clusters resultam em grupos menores e mais coesos).
	
	2. O ponto em que a redução na soma de variâncias começa a desacelerar significativamente (formando um "cotovelo" no gráfico) é considerado o melhor valor de k (segundo o método em questão).

## **Importante:**

	- O K-means funciona melhor quando os clusters são aproximadamente esféricos, têm tamanhos semelhantes e não possuem sobreposição significativa.
    
	- A escolha inicial dos centróides pode afetar o resultado. Métodos como o K-means++ ajudam a melhorar essa inicialização, escolhendo os pontos iniciais de forma mais informada.