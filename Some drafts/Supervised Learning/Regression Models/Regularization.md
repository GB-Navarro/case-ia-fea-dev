###  O que é Regularização?

**A regularização é uma técnica utilizada em aprendizado de máquina, mais especificamente em aprendizado supervisionado para melhorar a capacidade de generalização de modelos, especialmente em cenários onde há risco de overfitting.** Lembre-se que o overfitting ocorre quando um modelo se ajusta muito bem aos dados de treinamento, capturando padrões e ruídos específicos, mas apresenta desempenho insatisfatório em dados novos. **A regularização atua adicionando uma penalidade à função de custo do modelo, limitando a complexidade do modelo ou restringindo os valores dos parâmetros estimados.**

#### Intuição e Impacto

A regularização pode ser entendida como uma troca entre viés e variância. Ao adicionar um termo de penalização, estamos aceitando um aumento no viés em troca de uma redução na variância, o que geralmente resulta em um melhor desempenho do modelo em dados não vistos.

**Por exemplo, ao usar Ridge Regression, o modelo é "encorajado" a buscar soluções onde os coeficientes são pequenos, mesmo que isso signifique um ajuste menos preciso nos dados de treinamento. No entanto, isso melhora sua robustez para dados novos, resultando em previsões mais confiáveis.**

### O que a Regularização faz?

**A regularização modifica a função de custo que o modelo tenta minimizar durante o treinamento.** Essa modificação introduz um termo de penalização que aumenta a função de custo à medida que os parâmetros do modelo (como coeficientes de uma regressão linear) se tornam muito grandes ou complexos. Essa penalização tem dois principais efeitos:

1. **Evita Coeficientes Excessivamente Grandes**: Em modelos como regressões lineares e redes neurais, coeficientes muito altos podem indicar que o modelo está superajustado aos dados de treinamento. Regularização restringe os valores dos coeficientes, resultando em modelos mais simples e generalizáveis.
    
2. **Controla a Complexidade do Modelo**: Ao limitar a complexidade, a regularização força o modelo a ser mais "conservador" em suas predições, preferindo soluções mais estáveis, ainda que ligeiramente enviesadas *(em termos de machine learning)*.
    
### Principais tipos de Regularização

Existem diferentes formas de regularização, dependendo de como o termo de penalização é definido:

1. **L2 Regularization (Ridge Regression)**:
    
    - **Adiciona uma penalidade proporcional ao quadrado da magnitude dos coeficientes $(\sum\limits_{i} \beta_{i}^{2}).$**
    - Prefere coeficientes menores, **mas não os torna exatamente zero.**
    - **Indicada para problemas onde todas as variáveis preditoras têm alguma contribuição para o modelo.**
  
2. **L1 Regularization (Lasso Regression)**:
    
    - Adiciona uma penalidade proporcional ao valor absoluto dos coeficientes $(\sum\limits_{i}|\beta_{i}|)$.
    - **Pode zerar completamente alguns coeficientes, realizando seleção de variáveis implicitamente.**
    - **Útil quando se acredita que apenas algumas variáveis são relevantes para o modelo.**
  
3. **Elastic Net**:
    
    - **Combina L1 e L2, permitindo um equilíbrio entre seleção de variáveis e controle da magnitude dos coeficientes.**
  
4. **Regularização em Redes Neurais**:
    
    - **Dropout**: Desativa aleatoriamente algumas conexões entre neurônios durante o treinamento, reduzindo a dependência excessiva de conexões específicas.**
    - **Weight Decay**: Uma forma de L2 regularization aplicada ao treinamento de redes neurais.


### .
Em resumo, no aprendizado supervisionado, a regularização desempenha um papel fundamental, pois, além de melhorar a capacidade de generalização, ela estabiliza o modelo. Isso é especialmente importante em casos de colinearidade, onde variáveis preditoras estão altamente correlacionadas; a regularização ajuda a reduzir a instabilidade nas estimativas dos coeficientes, tornando o modelo mais robusto. Além disso, a regularização controla a complexidade dos modelos, prevenindo o overfitting ao restringir a magnitude dos coeficientes. Por fim, ela pode facilitar a interpretação dos modelos, como no caso da regularização L1, onde algumas variáveis podem ser eliminadas por terem seus coeficientes zerados, resultando em um modelo mais enxuto e fácil de entender.