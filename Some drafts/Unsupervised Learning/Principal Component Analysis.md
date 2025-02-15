
**Principal Component Analysis (PCA)**, ou Análise de Componentes Principais, é uma técnica amplamente utilizada para redução de dimensionalidade em problemas de aprendizado não supervisionado. **O objetivo do PCA é projetar dados de uma dimensão superior para uma dimensão inferior, enquanto se preserva a maior quantidade possível de variabilidade presente nos dados originais.** Por exemplo, pode-se reduzir dados de 10 dimensões para 2, facilitando a visualização e/ou a análise.

Embora o PCA compartilhe semelhanças com técnicas como o **Linear Discriminant Analysis (LDA)**, há diferenças fundamentais. **O PCA é não supervisionado, ou seja, ele não utiliza rótulos das amostras e, portanto, busca as direções principais baseando-se exclusivamente na estrutura dos dados. O objetivo do PCA é identificar as direções (ou componentes principais) que explicam a maior variância nos dados, sem considerar informações de classes ou categorias.**

Essa técnica é fundamentada em conceitos de álgebra linear, como autovalores e autovetores, e é amplamente aplicada em áreas como compressão de dados, visualização de alto desempenho e pré-processamento para algoritmos de aprendizado de máquina.

---

## **Uma visão intuitiva do PCA**

Imagine um conjunto de dados tridimensional (3D) com pontos dispersos. O PCA procura identificar os eixos (componentes principais) em torno dos quais os dados têm maior variância. Em essência:

1. **Primeira componente principal**: Define a direção ao longo da qual a variância dos dados é máxima.
2. **Segunda componente principal**: Define a **direção ortogonal à primeira componente** com a próxima maior variância.
3. **Componentes subsequentes**: Continuam o processo para as dimensões restantes, **sempre garantindo ortogonalidade às componentes anteriores.**

Reduzir a dimensionalidade com PCA consiste em projetar os dados originais em um subconjunto dessas componentes principais, de modo que a maior parte da variabilidade dos dados seja preservada.

---

## **O passo a passo do PCA**

---

### 1. **Preparação dos dados**

- **Entrada**: Um conjunto de dados de $n$-dimensões com $N$ amostras, onde cada amostra $x_{i} \in R^{n}$.
- **Pré-processamento**:
    - Centralize os dados subtraindo a média de cada variável (para garantir que as componentes principais sejam centradas na origem).
    - Padronize os dados se as variáveis tiverem escalas diferentes, para evitar que variáveis com maiores amplitudes dominem o cálculo das componentes principais.

---

### 2. **Cálculo da matriz de covariância**

- A matriz de covariância captura as relações de variabilidade entre pares de variáveis. É calculada como:

$$
	\mathbb{C} = \dfrac{1}{N-1}\mathbb{X}^{T}\mathbb{X}
$$

Onde $\mathbb{X}$ é a matriz de dados centralizada, com $N$ amostras e $n$ dimensões.

---

### 3. **Decomposição em valores próprios**

- Resolva o problema de autovalores e autovetores para a matriz de covariância:

$$
	\mathbb{C_{v_{i}}} = \lambda_{i}v_{i}
$$

Onde:

- $v_{i}$ são os autovetores (as direções das componentes principais).
- $\lambda_{i}$ são os autovalores (a variância explicada por cada componente principal).

---

### 4. **Ordenação dos componentes principais**

- Os autovalores $\lambda_{i}$ são ordenados em ordem decrescente. As componentes principais correspondem aos autovetores associados aos maiores autovalores.

---

### 5. **Seleção do número de componentes**

- Defina o número de componentes principais $k$ a serem utilizados. **A escolha de $k$ pode ser feita com base no percentual de variância explicada acumulada**:

- Um limiar comum é selecionar $k$ tal que a variância explicada acumulada seja maior que, por exemplo, 95%.

---

### 6. **Projeção dos dados**

- A matriz de transformação $\mathbb{W}$ é formada pelos $k$ autovetores correspondentes aos maiores autovalores:

$$
	\mathbb{W} = [v_{1},v_{2},...,v_{k}]
$$

- Os dados originais $\mathbb{X}$ são projetados no espaço de menor dimensionalidade:

$$
	\mathbb{X}_{projetado} = \mathbb{X}\mathbb{W}
$$


---

## **Propriedades e aplicações do PCA**

### **Propriedades do PCA**

1. **Ortogonalidade**: As componentes principais são mutuamente ortogonais.
2. **Maximização da variância**: Cada componente principal captura a maior variância possível restante nos dados.
3. **Redução de dimensionalidade**: Projeta os dados em um espaço de menor dimensionalidade enquanto preserva a maior parte da informação original.

---

### **Exemplos de aplicações**

1. **Visualização de dados**: Redução de dados de alta dimensionalidade para 2D ou 3D para facilitar a visualização.
2. **Compressão de dados**: Retenção de informações essenciais com menor espaço de armazenamento.
3. **Pré-processamento**: Remoção de redundâncias e ruído antes de aplicar modelos de aprendizado de máquina.