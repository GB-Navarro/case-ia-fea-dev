A **regressão linear** é uma das técnicas mais fundamentais na estatística e no aprendizado supervisionado, amplamente utilizada para modelar e analisar relações entre variáveis. **Por meio dela, é possível descrever, prever e compreender como uma ou mais variáveis independentes influenciam uma variável dependente.**

### O Método dos Mínimos Quadrados Ordinários (OLS)

O núcleo da regressão linear é o **método dos mínimos quadrados ordinários (OLS, do inglês _Ordinary Least Squares_)**, que busca determinar os coeficientes que minimizam a soma dos quadrados das diferenças entre os valores observados e os valores previstos pelo modelo.

Esse método é utilizado para encontrar a melhor linha reta que representa a relação entre as variáveis, garantindo que os erros de previsão sejam os menores possíveis, no sentido quadrático.

### A equação da reta 

Podemos compreender a regressão linear como o processo de encontrar a reta que melhor descreve a relação entre uma variável dependente $y$ e uma ou mais variáveis independentes $x$. 

A regressão linear ajusta uma equação do tipo:
$$
y = \beta_{0} + \beta_{1}x + \epsilon  
$$

Onde:

- $y$ é a variável dependente *(variável alvo).*
	
- $x$ é a variável independente *(variável preditora ou explicativa)*.
	
- $\beta_{0}$​ é o intercepto, isto é, valor de $y$ quando $x = 0$.
	
- $\beta_{1}$​ é o coeficiente angular, que indica a inclinação da reta e representa a mudança esperada em $y$.
	
- $\epsilon$  representa o termo de erro, responsável por capturar variações não explicadas pelo modelo.

### Avaliação do Modelo: Resíduos e Qualidade do Ajuste

#### Resíduos 

Resíduos são as diferenças entre os valores observados (reais) e os valores previstos (ajustados) pelo modelo de regressão. Em outras palavras, eles representam o erro de previsão do modelo para cada ponto de dados. Matematicamente, os resíduos são definidos como:

$$
	e_{i} = y_{i} - \hat{y}_{i}
$$

Onde:

- $e_{i}$​ é o resíduo para o $i$-ésimo ponto de dados.
- $y_{i}$​ é o valor observado (real) da variável dependente no ponto $i$.
- $\hat{y}_{i}$​ é o valor previsto pelo modelo para o ponto $i$.

Os resíduos ajudam a avaliar a qualidade do ajuste do modelo. **Se o modelo for adequado, os resíduos devem se distribuir aleatoriamente em torno de zero, sem apresentar padrões sistemáticos.** Isso indica que o modelo conseguiu capturar bem a relação entre as variáveis e que os erros são apenas variações aleatórias. 

No entanto, **se os resíduos mostrarem padrões (como curvaturas ou agrupamentos), isso pode ser um sinal de que o modelo não está explicando adequadamente os dados, sugerindo, por exemplo, a necessidade de um modelo não linear ou a inclusão de variáveis adicionais.**

#### Coeficiente de determinação ($R^{2}$)

Podemos medir a variabilidade dos dados que o modelo **não consegue explicar** através da seguinte fórmula *(Soma dos quadrados dos resíduos)*:
$$
	SS_{fit} = \sum\limits_{i = 1}^{n}(y_{i} - \hat{y}_{i})^{2}
$$
Além disso, podemos medir a variabilidade dos dados que o modelo **consegue explicar** através da seguinte fórmula *(Soma dos quadrados de regressão)*:
$$
	SS_{mean} =  \sum\limits_{i = 1}^{n}(\hat{y}_{i} - \bar{y})^{2}
$$
Onde
- $\bar{y}$ é a média dos valores observados da variável dependente $y$.

A seguinte relação conecta as duas relações expostas acima:
$$
	SS_{tot} = SS_{fit} + SS_{mean}
$$
A relação acima mostra que a variabilidade total nos dados é composta pela variabilidade explicada pelo modelo $(SS_{mean})$ e a variabilidade não explicada pelo modelo $(SS_{fit})$.

Na análise de regressão linear, um dos indicadores mais utilizados para avaliar a qualidade do ajuste é o **coeficiente de determinação**, conhecido como $R^{2}$. Esse coeficiente fornece uma medida numérica da proporção da variabilidade total da variável dependente que é explicada pelas variáveis independentes incluídas no modelo.

Matematicamente, o $R^{2}$ é definido como:

$$
	R^{2} = 1 - \dfrac{SS_{fit}}{SS_{tot}}
$$

Em termos práticos, o $R^{2}$ pode ser interpretado da seguinte forma:

- **$R^{2}=1$:** Indica que o modelo ajusta perfeitamente os dados, ou seja, toda a variação observada na variável dependente é explicada pelas variáveis independentes.
- **$R^{2}=0$:** Sugere que o modelo não explica nenhuma variação nos dados, ou seja, o ajuste não oferece informações melhores do que simplesmente usar a média da variável dependente como previsão.

Valores intermediários de $R^{2}$ indicam a proporção da variação total na variável dependente que é explicada pelas variáveis independentes incluídas no modelo. Por exemplo, um $R^{2}=0,75$ significa que o modelo é capaz de explicar 75% da variação observada nos dados, enquanto os 25% restantes correspondem a fatores que o modelo não consegue capturar. **Esses fatores podem ser diversos, como variáveis que não foram incluídas na análise ou a presença de "ruído" nos dados, ou ainda uma estrutura mais complexa, como uma relação não linear, que não é adequadamente modelada por uma regressão linear.**

Vale destacar que, embora um $R^{2}$ elevado sugira um bom ajuste do modelo, um valor menor que 1 não implica necessariamente que haja uma relação não linear entre as variáveis. Isso apenas indica que o modelo linear não conseguiu capturar completamente a variabilidade dos dados. Se existirem padrões nos resíduos que sugerem uma estrutura não aleatória ou curvatura, isso pode ser um indício de que a relação entre as variáveis seja não linear e que um modelo linear não seja o mais adequado para os dados. Nesse caso, seria útil explorar outras abordagens de modelagem que possam capturar melhor essa complexidade.

##### Como saber se há uma relação não linear?

Se os resíduos do modelo de regressão linear  apresentarem padrões sistemáticos, isso pode indicar que o modelo linear não está capturando alguma estrutura subjacente nos dados, sugerindo uma possível relação não linear. Nesse caso, vale a pena considerar:

- **Gráficos de resíduos:** Ao plotar os resíduos em relação às variáveis independentes, podemos observar padrões. Se houver uma estrutura claramente não aleatória (por exemplo, uma curva), isso pode indicar uma relação não linear.
- **Modelos não lineares:** Se suspeitarmos de uma relação não linear, podemos tentar modelos de regressão polinomial, redes neurais, árvores de decisão, ou outras técnicas que capturam relações não lineares.

#### Limitações do $R^{2}$

Embora o $R^{2}$ seja uma métrica valiosa, ele tem limitações. Um $R^{2}$ alto não garante necessariamente que o modelo é bom ou adequado, pois ele não considera a complexidade do modelo nem verifica a validade dos pressupostos da regressão. Além disso, adicionar mais variáveis ao modelo sempre aumenta ou mantém o valor de $R^{2}$, mesmo que essas variáveis não tenham relevância estatística. Por isso, muitas vezes utiliza-se o $R^{2}$ ajustado, que penaliza a inclusão de variáveis irrelevantes.

O coeficiente de determinação ajustado, conhecido como $R^{2}$ ajustado, é uma métrica essencial na análise de regressão, especialmente quando lidamos com modelos que incluem múltiplas variáveis independentes. Enquanto o $R^{2}$ tradicional mede a proporção da variabilidade da variável dependente explicada pelo modelo, ele pode aumentar simplesmente pela adição de variáveis, mesmo que essas não sejam realmente relevantes. Isso ocorre porque variáveis irrelevantes, ao capturar flutuações aleatórias nos dados, podem reduzir artificialmente a soma dos quadrados dos ajustes $(SS_{fit}​)$, levando a uma melhora ilusória do $R^{2}$.

O $R^{2}$ ajustado corrige esse problema ao penalizar a inclusão de variáveis desnecessárias, considerando tanto o número de variáveis quanto o tamanho do conjunto de dados. Dessa forma, ele fornece uma métrica mais realista para avaliar o desempenho do modelo, reduzindo a chance de que padrões aleatórios nos dados sejam interpretados como informações significativas. Em essência, o $R^{2}$ ajustado promove a construção de modelos mais parcimoniosos, ou seja, que explicam os dados de forma eficiente sem incluir complexidades desnecessárias.

Além de calcular o $R^{2}$ *(de preferência, ajustado)*, é importante verificar a significância estatística do modelo. Isso é feito utilizando o **p-valor**, que no contexto da regressão linear **indica a probabilidade de observarmos uma relação entre as variáveis tão forte quanto a encontrada, caso a hipótese nula seja verdadeira (isto é, que não existe relação linear).** Um p-valor pequeno (geralmente menor que 0,05) sugere que os coeficientes estimados no modelo são significativamente diferentes de zero, confirmando que a relação entre as variáveis é estatisticamente significativa.

**Assim, ao aplicar a regressão linear, o objetivo é não apenas encontrar a melhor reta que ajusta os dados, mas também avaliar se esse ajuste é significativo e representa bem a relação entre as variáveis estudadas.**



### .

Mesmo que a regressão linear não seja sempre a melhor escolha para **previsão** (predição), ela é uma ferramenta poderosa para entender a relação entre variáveis, ou seja, **como uma variável independente influencia a variável dependente**.

### Verificando a significância estatística do $R^{2}$ através do $p-value$

A significância estatística do $R^{2}$ em uma análise de regressão é frequentemente avaliada por meio de um **teste F**, que nos ajuda a determinar se o modelo como um todo tem poder explicativo significativo. **O teste F compara a variabilidade explicada pelo modelo com a variabilidade residual (não explicada), avaliando se a proporção explicada $(R^{2})$ é estatisticamente diferente de zero.**

#### O que é o teste F?

O **F** é uma estatística de teste que segue a distribuição **F de Fisher-Snedecor** sob a hipótese nula. No contexto do $R^{2}$, a hipótese nula $(H_{0}​)$ assume que todas as variáveis independentes no modelo não têm relação com a variável dependente, ou seja, que os coeficientes associados às variáveis independentes são todos iguais a zero $(β_{1}​=β_{2}​=⋯=β_{p}​=0)$.

O valor de F é calculado como uma razão de variâncias:

$$
	F = \dfrac{Variância \ explicada \ pelo \ modelo}{Variância \ residual \ por \ grau \ de \ liberdade}
$$

Essa fórmula pode ser escrita em termos de somas de quadrados e graus de liberdade:

$$
	F = \dfrac{\dfrac{SS_{modelo}}{k}}{\dfrac{SS_{resíduos}}{n-k-1}}
$$

Onde:

- $SS_{modelo}$​: Soma dos quadrados explicada pelo modelo.
- $SS_{resíduo}$​: Soma dos quadrados dos resíduos.
- $k$: Número de variáveis independentes.
- $n$: Número total de observações.

**O F mede quão bem o modelo se ajusta aos dados em comparação com um modelo nulo (ou seja, um modelo que apenas usa a média da variável dependente como previsão).**

#### Como funciona o cálculo do p-valor para $R^{2}$?

Com a estatística F calculada, o próximo passo é determinar o **p-valor** associado a ela. O p-valor nos dá a probabilidade de observarmos um valor de F tão extremo quanto o obtido, assumindo que a hipótese nula $(H_{0}​)$ seja verdadeira. Em **outras** palavras, ele mede a evidência contra a hipótese de que o modelo não tem poder explicativo.

Para calcular o p-valor:

1. Compara-se o valor de F obtido com a **distribuição F** de Fisher-Snedecor, que depende de dois parâmetros:
    - **Graus de liberdade do numerador**: $k$ *(número de variáveis independentes no modelo)*.
    - **Graus de liberdade do denominador**: $n−k−1$ *(número de observações menos o número de variáveis independentes e o intercepto)*.
2. A área sob a curva da distribuição F, à direita do valor observado, fornece o p-valor. Essa área representa a probabilidade de obter um F tão grande, ou maior, caso a hipótese nula seja verdadeira.

Se o p-valor for pequeno *(geralmente menor que 0,05)*, rejeitamos a hipótese nula e concluímos que o modelo tem um poder explicativo significativo. Isso implica que o $R^{2}$ não é zero e que pelo menos uma das variáveis independentes está significativamente associada à variável dependente.

Em resumo, o teste F fornece uma maneira robusta de avaliar a significância estatística do $R^{2}$, ajudando a validar a utilidade do modelo como um todo. Ao calcular o p-valor associado à estatística F, podemos determinar se o modelo explica uma proporção significativa da variabilidade nos dados, descartando a possibilidade de que o $R^{2}$ tenha surgido apenas por acaso.

### A Regularização em Regressões Lineares

A regularização é uma técnica que adiciona uma penalidade à função de custo da regressão linear para controlar a complexidade do modelo. Isso ajuda a evitar o overfitting, restringindo os coeficientes e tornando o modelo mais simples e robusto, especialmente em casos de variáveis colineares ou quando o modelo tem muitos parâmetros. Métodos como **Ridge Regression** (L2) e **Lasso Regression** (L1) são exemplos de regularização, que melhoram a generalização e a interpretabilidade de modelos de regressão linear.
