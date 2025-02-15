
O **Boosting** é uma técnica de aprendizado de máquina dentro do contexto de ensemble learning, cujo objetivo é melhorar o desempenho preditivo ao combinar uma série de modelos "fracos" (modelos que têm desempenho ligeiramente melhor que o aleatório) para formar um modelo "forte". Diferente do Bagging, que treina modelos independentemente, o Boosting constrói os modelos sequencialmente, com cada um tentando corrigir os erros cometidos pelos anteriores.

### A Intuição por Trás do Boosting

O princípio fundamental do Boosting é priorizar os exemplos mal classificados por modelos anteriores. Isso significa que, à medida que os modelos são adicionados, eles se concentram nas instâncias mais difíceis, ajustando o aprendizado para lidar com essas situações. Esse processo resulta em um modelo combinado que é mais preciso e focado.

### Como o Boosting Funciona?

### 1. **Treinamento Inicial**

	- O processo começa com o treinamento do primeiro modelo base (geralmente um modelo simples, como uma árvore de decisão rasa) em todo o conjunto de dados de treinamento.
	
	- Após o treinamento, esse modelo faz previsões, e os erros cometidos são identificados. Cada instância mal classificada é destacada e recebe um peso maior na próxima iteração. Esses pesos representam a "importância" de cada exemplo. Instâncias mais difíceis de prever (mal classificadas) terão pesos mais altos, para que os modelos futuros se concentrem nelas.

### 2. **Foco em Erros**

	- O próximo modelo base é então treinado, mas com os dados ajustados pelos pesos atualizados. Instâncias com maior peso têm mais influência no treinamento, incentivando o novo modelo a corrigir os erros cometidos pelo anterior.
	
    - Por exemplo, se uma instância difícil foi classificada incorretamente no primeiro modelo, ela terá maior impacto no ajuste do segundo modelo. Esse processo continua iterativamente, com cada novo modelo base sendo ajustado para corrigir os erros deixados pelos anteriores.

### 3. **Combinação dos Modelos**

	-Ao final do treinamento, todos os modelos base criados durante as iterações são combinados de forma ponderada para gerar a previsão final.
    
	- A "ponderação" refere-se ao peso atribuído a cada modelo base com base em sua precisão ou desempenho. Modelos mais precisos terão maior influência na previsão final, enquanto os menos precisos terão impacto reduzido. Por exemplo, no AdaBoost, cada modelo recebe um peso que é inversamente proporcional à sua taxa de erro: quanto menor o erro, maior sua contribuição no ensemble.
    
	- Os modelos mencionados são todos os modelos base criados ao longo das iterações. Eles podem ser árvores de decisão, regressões lineares ou qualquer outro algoritmo escolhido como base, dependendo do problema.

No final, o Boosting combina o poder desses modelos sequenciais para criar uma predição robusta que corrige os erros acumulados ao longo do caminho.

### Tipos Populares de Boosting

1. **AdaBoost (Adaptive Boosting)**

		É o algoritmo clássico de boosting e um dos primeiros a ser formalmente introduzidos. O AdaBoost constrói modelos sequencialmente, ajustando o foco em exemplos que foram mal classificados nas iterações anteriores. Cada instância no conjunto de dados recebe um peso inicial igual. Após cada iteração, os pesos das instâncias mal classificadas são aumentados, e os pesos das instâncias corretamente classificadas podem ser reduzidos. Isso força os modelos subsequentes a se concentrarem nos exemplos mais difíceis. A previsão final é uma combinação ponderada dos modelos base, onde o peso de cada modelo é inversamente proporcional à sua taxa de erro.

1. **Gradient Boosting**

		O Gradient Boosting otimiza os modelos base sequencialmente, mas, em vez de ajustar diretamente os pesos das instâncias como no AdaBoost, ele ajusta os modelos para minimizar uma função de perda (por exemplo, erro quadrático médio para regressão ou log-loss para classificação). Cada novo modelo base é treinado para prever os resíduos (erros) do modelo anterior, movendo as previsões em direção ao mínimo da função de perda. Esse processo é análogo ao gradiente descendente em métodos de otimização: os modelos são ajustados iterativamente na direção que reduz o erro mais rapidamente.

	Provavelmente, a  implementações do Gradient Boosting mais utilizada seja a XGBoost (Extreme Gradient Boosting), isso se deve a alguns motivos:

		- É uma implementação otimizada de Gradient Boosting amplamente usada devido à sua velocidade e eficiência. Inclui técnicas como:
    
		- Regularização (para evitar overfitting).
    
		- Processamento paralelo.
    
		- Suporte para missing values.
    
		- É conhecido por seu desempenho superior em competições de machine learning.

3. Stochastic Gradient Boosting

		É uma variante do Gradient Boosting que introduz amostragem aleatória em diferentes partes do treinamento para aumentar a robustez e reduzir o risco de overfitting.
