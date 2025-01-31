# Distribuição Chi-Quadrado 

Para cada $m$ positivo, a distribuição $Gamma(m/2, 1/2)$ é chamada de distribuição $\chi^2$. Ela foi primeiramente descrita por Helmert para computar a distribuição amostral de uma população normal. Vamos ver como a normal se relaciona mais a frente. 

$$
f(x) = \frac{1}{2^{m/2}\Gamma(m/2)}x^{m/2 - 1}e^{-x/2}
$$


## Propriedades

Se $X \sim \chi^2(m)$, então:

$$
E(X) = m
$$

$$
Var(X) = 2m
$$

$$
\psi(t) = \left(\frac{1}{1-2t}\right)^{m/2}, t < \frac{1}{2}
$$

## Soma de $\chi^2$

Se $X_1, ..., X_k$ são independentes e cada uma tem grau de liberdade $m_i$, então $X_1 + ... + X_n$ tem distribuição $\chi^2(m_1 + .... + m_k)$

## Relação com a Normal

Se $X$ tem distribuição normal padrão, $Y = X^2 \sim \chi^2(1)$

De fato, se juntarmos as últimos dois teoremas, veremos que a soma de quadrados de normais independentes e identicamente distribuidas será $\chi^2(m)$, onde $m$ é o número de parcelas. 

## Implementação


```python
import numpy as np 
import matplotlib.pyplot as plt
from scipy.stats import chi2

from matplotlib import animation, cm
from IPython.display import HTML

# Random Object
ro = np.random.default_rng(1000)  # Para assegurar reprodutibilidade
```


```python
degree_freedom = 10
mean, var, skew, kurt = chi2.stats(degree_freedom, moments = 'mvsk')
print('Propriedades')
print('Média: {}'.format(mean))
print('Var: {}'.format(var))
print('Assimetria: {}'.format(skew))
print('Curtose: {}'.format(kurt))
```

    Propriedades
    Média: 10.0
    Var: 20.0
    Assimetria: 0.8944271909999159
    Curtose: 1.2



```python
fig, ax = plt.subplots(1, 1)
x = np.linspace(chi2.ppf(0.01, degree_freedom), 
                chi2.ppf(0.99, degree_freedom), 100)
ax.plot(x, chi2.pdf(x, degree_freedom), 'r-', lw=5, alpha=0.6, label='chi2 pdf')

r = chi2.rvs(degree_freedom, size = 10000)
ax.hist(r, density = True, alpha = 0.2)

ax.legend()

plt.show()
```


![png](output_4_0.png)



```python
fig, ax = plt.subplots()

line, = ax.plot(x, chi2.pdf(x, degree_freedom), 'r-', lw=5, alpha=0.6)

ax.set_xlim((0,150))
ax.set_title('Chi-Square')

def animate(i, degree_freedom):
    
    x = np.linspace(0, chi2.ppf(0.99, degree_freedom + i), 100)

    line.set_data(x, chi2.pdf(x, degree_freedom + i))
    
    return line,

anim = animation.FuncAnimation(fig, animate, frames = 100,
                               interval = 50, fargs=(degree_freedom,), repeat = False)
HTML(anim.to_html5_video())
```




<video width="432" height="288" controls autoplay>
  <source type="video/mp4" src="data:video/mp4;base64,AAAAIGZ0eXBNNFYgAAACAE00ViBpc29taXNvMmF2YzEAAAAIZnJlZQAATVhtZGF0AAACrgYF//+q
3EXpvebZSLeWLNgg2SPu73gyNjQgLSBjb3JlIDE2MCByMzAxMSBjZGU5YTkzIC0gSC4yNjQvTVBF
Ry00IEFWQyBjb2RlYyAtIENvcHlsZWZ0IDIwMDMtMjAyMCAtIGh0dHA6Ly93d3cudmlkZW9sYW4u
b3JnL3gyNjQuaHRtbCAtIG9wdGlvbnM6IGNhYmFjPTEgcmVmPTMgZGVibG9jaz0xOjA6MCBhbmFs
eXNlPTB4MzoweDExMyBtZT1oZXggc3VibWU9NyBwc3k9MSBwc3lfcmQ9MS4wMDowLjAwIG1peGVk
X3JlZj0xIG1lX3JhbmdlPTE2IGNocm9tYV9tZT0xIHRyZWxsaXM9MSA4eDhkY3Q9MSBjcW09MCBk
ZWFkem9uZT0yMSwxMSBmYXN0X3Bza2lwPTEgY2hyb21hX3FwX29mZnNldD0tMiB0aHJlYWRzPTYg
bG9va2FoZWFkX3RocmVhZHM9MSBzbGljZWRfdGhyZWFkcz0wIG5yPTAgZGVjaW1hdGU9MSBpbnRl
cmxhY2VkPTAgYmx1cmF5X2NvbXBhdD0wIGNvbnN0cmFpbmVkX2ludHJhPTAgYmZyYW1lcz0zIGJf
cHlyYW1pZD0yIGJfYWRhcHQ9MSBiX2JpYXM9MCBkaXJlY3Q9MSB3ZWlnaHRiPTEgb3Blbl9nb3A9
MCB3ZWlnaHRwPTIga2V5aW50PTI1MCBrZXlpbnRfbWluPTIwIHNjZW5lY3V0PTQwIGludHJhX3Jl
ZnJlc2g9MCByY19sb29rYWhlYWQ9NDAgcmM9Y3JmIG1idHJlZT0xIGNyZj0yMy4wIHFjb21wPTAu
NjAgcXBtaW49MCBxcG1heD02OSBxcHN0ZXA9NCBpcF9yYXRpbz0xLjQwIGFxPTE6MS4wMACAAAAP
+2WIhAA3//728P4FNjuY0JcRzeidMx+/Fbi6NDe9zgAAAwAAN9zmRP7KkxJl8J7BxwANoQ7On2gW
ANKorz63stWBcBQll9FTOfNhvUeG2fcVcFUeu7D6RuGcKJsPdixS6EfEFXal/EPDE5NKwf/syz7w
tOmTc3KF55e4x55Z5P7NIjE2LKZDVjv041dYPBXvAFniMNVoZ0w0/s08AzqC44U0YIL8TPoFXK2p
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
AAAAHGVsc3QAAAAAAAAAAQAAE4gAAAQAAAEAAAAABiRtZGlhAAAAIG1kaGQAAAAAAAAAAAAAAAAA
ACgAAADIAFXEAAAAAAAtaGRscgAAAAAAAAAAdmlkZQAAAAAAAAAAAAAAAFZpZGVvSGFuZGxlcgAA
AAXPbWluZgAAABR2bWhkAAAAAQAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVy
bCAAAAABAAAFj3N0YmwAAAC3c3RzZAAAAAAAAAABAAAAp2F2YzEAAAAAAAAAAQAAAAAAAAAAAAAA
AAAAAAABsAEgAEgAAABIAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAY
//8AAAA1YXZjQwFkABX/4QAYZ2QAFazZQbCWhAAAAwAEAAADAKA8WLZYAQAGaOvjyyLA/fj4AAAA
ABx1dWlka2hA8l8kT8W6OaUbzwMj8wAAAAAAAAAYc3R0cwAAAAAAAAABAAAAZAAAAgAAAAAUc3Rz
cwAAAAAAAAABAAAAAQAAAtBjdHRzAAAAAAAAAFgAAAAGAAAEAAAAAAEAAAgAAAAAAgAAAgAAAAAB
AAAGAAAAAAEAAAIAAAAAAQAACAAAAAACAAACAAAAAAEAAAgAAAAAAgAAAgAAAAABAAAIAAAAAAIA
AAIAAAAAAQAABgAAAAABAAACAAAAAAEAAAYAAAAAAQAAAgAAAAABAAAIAAAAAAIAAAIAAAAAAQAA
CgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAGAAAAAAEAAAIAAAAAAQAABgAAAAABAAAC
AAAAAAEAAAgAAAAAAgAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAgA
AAAAAgAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAYAAAAAAQAAAgAA
AAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAABAAAAAAAA
AAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAA
AQAAAAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAAB
AAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEA
AAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAA
AgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAABAAAA
AAAAAAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAEAAAAABxzdHNj
AAAAAAAAAAEAAAABAAAAZAAAAAEAAAGkc3RzegAAAAAAAAAAAAAAZAAAErEAAAKjAAABZgAAASwA
AADlAAAA3AAAAWoAAACTAAAAfwAAARUAAABvAAABTgAAAHAAAABaAAABFwAAAH4AAABXAAABFAAA
AGQAAABKAAAA6AAAAFQAAADjAAAATwAAAQQAAAB2AAAASwAAAU8AAABuAAAAZwAAAFEAAAEnAAAA
QwAAAO4AAABNAAAA1AAAAFsAAABIAAAA9gAAAGEAAAA+AAAASAAAAP8AAABZAAAAUAAAARoAAABp
AAAASQAAAEMAAADKAAAASwAAARUAAABnAAAATwAAAEoAAAFOAAAAbwAAAE0AAABGAAABEwAAAGIA
AABbAAAAVAAAAPIAAAB1AAAAUQAAAEAAAAETAAAAZAAAAFIAAABRAAABDwAAAGsAAABKAAAATQAA
APQAAABpAAAATAAAAFMAAADsAAAAeQAAAEkAAABLAAAA7gAAAG0AAABJAAAASwAAAP8AAABzAAAA
RQAAAEMAAADlAAAAewAAAFIAAABUAAAAdwAAAGoAAABTAAAATwAAAGMAAAAUc3RjbwAAAAAAAAAB
AAAAMAAAAGJ1ZHRhAAAAWm1ldGEAAAAAAAAAIWhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAA
AAAALWlsc3QAAAAlqXRvbwAAAB1kYXRhAAAAAQAAAABMYXZmNTguNDUuMTAw
">
  Your browser does not support the video tag.
</video>




![png](output_5_1.png)


# Distribuição Conjunta da média e variância amostrais

$X_1,...,X_n$ formam uma amostra aleatória com distribuição normal e com média $\mu$ e variância $\sigma^2$ desconhecidos. Estamos interessados na distribuição conjunta dos estimadores de máxima verossimilhança para média e variância da amostra. 

## Teorema de Basu

Sejam $\hat{\mu} = \bar{X}_n$ e $\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (X_i - \bar{X}_n)^2$ a média e variância amostrais, respectivamente. Então $\hat{\mu}$ tem distribuição normal com média $\mu$ e variância $\sigma^2 /n$, enquanto $n\hat{\sigma}^2/\sigma^2$ tem a distribuição $\chi^2(n-1)$, isto é, com $n-1$ grau de liberdade. Além disso elas são independentes. 

Esse teorema é um pouco mais complexo e, na verdade, essa seria uma espécie de aplicação do teorema, na verdade. O teorema de Basu diz que: 

> Se $T$ é uma estatística suficiente [completa](https://lucasmoschen.github.io/TA_sessions/infestatistica_BSc/SufficientStatistics/#definicoes-adicionais) (Considere, nesse teorema, $g$ uma função integrável limitada) para $\theta$ e $A$ uma estatística ancillary, então $T$ é independente de $A$. Nesse caso $\hat{\mu}$ é completa suficiente e $\hat{\sigma}^2$ é ancillary, por que não depende de $\mu$. 

O mais interessante é que essa propriedade é só vista com a [distribuição normal](https://arxiv.org/pdf/1810.01768.pdf)! Olhem a página 9.  

### Demonstração 

O livro tem uma abordagem um pouco mais voltado à Álgebra Linear. Aqui vou mostrar uma ideia um pouco diferente, onde vocês podem demonstrar os passos, como exercício. 

1. Passo 1: $\sum_{i=1}^n X_i^2 = n\hat{\sigma}^2 + n\hat{\mu}^2$

    - Dica: Escrever $\hat{\sigma}^2$ e abrir em três somatórios. 

2. Passo 2: $\sum_{i=1}^n (X_i - \mu)^2 = n\hat{\sigma}^2 + n(\hat{\mu} - \mu)^2$

    - Dica: O Passo 1 é um caso especial do Passo 2. O processo é o mesmo.

3. Passo 3: $\hat{\mu}$ é independente de $X_i - \hat{\mu}, i = 1,...,n$.

    - Dica: Montar a pdf conjunta de $X_1, ..., X_n$ (já fizemos isso atraveś da verossimilhança) e fazer uma mudança de variável $Y_1 = \hat{\mu}, Y_2 = X_2 - \hat{\mu}, ..., Y_n = X_n - \hat{\mu}$. Com essa mudança, é possível montar a pdf como função de $y_1,...,y_n$. Esse processo é um pouco mais chato, mas é bom lembrar como fazez mudança de variável para pdfs. [Aqui você pode conferir como](https://en.wikipedia.org/wiki/Probability_density_function#Vector_to_vector). É importante lembrar que é uma função de $y$ após transformada e não de $x$. 
    - Dica 2: Fatorizar a pdf conjunta. Você vai ver como se destaca a independência aqui. 

4. Passo 4: Mostrar que $\hat{\mu}$ e $\hat{\sigma}^2$ são independentes. 


#### Referências

[1](https://jekyll.math.byuh.edu/courses/m321/handouts/mean_var_indep.pdf)
[2](http://www2.stat.duke.edu/courses/Fall18/sta611.01/Lecture/lec12_mean_var_indep.pdf)


## Simples visualização

Eu gostaria de comparar o que acontece com a média e variância amostral da distribuição normal e da distribuição gamma. Para isso, geero amostras de tamanho $n$, calculo as estatísticas e salvo. Faço esse procedimento o número de pontos que quiser. 


```python
ite = 10000
n = 10000
# Parâmetros da Normal
mu = 5
sigma = 2
# Parâmetros da Gamma
alpha = 5
beta = 4
```


```python
means = np.zeros((ite,2))
variances = np.zeros((ite,2))

for i in range(ite): 
    X = ro.normal(loc = mu, scale = sigma, size = n)
    Y = ro.gamma(shape = alpha, scale = 1/beta, size = n)
    
    means[i,0] = np.mean(X)
    means[i,1] = np.mean(Y)

    variances[i,0] = np.var(X, ddof = 0)
    variances[i,1] = np.var(Y, ddof = 0)

coef_normal = np.polyfit(x = means[:,0], y = variances[:,0], deg = 1)
coef_gamma = np.polyfit(x = means[:,1], y = variances[:,1], deg = 1)
```


```python
fig, ax = plt.subplots(1,2,figsize = (14,5))
fig.suptitle('Comparando média e variância amostral')

ax[0].scatter(means[:,0], variances[:,0])
ax[1].scatter(means[:,1], variances[:,1])
ax[0].plot(means[:,0], coef_normal[0]*means[:,0] + coef_normal[1], color = 'red')
ax[1].plot(means[:,1], coef_gamma[0]*means[:,1] + coef_gamma[1], color = 'red')


ax[0].set_xlabel(r'$\bar{X}_n$', fontsize = 18)
ax[1].set_xlabel(r'$\bar{X}_n$', fontsize = 18)
ax[0].set_ylabel(r'$\sum (X_i - \bar{X}_n)^2$', fontsize = 18)
ax[1].set_ylabel(r'$\sum (X_i - \bar{X}_n)^2$', fontsize = 18)
ax[0].set_title('Distribuição Normal')
ax[1].set_title('Distribuição Gamma')
ax[0].grid(alpha = 0.5, linestyle = '--')
ax[1].grid(alpha = 0.5, linestyle = '--')
plt.show()
```


![png](output_10_0.png)


*Obs: A não inclinação da reta não significa que existe independência, mas como são independentes, a gente espera que a inclinação seja pequena.* 

# Distribuições T Student 

[Artigo original](http://seismo.berkeley.edu/~kirchner/eps_120/Odds_n_ends/Students_original_paper.pdf): Olhe a página 9!

### Definição 

Sejam $Y \sim \chi^2(m)$ e $Z \sim N(0,1)$ independentes. Então 

$$
X = \frac{Z}{\left(\frac{Y}{m}\right)^{1/2}} \sim t(m)
$$

onde $t(m)$ é a distribuição t-student com $m$ graus de liberdade. 

## Função densidade de probabilidade 

Para escrever essa função de probabilidade, defina $X$ como acima e $W = Y$. Já sabemos a distribuição conjunta de $Y$ e $Z$, pois eles são independentes. Com essa  mudança de variável ([confira aqui se não lembra como é feito](http://dept.stat.lsa.umich.edu/~moulib/426-notes-3.pdf)), você conseque escrever a distribuição conjunta de $X$ e $W$. Depois, basta calcular a distribuição marginal de $X$, integrando em $W$.

$$
f(x) = \frac{\Gamma\left(\frac{m+1}{2}\right)}{(m\pi)^{1/2}\Gamma\left(\frac{m}{2}\right)}\left(1 + \frac{x^2}{m} \right)^{-(m+1)/2}, x \in \mathbb{R},
$$

onde $\Gamma$ é a [função Gamma](https://en.wikipedia.org/wiki/Gamma_function), tal que, 

1. $n \in \mathbb{N}, \Gamma(n) = (n-1)!$
2. $\Gamma(z+1) = z\Gamma(z)$ 
3. $\Gamma(1/2) = \sqrt{\pi}$

Quando $m \leq 1$, a média é divergente. Isso pode ser vizualizado pelo expoente que será $\leq -1$, o que diverge (lembre de $\int 1/x$). Quando $m > 1$, a média existe e é 0 pela simetria da distribuição. Em particular, podemos mostrar que se $k < m$, $E[|X^k|] < + \infty$ e se $k \geq m$, o momento diverge. 

Se $X \sim t(m), m > 2$, $Var(X) = \frac{m}{m-2}$

## Teorema 

Seja $X_1, ..., X_n \overset{iid}{\sim} N(\mu,\sigma^2)$. Seja

$$
\sigma ' = \left[\frac{\sum_{i=1}^n (X_i - \bar{X}_n)^2}{n-1}\right]^{1/2}
$$

Então $n^{1/2}(\bar{X}_n - \mu)/\sigma ' \sim t(n-1)$

## Relação com a Normal e Cauchy

Da mesma forma que a distribuição normal e a distribuição Cauchy, a distribuição t é centrada em $0$ e tem sua moda nesse valor. Entretanto a cauda a distribuição t (quando $x \to -\infty$ ou $x \to +\infty$), é mais pesada, no sentido de que tende para $0$ em uma velocidade menor do que a normal. Outra coisa interessante é que a ditrivuição $t(1)$ é a [distribuição Cauchy](https://en.wikipedia.org/wiki/Cauchy_distribution). Além disso, quando $n \to \infty$, converge para a pdf da normal padrão ($Normal(0,1)$).

### Ferramentas para demonstrar a convergência

1. [Teorema de Slutsky](https://lucasmoschen.github.io/TA_sessions/infestatistica_BSc/LargeRandomSamples/LargeRandomSamples/#metodo-delta): Considere o corolário com $f(x,y) = \frac{x}{y}$ 

2. [Lei dos Grandes Números](https://lucasmoschen.github.io/TA_sessions/infestatistica_BSc/LargeRandomSamples/LargeRandomSamples/#lei-dos-grandes-numeros): Escreva a qui-quadrado como soma de normais. 


```python
from scipy.stats import t, norm, cauchy
```

## Implementação 

Primeiro vamos ver a cara da distribuição t


```python
m = 10
X = t(df = m) 
w = np.arange(-3, 3, 0.1)

fig, ax = plt.subplots(1,2,figsize = (12,5))
ax[0].plot(w, X.pdf(w), lw = 5, color = 'orange')
ax[1].plot(w, X.cdf(w), lw = 5, color = 'orange')
ax[0].set_title('PDF t-Student')
ax[1].set_title('CDF t-Student')
plt.show()
```


![png](output_15_0.png)


Vamos ver o que acontece quando $m \leq 1$?


```python
ite = 1000
n = 10000
m1 = 10
m2 = 0.5

means = np.zeros((ite,2))
for i in range(ite): 
    X = ro.standard_t(df = m1, size = n)
    Y = ro.standard_t(df = m2, size = n)
    means[i,0] = np.mean(X)
    means[i,1] = np.mean(Y)
```


```python
fig, ax = plt.subplots(1,2,figsize = (14,5))
ax[0].hist(means[:,0], bins = 100)
ax[1].hist(np.log(means[:,1]), bins = 10)
ax[0].set_xlabel('E[X]')
ax[1].set_xlabel('log E[X]')
ax[0].set_title('m = 10')
ax[1].set_title('m = 0.5')
plt.show()
```

    <ipython-input-11-2bfd1961d53b>:3: RuntimeWarning: invalid value encountered in log
      ax[1].hist(np.log(means[:,1]), bins = 10)



![png](output_18_1.png)


No eixo $x$ do segundo gráfico plotei o logaritmo, dado que alguns resultados eram extremamente grandes! Isso indica visualmente que a média diverge!

### Relação com a Normal e com Cauchy


```python
C = cauchy()
Z = norm(loc = 0, scale = 1) 
T = t(df = 1)

fig, ax = plt.subplots(1,2,figsize = (14,5))
ax[0].plot(w,C.pdf(w), label = 'Cauchy')
ax[0].scatter(w, T.pdf(w), c = 'red', marker = "*", label = 't-Student')
ax[0].legend()
ax[0].set_title('t-Student e Cauchy quando m = 1')
ax[1].plot(w,Z.pdf(w), label = 'N(0,1)')
ax[1].set_title('Convergência da t para a normal')

for i in np.logspace(np.log10(1), np.log10(20), 5):
    T = t(df = int(i))
    ax[1].plot(w, T.pdf(w), linestyle = '--', alpha = i/40 + 0.5, color = 'grey', label = 't({})'.format(int(i)))
ax[1].legend(loc = 'upper right')
plt.show()
```


![png](output_21_0.png)


# Distribuição F

Sejam $Y \sim \chi^2_m$ e $W \sim \chi^2_n$ independentes. Defina

$$
X = \frac{Y/m}{W/n} = \frac{nY}{mW}
$$

Dizemos que $X$ tem distribuição $F$. A sua motivação vem do teste de hipóteses que compara variâncias de duas normais. 

## Função de densidade de probabilidade

Seja $X \sim F_{m,n}$. Então sua pdf tem suporte em $x > 0$ e pe definida
$$
f(x) = \frac{\Gamma\left[\frac{1}{2}(m+n)\right]m^{m/2}n^{n/2}}{\Gamma\left(\frac{1}{2}m\right)\Gamma\left(\frac{1}{2}n\right)}\cdot \frac{x^{(m/2) - 1}}{(mx + n)^{(m+n)/2)}}
$$

Observe que ela não é simétrica em $m$ e $n$. Assim, se trocarmos eles de lugar, teremos um resultado diferente. 

## Propriedades 

Seja $X \sim F_{m,n}$. Então $1/X \sim F_{n,m}$. Se $Y \sim t_n$, então $Y^2 \sim F_{1,n}$. 

Existem diversas relações que são encontradas com outras distribuições. [Confira aqui](https://en.wikipedia.org/wiki/F-distribution#Properties_and_related_distributions)

$$
E[X] = \frac{n}{n-2}, n > 2
$$
$$
Var[X] = \frac{2n^2(m + n - 2)}{m(n-2)^2(n-4)}
$$



```python
import numpy as np
from scipy.stats import f
import matplotlib.pyplot as plt
```

Vamos ver como é a cara dessa distribuição:


```python
m, n = 20, 10
```


```python
X = f(dfn = m, dfd = n) 
w = np.arange(0, 5, 0.1)

fig, ax = plt.subplots(1,2,figsize = (12,5))
ax[0].plot(w, X.pdf(w), lw = 5, color = 'orange')
ax[1].plot(w, X.cdf(w), lw = 5, color = 'orange')
ax[0].set_title('PDF Distribuição F')
ax[1].set_title('CDF Distribuição F')
plt.show()
```


![png](output_26_0.png)

