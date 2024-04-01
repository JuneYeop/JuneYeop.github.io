---
use_math: true
comments: true
title:  "Generating Function and Integral Representation of the Bessel Function"
excerpt: "The Bessel function can be expressed not only in an infinite series form, but also in an integral from."
writer: Junyeop Kim
categories:
  - Mathematical Physics
tags:
  - [Bessel function]
date: 2023-12-16
last_modified_at: 2023-12-16
---
<head>
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<head/>

<body>
<p>In general, the Bessel function is expressed as infinite series,
since we solve the Bessel equation using the Frobenious method
ordinarily. However, we can write the Bessel function not only in the
infinite series form, but also in an integral representation.<br />
In order to obtain the integral form of the Bessel function, we should
figure out generating function of the Bessel function beforehand.<br />
<br />
</p>
<h2 class="unnumbered"
id="generating-function-of-the-1st-kind-bessel-function">Generating
Function of the 1st Kind Bessel Function</h2>
<div class="theorem">
<p><strong>Proposition 1</strong>. <em>The function below generates the
1st kind Bessel function as <span class="math display">\[\exp \left[
\frac{x}{2} \left(h-\frac{1}{h}\right) \right] =
\sum_{n=-\infty}^{\infty} { J_{n}(x) \, h^n } \; .\]</span></em></p>
</div>
<p><br />
<strong><em>proof.</em></strong> First, let us expand the exponential
function as</p>
<p><span class="math display">\[\exp \left[ \frac{x}{2}
\left(h-\frac{1}{h}\right) \right] = e^{\frac{xh}{2}} e^{-\frac{x}{2h}}
= \sum_{r=0}^{\infty} { \frac{1}{r!} \left( \frac{xh}{2} \right)^r }
\cdot \sum_{s=0}^{\infty} { \frac{1}{s!} \left( - \frac{x}{2h} \right)^s
} = \sum_{r=0}^{\infty} \sum_{s=0}^{\infty} { (-1)^{s} \left(
\frac{x}{2} \right)^{r+s} \frac{h^{r-s}}{r!\,s!} } \; .\]</span></p>
<p>Replace <span class="math inline">\(n\)</span> by <span
class="math inline">\(n=r-s\)</span>. Then, <span
class="math display">\[\exp \left[ \frac{x}{2}
\left(h-\frac{1}{h}\right) \right] = \sum_{n=-\infty}^{\infty} h^n
\,\left[ \, \sum_{s=0}^{\infty} (-1)^s \frac{1}{s!\,(n+s)!} \left(
\frac{x}{2} \right)^{2s+n} \, \right] \; .\]</span></p>
<p>Note that the <span class="math inline">\(s\)</span> summation term
inside the square brackets above is identical to the usual infinite
series representation of 1st kind Bessel function!<br />
Therefore, <span class="math display">\[\therefore \qquad \exp \left[
\frac{x}{2} \left(h-\frac{1}{h}\right) \right] =
\sum_{n=-\infty}^{\infty} J_{n}(x) \, h^n \qquad \qquad
\blacksquare\]</span><br />
<br />
</p>
<h2 class="unnumbered"
id="integral-representation-of-the-1st-kind-bessel-function">Integral
Representation of the 1st Kind Bessel Function</h2>
<p><strong>proposition.</strong> The 1st kind Bessel Function can be
written as <span class="math display">\[J_{n}(x) = \frac{1}{n}
\int_{0}^{\pi} d\theta \, \cos(x\sin{\theta} - n\theta)  \quad \forall x
\in \mathbb{R} \; , \; \forall n \in \mathbb{Z} \; .\]</span>
<strong><em>proof.</em></strong> Consider an integral of the generating
function on complex plane along a closed contour <span
class="math display">\[\oint_{C}
\frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} \; ,\]</span> where <span
class="math inline">\(C\)</span> is a positively oriented unit circle
centered at the origin.<br />
Let <span class="math inline">\(z=e^{i\theta}\)</span> where <span
class="math inline">\(\theta\)</span> runs from <span
class="math inline">\(0\)</span> to <span
class="math inline">\(2\pi\)</span>. Then, <span
class="math inline">\(\;  dz = ie^{i\theta}d\theta  \;\)</span> and
<span class="math inline">\(\;  z-z^{-1} = 2i\sin{\theta}\)</span>. By
changing the variable, we obtain</p>
<p><span class="math display">\[\oint_{C}
\frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} \;=\; \int_{0}^{2\pi}
d\theta \, ie^{i\theta} \frac{e^{ix \sin{\theta}}}{e^{i(n+1)\theta}}
\;=\; i \int_{0}^{2\pi} d\theta \, \exp{(ix \sin{\theta} - in\theta)} \;
.\]</span><br />
Note also that, <span class="math display">\[\oint_{C}
\frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} \;=\; \oint_{C} dz
\sum_{m=-\infty}^{\infty} J_m(x)\, z^{m-n-1} \; .\]</span><br />
Split the integral above into three parts as below. <span
class="math display">\[\oint_{C} dz \sum_{m=-\infty}^{\infty} J_m(x)\,
z^{m-n-1} \;=\; \oint_{C} dz \sum_{m=-\infty}^{n-1}
\frac{J_{m}(x)}{z^{n-m+1}}  \;+\; \oint_{C} dz \sum_{m=n+1}^{\infty}
J_m(x)\, z^{m-n-1}  \;+\; \oint_{C} dz\, \frac{J_{n}(x)}{z}\]</span></p>
<p>For the right hand side, observe that both integrands inside the
first and the second integrals are holomorphic on and inside the
integration contour <span class="math inline">\(C\)</span>. Hence, both
first and second term vanish! The third term is, however, not
holomorphic anywhere and has a simple pole at <span
class="math inline">\(z=0\)</span>.<br />
Applying the Cauchy residue theorem, we obtain <span
class="math display">\[\oint_{C}
\frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} \;=\; 2\pi i \, J_{n}(x)
\; .\]</span></p>
<p>Consequently, <span class="math display">\[\oint_{C}
\frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} \;=\; 2\pi i \, J_{n}(x)
\;=\; i \int_{0}^{2\pi} d\theta \, \exp{(ix \sin{\theta} - in\theta)} \;
.\]</span><br />
Note that <span class="math inline">\(J_{n}(x)\)</span> is a real-valued
function. Hence, by picking only imaginary parts, we obtain <span
class="math display">\[J_{n}(x) \;=\; \frac{1}{2\pi} \int_{0}^{2\pi}
d\theta \, \cos{(x\sin{\theta} - n\theta)} \; .\]</span><br />
From the even symmetry of <span
class="math inline">\(\cos{(x\sin{\theta}-n\theta)}\)</span> w.r.t.
<span class="math inline">\(\theta=\pi\)</span>, we can conclude that
<span class="math display">\[\therefore \qquad J_{n}(x) = \frac{1}{\pi}
\int_{0}^{\pi} d\theta \, \cos{(x\sin{\theta}-n\theta) } \qquad \qquad
\blacksquare\]</span><br />
<br />
</p>
<h2 class="unnumbered" id="references">References</h2>
<ul>
<li><p>George B. Arfken, Mathematical Methods for Physicists, Academic
Press</p></li>
<li><p>K. F. Riley, Mathematical Methods for Physics and Engineering,
Cambridge University Press</p></li>
</ul>  
</body>



