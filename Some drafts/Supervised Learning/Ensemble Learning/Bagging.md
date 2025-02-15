

**Bagging** *(ou Bootstrap Aggregating)* é uma técnica de aprendizado de máquina usada para melhorar a precisão e a estabilidade de modelos preditivos. É uma das abordagens mais populares de ensemble learning e funciona combinando previsões de múltiplos modelos treinados de forma independente. Vamos entender em detalhes como ela funciona, por que é eficaz e onde é amplamente aplicada.

### A intuição por trás do Bagging

A principal ideia do **Bagging** (Bootstrap Aggregating) é reduzir a **variância** de modelos preditivos, um dos componentes fundamentais no tradeoff entre viés e variância. Modelos como árvores de decisão são suscetíveis a variações nos dados de treinamento, o que pode resultar em previsões altamente instáveis quando os dados apresentam pequenas mudanças. Esse comportamento é característico de modelos com baixa tendência ao viés, mas alta variância.

O bagging combate essa instabilidade ao treinar vários modelos em subconjuntos ligeiramente diferentes do conjunto de dados original, criados por meio de **amostragem com reposição**. Esses modelos base, embora individualmente instáveis, capturam diferentes aspectos dos dados. Ao combinar suas previsões — geralmente por média (em regressão) ou votação majoritária (em classificação) —, o bagging reduz a variância total do modelo final, suavizando flutuações individuais e aumentando a estabilidade.

Esse processo reduz a sensibilidade a ruídos no conjunto de treinamento sem aumentar significativamente o viés, resultando em um modelo mais robusto e com melhor capacidade de generalização. Assim, o bagging é particularmente útil em cenários onde a redução da variância é crítica para melhorar o desempenho preditivo.

### O Processo em mais detalhes

1. **Amostragem com Reposição (Bootstrap):**
    
	    - O conjunto de dados original é usado para criar vários subconjuntos através de amostragem aleatória com reposição.
	    
	    - Cada subconjunto terá o mesmo tamanho do conjunto de dados original, mas algumas amostras podem aparecer várias vezes, enquanto outras podem ser ignoradas.
	    
	    - Isso garante que cada modelo base veja uma versão ligeiramente diferente dos dados, promovendo diversidade.
2. **Treinamento de Modelos Base:**
    
	    - Para cada subconjunto criado, um modelo base independente é treinado. Normalmente, usa-se algoritmos suscetíveis a alta variância, como árvores de decisão.
3. **Combinação das Previsões:**
    
	    - Após o treinamento, as previsões de todos os modelos base são combinadas. A forma de combinação depende do tipo de problema:
	
        - Para regressão: A média das previsões dos modelos é utilizada.
    
        - Para classificação: É feita uma votação majoritária, onde a classe mais frequentemente predita pelos modelos base é escolhida.

### Principais vantagens de usar Bagging

1. **Reduz a variância:**
    
	    - Ao combinar previsões de modelos treinados em amostras diferentes, as flutuações e os erros individuais tendem a se cancelar, resultando em uma previsão mais estável.
2. **Diminui a chance de Overfitting:**
    
	    - Apesar de modelos complexos, como árvores de decisão, poderem se ajustar excessivamente aos dados de treinamento, o bagging reduz essa tendência ao diversificar os dados usados no treinamento.
3. **Gera um modelo mais robusto e generalizado:**
    
	    - O modelo combinado é menos propenso a se ajustar demais a peculiaridades específicas do conjunto de treinamento original, tornando-o mais capaz de generalizar para novos dados.

### .

O Random Forest é um exemplo amplamente conhecido de Bagging aplicado.
