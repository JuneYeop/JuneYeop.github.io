---
use_math: true
comments: true
title:  "Generating Function and Integral Representation of the Bessel Function"
summary: The Bessel function can be expressed not only in an infinite series form, but also in an integral from.
---

<br/>  
&ensp; In general, the Bessel function is expressed as infinite series, since we solve the Bessel equation using the Frobenious method ordinarily. However, we can write the Bessel function not only in the infinite series form, but also in an integral representation.  <br/>  

&ensp; In order to obtain the integral form of the Bessel function, we should figure out generating function of the Bessel function beforehand.
<br/>
<br/>

### <center> Generating Function of the Bessel Function </center> 
<hr/>  
<br/>  

$$ \mathrm{claim \; :  } \qquad G(x,h) = \exp \left[ \frac{x}{2} \left(h-\frac{1}{h}\right) \right] = \sum_{n=-\infty}^{\infty} { J_{n}(x) \, h^n } $$  

<br/>  

$\mathrm{proof)}$  

$$ G(x,h) = e^{\frac{xh}{2}} e^{-\frac{x}{2h}} = \sum_{r=0}^{\infty} { \frac{1}{r!} \left( \frac{xh}{2} \right)^r } \cdot \sum_{s=0}^{\infty} { \frac{1}{s!} \left( - \frac{x}{2h} \right)^s } = \sum_{r=0}^{\infty} \sum_{s=0}^{\infty} { (-1)^{s} \left( \frac{x}{2} \right)^{r+s} \frac{h^{r-s}}{r!\,s!} } $$  

<br/>
&ensp; Let us define $n$ by $n=r-s$. Then,  

$$ G(x,h) = \sum_{n=-\infty}^{\infty} h^n \,\left[ \, \sum_{s=0}^{\infty} (-1)^s \frac{1}{s!\,(n+s)!} \left( \frac{x}{2} \right)^{2s+n} \, \right] \; .$$  

<br/>
&ensp; Note that the $s$ summation term is identical to the 1st kind Bessel function!  
<br/>
&ensp; Therefore,  

$$ \therefore \qquad \qquad G(x,h) = \sum_{n=-\infty}^{\infty} J_{n}(x) \, h^n \qquad \qquad \qquad \begin{matrix} {}\\{\blacksquare} \end{matrix} $$  

<br/>
<br/>

&ensp; Once we obtained the generating function of the Bessel function, it is a cakewalk to obtain the integral representation of the Bessel function.  

<br/>
<br/>  
<br/>  

### <center> Integral Representation of the Bessel Function </center>
<hr/>  
<br/>  

$$ \mathrm{claim \; :  } \qquad J_{n}(x) = \frac{1}{n} \int_{0}^{\pi} d\theta \, \cos(x\sin{\theta} - n\theta)  \qquad \forall x \in \mathbb{R} \; , \; \forall n \in \mathbb{Z} $$  

<br/>  

$\mathrm{proof)}$  

&ensp; Consider a complex closed contour integral,  
$$ \oint_{C} dz\, \frac{G(x,z)}{z^{n+1}} \;=\; \oint_{C} \frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} $$  
where $C$ is a positively oriented unit circle (i.e. $|z| = 1$).  

<br/>  

&ensp; Let $ z=e^{i\theta} $ where $\theta$ runs from $0$ to $2\pi$. Then, $\;  dz = ie^{i\theta}d\theta  \;$ and $\;  z-z^{-1} = 2i\sin{\theta}  $ .  
<br/>  
&ensp; By changing the variable, we might obtain  

$$ \oint_{C} \frac{e^{\frac{x}{2}(z-\frac{1}{z})}}{z^{n+1}} \;=\; \int_{0}^{2\pi} d\theta \, ie^{i\theta} \frac{e^{ix \sin{\theta}}}{e^{i(n+1)\theta}} \;=\; i \int_{0}^{2\pi} d\theta \, \exp{(ix \sin{\theta} - in\theta)} \; . $$  

<br/>

&ensp; Note also that,  

$$ \oint_{C} dz\, \frac{G(x,z)}{z^{n+1}} \;=\; \oint_{C} dz \sum_{m=-\infty}^{\infty} J_m(x)\, z^{m-n-1} \; . $$  

<br/>

&ensp; Let us split the integral above into three parts.

$$ \oint_{C} dz \sum_{m=-\infty}^{\infty} J_m(x)\, z^{m-n-1} \;=\; \oint_{C} dz \sum_{m=-\infty}^{n-1} \frac{J_{m}(x)}{z^{n-m+1}}  \;+\; \oint_{C} dz \sum_{m=n+1}^{\infty} J_m(x)\, z^{m-n-1}  \;+\; \oint_{C} dz\, \frac{J_{n}(x)}{z}  $$  

<br/>  

&ensp; Observe that the integrand of the first term is holomorphic on $\mathbb{C}\setminus\{0\}$ and the integrand of the second term is entire. Hence, both integrands are analytic on the integration curve $C$ and therefore, both first term and second term vanish!  

<br/>  

&ensp; The third term is, however, not holomorphic anywhere and has a simple pole at $z=0$. Using the Cauchy residue theorem, we obtain  

$$ \oint_{C} dz\, \frac{G(x,z)}{z^{n+1}} \;=\; 2\pi i \, J_{n}(x) \; . $$  

<br/>  

&ensp; Consequently,  

$$ \oint_{C} dz\, \frac{G(x,z)}{z^{n+1}} \;=\; 2\pi i \, J_{n}(x) \;=\; i \int_{0}^{2\pi} d\theta \, \exp{(ix \sin{\theta} - in\theta)} \; . $$  

<br/>  

&ensp; Since the $J_{n}(x)$ is a real function, by picking only imaginary parts we obtain  

$$ J_{n}(x) \;=\; \frac{1}{2\pi} \int_{0}^{2\pi} d\theta \, \cos{(x\sin{\theta} - n\theta)} = \frac{1}{\pi} \int_{0}^{\pi} d\theta \, \cos{(x\sin{\theta}-n\theta) } \; . $$  

<br/>  

&ensp; Since $\cos{(x\sin{\theta}-n\theta)}$ has even symmetry w.r.t.  $\theta=\pi$, we might conclude that

$$ \therefore \qquad \qquad J_{n}(x) = \frac{1}{\pi} \int_{0}^{\pi} d\theta \, \cos{(x\sin{\theta}-n\theta) } \qquad \qquad \qquad \begin{matrix} {}\\{\blacksquare} \end{matrix} $$  

<br/>  
<br/>  
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style1" />
<br/>  


