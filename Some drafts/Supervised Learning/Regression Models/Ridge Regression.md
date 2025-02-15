
A **Ridge Regression ou L2 regularization** é uma técnica de regularização aplicada em modelos de regressão linear que visa melhorar a capacidade de generalização do modelo. Em cenários onde a regressão linear simples se adapta muito bem aos dados de treinamento (overfitting), o modelo tende a capturar ruídos ou variações específicas dos dados, resultando em alta variância e baixo viés. Isso pode levar a desempenhos insatisfatórios nos dados de teste.

A principal ideia da Ridge Regression é introduzir um pequeno viés no modelo para reduzir sua variância, promovendo uma melhor generalização. Isso é feito adicionando um termo de penalização à função de custo original. Esse termo penaliza os coeficientes elevados da regressão linear, restringindo-os e suavizando o modelo. O equilíbrio entre o erro nos dados de treinamento e o viés induzido pela regularização é controlado por um hiperparâmetro, frequentemente chamado de $\lambda$.

**Para ilustrar, imagine uma situação onde a regressão linear ajusta perfeitamente uma reta nos dados de treinamento, resultando em previsões precisas para esses dados. No entanto, ao testar em novos dados, o modelo apresenta um desempenho insatisfatório devido à sua alta variância. A Ridge Regression pode suavizar essa curva, ajustando-a para ser menos sensível a flutuações nos dados de treinamento, o que permite que ela generalize melhor em novos conjuntos de dados.**

Além disso, a Ridge Regression é particularmente útil para previsões de longo prazo. Em contextos onde os dados podem ser ruidosos ou onde existe colinearidade entre variáveis preditoras, ela ajuda a estabilizar as estimativas dos coeficientes, evitando que o modelo se torne instável ou exageradamente dependente de determinadas variáveis. Isso resulta em previsões mais confiáveis e robustas ao longo do tempo.

### Como funciona a Ridge Regression

De modo geral, o que muda de uma **Linear Regression** comum para uma **Ridge Regression** é que, em uma regularização L2 o objetivo é minimizar a seguinte função de custo:

$$
	J(\beta) = \sum\limits_{i=1}^{n}(y_{i} - \hat{y}_{i})^{2} + \lambda \sum\limits_{j=1}^{p}\beta_{j}^{2}
$$


Enquanto na regressão linear simples queremos minimizar apenas

$$
	J(\beta) = \sum\limits_{i=1}^{n}(y_{i} - \hat{y}_{i})^{2} 
$$

Onde:

- $\sum\limits_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}$: Soma dos quadrados dos resíduos, ou seja, o erro padrão de uma regressão linear.
- $\lambda$: Hiperparâmetro que controla a força da penalização. Quanto maior o valor de $\lambda$, maior a penalização sobre os coeficientes.
- $\sum\limits_{j=1}^{p}\beta_{j}^{2}$​: Penalização L2, que é a soma dos quadrados dos coeficientes de regressão.

**Principais características:**

- Penaliza grandes valores de $\beta_{j}$​, forçando os coeficientes a serem menores.
- Não elimina variáveis completamente (os coeficientes raramente chegam a zero).
- Funciona bem em situações em que há multicolinearidade (forte correlação entre variáveis independentes), porque estabiliza os coeficientes.

### Por que a Regressão Ridge não chega a zerar os coeficientes ?

- A Ridge utiliza a penalização L2, isto é, a soma dos quadrados dos coeficientes $\sum\limits_{j=1}{p}B_{j}^{2}$ como penalização.
- A função de penalização L2 tem forma de uma **esfera** em um espaço bidimensional, com contornos suaves.
- Como não há "cantos" na penalização L2, os coeficientes são reduzidos (encolhidos), mas não forçados exatamente a zero.