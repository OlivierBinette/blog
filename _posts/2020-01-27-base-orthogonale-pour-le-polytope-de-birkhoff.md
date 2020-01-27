---
layout: post
title: Base orthogonale pour le polytope de Birkhoff (matrices stochastiques planes)
categories: [Misc]
---

*Old note from 2015. Gives an orthogonal basis to the Birkhoff polytope in dimension $\geq 2$.*

## Notions de base

Le polytope de Birkhoff est l'ensemble des matrices carrées de format $n\times n$ à coefficients positifs, et dont la somme de chaque ligne et de chaque colonne est $1$. On le note par

$$
\mathfrak{B}_n = \left\{ [a_{i,j}]_{i, j=1}^n : a_{i,j} \ge 0,\, \sum_i a_{i, j} = 1,\, \sum_{j}a_{i, j}=1 \right\}\,.
$$

Cet ensemble permet de représenter des projections sur $\mathbb{R}^{n^2}$ de fonctions de densités de probabilité aux marges uniforme. Ainsi, on associera à une densité de probabilité $f : [0,1]^2 \rightarrow \R$, où de plus $\int_{0}^1 f(x, y) dx = \int_{0}^1 f(x, y) dy = 1$, la matrice $[a_{i,j}]_{i, j=1}^n$ de $\mathfrak{B}_n$ donnée par
$a _ {i,j} = \int _ {[\frac{i-1}{n}, \frac{i}{n}] \times [\frac{j-1}{n}, \frac{j}{n}]} f \,.$

<!--more-->

C'est utile à la spécification de mesures de probabilités sur l'espace de dimension infinie des densités aux marges uniforme, aussi dites des densités de copules. Il suffit alors de spécifier une distribution de la dimension $n$ de $\mathfrak{B}_n$, et puis une distribution sur $\mathfrak{B}_n$. Ensuite, pour un $n$ aléatoire, on retransforme une matrice aléatoire de $\mathfrak{B}_n$ en une densité de copule, ce qui induit une densité de copule aléatoire.

Dans le cas plus général des densités de copules définies sur $[0,1]^d$, on doit considérer l'ensemble

$$
\mathfrak{B}_n^d = \left\{ b:\{1, \dots, n\}^d \rightarrow \mathbb{R}\,\bigg|\, b \ge 0,\, \sum_{1 \le i_j \le n\, (j\not= k),\, i_k = c} b(i_1, \dots, i_d) = 1\; ( 1 \le k \le d,\,  1 \le c \le n) \right\}
$$

Pour une matrice $b$ de $\mathfrak{B}_n^d$ et une coordonnée $(i_1, \dots, i_d) \in \{1, \dots n\}^d$, $b(i_1, \dots, i_d)$ correspond à l'intégrale sur un petit hypercube d'une certaine densité de copule $f$:

$$
	b(i_1, \dots, i_d) = \int_{\prod_{k=1}^d [\frac{i_k-1}{n}, \frac{i_k}{n}]} f \,.
$$

De plus, on peut remarquer que $\mathfrak{B}_n^d$, vu comme un sous-ensemble de $\mathbb{R}^{n^d}$, est l'intersection du « quadrant » positif, $\{ (b_1,\dots, b_{n^d})\in \mathbb{R}^{n^d} : b_i \ge 0\; (1 \le i \le n) \}$, et d'un certain sous-espace affine $P$. Il peut être vérifié que ce sous-espace est de dimension $n^d -d(n-1)-1$. 

## Matrices multidimensionnelles

Considérons les fonctions $\{1, \dots, n\}^d \rightarrow \R$ de $\mathfrak{B}_n^d$ comme des éléments de $\mathbb{R}^{n^d}$. Dans le cas $d=2$, on retrouve donc des matrices carrées, et $\mathfrak{B}_n^2 = \mathfrak{B}_n$. Dans le cas général, on peut alors considérer les éléments de $\mathfrak{B}_n^d$ comme étant des matrices multidimensionnelles, c'est-à-dire un ensemble de réels attachés aux points d'un hypercube de $\mathbb{Z}^d$. Les conditions de $\mathfrak{B}_n^d$ deviennent:

- à chaque point de $\{1, \dots, n\}^d$ doit correspondre un réel non-négatif;

- la somme des réels attachés à l'intersection de $\{1, \dots, n\}^d$ et des plans d'équation $i_k = c\;$, pour $(i_1, \dots, i_d) \in \mathbb{R}^{n^d}$, doit être 1.

Affairons-nous maintenant à trouver une base orthogonale pour le sous-espace vectoriel attaché à $V$, ainsi que des conditions, faciles à vérifier, pour savoir quelles combinaisons linéaires d'élément de cette base sont dans $\mathfrak{B}_n^d$.

## Base orthogonale
On considère le produit scalaire usuel sur $\mathbb{R}^{n^d}$. Pour $a, b \in \mathfrak{B}_n^d$, on a donc
$$
	\langle a, b \rangle = \sum_{i_1, \dots, i_d = 1}^n a(i_1, \dots, i_d) b(i_1, \dots, i_d)\,.
$$

Pour des vecteurs $u_1, \dots, u_k \in \mathbb{R}^n$, $u_i = (u_{i,1}, \dots, u_{i,n})$, on défini le produit de $u_1, \dots, u_k$, noté par $u_1 \otimes \dots \otimes u_k$ comme étant la fonction

$$
	\{1, \dots, n\}^k \rightarrow \mathbb{R}: (i_1, \dots, i_k) \mapsto u_{1, i_1} \cdot \dots \cdot u_{k, i_k}\,.
$$

En particulier, dans le cas de deux vecteurs $u=(u_1, \dots, u_n)$ et $v =(v_1, \dots, v_n)$ de $\mathbb{R}^n$, on peut voir $u \otimes v$ comme étant la matrice $[a_{i, j}] = u^{T}v$, car alors $a_{i, j} = u_i \cdot v_j$.

Soit $P$ le plus petit sous-espace affine de $\mathbb{R}^{n^d}$ contenant $\mathfrak{B}_n^d$. Il est montré en [...] que $P$ est de dimension $n^d - d(n-1) -1$. On cherche une base orthogonale pour le sous-espace vectoriel $V$ attaché à $P$, qui l'ensemble des $b : \{1, \dots, n\}^d \rightarrow \R$ satisfaisant les équations

$$
	\sum_{1 \le i_j \le n\, (j\not= k),\, i_k = c} b(i_1, \dots, i_d) = 0\; ( 1 \le k \le d,\,  1 \le c \le n)\,.
$$

On peut remarquer que $P = V + [\frac{1}{n^{d-1}}]_{i_1, \dots, i_d=1}^n$.

**Proposition.**
Soient $u_{i} = (\underbrace{1, \dots, 1}_{i \text{ fois}}, -i, 0, \dots, 0) \in \mathbb{R}^n$, pour $1 \le i < n$, et $u_n = (1,1, \dots, 1)\in \mathbb{R}^n$. Alors,
$$
\mathcal{B} = \{ u_{i_1} \otimes \dots \otimes u_{i_d} : |\{k: i_k < n\}| > 1 \}
$$

est une base orthogonale de V. Autrement dit, $\mathcal{B}$ est l'ensemble des $u_{i_1} \otimes \dots \otimes u_{i_d}$ tels que $i_k < n$ pour plus de 1 indice $k$.

*Preuve.*
Montrons tout d'abord que $|\mathcal{B}| = \dim V = n^d - d(n-1) -1$. Supposons que $u_{i_1} \otimes \dots \otimes u_{i_d} \not = u_{j_1} \otimes \dots \otimes u_{j_d}$, lorsque $(i_1, \dots, i_d) \not= (j_1, \dots, j_d)$. On a alors que
$$
|\mathcal{B}| = |{ (i_1, \dots, i_d) \in {1, \dots, n}^d : |{k : i_k < n}| > 1 }|\\
= | { (i_1, \dots, i_d) : |{k : i_k < n}| > 1 \text{ ou } (i_1, \dots, i_d) = (n, \dots, n)}\backslash {(n, \dots, n)}|\\
= | \left[ {(i_1, \dots, i_d) : \exists! k \text{ avec } i_k < n} \cup {(n, \dots, n)}\right]^c |\\
= n^d - (d(n-1) + 1) \,.
$$
Soient $\alpha, \beta \in \mathcal{B}$, disons $\alpha = u_{i_1}\otimes \dots \otimes u_{i_d}$ et $\beta = u_{j_1}\otimes \dots \otimes u_{j_d}$, avec de plus $(i_1, \dots, i_d) \not = (j_1, \dots, j_d)$. Il est facile de voir, par réccurence sur $d$, que $\alpha, \beta \in V$. Montrons que $\langle \alpha, \beta \rangle = 0$. Comme $\alpha \not = 0$ et $\beta \not = 0$, on pourra aussi conclure que $\alpha \not = \beta$, et puis, comme $|\mathcal{B}| = \dim V$, que $\mathcal{B}$ est une base orthogonale de $V$.

On peut supposer, sans perte de généralité, que $i_1 < j_1$. Ainsi, $i_1 < n$, et $\sum_{x=1}^n u_{i_1}(x)u_{j_1}(x) = \sum_{x=1}^n u_{i_1}(x) = 0$. On calcule alors

$$
\langle \alpha, \beta \rangle = \sum_{x_d, \dots, x_d = 1}^n \alpha(x_1, \dots, x_d) \beta(x_1, \dots, x_d)\\
= \sum_{x_1, \dots, x_d = 1}^n u{i_1}(x_1)  \dots  u_{i_d}(x_d) u_{j_1}(x_1)  \dots  u_{j_d}(x_d)\\
= \left(\sum_{x_1 = 1}^n u_{i_1}(x_1)\right)  \sum_{x_2, \dots, x_d = 1}^n u_{i_2}(x_2)  \dots  u_{i_d}(x_d) u_{j_2}(x_2)  \dots  u_{j_d}(x_d)\\
= 0.
$$

## Conditions pour l'appartenance à $\mathfrak{B}_n^d$

Considérons tout d'abord le cas $d = 2$. Fixons $n \in \N$ et considérons la base orthogonale $\mathcal{B}$ du sous-espace vectoriel $V$ attaché à $\mathfrak{B}_n$, donnée dans la section précédente. On souhaite trouver des conditions sur les combinaisons linéaires d'éléments de $\mathcal{B}$ pour qu'elles soient dans $\mathfrak{B}_n - [\frac{1}{n}]_{i, j=1}^n$. On appliquera ensuite la translation $b \mapsto b+[\frac{1}{n}]_{i, j=1}^n$ pour se ramener dans $\mathfrak{B}_n$.

Soient $c_{i, j} \in \R$, $b_{i, j}$ les éléments de $\mathcal{B}$, et $b = \sum_{i, j =1}^{n-1}c_{i, j} b_{i, j}$. Alors, $b \in \mathfrak{B}_n - [\frac{1}{n}]_{i, j=1}^n$ si et seulement si $b(x, y) \ge -\frac{1}{n}$, pour tout $1 \le x, y \le n$. En notant $[a_{i, j}]_{i, j}= [a_{i, j}]_{i, j=1}^{n-1}$, calculons $b(x, y)$:
$$
b(x, y) = \sum_{i, j = 1}^{n-1}c_{i, j}b_{i, j}(x, y)\\
	= \langle [c_{i, j}]_{i, j}, [b_{i, j}(x, y)]_{i, j}\rangle\\
	= \langle [c_{i, j}]_{i, j}, [u_i(x)u_j(y)]_{i, j}\rangle\\
	= \langle [c_{i, j}]_{i, j}, [u_i(x)]_{i=1}^{n-1} \otimes [u_j(y)]_{j=1}^{n-1}\rangle\,.
$$


Or, on peut remarquer que
$$
[u_i(1)]_{i=1}^{n-1} = (1, \dots, 1) \\ 
[u_i(2)]_{i=1}^{n-1} = (-1,1, \dots, 1) \\ 
[u_i(3)]_{i=1}^{n-1} = (0,-2,1 \dots, 1)\,,
$$
et, en général, si $x > 1$, 
$$
	[u_i(x)]_{i=1}^{n-1} = (\underbrace{0,\dots, 0, 1-x}_{x-1 \text{ fois}}, 1, \dots, 1) \in \mathbb{R}^{n-1} \,.
$$

Notons donc $u_x^* = (\underbrace{0,\dots, 0, 1-x}_{x-1 \text{ fois}}, 1, \dots, 1) \in \mathbb{R}^{n-1}$, si $x > 1$, et $u_1^* = (1, \dots, 1) \in \mathbb{R}^{n-1}$, de sorte que $u_x^* = [u_i(x)]_{i=1}^{n-1}$ et

$$
	b(x, y) = \langle [c_{i, j}]_{i, j}, (u_x^*)^T u_y^*\rangle \,.
$$

Conséquemment, $b \in \mathfrak{B}_n - [\frac{1}{n}]_{i, j=1}^n$ si et seulement si

$$
  b(x, y) = \langle [c_{i, j}]_{i, j}, (u_x^*)^T u_y^*\rangle \ge -\frac{1}{n}
$$

pour tout $1 \le x, y \le n$.


