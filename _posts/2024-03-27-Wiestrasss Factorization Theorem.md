---
use_math: true
comments: true
title:  "Wiestrass Factorization Theorem and Its Applications"
excerpt: "We can express a transcendental function which has zeros in terms of infinite multiplications of linear polynomials."
writer: Junyeop Kim
categories:
  - Mathematical Physics
tags:
  - [complex analysis]
  - [Wiestrass factorization theorem]
date: 2024-03-27
last_modified_at: 2024-03-27
---


We sometimes need to be able to express transcendental functions in a
form of infinite products of linear polynomials. 

For examples, when we attempt to derive a set of eigenstates of 1-dim
quantum harmonic oscillator using Feynmann path integral (Das. Lectures
on quantum mechanics. p.515), or when deduce a partition function of
ideal spin-0 Bose gas through Euclidean path integral (Brown. Quantum
field theory. p.96), it is useful if we can express some trigonometric
functions in a form of infinite products of linear polynomials.\

## 0. Motivation {#motivation .unnumbered}

From the \"Fundamental Theorem of Algebra\", we know the fact that\
*\"Any polynomial
$$P(z) \;=\; a_0 + a_1 z + a_2 z^2 + \cdots + a_n z^n$$ of degree $n$
where each $a_n$ is nonzere has at least one zero.\"*\
[(Can be deriven from Liouville's theorem)]{style="color: gray"}\
Using the mathematical induction, we may generalize our previous
statement to\
*\"Any polynomial $P(z)$ of degree $n$ can be expressed as a product of
$n$ linear factors : $$P(z) \;=\; c\, (z-z_1)(z-z_2)\cdots (z-z_n)$$
where $c$ and $z_k$ are complex constants.\"*\
[(Actually, we can directly derive this statement from Rouche's
theorem.)]{style="color: gray"}\
Then we may want to ask a question :\
*\"Can any entire function, say $f(z)$, be factorized as
$$f(z) \;=\; c\,\prod_{i=0}^{\infty} \, (z-z_i)$$ where $c$ is a complex
constant and $\{z_i\}$ is a set of all zeros of $f(z)$?\"*\
In order to answer on this question, we need to discuss the convergence
of the above infinite product.\

::: center
This notion is a runway for t toward the Weierstrass Factorization
Theorem !
:::

\

## 1. Proof {#proof .unnumbered}

### Definition 1.(Weierstrass elementary factor).  {#definition-1.weierstrass-elementary-factor. .unnumbered}

*Let $n$ be a positive integer. An elementary factor $E_n$ (which is a
function) is defined as equations below.* $$\begin{aligned}
&E_0 (z) \;=\; 1-z \\ 
&E_n (z) \;=\; (1-z) \, \mathrm{exp}\left(z + \frac{z^2}{2} + \cdots + \frac{z^n}{n} \right) \qquad , n \,\ge\, 1 \end{aligned}$$\
Observe that the function $E_n (z/a)$ has an unique zero of order 1 in
which $z=a$.\
\

### Theorem 1  {#theorem-1 .unnumbered}

*Let $|z| \, \le \, 1$ and $p \,\ge\, 0$. Then
$| E_n (z) - 1 | \; \le \; |z|^{n+1}$.*\
***proof.*** It is trivial for $n=0$ since
$| E_n(z) - 1 | = | (1-z)-1 | = |z|$. Hence, let us focus our attention
on positive $n$.

Consider a Laurent series expansion of $E_n (z)$ about $z=0$. Since
$E_n (z)$ is non-singular at $z=0$ (bcs it is entire),
$$E_n (z) \;=\; 1 + \sum_{k=1}^{\infty} a_k z^k$$ By differentiating
$E_n (z)$ with respect to $z$ we obtain
$$E'_n (z) \;=\; \sum_{k=1}^{\infty} k\, a_k\, z^{k-1} \;=\; - z^n \,\mathrm{exp}\left( z + \cdots + \frac{z^n}{n} \right)$$
The second equality comes from the definition of $E_n (z)$. By comparing
the two expressions of $E'_n (z)$ we obtain
$a_1 = a_2 = \cdots = a_n = 0$ since the lowest order of $E'_n (z)$
is 1. Furthermore, since the coefficients of the expantions of
$\mathrm{exp}(z+\cdots+z^p /p)$, $a_k \,\le\, 0$ for $k \,\ge\, n+1$.

Observe that
$$E_n (1) \;=\; 0 \;=\; 1 + \sum_{k = n+1}^{\infty} a_k \;=\; - \sum_{k = n+1}^{\infty} |a_k| \qquad \longrightarrow \qquad \sum_{k = n+1}^{\infty} |a_k| \;=\; 1$$

Hence, for the region in which $|z| \,\le\, 1$,
$$| E_n (z) - 1 | \;=\; \left| \sum_{k=n+1}^{\infty} a_k \, z^k \right| \;=\; |z|^{n+1} \, \left| \sum_{k = n+1}^{\infty} a_k \, z^{n-p-1} \right| \;\le\; |z|^{n+1} \, \sum_{k=n+1}^{\infty} | a_n | \;=\; |z|^{n+1}$$

and this is what we wanted. $\quad \blacksquare$\
\

### Theorem 2  {#theorem-2 .unnumbered}

*Let $\{ a_n \}$ be a complex number sequence such that
$\lim_{n \to \infty} | a_n | = \infty$ and anyone is nonzero.*

*Let $\{ \xi_n \}$ be any sequence of non-negative integers for which
$$\sum_{n=1}^{\infty} \left( \frac{r}{|a_n|} \right)^{\xi_n + 1} \qquad (2)$$
converges for all $r>0$.*\
*Then
$$f(z) \;=\; \prod_{n=1}^{\infty} E_{\xi_n} \left( \frac{z}{a_n} \right)$$
converges uniformly absolutely and entire with zeros only at points
$a_n$.*\
***proof.*** Suppose that there are integers $\xi_n$ such that eqn(1) is
satisfied. Then, according to the previous theorem,

$$\left| 1 - E_{\xi_n} \left(\frac{z}{a_n}\right) \right| \; \le \; \left| \frac{z}{a_n} \right|^{\xi_n + 1} \; \le \; \left( \frac{r}{|a_n|} \right)^{\xi_n + 1} \qquad (3)$$

whenever $|z| \,\le\, r$ and $r/|a_n| \,\le\, 1$.

Consider an infinite sum which is defined by

$$\sum_{n=1}^{\infty} \left[ {1 - E_{\xi_n} \left( \frac{z}{a_n} \right) } \right] \; .$$

From the just previous inequality(2) and our hypothesis(3), the infinite
sum above is convergent uniformly according to the Weierstrass M-test.\
WILL BE FILLED SOON $\quad \blacksquare$\
\
\
Before proceeding the present proof, however, we need a slight red
herring into another topic.\
WILL BE FILLED SOON\
\
\

### Weierstrass Factorization Theorem  {#weierstrass-factorization-theorem .unnumbered}

Let $f$ be an entire function.\
Let $\{ a_n \}$ be the set of all non-zero zeros of $f$ repeated
according to multiplicity.\
Let $f$ has a zero at $z=0$ of order $m \ge 0$.\
Then, there is an entire function $f$ and a sequance of integers
$\{\xi_n\}$ such that
$$f(z) \;=\; z^m e^{g(z)} \, \prod_{n=1}^{\infty} E_{\xi_n} \left( \frac{z}{a_n} \right) \; .$$\
***proof.*** ALSO WILL BE FILLED SOON\...\... $\quad \blacksquare$\
\

## 2. Applications {#applications .unnumbered}

### Trigonometric Functions {#trigonometric-functions .unnumbered}

blahblah

### Gamma Function {#gamma-function .unnumbered}

blahblah\
\

## References {#references .unnumbered}

-   John B. Conway, Functions of One Complex Variable II, Springer
