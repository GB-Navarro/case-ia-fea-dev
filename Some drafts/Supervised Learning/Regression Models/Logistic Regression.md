**Logistic Regression (Regressão Logística)** é uma técnica de aprendizado supervisionado amplamente utilizada para resolver problemas de classificação binária e, em suas extensões, problemas de classificação multiclasse. Apesar do nome, a Regressão Logística não é usada para tarefas de regressão no sentido tradicional (predição de valores contínuos), mas sim para prever a probabilidade de uma amostra pertencer a uma determinada classe.

O modelo é baseado em uma **função logística (ou sigmoide)**, que transforma uma combinação linear das variáveis de entrada em um valor no intervalo $[0,1]$, interpretado como uma probabilidade. **Dessa forma, a Regressão Logística pode ser usada para modelar problemas de classificação onde o objetivo é determinar se uma amostra pertence a uma classe específica (por exemplo, positivo ou negativo).**

## **Uma visão intuitiva da Regressão Logística**

Considere um problema de classificação em que é necessário separar dados em duas categorias, por exemplo, 0 e 1. Uma abordagem inicial poderia ser utilizar modelos lineares, como a regressão linear, para estimar uma fronteira de decisão entre essas classes. No entanto, essa escolha apresenta duas limitações importantes:

1. **Predições fora do intervalo $[0,1]$**: A regressão linear não está restrita ao intervalo de probabilidade. Dependendo dos dados, pode produzir valores negativos ou maiores que 1, o que é incoerente para a interpretação probabilística.
2. **Incapacidade de capturar a natureza probabilística**: Classificação é intrinsecamente um problema probabilístico. Em vez de fornecer uma decisão direta, o modelo deve refletir a probabilidade de cada classe, permitindo interpretações mais robustas.

**A Regressão Logística** resolve esses problemas ao aplicar a função sigmoide à saída de uma combinação linear das variáveis de entrada. A função sigmoide é definida como:

$$
	\sigma(z) = \dfrac{1}{1+e^{-z}}
$$

**Aqui, $z = w^{T}x + b$ é uma combinação linear da variável preditora $x$, com os pesos $w$ e o viés $b$.** Essa transformação comprime os valores de $z$ para o intervalo $[0,1]$, tornando-os interpretáveis como probabilidades.

## Comparação: Ajuste na Regressão Linear vs Regressão Logística

1. **Regressão Linear**:  
    Na regressão linear, ajustamos uma linha reta aos dados minimizando a soma dos erros quadráticos (MSE). Para problemas de classificação, isso significa ajustar uma linha que tenta distinguir as classes. Contudo, esse método apresenta um principal problema, como ele pode  produzir predições fora do intervalo $[0,1]$, como valores negativos ou acima de $1$. Ele acaba por não se alinhar bem com a interpretação probabilística exigida em tarefas de classificação.
    
2. **Regressão Logística**:  
    A regressão logística ajusta a **função sigmoide** aos dados. Em vez de prever diretamente $y$, ela estima $P(y=1∣x)$, que representa a probabilidade da amostra pertencer à classe $1$ dado $x$. O ajuste ocorre maximizando a **verossimilhança**, ou seja, otimizando os parâmetros $w$ e $b$ para que as predições do modelo sejam o mais próximas possíveis das probabilidades observadas nos dados.

Em resumo, a **regressão linear** ajusta uma linha reta aos dados, enquanto a **regressão logística** ajusta uma curva sigmoide. Na regressão linear, os valores previstos podem variar entre $(-\infty, +\infty)$, o que é inadequado para problemas de classificação, pois esses valores não representam probabilidades. Já na regressão logística, as predições são sempre limitadas ao intervalo $[0,1]$, permitindo que sejam interpretadas como probabilidades. **Além disso, as duas técnicas utilizam funções de perda diferentes: a regressão linear minimiza a soma dos erros quadráticos (MSE), enquanto a regressão logística maximiza a log-verossimilhança, otimizando a correspondência entre as probabilidades previstas e as observadas.** Por fim, no que diz respeito à aplicação, a regressão linear é mais adequada para problemas de regressão, enquanto a regressão logística é projetada especificamente para problemas de classificação. 
## **O passo a passo da Regressão Logística**

### 1. **Preparação dos dados**

- **Entrada**: Um conjunto de dados com $N$ amostras e $n$ características, onde cada amostra $x_{i} \in R^{n}$ está associada a um rótulo $y_{i} \in \{0,1\}$ (para classificação binária).
- **Pré-processamento**:
    - Normalize ou padronize as variáveis, especialmente se tiverem escalas muito diferentes.
    - Certifique-se de que os dados estejam livres de valores ausentes ou inconsistências.
### 2. **Definição do modelo**

- O modelo baseia-se em uma combinação linear das variáveis de entrada:

$$
	z = w^{T}x+b
$$

Onde:

- $w$ é o vetor de pesos associados às variáveis.
    
- $b$ é o termo de bias (intercepto).
    
- A combinação linear $z$ é transformada por uma função logística (sigmoide):

$$
	\hat{y}=\sigma(z)=\dfrac{1}{1+e^{-z}}
$$


O valor $\hat{y}$ representa a probabilidade da amostra pertencer à classe $1$ *(Relembrar oque faz com que esse cálculo seja referente à classe 1 e não à classe 0)*.
### 3. **Função de custo**

- A Regressão Logística utiliza a **log-loss** (ou entropia cruzada) como função de custo, que mede a discrepância entre as probabilidades previstas $\hat{y}$ e os rótulos verdadeiros $y$:

$$
	J(w,b) = -\dfrac{1}{N}\sum\limits_{i=1}^{N}[y_{i} \cdot log(\hat{y}_{i}) + (1 - y_{i}) \cdot log(1-\hat{y}_{i})]
$$

Essa função penaliza fortemente predições incorretas, especialmente quando o modelo está muito confiante.

### 4. **Treinamento do modelo**

- **Método de otimização**: O treinamento consiste em minimizar a função de custo $J(w, b)$ ajustando os parâmetros $w$ e $b$. O método mais comum para isso é o **Gradiente Descendente**, que atualiza os parâmetros iterativamente:

$$
	w \leftarrow w - \alpha\dfrac{\partial J}{\partial w},\  b \leftarrow b - \alpha \dfrac{\partial J}{\partial b}
$$

Onde $\alpha$ é a taxa de aprendizado.

- **Regularização**: Para evitar overfitting, é comum adicionar termos de regularização à função de custo, como:
    - **L1 (lasso)**: Promove sparsidade nos pesos $(|w|)$.
    - **L2 (ridge)**: Penaliza grandes valores dos pesos $(w^{2})$.


### 5. **Predição e classificação**

- Durante a predição, o modelo calcula a probabilidade $\hat{y}$ para cada amostra.
- Para classificar uma amostra, utiliza-se um limiar (geralmente 0.5):

### 6. **Avaliação do modelo**

- Métricas comuns para avaliar a performance incluem:
    - **Acurácia**: Percentual de predições corretas.
    - **Precisão e Recall**: Úteis em problemas desbalanceados.
    - **Curva ROC e AUC**: Avaliam o desempenho em termos de separação entre as classes.

## Logistic Regression and The Wald Test

O **Wald Test** é amplamente utilizado em **regressão logística** para avaliar a significância estatística dos coeficientes de um modelo. Ele responde à pergunta: *o coeficiente de uma variável independente é significativamente diferente de zero?*

### Relação entre o Wald Test e a Regressão Logística

Na regressão logística, os coeficientes $\beta$ são estimados para descrever a relação entre as variáveis independentes e a variável dependente binária (0 ou 1). Após ajustar o modelo, o Wald Test ajuda a determinar se os coeficientes das variáveis independentes são estatisticamente significativos, ou seja, se eles contribuem de maneira relevante para o modelo.

---

### Como o Wald Test funciona?

**Hipóteses**:
-  **Hipótese Nula $(H_{0}​)$**: O coeficiente é igual a zero $(\beta = 0)$, ou seja, a variável independente não tem efeito significativo.
- **Hipótese Alternativa $(H_{1})$**: O coeficiente é diferente de zero $(\beta \neq 0)$.

**Cálculo do Wald Test**:  
    O teste calcula o valor da estatística $W$, que é a razão entre o coeficiente estimado e seu erro padrão:

$$
	W = \dfrac{\hat{\beta}}{SE(\hat{\beta})}
$$


Aqui:
 - $\hat{\beta}$​: Coeficiente estimado.
 - $SE(\hat{\beta})$: Erro padrão do coeficiente.
 
 **Distribuição e decisão**:  
    O valor $W^{2}$ segue uma distribuição qui-quadrado $(χ^{2})$ com 1 grau de liberdade. Com base no valor $p$ associado ao teste, avaliamos se rejeitamos ou não $H_{0}$​:
    
- Se $p-valor < nível \ de \ significância \ \alpha$, rejeitamos $H_{0}$​, indicando que o coeficiente é significativamente diferente de zero.
-  Caso contrário, não há evidência suficiente para rejeitar $H_{0}$​.

---

### Por que o Wald Test é relevante na Regressão Logística?

- **Interpretação dos coeficientes**: Em um modelo de regressão logística, os coeficientes determinam o impacto das variáveis independentes nas probabilidades previstas. O Wald Test ajuda a identificar quais variáveis têm influência significativa.
- **Seleção de variáveis**: Ele pode ser usado para remover variáveis irrelevantes do modelo, simplificando-o e melhorando sua interpretabilidade.
- **Validação do modelo**: Ao identificar quais coeficientes são significativos, o teste contribui para avaliar a adequação do modelo aos dados.

---

### Limitações do Wald Test na Regressão Logística

- **Colinearidade**: Se há alta colinearidade entre variáveis independentes, o erro padrão do coeficiente pode ser inflado, levando a valores $W$ e $p-valores$ menos confiáveis.
- **Coeficientes grandes**: Quando os coeficientes são muito grandes, o Wald Test pode se tornar instável, dificultando a avaliação da significância.

---

Em resumo, o Wald Test é uma ferramenta estatística fundamental para interpretar os coeficientes em regressão logística, ajudando a validar quais variáveis são importantes no modelo. Contudo, suas limitações devem ser consideradas em conjunto com outras técnicas, como o **Likelihood Ratio Test** ou o **Teste de Razão de Verossimilhança**.


#### Wald Test e Logistic Regression x F-Test e Linear Regression

O **Teste de Wald** na regressão logística e o **Teste F** na regressão linear têm funções similares: avaliar a significância de variáveis no modelo, mas diferem no contexto e na abordagem. 

**O Teste de Wald, utilizado na regressão logística, avalia individualmente se os coeficientes $(\beta)$ das variáveis independentes são significativamente diferentes de zero, testando a relevância de cada variável para a previsão da probabilidade de um evento binário.** Já o Teste F, na regressão linear, verifica simultaneamente a significância de um conjunto de variáveis, avaliando se a variabilidade explicada pelo modelo é significativamente maior do que a variabilidade residual. 

Enquanto o Teste de Wald é adequado para modelos onde as respostas são probabilísticas e não seguem uma distribuição normal, o Teste F assume uma estrutura de erros normalmente distribuídos e é mais adequado para modelos de previsão contínua. Assim, ambos os testes auxiliam na validação dos modelos, mas estão adaptados às diferentes naturezas dos problemas de regressão logística e linear.