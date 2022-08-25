# Espaços com produto interno 

Primeiro, destacamos algumas definições iniciais importantes para a fluência do estudo.
Depois, definimos o produto interno e suas principais consequências.
Atenção para o processo de Gram-Schmidt é dada em uma subseção separada.

## Conceitos introdutórios

Um conceito fundamental é o de base:

> **Definição:**  Um conjunto de vetores é dito **linearmente independente** se todo subconjunto finito é linearmente independente, isto é, 
> $$
> \sum_{i=1}^n \alpha_i x_i = 0 \implies \alpha_i = 0, \forall i.
> $$
> Se um conjunto de vetores linearmente independente tem a propriedade de que todo vetor pode ser escrito como uma combinação linear de seus elementos, então ele é uma **base**, também chamada de **base de Hamel**. 
> Note que *combinação linear* se refere a uma soma finita. 

Por extensão, uma coleção de subespaços $M_1, \dots, M_n$ é **linearmente independente** se, para todo $i$, 
$$
M_i \cap \sum_{j \neq i} M_j = \{0\},
$$
isto é nenhum vetor de $M_i$ pode ser representado como soma de vetores dos outros conjuntos.
Nesse caso, se $M_1, \dots, M_n$ é linearmente independente e 
$$
X = M_1 + \dots + M_n, 
$$
então esses conjuntos formam uma **decomposição soma direta (interna)**  de $X$, geralmente escrito como 
$$
X = M_1 \oplus \dots \oplus M_n.
$$

Com essas definições básicas, podemos introduzir o **produto interno**.

## Produto interno e suas implicações

> **Definição:** Um produto interno no espaço vetorial $X$, sobre os complexos ou reais, é um mapeamento 
> $$
> X \times X \to F, \text{ tal que } (x,y) \to \langle x,y \rangle, 
> $$
> com as propriedades:

> 1. $\langle x, y \rangle = \overline{\langle y, x \rangle}$ para todo $x,y$.
> 2. $\langle \alpha x + \beta y, x \rangle = \alpha \langle x, z \rangle + \beta \langle y, z \rangle$.
> 3. $\langle x, x \rangle \ge 0$ para todo $x$ e se anula somente se $x=0$.

Note que todo espaço com produto interno é um espaço normado com a norma 
$$
\|x\| = \sqrt{\langle x, x \rangle}.
$$

Alguns exemplos clássicos

---
``📝`` **Exemplo (Espaço Euclidiano)**

O espaço $X = \mathbb{C}^n$ com o mapa 
$$
\langle x, y \rangle = \sum_{i=1}^n x_i\bar{y}_i.
$$
é um espaço com produto interno.

---

---
``📝`` **Exemplo (Funções contínuas)**

O espaço $X = C[a,b]$ o espaço das funções contínuas com imagem complexa com o mapa
$$
\langle f, g \rangle = \int_a^b f(x) \bar{g}(x) \, dx.
$$
é um espaço com produto interno.

---

---
``📝`` **Exemplo (Funções mensuráveis)**

Seja $X = L_2(E, \mu)$ o espaço das funções mensuráveis com respeito a medida $\mu$ em um subconjunto $E$ de uma $\sigma$-álgebra.
Restrinja essas funções pelas classes de equivalência determinadas pela propriedade "iguais exceto em um conjunto de medida nula" e defina o mapeamento
$$
\langle f, g \rangle = \int_E f \bar{g} \, d\mu.
$$
Então $\left(X, \langle \cdot, \cdot \rangle\right)$ é um espaço com produto interno.

---

Alguns teoremas importantes que advém da definição de produto interno:

**Teorema (Cauchy-Schwarz):** Seja $X$ um espaço com produto interno. 
Então, 
$$
|\langle x,y \rangle| \le \|x\|\|y\|,
$$
em que a igualdade só vale se $x$ e $y$ são linearmente dependentes.

**Teorema (Polarização):** Seja $X$ um espaço com produto interno. Então, 
$$
\langle x,y \rangle = \frac{1}{4} \|x+y\|^2 - \frac{1}{4} \|x-y\|^2 + \frac{i}{4}c \|x+iy\|^2 - \frac{i}{4}c \|x-iy\|^2, 
$$
em que $c = 1$ se o espaço é complexo e $c = 0$ se é real.

**Teorema (Lei do Paralelogramo):** Seja $X$ um espaço com produto interno. Então
$$
\|x+y\|^2 + \|x-y\|^2 = 2\|x\|^2 + 2\|y\|^2.
$$

> **Definição:** Dizemos que $x$ e $y$ são **ortogonais** se $\langle x,y \rangle = 0$ e denotamos por $x \perp y$.

**Teorema de Pitágoras:** Se $x \perp y$, então $\|x+y\|^2 = \|x\|^2 + \|y\|^2$.

> **Conjunto ortogonal de vetores:** $S \subset X$ com a propriedade de que $\forall x,y \in S, \langle x,y \rangle = 0$.
Além do mais, se $\|x\| = 1$ para todo $x \in S$, ele é dito **ortonormal**.

---
``📝`` **Exemplo (Espaço de sequências)**

Seja $l_2$ o espaço das sequências de números reais com $\sum_{i=1}^{\infty} x_i^2 < \infty$ e o produto interno nesse espaço 
$$
\langle x,y \rangle = \sum_{i=1}^{\infty} x_i y_i.
$$
O subconjunto $S = \{e_i : i \in  \mathbb{N}\}$, em que $(e_i)_j = 1$ se $j=i$ e $0$ caso contrário, forma um conjunto ortonormal de $l_2$.

---

---
``📝`` **Exemplo (Espaço $L_2$)**

Considere o espaço $L_2([-\pi, \pi])$. A coleção de funções 
$$
x_n = \frac{1}{\sqrt{2\pi}} e^{i n t}
$$
é um conjunto de vetores ortonormal.

---

**Teorema:** Se $X$ é espaço de produto interno e $S \subseteq X$ é ortonormal tal que $0 \not \in S$, então $X$ é LI.

---
Ideia da prova:

Escolha $x_1, \dots, x_n \in S$ e faça $y = \alpha_1 x_1 + \dots + \alpha_n x_n = 0$.
Note que $\langle y, x_i \rangle = 0$, mas pela definição de $S$, $\langle y, x_i \rangle = \alpha_i \langle x_i, x_i \rangle = 0$,
que implica que $\alpha_i = 0$, como queríamos mostrar.

---

### Processo de Gram-Schmidt

Seja $X$ um espaço de produto interno e $\{y_1, \dots, y_n, \dots, \}$ um conjunto de vetores LI.
Então, existe um conjunto ortonormal $\{x_1, \dots, x_n, \dots\}$ tal que 
$$
[\{y_1, \dots, y_n\}] = [\{x_1, \dots, x_n\}], \forall n \in \N.
$$

---
Ideia da prova:

1. Verifique para $n=1$ com $x_1 = y_1/\|y_1\|$.
2. Assuma que exista uma construção de vetores $x_1, \dots, x_{n-1}$ com a propriedade desejada.
Queremos construir o $n$-ésimo vetor:
$$
w = y_n - \sum_{i=1}^{n-1} \langle y_n, x_i \rangle x_i \implies \langle w, x_i \rangle = 0, 1 \le i \le n.
$$
3. É claro que $w \neq 0$, pois nesse caso $y_n$ seria combinação linear de $y_1, \dots, y_{n-1}$, absurdo.
4. Faça $x_n = w/\|w\|$ e prove que $[\{y_1, \dots, y_n\}] = [\{x_1, \dots, x_n\}]$.

---

O interessante desse teorema é que a partir de vetores LI, construímos uma ideia inicial de "base" ortogonal, que é muito mais fácil de se trabalhar. Em particular, os coeficientes de qualquer vetor nessa base são dados por produtos internos simples!

> **Definição:** Seja $X$ um espaço com produto interno. Chamamos 
> $$
> S^{\perp} = \{y \in X : y \perp x, \forall x \in S\}
> $$
> de **complemento ortogonal** de $S$. 

Mesmo que $S$ seja só um conjunto, temos que $S^{\perp}$ é um subespaço de $X$.

**Teorema:** Seja $X$ um espaço com produto interno e $M$ subespaço de dimensão finita. Então $X = M \oplus M^{\perp}$, isto é, para todo $x \in X$, existe $a \in M$ e $b \in M^{\perp}$ tal que $x = a+b$ e $M \cap M^{\perp} = \{0\}$.

## Teorema da Representação de Riesz

Temos que $f$ é um funcional linear limitado definido em um espaço de Hilbert $X$ se, e somente se, existe um único $y \in X$ tal que
$$
f(x) = \langle x,y \rangle.
$$
Em termos do espaço conjugado, podemos descrever esse teorema como 
$$
\tilde{X} = \{f_y(\cdot) = \langle \cdot,y \rangle | \, y \in X\}.
$$

### Operador adjunto

Seja $X$ de dimensão finita e $A : X \to X$ uma transformação linear.
Para $y \in X$, o mapa $f^y(x) = \langle Ax, y \rangle$ é um funcional linear em $X$. 
Pelo Teorema de Riesz, existe $z \in X$ tal que $f^y(x) = \langle x, z \rangle$, isto é, 
$$
\langle Ax, y \rangle = \langle x, z \rangle, \forall x \in X.
$$
Como para cada $y$ existe um único $z$, podemos definir uma função 
$$
A^*(y) = z,
$$
e então, 
$$
\langle Ax, y \rangle = \langle x, A^*y \rangle, \forall x \in X,
$$
o que define $A^*$ como **operador adjunto** de $A$.
Além disso, podemos verificar que ele é uma transformação linear.

Além disso, se $A = A^*$, o operador é **auto-adjunto** e se $AA^* = A^*A$, o operador é **normal**.

## Espaço de Hilbert

Seja $X$ um espaço com produto interno e defina a métrica
$$
d(x,y) = \sqrt{\langle x-y, x-y\rangle}.
$$
Então $(X,d)$ é um espaço métrico. 
Se ele for completo, dizemos que $X$ é um **espaço de Hilbert**.

Já provamos que todo espaço métrico possui um completamento e que todo espaço normado pode ser completado para um espaço de Banach.
Para espaços com produto interno isso também é válido, definindo
$$
\langle x^*, y^* \rangle = \lim_n \langle x_n, y_n \rangle, 
$$
em que $x^*, y^* \in X^*$ é o espaço das classes de equivalência de sequências de Cauchy.

---
``📝`` **Exemplo (Funções contínuas)**

O espaço $X = C[a,b]$ com o produto interno
$$
\langle f, g \rangle = \int_a^b f(x) \bar{g}(x) \, dx.
$$
não é espaço de Hilbert.

---

## Desigualdade de Bessel

Considere o seguinte importante resultado

**Teorema:** Seja $X$ um espaço com produto interno, $A$ um conjunto de vetores ortonormal e $y \in X$. 
Então 

1. (**Desigualdade de Bessel**): $\sum_{i=1}^n |\langle y, x_i \rangle|^2 \le \|y\|^2, \forall x_1, \dots, x_n \in A$.

2. $E = \{x \in A : \langle y, x \rangle \neq 0\}$ é enumerável.

3. Se $z \in X$, então $\sum_{x \in A} |\langle y,x \rangle ||\overline{\langle z, x \rangle}| \le \|y\|\|z\|$.

Outra caracterização de conjuntos ortogonais é que se $X$ for separável e $A$ ortonormal, então ele será enumerável.

## Conjuntos Ortonormais Completos

Definimos um conjunto ortonormal como **completo** se não existe outro conjunto ortonormal que contenha-o. 
Em outras palavras, ele é completo se é o conjunto ortonormal maximal.
Como essa definição é complicado em geral, o seguinte critério ajuda bastante:

**Proposição:** Um conjunto ortonormal $A$ é completo se, e só se, para todo $x$ tal que $x \perp A$, tem-se que $x = 0$.

Além do mais, 

1. Existe um conjunto ortonormal completo em $X$, e

2. Qualquer conjunto ortonormal pode ser estendido para um conjunto ortonormal completo.

**Proposição:** Um conjunto ortonormal completo infinito nunca é uma base (de Hamel) em um espaço de Hilbert.

A prova dessa proposição se dá por contradição extraindo uma sequência de pontos em um conjunto ortonormal completo infinito e observado a soma 
$$
\sum_{k=1}^{\infty} \frac{1}{k^2} x_k = x,
$$
pela Desigualdade de Bessel.
Mas esse elemento deveria ser uma combinação linear finita de elementos de $A$, o que não é possível.

**Teorema:** Suponha que $A$ seja conjunto ortonormal e $\overline{[A]} = X$. 
Então $A$ é completo. Se $X$ é espaço de Hilbert, vale a recíproca.

## Identidade de Parseval

Seja $X$ um espaço com produto interno e $A = \{x_{\alpha}\}$ um conjunto ortonormal.
Então, se para todo $x \in X$,
$$
\|x\|^2 = \sum_{\alpha} |\langle x, x_{\alpha} \rangle|^2, 
$$
então $A$ é completo.
Além disso, se $X$ é Hilbert e $A$ é ortonormal completo, a relação acima vale para todo $x \in X$.