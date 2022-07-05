# Estatística suficiente

Um estatístico usa a informação de uma amostra $X_1, \dots, X_n$ para fazer inferência sobre uma quantidade de interesse $\theta$.
De acordo com Fisher, em "On the Mathematical Foundations of Theoretical Statistics", "o objeto dos métodos estatísticos é a redução dos dados".
Como a quantidade de dados é incapaz de ser compreendida diretamente pelo cérebro, ela é reduzida por poucas quantidades que representam o todo, pelo menos a informação relevante para o problema. 
Nesse sentido, uma estatística é uma forma de representar esses dados, em geral diminuir sua dimensão (os próprios dados formam uma estatística, então isso não é uma condição necessária).
De forma precisa, a definição de **estatística** é:

> Seja $(\mathcal{T}, \mathcal{C})$ um espaço mensurável em que $\mathcal{C}$ contenha todos os conjuntos unitários formados pelo elementos de $\mathcal{T}$. Se $T : \mathcal{X} \to \mathcal{T}$ é mensurável, então $T$ é uma estatística.

Com isso, podemos definir uma **estatística suficiente** no sentido clássico (lembrando que temos uma contrapartida bayesiana baseada na posteriori).

> Seja $T: \mathcal{X} \to \mathcal{T}$ uma estatística e $\mathcal{P}$ uma família de distribuições parametrizada por $\theta$ e definida em $(\mathcal{X}, \mathcal{B})$ (espaço amostral com $\sigma$-álgebra $\mathcal{B}$). Suponha que existem $P_{\theta}(\cdot|T)$ e uma função $r : \mathcal{B} \times \mathcal{T} \to [0,1]$ tal que $r(\cdot, t)$ é uma medida de probabilidade em $(\mathcal{X}, \mathcal{B})$ para todo $t \in \mathcal{T}$, $r(A, \cdot)$ é mensurável para todo $A \in \mathcal{B}$ e, para todo $\theta \in \Theta$ e $B \in \mathcal{B}$,
> $$
P_{\theta}(B|T=t) = r(B,t)
> $$
> quase certamente. Então dizemos que $T$ é **estatística suficiente** para $\theta$.

Apesar dessa definição ser bastante complexa, a ideia é que a distribuição condicional de $X$ dado $T=t$ não depende de $\theta$, isto é, a informação trazida por $T=t$ sobre $\theta$ compreende toda a informação disponível de $X$.
Após observar $T(x) = t$, podemos amostrar de $r(\cdot, t)$ e teremos dados falsos que imitam os iniciais, pois a distribuição será a mesma.
Assim, se considerarmos dois experimentadores, um tendo a amostra inteira, e o outro tendo apenas uma estatística suficiente, ambos terão a mesma quantidade de informação sobre o parâmetro de interesse $\theta$.

Note que, pela lei da esperança total,
$$
P_{\theta}(X \in B) = \mathbb{E}_{\theta}[P_{\theta}(X \in B|T)] = \mathbb{E}_{\theta}[r(B, T)].
$$
Se tomarmos $Y \sim r(\cdot, t)$ quando $T=t$, teremos 
$$
P_{\theta}(Y \in B) = \mathbb{E}_{\theta}[P_{\theta}(Y \in B|T)] = \mathbb{E}_{\theta}[r(B, T)].
$$

**Proposição:** A estatística de ordem $(X_{(1)}, \dots, X_{(n)})$ é estatística suficiente.

## Fatorização de Fisher-Neyman

Seja $f(\boldsymbol{x}|\theta)$ a densidade de uma distribuição de $\boldsymbol{X} = (X_1, \dots, X_n)$ (com respeito a uma medida $\nu$ $\sigma$-finita, como a medida de Lebesgue em $\mathbb{R}^n$). Então $T(\boldsymbol{X})$ é estatística suficiente para $\theta$ se, e somente se, existem funções $m_1$ e $m_2$ tal que 
$$
f(\boldsymbol{x}|\theta) = m_1(\boldsymbol{x})m_2(T(\boldsymbol{x}) , \theta), \forall \theta \in \Theta.
$$

O lema 2.24 demonstrado no livro de Schervish determina que sob as hipóteses do teorema de Fisher-Neyman e assumindo que $T$ é suficiente, obtemos que existe uma medida em $(\mathcal{T}, \mathcal{C})$ que domina a distribuição de probabilidade de $T$ e define a densidade de $T=t$ sob o parâmetro $\theta$ como $m_2(t,\theta)$.

## Estatística suficiente mínima e completa

A estatística de ordem é uma estatística que pouco reduz a informação do dado. 
De fato, só retira a questão da ordenação. 
Todavia, algumas vezes uma estatística mais simples também é suficiente e, por isso, faz sentido definir quando ela é mínima.

> Uma estatística suficiente $T$ é dita **suficiente mínima** se para toda estatística $U$, existe uma função mensurável $g$ tal que $T = g(U)$ para todo $\theta$.

**Teorema (Lehmann-Scheffé):** Seja $f(x|\theta)$ a densidade e $T$ uma função mensurável tal que $T(x) = T(y) \iff y \in D(x)$, com
$$
D(x) = \{y \in \mathcal{X} : f(y|\theta) = f(x|\theta)h(x,y), \forall \theta \text{ e alguma função } h(x,y) \}.
$$

---
``📝`` **Exemplo**
}
Seja $X_1, \dots, X_n \overset{iid}{\sim} \operatorname{Bernoulli}(\theta)$. Temos que 
$$
f(x_1,\dots,x_n|\theta) = \theta^{S_x}(1-\theta)^{n-S_x},
$$
em que $S_x = \sum_{i=1}^n x_i$. 
Assim
$$
\frac{f(x_1,\dots,x_n|\theta)}{f(y_1,\dots,y_n|\theta)} = \left(\frac{\theta}{1-\theta}\right)^{S_x-S_y},
$$
que independe de $\theta$ se, e somente se, $S_x = S_y$. 
Isso mostra que $T(x) = S_x$ é estatística suficiente mínima.

---

---
``📝`` **Exemplo - Família Exponencial**

Considere uma distribuição com densidade 
$$
p_{\theta}(x) = \exp\{\eta(\theta)\cdot T(x) - B(\theta)\}h(x)
$$
com respeito a medida de Lebesgue. 
Pelo Teorema da Fatorização $T(x)$ é estatística suficiente.
Assim
$$
\log\left(\frac{p_{\theta}(y)}{p_{\theta}(x)}\right) = \eta(\theta)\cdot (T(y) - T(x)) + \log(h(y)) - \log(h(x)).
$$
Logo $T$ é estatística suficiente mínima se, e somente se, o complemento ortogonal de $\eta(\theta)$ possui apenas o $0$.

---

> Uma estatística $T$ é dita **completa** se para toda função $g$ mensurável e $\theta \in \Theta$, $\mathbb{E}_{\theta}[g(T)] = 0$ implique $g(T) = 0$. Ela será **completa limitada** se adicionamos a condição de que $g$ é limitada.

**Teorema de Bahadur:** Se $U$ é uma estatística suficiente completa limitada e de dimensão finita, então ela é suficiente mínima.

Ideias da demonstração:

- Tome uma outra estatística $T$ e defina $V_i(U) = (1 + \exp\{U_i\})^{-1}$ para cada componente de $U$. Note que $V$ é limitada.
- Defina $H_i(t)$ como o valor esperado de $V_i$ dado que $T=t$ e $L_i(u)$ como o valor esperado de  $H_i(T)$ quando $U=u$, que não dependem de $\theta$, pois as estatísticas são suficientes.
- Veja que $\mathbb{E}_{\theta}[V_i(U) - L_i(U)] = 0$, o que implica que $\mathbb{P}(V_i = L_i) = 1$ pois $U$ é completa.
- Conclua usando a Lei da Variância Total que $U_i = V_i^{-1}(H_i(T))$.

Note que se $U$ é completa, então $U$ é completa limitada, o que nos dá um resultado mais claro: Uma estatística suficiente e completa é suficiente mínima.

## Ancilaridade

Na outra ponta, temos estatísticas que são independentes do parâmetro.

> Uma estatística $U$ é dita anciliar se a sua distribuição independe de $\theta$.

---
``📝`` **Exemplo - Caso normal**

Sejam $X_1, X_2 \overset{iid}{\sim} \operatorname{Normal}(\mu, 1)$ e defina $U = X_2 - X_1$. Soma de normais independentes faz com que 
$U \sim \operatorname{Normal}(0, 2)$ e $U$ é anciliar.

---

Se $T=(T_1, T_2)$ é estatística suficiente mínima e $T_2$ é anciliar, dizemos que $T_1$ é **suficiente condicionalmente** dado $T_2$.

Quando uma estatística é anciliar, não significa que ela não tem importância e, portanto, deveria ser ignorada. 
Significa que se ela fosse a única observação possível, não mudaríamos a informação sobre $\theta$. 
Podemos, todavia, alterar a informação sobre outras quantidades, todavia.

Uma estatística ancilar $U$ é **maximal** se toda outra estatística ancilar é função de $U$.

**Teorema de Basu:** se $T$ é uma estatística suficiente completa limitada e $U$ é anciliar, então $U$ e $T$ são independentes sob $P_{\theta}$ para qualquer $\theta$.

## Computacional 

Nesse notebook, que está disponível [neste link](https://nbviewer.org/github/lucasmoschen/ta-sessions/blob/master/Statistical_Inference_MSc/Notebooks/Sufficient_Statistics.ipynb), faremos alguns poucos experimentos para ilustrar fatos verificados no capítulo de Estatística Suficiente.


```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats
from tqdm import tqdm
```

### Amostrando!

Seja $X_1, \dots, X_n$ uma amostra aleatória de uma distribuição $P_{\theta}$. 
Seja $T(X)$ uma estatística suficiente. 
Sabemos que $\mathbb{P}(X_1, \dots, X_n | T(X) = t)$ independe de $\theta$.
Suponha então que temos dois experimentadores. 
O primeiro captura todas as amostras e passa para o segundo experimentador apenas o valor de $T(X)$ para economizar!
Vamos verificar que o segundo experimentador consegue, agora, obter amostras fake da amostra original.

Vamos começar com um exemplo simples: $X_1, \dots, X_n \sim \operatorname{Normal}(\mu, 1)$. Uma estatística suficiente (mínima, inclusive) nesse caso é $\bar{X} = n^{-1}(X_1 + \dots + X_n)$.

Sabemos que $\bar{X} \sim \operatorname{Normal}(\mu, n^{-1})$. Assim, 
$$
f(X_1, \dots, X_n | \bar{X} = t) = \frac{(2\pi)^{-n/2}\exp\{-1/2 \sum_{i=1}^n(x_i-\mu)^2\}}{(2\pi n^{-1})^{-1/2}\exp\{-n/2(t-\mu)^2\}} \propto \exp\left\{-\frac{1}{2}(S_x^2 - 2\mu n t + n\mu^2 - nt^2 + 2\mu n t - n\mu^2).\right\} = \exp\left\{-\frac{1}{2}\sum_{i=1}^n (x_i^2 - t^2)\right\},
$$
em que $S_x^2 = \sum_{i=1}^n x_i^2$ e $X_n = nt - \sum_{i=1}^{n-1} X_i$.

Note que podemos escrever 
$$
f(X_1, \dots, X_{n-1} | \bar{X} = t) \propto \exp\left\{nt^2/2\right\}\exp\left\{-\frac{1}{2}\left[\sum_{i=1}^{n-1} x_i^2 + \left(nt - \sum_{i=1}^{n-1} x_i\right)^2 \right]\right\} = \exp\left\{nt^2/2\right\}\exp\left\{-\frac{1}{2}\left[\sum_{i=1}^{n-1} x_i^2 + n^2t^2 - 2nt\sum_{i=1}^{n-1} x_i + \left(\sum_{i=1}^{n-1} x_i\right)^2\right]\right\}
$$

Assim, 
$$
\begin{split}
f(X_1, \dots, X_{n-1} | \bar{X} = t) &\propto \exp\left\{nt^2/2\right\}\exp\left\{-\frac{1}{2}\left[\sum_{i=1}^{n-1} (x_i^2 - 2nt x_i + nt^2) +nt^2 + \left(\sum_{i=1}^{n-1} x_i\right)^2\right]\right\} \\
&= \exp\left\{-\frac{1}{2}\left[\sum_{i=1}^{n-1} (x_i^2 - 2t x_i + t^2) - 2(n-1)t\sum_{i=1}^{n-1} x_i + (n-1)^2t^2 + \left(\sum_{i=1}^{n-1} x_i\right)^2\right]\right\} \\
&= \exp\left\{-\frac{1}{2}\left[\sum_{i=1}^{n-1} (x_i - t)^2 + \left(\sum_{i=1}^{n-1} (x_i - t)\right)^2 \right]\right\} \\
&= \exp\left\{-\frac{1}{2}\left[\sum_{i=1}^{n-1} (x_i - t)^2 + \sum_{j=1}^{n-1} \sum_{i=1}^{n-1} (x_j-t)(x_i - t) \right]\right\}
\end{split}
$$

Com isso, observamos que $X_1, \dots, X_n | \bar{X} = t$ tem distribuição Normal Multivariada com $\mathbb{E}[X_i] = t$ para $i=1,\dots,n-1$
e matriz de covariância (dada pela inversa) 
$$
\Sigma^{-1} = I_{n-1} + \begin{bmatrix}
1 & \cdots & 1 \\
\vdots & \ddots & \vdots \\
1 & \cdots & 1
\end{bmatrix} := I + A
$$

Veja que $\Sigma = I - A/n$ (mostre!). 

Assim, $X_1, \dots, X_{n-1} | \bar{X} = t \sim \operatorname{Normal}((t,\dots,t), I - A/n)$.


```python
mu = 2
n = 10
Sigma = np.eye(n-1) - np.ones((n-1,n-1))/n
```

Façamos um exemplo em que $\mu = 2$ verdadeiro (e desconhecido para os dois estatísticos). Vamos fazer o seguinte experimento $M$ vezes, com $M = 100000$. Para o primeiro estatístico, oferecemos $n$ amostras. Para o segundo estatístico, só oferecemos a média dessas amostras e ele vai utilizar as contas acima para gerar outras $n$ amostras, isto, ele gerará amostras novas a partir de $X_1, \dots, X_{n-1} | \bar{X} = t \sim \operatorname{Normal}((t,\dots,t), I - A/n)$, pois ele conhecerá $\bar{X}$. 

Como faremos esses experimentos diversas vezes, vamos obter $M$ amostras de $X_1$ para o estatístico 1, e o estatístico 2 vai produzir outras $M$ a partir da distribuição calculada. Provamos que a distribuição delas será a mesma. Vamos verificar graficamente através do histograma.

```python
mu = 2
n = 10
M = 100000

estatistico1 = np.zeros((M, n))
estatistico2 = np.zeros_like(estatistico1)

for k in tqdm(range(M)):
    x = np.random.normal(loc=mu, scale=1, size=n)
    t = x.mean()

    x_fake = np.random.multivariate_normal(mean=t*np.ones(n-1), cov=np.eye(n-1) - np.ones((n-1, n-1))/n)
    x_n = n * t - x_fake.sum()
    x_fake = np.hstack([x_fake, x_n])
    
    estatistico1[k] = x
    estatistico2[k] = x_fake
```

    100%|█████████████████████████████████| 100000/100000 [00:19<00:00, 5034.15it/s]

Veja que de fato os histogramas são muito similares, como esperávamos! Assim, apenas tendo o valor da média, o estatístico 2 foi capaz de produzir novas amostras a partir da mesma distribuição do estatístico 1!

```python
plt.hist(estatistico1[:,0], bins=50, label='Estatístico 1')
plt.hist(estatistico2[:,0], alpha=0.5, bins=50, label='Estatístico 2')
plt.title('Comparando a distribuição do dado contra o dado falso')
plt.legend()
plt.show()
``` 
    
![png](output_9_0.png)

### Ancilaridade

Uma estatística anciliar não depende do parâmetro, então não pode atualizar a informação sobre ele. 
Será que significa que ela pode ser ignorada? 
Vamos verificar isso com um exemplo numérico. Seja $X_1, \dots, X_n \overset{iid}{\sim} \operatorname{Unif}[\theta-1/2, \theta+1/2]$. Assim 
$$
f(x_1, \dots, x_n | \theta) = \prod_{i=1}^n 1\{\theta -1/2 < x_i < \theta+1/2\} = 1\{\theta - 1/2 < \min\{x_i\}\}1\{\theta + 1/2 > \max\{x_i\}\}
$$
Portanto $T(X) = (\min(X_i), \max(X_i))$ é estatística suficiente mínima.
Seja $U(X) = \max(X_i) - \min(X_i)$.
Vamos verificar que $U$ é estatística anciliar 

Defina $Y_i = X_i - \theta + 1/2 \sim \operatorname{Uniform}(0,1)$. Assim, 
$$
U = \max(X_i) - \min(X_i) = \max(X_i-\theta+1/2) - \min(X_i-\theta+1/2) = \max(Y_i) - \min(Y_i).
$$
Como a distribuição de $Y$ independe de $\theta$, temos que a distribuição de $U$ também independe, o que mostra que $U$ é estatística anciliar.

Vamos visualizar a distribuição de $U$ de duas formas: partindo de $X$ e partido de $Y$.


```python
theta = 5
n = 10

X = np.random.uniform(theta-1/2, theta+1/2, size=(100000, n))
Y = np.random.uniform(size=(100000, n))

# Estamos tomando o máximo de cada linha de X e obtendo 100000 amostras para X.
U1 = X.max(axis=1) - X.min(axis=1)
U2 = Y.max(axis=1) - Y.min(axis=1)
```

Note que de fato as distribuições são muito similares.


```python
plt.hist(U1,  bins=50, label='U = max(X_i) - min(X_i)')
plt.hist(U2, alpha=0.5, bins=50, label='U = max(Y_i) - min(Y_i)')
plt.title('Comparando a distribuição de U')
plt.legend()
plt.show()
```
    
![png](output_13_0.png)
    
Se observamos que $U(X) = u$, podemos calcular que $\max(x_i) | U = u \sim \operatorname{Unif}(\theta-1/2+u, \theta+1/2)$. 
Assim, a distribuição de uma estatística muda com outra anciliar.
