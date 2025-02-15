	
## Problemas linearmente separáveis e não linearmente separáveis

#### Problemas Linearmente Separáveis

Um problema é considerado **linearmente separável** quando existe uma **linha**, **plano** ou **hiperplano** que pode dividir as classes de dados de forma clara, sem sobreposição, no espaço de características. Nesse cenário, todas as instâncias de uma classe estão de um lado do limite de decisão, e as instâncias da outra classe estão do outro lado.

- **Exemplo prático**:  

		Imagine um conjunto de dados 2D onde um grupo de pontos (classe A) está no lado esquerdo de uma linha e outro grupo de pontos (classe B) está no lado direito. Nesse caso, o problema pode ser resolvido por um classificador linear.
    
- **Soluções comuns**:
    
	    - Perceptron: Um dos primeiros algoritmos de aprendizado de máquina, ideal para problemas linearmente separáveis.
    
		- Support Vector Classifiers (SVC): Busca o hiperplano que maximiza a margem entre as classes.

#### Problemas Não Linearmente Separáveis

Quando as classes de dados não podem ser separadas por uma linha ou plano no espaço original, o problema é **não linearmente separável**. Isso ocorre quando as classes estão dispostas de forma complexa, como em padrões curvos, agrupamentos sobrepostos ou em espirais.

- **Exemplo prático**:  
    
	    Imagine dois conjuntos de pontos no plano 2D, onde um forma um círculo dentro do outro. Nenhuma linha reta pode separar essas classes.
    
- **Soluções comuns**:  

		Para resolver esses problemas, os modelos precisam transformar os dados ou usar técnicas avançadas, como:
    
		- Transformação de espaço e Kernel Trick: Para resolver problemas não linearmente separáveis, é possível projetar os dados para um espaço de maior dimensão, onde a separação linear se torna viável. Essa transformação pode ser realizada de forma eficiente por meio do Kernel Trick, uma técnica amplamente utilizada em SVMs. Em vez de calcular explicitamente as novas coordenadas dos dados no espaço transformado, o kernel calcula diretamente os produtos internos entre os pontos nesse espaço, simplificando o processo e reduzindo a complexidade computacional. Isso permite que limites de decisão complexos sejam aprendidos sem a necessidade de manipulação direta do espaço de maior dimensão.
	    
		- **Redes Neurais**: Modelos profundos conseguem capturar relações não lineares entre as variáveis, aprendendo limites de decisão complexos.

## Classificadores de Máxima Margem 

Os **classificadores de máxima margem** são classificadores que buscam encontrar o **hiperplano** que maximiza a distância entre as classes de dados, garantindo a maior separação possível entre os pontos mais próximos de cada classe, pontos esses conhecidos como **vetores de suporte**.
##### Por que a margem máxima é importante?

A margem máxima reduz o risco de erro na classificação, criando uma ampla zona de separação entre classes. Isso melhora a generalização do modelo para novos dados. Entretanto, há limitações, como a sensibilidade a valores extremos (**outliers**).
##### Problemas com valores extremos (outliers)

Os Classificadores de Máxima Margem *(Maximal Margin Classifiers)* podem apresentar dificuldades quando existem **outliers** (valores extremos) nos dados. Por exemplo, imagine duas classes bem separadas. Um único valor discrepante em uma das classes pode "arrastar" o limiar de classificação (a margem) para mais próximo da outra classe. Isso faz com que o modelo classifique incorretamente pontos que estão próximos à fronteira de separação, mesmo que esses pontos estejam, na prática, mais alinhados com a outra classe.

##### Classificadores de máxima margem em altas dimensões

	Em uma dimensão, o classificador é um ponto (um subespaço de dimensão 0, no jargão matemático).

	Em duas dimensões, o classificador é uma reta(um subespaço de dimensão 1, no jargão matemático).

	Em três dimensões, ele é um plano (um subespaço de dimensão 2, no jargão matemático).
	
	Em quatro ou mais dimensões, o classificador se torna um hiperplano, (que é um subespaço de uma dimensão a menos que o espaço de entrada, no jargão matemático).
## Soft Margin: Adicionando Flexibilidade

Para lidar com outliers e aumentar a robustez, podemos usar o conceito de **soft margin**, que permite algumas violações à margem ideal. Isso melhora a generalização, tolerando classificações incorretas no treinamento, especialmente para outliers. 

Perceba que o conceito de **soft margin** está intimamente conectado ao **Bias-variance tradeoff**.

Pois bem, vamos discutir com um pouco mais de detalhes o conceito de **soft margin**.

De modo geral, uma **soft margin** é uma adaptação da margem máxima que aceita que alguns pontos caiam dentro da margem ou do lado incorreto do hiperplano. Isso equilibra o Bias-variance tradeoff, reduzindo o risco de overfitting.

Dada a relevância das **soft margin** na generalização de certos modelos,  a escolha do valor ideal para ela *(que é controlada pelo hiperparâmetro C em SVMs)* é crucial. Valores altos de C levam a margens mais rígidas, priorizando a classificação perfeita nos dados de treinamento, mas com maior risco de overfitting. Por outro lado, valores baixos de C tornam a margem mais flexível, tolerando classificações incorretas nos dados de treinamento e favorecendo a generalização. De modo geral, a validação cruzada *(como o **k-fold cross-validation**)* é uma das abordagens mais comuns para selecionar o valor apropriado de C. Nesses casos, o objetivo é identificar o valor de C que otimiza o desempenho médio do modelo *(no conjunto de validação)* em uma métrica escolhida.

Por fim, ao utilizar a **soft margin**, é comum que os **outliers** sejam acomodados dentro da margem ou até classificados incorretamente, dependendo de sua posição em relação ao hiperplano. Essa flexibilidade é intencional e visa priorizar a **generalização do modelo** em vez de uma separação perfeita nos dados de treinamento. Como resultado, os modelos com **soft margin** demonstram maior **robustez** frente a ruídos e valores discrepantes, mantendo bom desempenho mesmo em cenários com dados imperfeitos.

## Support Vector Classifiers

O **Support Vector Classifier (SVC)** é um modelo de aprendizado supervisionado que busca encontrar um **hiperplano de separação** capaz de dividir os dados de diferentes classes, maximizando a **margem** entre elas. A margem é a distância entre o hiperplano de separação e os pontos mais próximos de cada classe, conhecidos como **vetores de suporte**, que são fundamentais para definir a posição e orientação do hiperplano.

O SVC é projetado para equilibrar a precisão na classificação dos dados de treinamento com a capacidade de generalização para novos dados, fundamentando-se em dois conceitos principais: a **margem máxima** e a **soft margin**. Embora seja classificado como um **classificador de máxima margem**, ele apresenta adaptações que o tornam mais robusto para lidar com dados reais.

Em situações ideais, onde os dados são **linearmente separáveis** e livres de ruído ou outliers, o SVC funciona como um **classificador de máxima margem tradicional**. Nesse contexto, o modelo busca um hiperplano que separa perfeitamente as classes, garantindo que nenhum ponto caia dentro da margem ou do lado errado do hiperplano.

No entanto, em cenários reais, os dados frequentemente apresentam **outliers** ou **ruído**, e as classes podem não ser perfeitamente separáveis. Para lidar com essas limitações, o SVC incorpora o conceito de **soft margin**, permitindo certa flexibilidade na definição da margem. Essa abordagem tolera erros, como pontos que ficam dentro da margem (entre o hiperplano e os vetores de suporte) ou que são classificados incorretamente.

O controle dessa flexibilidade é ajustado por meio do hiperparâmetro $C$, que equilibra dois objetivos principais:

- **Valores altos de $C$**: Priorizam a classificação perfeita dos dados de treinamento, reduzindo erros, mas aumentando o risco de **overfitting**.
- **Valores baixos de $C$**: Permitem uma margem mais ampla, priorizando a generalização do modelo, mesmo que alguns pontos sejam classificados incorretamente.











## Support Vector Machines

O **SVM (Support Vector Machine)** é um algoritmo de aprendizado supervisionado amplamente utilizado para **classificação** e, além disso, possui uma versão adaptada para **regressão**, conhecida como Support Vector Regression (SVR). 

O principal objetivo do SVM é encontrar o **hiperplano de separação** que divide de forma ótima as classes no espaço de entrada, maximizando a **margem** entre elas, de maneira semelhante aos **SVCs**. No entanto, ao contrário dos **SVCs**, o **SVM** possui a capacidade de lidar com dados **não linearmente separáveis** por meio do uso de **kernels**, que projetam os dados para um espaço de maior dimensão, onde a separação linear se torna viável.

Antes de explorarmos mais a fundo os detalhes do funcionamento do **SVM**, vamos primeiro entender algumas das terminologias associadas aos conceitos fundamentais de **SVCs** e **SVMs**:

-  **Hiperplano**: 

		A superfície que separa as diferentes classes no espaço de características. Em 1D, seria um ponto; em 2D, seria uma linha; em 3D, um plano; em dimensões superiores, um hiperplano.
    
-  **Vetores de suporte**: 

		Os pontos de dados mais próximos do hiperplano de separação. Eles são fundamentais, pois são usados para definir o posicionamento do hiperplano e a margem.
    
-  **Margem**: 

		A distância entre o hiperplano e os vetores de suporte. SVM busca maximizar essa margem para garantir uma melhor separação entre as classes.
    
- **Soft Margin**: 

		Permite que alguns pontos de dados violem a margem, equilibrando a necessidade de uma margem ampla com a possibilidade de aceitar erros (classificações incorretas), visando melhor generalização.

- **Kernel**: 

		Uma função que permite mapear os dados para um espaço de maior dimensão, facilitando a separação linear de dados que não são separáveis no espaço original. Exemplos de kernels incluem o **linear**, **polinomial** e **RBF (Radial Basis Function)**.

O **SVM** é um algoritmo de aprendizado supervisionado cujo principal objetivo é encontrar o **hiperplano de separação** que divide de forma ótima as classes no espaço de entrada, maximizando a **margem** entre elas, de maneira semelhante aos **SVCs**. No entanto, ao contrário dos **SVCs**, o **SVM** possui a capacidade de lidar com dados **não linearmente separáveis** por meio do uso de **kernels**, que projetam os dados para um espaço de maior dimensão, onde a separação linear se torna viável. É importante ressaltar que os **SVMs** utilizam os **SVCs** como sua base para problemas de classificação, sendo o **SVC** uma implementação específica dentro do conceito geral de **SVM**.

O nome **Support Vector Machine (SVM)** deriva do fato de que as observações mais próximas à margem, incluindo aquelas que caem dentro da **soft margin**, são chamadas de **vetores de suporte**.

### **Support Vector Machines e o Kernel Trick**

O maior avanço das **SVMs** sobre os classificadores tradicionais é o uso do **kernel trick**. Quando os dados não são linearmente separáveis no espaço original, os **SVMs** podem usar uma técnica chamada **kernel trick** para mapear os dados para um espaço de maior dimensão onde eles podem ser separáveis de forma linear. Além dessa ideia brilhante, o kernel trick possui uma outra sacada muito inteligente: Em vez de calcular diretamente as coordenadas no novo espaço, o kernel calcula o produto interno entre os pontos de dados mapeados, sem a necessidade de realizar a transformação explícita. Isso torna o processo mais eficiente e permite a criação de **fronteiras de decisão não lineares**. *(Vamos explicar melhor isso mais a frente)*

#### O que é um Kernel ?

Um **kernel** é uma função matemática usada em **Support Vector Machines (SVMs)** e em outros algoritmos de aprendizado de máquina para medir a **semelhança** ou **distância** entre dois pontos em um espaço de características. A principal vantagem do uso de um kernel é que ele permite calcular essas semelhanças de maneira eficiente sem precisar realizar a transformação explícita dos dados para um espaço de maior dimensão.

Em vez de calcular diretamente as coordenadas dos dados em um espaço de maior dimensão, o kernel calcula o **produto interno** entre os pontos transformados, o que simula como se os dados estivessem em uma dimensão superior. O kernel “faz isso” através de uma **função matemática** que, ao ser aplicada nos pontos, é capaz de calcular o produto interno correspondente ao espaço de maior dimensão sem precisar realmente fazer essa transformação.

**Os principais tipos de kernels incluem:**

		- Kernel linear: Usado quando os dados já são linearmente separáveis.
		
		- Kernel polinomial: Permite separar dados com relações polinomiais entre as classes.
		
		- Kernel RBF (Radial Basis Function): Usado para dados com separações complexas e curvas, muito eficaz em muitos problemas reais. 

#### O que é o Kernel Trick ?

O truque do kernel *(Kernel Trick)* é uma técnica engenhosa que permite resolver problemas de classificação não linear, ao simular a projeção dos dados em uma dimensão superior, sem a necessidade de projetar explicitamente os dados nessa dimensão. Para entender como isso funciona, é importante compreender o papel do **produto interno**.

O conceito central é que muitos algoritmos de aprendizado de máquina, incluindo as **SVMs**, dependem do cálculo de **distâncias** ou **relações geométricas** entre pontos de dados. Para isso, o produto interno entre dois vetores é frequentemente utilizado. Esse produto interno nos dá uma medida de similaridade entre os vetores, o que é crucial para definir a posição relativa dos pontos em relação ao hiperplano de separação.

Agora, suponha que temos dados que não podem ser separados linearmente no espaço original. A ideia por trás do kernel é que, se esses dados forem mapeados para um espaço de maior dimensão (potencialmente infinito), é mais provável que se tornem linearmente separáveis. No entanto, calcular explicitamente as coordenadas de cada ponto nesse novo espaço seria computacionalmente inviável, especialmente para grandes dimensões.

O **truque do kernel** resolve esse problema de forma elegante: ele utiliza uma função kernel que calcula diretamente o produto interno dos dados como se estivessem no espaço de dimensão superior, **sem jamais realizar a transformação explícita**. Em outras palavras, o kernel fornece o valor que seria obtido após o mapeamento, mas sem a necessidade de realmente mapear os dados.

Por exemplo, o **kernel gaussiano (RBF)** aplica uma função exponencial sobre a distância entre dois pontos no espaço original e retorna um valor que reflete como esses pontos se comportariam no espaço transformado. Assim, o algoritmo consegue construir uma **fronteira de decisão não linear** no espaço original, baseada nas relações de similaridade fornecidas pelo kernel.

Esse método não só economiza tempo e recursos computacionais, como também permite que as SVMs lidem com dados complexos e de alta dimensionalidade de maneira eficiente.

##### Exemplo:

###### Passo 1: Dados em uma dimensão $x$

Imagine que temos um conjunto de dados em duas dimensões (2D), representado por pontos $(x_{1},y_{1})$ e $(x_{2},y_{2})$, e essas classes não são separáveis linearmente. Isso significa que não existe uma linha reta que consiga dividir perfeitamente as duas classes.

###### Passo 2: Mapeamento para uma dimensão maior $x+1$

Com o **kernel trick**, ao invés de tentar desenhar uma linha reta (ou um hiperplano em mais dimensões) diretamente no espaço 2D, podemos mapear os dados para uma **dimensão superior**. No caso de 2D, os dados poderiam ser mapeados para 3D *(dimensão $x+1$)*.

Por exemplo, imagine que temos um mapeamento simples como:

$$
	\phi(x_{1},y_{1}) = \big(x_{1}^{2}, y_{1}^{2}, \sqrt(2) \cdot x_{1} \cdot y_{1}\big)
$$

Isso transforma um ponto $(x_{1},y_{1})$  em um ponto $(x_{1}^{2}, y_{1}^{2}, \sqrt(2) \cdot x_{1} \cdot y_{1})$ no espaço tridimensional.

###### Passo 3: Kernel Trick - Produto interno no novo espaço

Em vez de fazer o cálculo explícito da transformação dos dados para o espaço de maior dimensão *(o que pode ser computacionalmente caro)*, o **kernel trick** permite que calculemos o produto interno dos pontos no novo espaço, sem precisar realizar a transformação diretamente. O kernel é uma função que computa esse produto interno de forma eficiente.

No caso do exemplo acima, o kernel que realiza esse mapeamento pode ser expresso como:

$$K(x_{1},y_{1}) = (x_{1}+y_{1})^{2}$$

Esse kernel calcula o produto interno dos dados no novo espaço de forma implícita, sem a necessidade de mapear explicitamente os dados para 3D. Isso reduz a complexidade computacional, mantendo a flexibilidade de trabalhar em um espaço de maior dimensão.

###### Passo 4: Criando o SVC no espaço transformado

Agora, os dados mapeados para o novo espaço de dimensão $x+1$ se tornam separáveis linearmente. No novo espaço, um **SVC (Support Vector Classifier)** é treinado para encontrar o hiperplano que melhor separa as duas classes.

Em resumo, com o **kernel trick**, o SVM consegue transformar dados não linearmente separáveis em um espaço onde eles se tornam linearmente separáveis. O **SVC** é então treinado nesse novo espaço para encontrar o **hiperplano de máxima margem**. Isso permite que o SVM classifique dados que não poderiam ser separados por uma linha ou um hiperplano no espaço original.