---
use_math: true
comments: true
---

<br/>
&ensp; In general, the Bessel function is expressed as infinite series, since we solve the Bessel equation using the Frobenious method ordinarily. However, we can write the Bessel function not only in the infinite series form, but also in an integral representation.  <br/>
&ensp; In order to obtain the integral form of the Bessel function, we should figure out generating function of the Bessel function beforehand.
<br/>
<br/>

## <center> Generating Function of the Bessel Function </center> 
<br/>
$$ \text{Claim  :  } \qquad G(x,h) = \exp \left[ \frac{x}{2} \left(h-\frac{1}{h}\right) \right] = \sum_{n=-\infty}^{\infty} { J_{n}(x) \, h^n } $$  
<br/>
$\mathrm{proof)}$  

$$ G(x,h) = e^{\frac{xh}{2}} e^{-\frac{x}{2h}} = \sum_{r=0}^{\infty} { \frac{1}{r!} \left( \frac{xh}{2} \right)^r } \cdot \sum_{s=0}^{\infty} { \frac{1}{s!} \left( - \frac{x}{2h} \right)^s } = \sum_{r=0}^{\infty} \sum_{s=0}^{\infty} { (-1)^{s} \left( \frac{x}{2} \right)^{r+s} \frac{h^{r-s}}{r!\,s!} } $$  

<br/>
Let us define $n$ by $n=r-s$. Then,  
$$ G(x,h) = \sum_{n=-\infty}^{\infty} h^n \,\left[ \, \sum_{s=0}^{\infty} (-1)^s \frac{1}{s!\,(n+s)!} \left( \frac{x}{2} \right)^{2s+n} \, \right] $$  

<br/>
Note that the $s$ summation term is identical to the 1st kind Bessel function!  
<br/>
Therefore,  
$$ \therefore \qquad \qquad G(x,h) = \sum_{n=-\infty}^{\infty} J_{n}(x) \, h^n \qquad \qquad \qquad \begin{matrix} {}\\{\blacksquare} \end{matrix} $$


