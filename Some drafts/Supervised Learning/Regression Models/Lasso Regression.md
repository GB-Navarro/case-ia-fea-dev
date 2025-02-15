A **Lasso Regression ou L1 Regularization** é uma técnica de regularização utilizada em modelos de aprendizado supervisionado, principalmente em modelos de regressão linear. Ela é particularmente útil em cenários com alta dimensionalidade ou quando se deseja realizar seleção de variáveis. 

O objetivo de um modelo **Lasso Regression**  é minimizar a seguinte função de custo:

$$
	J(\beta) = \sum\limits_{i=1}^{n}(y_{i}-\hat{y})^{2}+ \lambda \sum\limits_{j = 1}^{p} |\beta_{j}|
$$

### Principais características:

1. **Penalização L1**:
    
    - A penalização L1 $(\sum\limits_{j=1}{p}|\beta_{j}|)$ incentiva coeficientes menores e pode até reduzi-los exatamente a zero. Isso resulta em um modelo mais simples e interpretável.
    - É ideal para problemas onde se espera que apenas algumas variáveis sejam relevantes.
2. **Seleção de variáveis**:
    
    - Por forçar coeficientes irrelevantes a zero, o Lasso realiza uma seleção automática de variáveis. Esse comportamento ajuda a evitar o overfitting em conjuntos de dados com muitas variáveis independentes.
3. **Controle de complexidade do modelo**:
    
    - O parâmetro $\lambda$ controla a força da penalização. Valores maiores de $\lambda$ aumentam a penalização, resultando em mais coeficientes sendo reduzidos a zero, enquanto valores menores produzem um modelo mais próximo de uma regressão linear padrão.
4. **Aplicação em alta dimensionalidade**:
    
    - É especialmente útil em situações onde o número de variáveis $(p)$ é comparável ou maior que o número de observações $(n)$.

### Por que a regressão Lasso pode zerar coeficientes ?

- A Lasso utiliza função de penalização L1, isto é, a soma dos valores absolutos dos coeficientes $\sum\limits_{j=1}^{p}|B_{j}|$ como penalização.
- A função de penalização L1 tem forma de um **losango** em um espaço bidimensional, com cantos pontiagudos. Esses cantos criam regiões em que os coeficientes tendem a ser exatamente zero.
- Durante a otimização, as restrições impostas pela penalização "empurram" os coeficientes para essas regiões de zero, principalmente se $\lambda$ for suficientemente grande.
### Casos de uso:

	1. Modelos onde algumas variáveis são irrelevantes ou redundantes.
	
	2. Cenários com dados esparsos ou alta dimensionalidade.

	3. Seleção de variáveis interpretável em pesquisas científicas e estudos empíricos.
