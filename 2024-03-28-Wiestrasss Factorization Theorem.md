---
use_math: true
comments: true
title:  "Weiestrass Factorization Theorem and Its Applications"
excerpt: "A transcendental function which has infinite numbers of zero can be written in terms of infinite multiplications of linear polynomials."
writer: Junyeop Kim
categories:
  - Mathematical Physics
tags:
  - [complex analysis]
  - [Wiestrass factorization theorem]
date: 2024-03-27
last_modified_at: 2024-03-27
---


<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="" xml:lang="">
<head>
  <meta charset="utf-8" />
  <meta name="generator" content="pandoc" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes" />
  <title>c7a638898a6444ab83c0cb1ff11a7a16</title>
  <style>
    html {
      line-height: 1.5;
      font-family: Georgia, serif;
      font-size: 20px;
      color: #1a1a1a;
      background-color: #fdfdfd;
    }
    body {
      margin: 0 auto;
      max-width: 36em;
      padding-left: 50px;
      padding-right: 50px;
      padding-top: 50px;
      padding-bottom: 50px;
      hyphens: auto;
      overflow-wrap: break-word;
      text-rendering: optimizeLegibility;
      font-kerning: normal;
    }
    @media (max-width: 600px) {
      body {
        font-size: 0.9em;
        padding: 1em;
      }
      h1 {
        font-size: 1.8em;
      }
    }
    @media print {
      body {
        background-color: transparent;
        color: black;
        font-size: 12pt;
      }
      p, h2, h3 {
        orphans: 3;
        widows: 3;
      }
      h2, h3, h4 {
        page-break-after: avoid;
      }
    }
    p {
      margin: 1em 0;
    }
    a {
      color: #1a1a1a;
    }
    a:visited {
      color: #1a1a1a;
    }
    img {
      max-width: 100%;
    }
    h1, h2, h3, h4, h5, h6 {
      margin-top: 1.4em;
    }
    h5, h6 {
      font-size: 1em;
      font-style: italic;
    }
    h6 {
      font-weight: normal;
    }
    ol, ul {
      padding-left: 1.7em;
      margin-top: 1em;
    }
    li > ol, li > ul {
      margin-top: 0;
    }
    blockquote {
      margin: 1em 0 1em 1.7em;
      padding-left: 1em;
      border-left: 2px solid #e6e6e6;
      color: #606060;
    }
    code {
      font-family: Menlo, Monaco, 'Lucida Console', Consolas, monospace;
      font-size: 85%;
      margin: 0;
    }
    pre {
      margin: 1em 0;
      overflow: auto;
    }
    pre code {
      padding: 0;
      overflow: visible;
      overflow-wrap: normal;
    }
    .sourceCode {
     background-color: transparent;
     overflow: visible;
    }
    hr {
      background-color: #1a1a1a;
      border: none;
      height: 1px;
      margin: 1em 0;
    }
    table {
      margin: 1em 0;
      border-collapse: collapse;
      width: 100%;
      overflow-x: auto;
      display: block;
      font-variant-numeric: lining-nums tabular-nums;
    }
    table caption {
      margin-bottom: 0.75em;
    }
    tbody {
      margin-top: 0.5em;
      border-top: 1px solid #1a1a1a;
      border-bottom: 1px solid #1a1a1a;
    }
    th {
      border-top: 1px solid #1a1a1a;
      padding: 0.25em 0.5em 0.25em 0.5em;
    }
    td {
      padding: 0.125em 0.5em 0.25em 0.5em;
    }
    header {
      margin-bottom: 4em;
      text-align: center;
    }
    #TOC li {
      list-style: none;
    }
    #TOC ul {
      padding-left: 1.3em;
    }
    #TOC > ul {
      padding-left: 0;
    }
    #TOC a:not(:hover) {
      text-decoration: none;
    }
    code{white-space: pre-wrap;}
    span.smallcaps{font-variant: small-caps;}
    div.columns{display: flex; gap: min(4vw, 1.5em);}
    div.column{flex: auto; overflow-x: auto;}
    div.hanging-indent{margin-left: 1.5em; text-indent: -1.5em;}
    ul.task-list{list-style: none;}
    ul.task-list li input[type="checkbox"] {
      width: 0.8em;
      margin: 0 0.8em 0.2em -1.6em;
      vertical-align: middle;
    }
  </style>
  <script
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml-full.js"
  type="text/javascript"></script>
  <!--[if lt IE 9]>
    <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.3/html5shiv-printshiv.min.js"></script>
  <![endif]-->
</head>
<body>
<p>We sometimes need to be able to express transcendental functions in a
form of infinite products of linear polynomials. </p>
<p>For examples, when we attempt to derive a set of eigenstates of 1-dim
quantum harmonic oscillator using Feynmann path integral (Das. Lectures
on quantum mechanics. p.515), or when deduce a partition function of
ideal spin-0 Bose gas through Euclidean path integral (Brown. Quantum
field theory. p.96), it is useful if we can express some trigonometric
functions in a form of infinite products of linear polynomials.<br />
</p>
<h2 class="unnumbered" id="motivation">0. Motivation</h2>
<p>From the "Fundamental Theorem of Algebra", we know the fact
that<br />
<em>"Any polynomial <span class="math display">\[P(z) \;=\; a_0 + a_1 z
+ a_2 z^2 + \cdots + a_n z^n\]</span> of degree <span
class="math inline">\(n\)</span> where each <span
class="math inline">\(a_n\)</span> is nonzere has at least one
zero."</em><br />
<span style="color: gray">(Can be deriven from Liouville’s
theorem)</span><br />
Using the mathematical induction, we may generalize our previous
statement to<br />
<em>"Any polynomial <span class="math inline">\(P(z)\)</span> of degree
<span class="math inline">\(n\)</span> can be expressed as a product of
<span class="math inline">\(n\)</span> linear factors : <span
class="math display">\[P(z) \;=\; c\, (z-z_1)(z-z_2)\cdots
(z-z_n)\]</span> where <span class="math inline">\(c\)</span> and <span
class="math inline">\(z_k\)</span> are complex constants."</em><br />
<span style="color: gray">(Actually, we can directly derive this
statement from Rouche’s theorem.)</span><br />
Then we may want to ask a question :<br />
<em>"Can any entire function, say <span
class="math inline">\(f(z)\)</span>, be factorized as <span
class="math display">\[f(z) \;=\; c\,\prod_{i=0}^{\infty} \,
(z-z_i)\]</span> where <span class="math inline">\(c\)</span> is a
complex constant and <span class="math inline">\(\{z_i\}\)</span> is a
set of all zeros of <span
class="math inline">\(f(z)\)</span>?"</em><br />
In order to answer on this question, we need to discuss the convergence
of the above infinite product.<br />
</p>
<div class="center">
<p>This notion is a runway for t toward the Weierstrass Factorization
Theorem !</p>
</div>
<p><br />
</p>
<h2 class="unnumbered" id="proof">1. Proof</h2>
<h3 class="unnumbered"
id="definition-1.weierstrass-elementary-factor.">Definition
1.(Weierstrass elementary factor).<br />
</h3>
<p><em>Let <span class="math inline">\(n\)</span> be a positive integer.
An elementary factor <span class="math inline">\(E_n\)</span> (which is
a function) is defined as equations below.</em> <span
class="math display">\[\begin{aligned}
&amp;E_0 (z) \;=\; 1-z \\
&amp;E_n (z) \;=\; (1-z) \, \mathrm{exp}\left(z + \frac{z^2}{2} + \cdots
+ \frac{z^n}{n} \right) \qquad , n \,\ge\, 1
\end{aligned}\]</span><br />
Observe that the function <span class="math inline">\(E_n (z/a)\)</span>
has an unique zero of order 1 in which <span
class="math inline">\(z=a\)</span>.<br />
<br />
</p>
<h3 class="unnumbered" id="theorem-1">Theorem 1<br />
</h3>
<p><em>Let <span class="math inline">\(|z| \, \le \, 1\)</span> and
<span class="math inline">\(p \,\ge\, 0\)</span>. Then <span
class="math inline">\(| E_n (z) - 1 | \; \le \;
|z|^{n+1}\)</span>.</em><br />
<strong><em>proof.</em></strong> It is trivial for <span
class="math inline">\(n=0\)</span> since <span class="math inline">\(|
E_n(z) - 1 | = | (1-z)-1 | = |z|\)</span>. Hence, let us focus our
attention on positive <span class="math inline">\(n\)</span>.</p>
<p>Consider a Laurent series expansion of <span
class="math inline">\(E_n (z)\)</span> about <span
class="math inline">\(z=0\)</span>. Since <span
class="math inline">\(E_n (z)\)</span> is non-singular at <span
class="math inline">\(z=0\)</span> (bcs it is entire), <span
class="math display">\[E_n (z) \;=\; 1 + \sum_{k=1}^{\infty} a_k
z^k\]</span> By differentiating <span class="math inline">\(E_n
(z)\)</span> with respect to <span class="math inline">\(z\)</span> we
obtain <span class="math display">\[E&#39;_n (z) \;=\;
\sum_{k=1}^{\infty} k\, a_k\, z^{k-1} \;=\; - z^n \,\mathrm{exp}\left( z
+ \cdots + \frac{z^n}{n} \right)\]</span> The second equality comes from
the definition of <span class="math inline">\(E_n (z)\)</span>. By
comparing the two expressions of <span class="math inline">\(E&#39;_n
(z)\)</span> we obtain <span class="math inline">\(a_1 = a_2 = \cdots =
a_n = 0\)</span> since the lowest order of <span
class="math inline">\(E&#39;_n (z)\)</span> is 1. Furthermore, since the
coefficients of the expantions of <span
class="math inline">\(\mathrm{exp}(z+\cdots+z^p /p)\)</span>, <span
class="math inline">\(a_k \,\le\, 0\)</span> for <span
class="math inline">\(k \,\ge\, n+1\)</span>.</p>
<p>Observe that <span class="math display">\[E_n (1) \;=\; 0 \;=\; 1 +
\sum_{k = n+1}^{\infty} a_k \;=\; - \sum_{k = n+1}^{\infty} |a_k| \qquad
\longrightarrow \qquad \sum_{k = n+1}^{\infty} |a_k| \;=\;
1\]</span></p>
<p>Hence, for the region in which <span class="math inline">\(|z|
\,\le\, 1\)</span>, <span class="math display">\[| E_n (z) - 1 | \;=\;
\left| \sum_{k=n+1}^{\infty} a_k \, z^k \right| \;=\; |z|^{n+1} \,
\left| \sum_{k = n+1}^{\infty} a_k \, z^{n-p-1} \right| \;\le\;
|z|^{n+1} \, \sum_{k=n+1}^{\infty} | a_n | \;=\; |z|^{n+1}\]</span></p>
<p>and this is what we wanted. <span class="math inline">\(\quad
\blacksquare\)</span><br />
<br />
</p>
<h3 class="unnumbered" id="theorem-2">Theorem 2<br />
</h3>
<p><em>Let <span class="math inline">\(\{ a_n \}\)</span> be a complex
number sequence such that <span class="math inline">\(\lim_{n \to
\infty} | a_n | = \infty\)</span> and anyone is nonzero.</em></p>
<p><em>Let <span class="math inline">\(\{ \xi_n \}\)</span> be any
sequence of non-negative integers for which <span
class="math display">\[\sum_{n=1}^{\infty} \left( \frac{r}{|a_n|}
\right)^{\xi_n + 1} \qquad (2)\]</span> converges for all <span
class="math inline">\(r&gt;0\)</span>.</em><br />
<em>Then <span class="math display">\[f(z) \;=\; \prod_{n=1}^{\infty}
E_{\xi_n} \left( \frac{z}{a_n} \right)\]</span> converges uniformly
absolutely and entire with zeros only at points <span
class="math inline">\(a_n\)</span>.</em><br />
<strong><em>proof.</em></strong> Suppose that there are integers <span
class="math inline">\(\xi_n\)</span> such that eqn(1) is satisfied.
Then, according to the previous theorem,</p>
<p><span class="math display">\[\left| 1 - E_{\xi_n}
\left(\frac{z}{a_n}\right) \right| \; \le \; \left| \frac{z}{a_n}
\right|^{\xi_n + 1} \; \le \; \left( \frac{r}{|a_n|} \right)^{\xi_n + 1}
\qquad (3)\]</span></p>
<p>whenever <span class="math inline">\(|z| \,\le\, r\)</span> and <span
class="math inline">\(r/|a_n| \,\le\, 1\)</span>.</p>
<p>Consider an infinite sum which is defined by</p>
<p><span class="math display">\[\sum_{n=1}^{\infty} \left[ {1 -
E_{\xi_n} \left( \frac{z}{a_n} \right) } \right] \; .\]</span></p>
<p>From the just previous inequality(2) and our hypothesis(3), the
infinite sum above is convergent uniformly according to the Weierstrass
M-test.<br />
WILL BE FILLED SOON <span class="math inline">\(\quad
\blacksquare\)</span><br />
<br />
<br />
Before proceeding the present proof, however, we need a slight red
herring into another topic.<br />
WILL BE FILLED SOON<br />
<br />
<br />
</p>
<h3 class="unnumbered"
id="weierstrass-factorization-theorem">Weierstrass Factorization
Theorem<br />
</h3>
<p>Let <span class="math inline">\(f\)</span> be an entire
function.<br />
Let <span class="math inline">\(\{ a_n \}\)</span> be the set of all
non-zero zeros of <span class="math inline">\(f\)</span> repeated
according to multiplicity.<br />
Let <span class="math inline">\(f\)</span> has a zero at <span
class="math inline">\(z=0\)</span> of order <span
class="math inline">\(m \ge 0\)</span>.<br />
Then, there is an entire function <span class="math inline">\(f\)</span>
and a sequance of integers <span
class="math inline">\(\{\xi_n\}\)</span> such that <span
class="math display">\[f(z) \;=\; z^m e^{g(z)} \, \prod_{n=1}^{\infty}
E_{\xi_n} \left( \frac{z}{a_n} \right) \; .\]</span><br />
<strong><em>proof.</em></strong> ALSO WILL BE FILLED SOON...... <span
class="math inline">\(\quad \blacksquare\)</span><br />
<br />
</p>
<h2 class="unnumbered" id="applications">2. Applications</h2>
<h3 class="unnumbered" id="trigonometric-functions">Trigonometric
Functions</h3>
<p>blahblah</p>
<h3 class="unnumbered" id="gamma-function">Gamma Function</h3>
<p>blahblah<br />
<br />
</p>
<h2 class="unnumbered" id="references">References</h2>
<ul>
<li><p>John B. Conway, Functions of One Complex Variable II,
Springer</p></li>
</ul>
</body>
</html>