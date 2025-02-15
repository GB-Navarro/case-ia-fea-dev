**Ensemble Learning** é uma abordagem de aprendizado de máquina que combina as previsões de vários modelos individuais (geralmente chamados de **modelos base**) para obter um desempenho superior ao que seria possível com um único modelo.

A ideia central é que a combinação de múltiplos modelos "fracos" pode produzir um modelo "forte". Em outras palavras, erros individuais de alguns modelos base podem ser corrigidos por outros, resultando em um modelo final mais robusto e menos suscetível a **overfitting**.

Existem três abordagens principais em **Ensemble Learning**:

-  **Bagging** (_Bootstrap Aggregating_):
	    
		- Nesta abordagem, diversos modelos independentes são treinados em diferentes subconjuntos do conjunto de dados (geralmente criados por amostragem com reposição). As previsões desses modelos são então combinadas, frequentemente por votação ou média. Um exemplo popular é o **Random Forest**, que utiliza bagging com árvores de decisão como modelos base.

- **Boosting**:
    
	    - Aqui, os modelos são treinados de forma sequencial, onde cada modelo subsequente se concentra em corrigir os erros cometidos pelo anterior. Isso resulta em um modelo combinado mais preciso e focado. Exemplos incluem **AdaBoost** e **Gradient Boosting**.

- **Stacking**:

		- Nessa abordagem, os modelos base fazem suas previsões e um segundo modelo, chamado de **meta-modelo**, é treinado para aprender a melhor forma de combiná-las. Essa técnica é especialmente eficaz porque permite explorar diferentes tipos de modelos base e capturar relações complexas entre suas previsões.

Essas técnicas são amplamente utilizadas para melhorar a precisão e a capacidade de generalização, especialmente em problemas complexos e de alta dimensionalidade. 