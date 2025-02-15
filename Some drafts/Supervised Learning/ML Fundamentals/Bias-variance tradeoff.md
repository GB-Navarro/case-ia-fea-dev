No contexto de machine learning, **bias** e **variance** são conceitos centrais para entender o erro total de um modelo e avaliar sua capacidade de generalização. Esses componentes descrevem como o modelo se comporta ao lidar com novos dados, ou seja, dados que não foram usados durante o treinamento, e ajudam a identificar as causas de diferentes tipos de erro.

O **bias** está associado à **incapacidade do modelo de captar as complexidades subjacentes nos dados**. Modelos com alto bias fazem suposições simplificadas, resultando em um desempenho ruim tanto nos dados de treino quanto nos de teste. **Esse comportamento caracteriza o subajuste**, quando o modelo não consegue representar adequadamente as relações reais nos dados. 

	Por exemplo, ao aplicar uma regressão linear para modelar dados com relações não lineares, o modelo apresentará alto bias (subajuste), pois falha em capturar a complexidade inerente aos dados.

Por outro lado, a **variance** reflete a **sensibilidade do modelo às flutuações nos dados de treino**. **Modelos com alta variance não apenas aprendem os padrões gerais, mas também o ruído específico dos dados de treino**. Isso resulta em um excelente desempenho nos dados de treino, mas um desempenho ruim em novos dados, caracterizando o **superajuste** *(overfitting)*. Modelos complexos, como redes neurais profundas sem regularização adequada, são exemplos típicos de sistemas com alta variance.

A capacidade de generalização de um modelo depende de encontrar um equilíbrio entre bias e variance. **Um modelo com alto bias é muito simples e subajusta os dados, enquanto um modelo com alta variance é excessivamente complexo e superajusta os dados de treino.** 

Em resumo, modelos com alto bias estão associados ao **underfitting**, ou seja, são incapazes de captar adequadamente as relações existentes nos dados, resultando em uma representação insuficiente da complexidade do problema. Por outro lado, modelos com alta variance tendem a sofrer de **overfitting**, ajustando-se não apenas aos padrões gerais, mas também ao ruído presente nos dados de treino, o que compromete sua capacidade de generalização para dados não vistos.

## Definição formal de bias e variance [Melhorar]

1. **Bias (Viés)**

		O bias mede o erro sistemático do modelo. Formalmente, ele se refere à diferença entre o valor médio das predições do modelo e o valor verdadeiro que estamos tentando prever. Matematicamente, para uma variável-alvo y, com base em entradas x, o bias é definido como:

$$
	Bias(\hat{f}(x)) = \mathbb{E}[\hat{f}(x)] - f(x)
$$

Onde:

- $E[\hat{f}(x)]$ é o valor esperado das predições do modelo (considerando diferentes amostras de treino).
- $f(x)$ é o verdadeiro mapeamento subjacente (função real que gera os dados).

2. **Variance**

		A variance mede a sensibilidade do modelo às flutuações nos dados de treino. Ela descreve o quanto as predições do modelo variam em relação à média das predições quando o modelo é treinado com diferentes amostras de treino. Formalmente, a variance é definida como:

$$
	Var(\hat{f}(x)) = \mathbb{E}[(\hat{f}(x) - \mathbb{E}[\hat{f}(x)])^{2}] 
$$

Onde:

- $\hat{f}(x)$ é a predição do modelo.
- $\mathbb{E}[\hat{f}(x)]$ é o valor esperado das predições do modelo.