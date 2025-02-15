**Linear Discriminant Analysis (LDA)**, ou Análise Discriminante Linear, é uma técnica de redução de dimensionalidade amplamente utilizada em problemas de aprendizado supervisionado. Assim como outras técnicas de redução de dimensionalidade, como a Análise de Componentes Principais (PCA), o objetivo do LDA é projetar dados de uma dimensão superior para uma dimensão inferior. Por exemplo, podemos reduzir dados de 7 dimensões para 3, facilitando a visualização e/ou a classificação.

Embora o LDA seja conceitualmente semelhante ao PCA, as duas abordagens têm diferenças importantes. O PCA é aplicado em problemas de aprendizado não supervisionado, buscando direções que maximizem a variação dos dados sem levar em conta rótulos. **Já o LDA, por ser supervisionado, utiliza os rótulos das classes para encontrar projeções que melhor separam as categorias. O objetivo do LDA é, especificamente, encontrar vetores de projeção que maximizem a separação entre as classes e minimizem a variância dentro de cada classe.**

Esse problema é resolvido por meio de um sistema de valores próprios que considera a relação entre a dispersão entre as classes e a dispersão dentro das classes. As projeções resultantes transformam os dados para um espaço de menor dimensionalidade, preservando as características mais relevantes para a separação das categorias.

**O LDA é muito conectado com a distribuição normal, essa conexão está na suposição *(feita pelo LDA)* de que os dados de cada classe seguem uma distribuição normal multivariada no espaço original. Essa hipótese permite modelar cada classe por meio de uma média vetorial $\mu_{c}$ e uma matriz de covariância $\Sigma$, que é assumida igual para todas as classes.** Essa modelagem é fundamental para derivar as projeções ótimas e construir fronteiras de decisão lineares entre as categorias no espaço projetado. Além disso, a regra de Bayes, combinada com a densidade da distribuição normal, é utilizada para classificar amostras no novo espaço, tornando o LDA uma técnica poderosa e matematicamente fundamentada para problemas supervisionados.

## Uma visão intuitiva do LDA

Considere um conjunto de dados bidimensional (2D) no qual os pontos precisam ser classificados em duas categorias, mas não podem ser separados linearmente por uma única reta. O LDA resolve esse problema criando um novo eixo que projeta os dados de forma a:

1. **Maximizar a separação entre as classes**: garante que os centroides das categorias estejam o mais distantes possível no novo eixo.
2. **Minimizar a variância dentro das classes**: reduz a dispersão dos pontos pertencentes a uma mesma categoria.

A projeção dos pontos para esse novo eixo transforma os dados de 2D para 1D, preservando as características relevantes para a classificação *(esse processo pode ser estendido para dimensões superiores, reduzindo dados de $n$-dimensões para $m$-dimensões ($m<n$))*. Após reduzir a dimensionalidade, o **Linear Discriminant Analysis (LDA)** classifica os dados utilizando **limiares de decisão** no novo espaço projetado.

## O passo a passo do LDA

---

### 1. **Preparação dos dados**

- **Entrada**: Um conjunto de dados de $n$-dimensões com $N$ amostras, onde cada amostra $x_{i} \in R^{n}$ está associada a uma classe $y_{i}$​ (isto é, a uma de $C$ categorias).

- Os dados devem estar rotulados, pois o LDA é uma técnica supervisionada.

- **Pré-processamento**: Normalize ou padronize os dados para garantir que todas as variáveis estejam na mesma escala.

---

### 2. **Cálculo das médias de classe e geral**

- **Média de cada classe** $μ_{c}$
$$μ_{c} = \dfrac{1}{N_{c}}\sum\limits_{i \ \in \ classe \ c} x_{i}$$
Onde $N_{c}$ é o número de elementos na classe c
- **Média geral** $\mu$ 
$$ μ = \dfrac{1}{N} \sum\limits_{i = 1}^{N} x_{i}$$
Onde $N$ é o número total de elementos no dataset. 

---

### 3. **Cálculo das matrizes de dispersão (scatter matrices)**

- **Dispersão dentro das classes $S_{W}$:**: Mede a variação dos dados dentro de cada classe. Para cada classe $c$, é dado por:
$$
	S_{w} = \sum\limits_{c = 1}^{C}\sum\limits_{i \  \in \ classe \ c} (x_{i} - \mu_{c})(x_{i}-\mu_{c})^{T}
$$

- **Dispersão entre as classes $S_{B}$​**: Mede a variação entre as médias das classes em relação à média geral: 
$$
	S_{B} = \sum\limits_{c = 1}^{C} N_{c}(\mu_{c}-\mu)(\mu_{c}-\mu)^{T}
$$

---


### 4. **Resolução do problema de otimização**

- O objetivo do LDA é encontrar vetores de projeção **$w$** que maximizem a separação entre as classes e minimizem a variância dentro das classes. Isso é feito resolvendo: 
$$
	w = argmax \dfrac{w^{T}S_{B}w}{w^{T}S{w}w}
$$

- Esse problema é equivalente a resolver o sistema de valores próprios: 
$$
S^{-1}_{w}S_{B}w = \lambda w
$$
- Onde $\lambda$ são os autovalores, e $w$ são os autovetores.

---

### 5. **Seleção dos vetores de projeção**

- Ordene os autovalores $\lambda$ em ordem decrescente e selecione os $k$ maiores autovalores correspondentes aos $k$ autovetores $w_{1},w_{2},…,w_{k}$.
- Esses autovetores formam a matriz de transformação $\mathbb{W}$ que será usada para reduzir a dimensionalidade: 
$$
\mathbb{W} = [w_{1},w_{2},...,w_{k}]
$$

---

### 6. **Projeção dos dados**

- Os dados originais $\mathbb{X}$ são projetados no novo espaço de menor dimensionalidade:
$$
	\mathbb{X}_{projetado} = \mathbb{X}\mathbb{W}
$$

---

### 7. **Classificação**

	Após a projeção, o LDA classifica as amostras utilizando as propriedades estatísticas das classes. Com base na regra de Bayes, as probabilidades de pertença de uma amostra a cada classe são calculadas considerando que os dados seguem uma distribuição normal multivariada. Na prática, para duas classes, define-se um limiar de decisão no espaço projetado (frequentemente o ponto médio entre as médias das classes projetadas). Para múltiplas classes, a classificação é feita considerando a proximidade das amostras projetadas aos centroides das classes.

---

## .

Esse processo não apenas reduz a dimensionalidade, mas também alinha o espaço projetado para maximizar a separação entre as classes.