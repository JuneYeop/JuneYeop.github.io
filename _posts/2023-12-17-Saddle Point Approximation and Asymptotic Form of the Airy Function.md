---
use_math: true
comments: true
title:  "Saddle Point Approximation and Asymptotic Form of the Airy Function"
excerpt: "The most powerful tool to obtain asymptotic approximations : saddle point approximation"
writer: Junyeop Kim
categories:
  - Mathematical Physics
tags:
  - [Bessel function]
date: 2023-12-16
last_modified_at: 2023-12-16
---


 WKB approximation을 공부하다 보면 Airy function의 asymptotic form이 필요한데 교재에서는 그냥 휙 하고 던져 줄 것이다. 이것 참 맘에 안 드는데...   
   
 그래서 이번에는 Airy function의 asypmtotic form을 구할 때 사용하는 approximation method인 saddle point approximation에 대해 소개하고, 이것을 이용해서 Airy function의 asymptotic form을 직접 유도해보려고 한다.  
 

  
 

#### **Derivation of the Saddle Point Approximation**

---

" How do we obatin an approximation form of a fucntion $f(t), \\forall t \\in \\mathbb{R}$ ? "

   
   
   
Let us write the real valued function $f(t)$ in a contour integral form $$ f(t) = \\int\_{C} dz\\, F(z,t) $$ where $F$ is an analytic function and $\\forall t \\in \\mathbb{R}$.  
   
   
Let, $$ F(z,t) = e^{w(z,t)} $$ where $$w(x,y) = u(x,y) + i \\, v(x,y)  \\qquad \\forall x,y \\in \\mathbb{R} \\;\\;. $$  
   
   
Since $F$ is analytic, $w$ should be anayltic as well because an exponential function preserves holomorphism. Thus, both $u$ and $v$ cannot have extremum.  
   
Why?  
Assume that $u(x,y)$ has a local minimum(maximum) at $(x,y) = (x\_0, y\_0)$. Then, the Hessian matrix of $u(x,y)$ at $(x\_0, y\_0)$ shold be positively(negatively) definite, and this implies $\\left.\\frac{\\partial^2 u}{\\partial x^2}\\right|\_{x\_0,y\_0}$ and $\\left.\\frac{\\partial^2 u}{\\partial y^2}\\right|\_{x\_0,y\_0}$ have same signs. Unless, the determinant of Hessian matrix might be negative, which violates the pre-stated condition. Since $w(x,y)$ is analytic, however, $u(x,y)$ must satisfy $ {\\nabla}^2 u(x,y) = 0 $. This implies $\\left.\\frac{\\partial^2 u}{\\partial x^2}\\right|\_{x\_0,y\_0}$ and $\\left.\\frac{\\partial^2 u}{\\partial y^2}\\right|\_{x\_0,y\_0}$ cannot have same signs, and we get a contradiction! Therefore, there is NO extremum for $u$ and $v$ if $ w = u + i v $ is analytic.  
   
   
Although $u(x,y)$ and $v(x,y)$ cannot have extremum, both can have a saddle point (say $z\_0$).  
   
   
Let us expand $w(z,t)$ near the saddle point $z=z\_0$ up to second order of $z$. $$\\begin{equation} w(z,t) = w(z\_0,t) + \\frac{1}{2} \\left.\\frac{\\partial^2 w}{\\partial z^2}\\right|\_{z\_0} (z-z\_0)^2 + \\cdots  \\tag{1} \\end{equation} $$ Note that $ \\left.\\frac{dw}{dz}\\right|\_{z\_0}$ is vanished since $z\_0$ is a saddle point.  
   
   
Let us introduce some abbreviations and denote the phases explicitly. $$ \\left.\\frac{\\partial w}{\\partial z}\\right|\_{z\_0} = w\_0 , \\quad \\left.\\frac{\\partial^2 w}{\\partial z^2}\\right|\_{z\_0} = w''\_0 = \\left|{w''\_0}\\right| e^{i\\alpha} , \\quad z-z\_0 = re^{i\\theta} \\;\\;. $$  
   
Then we can rewrite the $w(z,t)$ as $$ \\begin{align\*} w(z,t) &= w\_0 + \\frac{1}{2}\\left|w''\_0\\right| e^{i\\alpha} (r e^{i\\theta})^2 + \\mathrm{O}(r^3) \\\\ &= w\_0 + \\frac{1}{2}\\left|w''\_0\\right| r^2 e^{ i(\\alpha + 2\\theta) } + \\mathrm{O}(r^3) \\\\ &= w\_0 + \\frac{1}{2} \\left|w''\_0\\right| r^2 \\left\[ \\cos(\\alpha + 2\\theta) + i \\, \\sin(\\alpha + 2\\theta) \\right\] + \\mathrm{O}(r^3) \\\\ &\\approx \\left\[ w\_0 + \\frac{1}{2} \\left|w''\_0\\right| r^2 \\cos(\\alpha + 2\\theta) \\right\] + i \\, \\left\[ \\frac{1}{2} \\left|w''\_0\\right| r^2 \\sin(\\alpha + 2\\theta) \\right\] \\;\\;. \\end{align\*} $$  
   
Remember that we have defined $w(z,t)$ by $ w = u + i v $. Hence we obtain  
$$ \\begin{cases} \\quad u(z,t) = w\_0 + \\frac{1}{2} \\left|w''\_0\\right| r^2 \\cos(\\alpha + 2\\theta)  \\\\ {} \\\\  \\quad  v(z,t) = \\frac{1}{2} \\left|w''\_0\\right| r^2 \\sin(\\alpha + 2\\theta)  \\end{cases} $$  
   
Consider the situation in which **$z$ departs from $z\_0$** (i.e. as r increases from 0).  
 

  
$\\mathbf{\\cdot}$ For $u(z,t)$  
   
$\\qquad$ i) $u$ will increase most rapidly when  
$$ \\cos(\\alpha + 2\\theta) = 1 \\quad \\Rightarrow \\quad \\alpha + 2\\theta = 2n\\pi \\quad \\Rightarrow \\quad \\theta = -\\frac{\\alpha}{2} +n\\pi $$  
$\\qquad$ ii) $u$ will decrease most rapidly when  
$$ \\cos(\\alpha + 2\\theta) = -1 \\quad \\Rightarrow \\quad \\alpha + 2\\theta = (2n+1)\\pi \\quad \\Rightarrow \\quad \\theta = -\\frac{\\alpha}{2} + \\left(n+\\frac{1}{2}\\right)\\pi $$  
$\\qquad$ iii) $u$ will be invariant when  
$$ \\cos(\\alpha + 2\\theta) = 0 \\quad \\Rightarrow \\quad \\alpha + 2\\theta = \\left(n+\\frac{1}{2}\\right)\\pi \\quad \\Rightarrow \\quad \\theta = -\\frac{\\alpha}{2} + \\left(\\frac{n}{2}+\\frac{1}{4}\\right)\\pi $$  
   
$\\mathbf{\\cdot}$ For $v(z,t)$  
   
$\\qquad$ i) $v$ will increase most rapidly when  
$$ \\sin(\\alpha + 2\\theta) = 1 \\quad \\Rightarrow \\quad \\alpha + 2\\theta = \\left(2n+\\frac{1}{2}\\right)\\pi \\quad \\Rightarrow \\quad \\theta = -\\frac{\\alpha}{2} +\\left(n+\\frac{1}{4}\\right)\\pi $$  
$\\qquad$ ii) $v$ will decrease most rapidly when  
$$ \\sin(\\alpha + 2\\theta) = -1 \\quad \\Rightarrow \\quad \\alpha + 2\\theta = \\left(2n+\\frac{3}{2}\\right)\\pi \\quad \\Rightarrow \\quad \\theta = -\\frac{\\alpha}{2} + \\left(n+\\frac{3}{4}\\right)\\pi $$  
$\\qquad$ iii) $v$ will be invariant when  
$$ \\sin(\\alpha + 2\\theta) = 0 \\quad \\Rightarrow \\quad \\alpha + 2\\theta = n\\pi \\quad \\Rightarrow \\quad \\theta = -\\frac{\\alpha}{2} + \\frac{n\\pi}{2} $$  
 

[##_Image|kage@ycJkL/btst87Pp9UZ/RhgKyaBgARxbVkaV2yVJ7k/img.png|CDM|1.3|{"originWidth":1330,"originHeight":603,"style":"alignCenter","width":800,"height":363,"caption":"Arrows indicate ascending directions of each $u$ and $v$."}_##]

   
   
 

**$\\bullet$ How do we choose an optimum integration contour?**  
 

  We need to choose **a contour that passes through the saddle point $z\_0$ in the directions of maximum rate of decrease in $u$ with distance from $z\_0$, and therefore also in $\\vert F \\vert$ (since $\\vert F \\vert = e^{u}$)**. These directions are level lines of $v(x,y)$, so the phase factor of $F$ (i.e. $e^{iv}$) will not change as we leave tha saddle point.  
  If we chose $z\_0$ to be a point other than a saddle point, then the expansion of $w$ (eqn. (1)) would have contained a non-zero linear term in $r$ (since $ \\left.\\frac{\\partial u}{\\partial z}\\right|\_{z\_0} $ does not vanish.), and it might be impossible to construct a curve which passes through $z\_0$ that makes $\\vert F \\vert = e^u $ to decrease and keeps the phase of F (i.e. $e^{iv}$) constant, as $z$ departs from $z\_0$.   
   
   
 

**$\\bullet$ Evaluation of the integral**

   
 Let us ssume that ${\\vert w''\_0 \\vert}$, the measure of the rate of decrease in $\\vert F \\vert$ as we leave $z\_0$, is large enough that the bulk of the value of the integral has already been attained for small $R$. (i.e. The significant contribution to the integral only comes from the immediate vicinity of the saddle point $z\_0$.)

 Split the integration range as below. Note that near the critical point, $ z = z\_0 + r e^{i\\theta} $ gives $ dz = e^{i\\theta} dr $ since we can assume that the contour is a straight line right near the critical point. $$ \\begin{align\*} f(t) \\;=\\; \\int\_{C} dz\\,F(z,t) \\; &= \\; \\int\_{\\text{near the saddle point}} dz \\, F(z,t) \\;+\\; \\int\_{\\text{error contribution}} dz \\, F(z,t) \\\\ &{} \\\\ &= \\; \\int\_{\\text{descend from } F(z\_0)} dz \\, F(z,t) \\;+\\; \\int\_{\\text{ascend to } F(z\_0)} dz \\, F(z,t) \\;+\\; \\int\_{\\text{error contribution}} dz \\, F(z,t) \\\\ &{} \\\\ &=\\; \\int\_{0}^{R} dr \\, r^2 e^{i\\theta} \\exp{ \\left( w\_0 + \\frac{1}{2} {\\vert w''\_0 \\vert} e^{i(\\alpha+2\\theta)} \\right)} \\;+\\; \\int\_{R}^{0} dr \\, r^2 e^{i\\bar{\\theta}} \\exp{ \\left( w\_0 + \\frac{1}{2} {\\vert w''\_0 \\vert} e^{i(\\alpha+2\\bar{\\theta})} \\right)} \\;+\\; \\text{errer term} \\;\\;. \\end{align\*} $$ where  $ \\bar{\\theta} = \\theta - \\pi$ .  
   
Since we've set the integration contour to satisfy $ e^{i(\\alpha + 2\\theta)} = e^{i(2n+1)\\pi} = -1 $ right near the saddle point, $$ \\begin{align\*} f(t) \\;&=\\; e^{w\_0 + i\\theta} \\int\_{0}^{R} dr \\, r^2 e^{ - \\frac{1}{2} {\\vert w''\_0 \\vert}^2 } \\;+\\; e^{w\_0 + i(\\theta-\\pi)} \\int\_{R}^{0} dr \\, r^2 e^{ - \\frac{1}{2} {\\vert w''\_0 \\vert} } \\;+\\; \\text{errer term} \\\\ &=\\; 2 \\, e^{w\_0 + i\\theta} \\int\_{0}^{R} dr\\, e^{-\\frac{1}{2} {\\vert w''\_0 \\vert} r^2 } \\;+\\; \\text{error term} \\;\\;. \\end{align\*} $$

  
Note that our assumption enavles us to replace $ R \\to \\infty$ without making any significant error.  
   
$$ f(t) \\;\\approx \\; 2\\, e^{w\_0 + i\\theta} \\int\_{0}^{\\infty} dr \\, e^{-\\frac{1}{2} {\\vert w''\_0 \\vert} r^2} \\;=\\; 2\\,e^{w\_0 + i\\theta} \\frac{1}{2} \\sqrt{ \\frac{2\\pi}{\\vert w''\_0 \\vert} } \\;=\\; e^{w(z\_0,t)} e^{i\\theta} \\sqrt{ \\frac{2\\pi}{\\vert{ w''(z\_0,t) \\vert} } }$$  
   
   
**Therefore, for $\\vert t \\vert \\to \\infty$, we can approximate the $f(t)$ as**  
   
**$$ \\therefore \\qquad f(t) \\overset{|t| \\to \\infty}{\\approx} F(z\_0,t) \\, e^{i\\theta} \\sqrt{ \\frac{2\\pi}{\\vert w''(z\_0,t) \\vert} } $$**  
**where $z\_0$ is a saddle point of $w(z,t)$ and**  
**$$ \\theta = -\\frac{1}{2} \\mathrm{arg}{\\left\[w''(z\_0,t)\\right\]} + { \\left( { \\frac{\\pi}{2} \\text{ or } \\frac{3\\pi}{2} } \\right) } $$**  
Choice of $\\theta$ (which affects only the sign of the final result) is determined from the sense in which the contour passes through the saddle point $z\_0$.  
 

---

   
   
이제 saddle point approximation을 사용해서 Airy function의 asymptotic form을 구해보자.  
   
Integration contour를 잡는 부분이 조금 까다롭긴 한데, 그것만 제외하면 어려운 부분은 없을 것이다... 아마도?  
   
   
   
 

#### **Asymptotic Form of the Airy Function**

---

 To apply the saddle point approximation, we need to express the Airy function in a complex contour integral form.  
   
Consider the Stoke's differential equation whose solutions are Airy functions, say $f(t)$.

  
$$ \\begin{align} \\frac{d^2 f}{d t^2} = t\\, f(t)    \\tag{1} \\end{align} $$  
Let us write the $f(t)$ by $$ \\begin{align} f(t) = \\int\_{C} dz \\, h(z)\\,e^{tz} \\qquad \\forall z \\in \\mathbb{C}    \\tag{2} \\end{align} $$ and this must satisfy the above Stoke's differential equation (1).  
   
By plugging (2) into (1), L.H.S. becomes $$ \\frac{d^2 f}{d t^2} = \\int\_{C} dz \\, h(z)\\frac{d^2}{d t^2}e^{tz} = \\int\_{C} dz\\, z^2 h(z) e^{tz} $$ and, by integrating by parts, R.H.S. becomes $$ t\\,f(t) = \\int\_{C} dz\\, h(z) t\\, e^{tz} = \\left\[\\, h(z)\\,e^{tz} \\,\\right\]\_{\\text{ends of } C} - \\int\_{C} dz\\,e^{tz}\\frac{dh}{dz} \\;. $$  
In order to make these two formulae equal, first we set $$\\begin{equation} \\left\[\\, h(z)\\,e^{tz} \\,\\right\]\_{\\text{ends of } C} = 0 \\end{equation} \\; .$$  
After then, $ h(z) $ must be in a form of $$ z^2 h(z) = -\\frac{dh}{dz} \\quad \\Rightarrow \\quad h(z) = c \\cdot e^{-\\frac{1}{3}z^3} $$ so as to ensure (1).  
   
Since we've set the square bracket term to vanish, each end point of the integration contour $C$ must satisfy $$ \\exp{\\left\[ -\\frac{1}{3} {z^3\_\\text{end}} + t\\, z\_{\\text{end}} \\right\]} = 0 \\; .$$  
This condition implies $$ \\mathrm{Re}{(z^3\_{\\text{end}})} > 0 \\qquad \\text{and} \\qquad \\left| \\, z\_{\\text{end}} \\, \\right| \\to \\infty $$ since $z^3$ is divergent much faster than $z$ as $|z|$ increases.  
   
From $\\mathrm{Re}{(z^3\_{\\text{end}})}>0$, we obtain $$\\begin{equation} \\frac{2n\\pi}{3} - \\frac{\\pi}{6} \\, < \\, \\arg{(z\_{\\text{end}})} \\,<\\, \\frac{2n\\pi}{3} + \\frac{\\pi}{6} \\; .   \\tag{3} \\end{equation}$$   
   
From the above results, the complex plane is divided as below.

[##_Image|kage@dE3jwp/btst6MLEcOM/wcEidt53pjRWJrBjvlADnk/img.png|CDM|1.3|{"originWidth":713,"originHeight":665,"style":"alignCenter","width":450,"height":420}_##]

   
Due to (3), we must set our integration curve $C$ to start from an infinity in one gray sector, and terminate at infinity in the other gray sector. Note also that since there are three different sectors that satisfy the condition (3), we can make three different contours, say $C\_1, C\_2, C\_3$, and each choice will give correspoinding solutions $f\_1, f\_2, f\_3$.  
   
Consequently, the general solutions(contour integral form) to the Stoke's equation (1) can be written as  
   
$$ \\begin{flalign\*} & \\qquad \\qquad \\mathrm{Ai}\\,(t) = \\frac{1}{2\\pi i} \\int\_{C\_1} dz\\,e^{zt-\\frac{z^3}{3}} \\\\ &{} \\\\ & \\qquad \\qquad \\mathrm{Bi}\\,(t) = \\frac{1}{2\\pi} \\int\_{C\_2 - C\_3} dz\\, e^{zt-\\frac{z^3}{3}} \\end{flalign\*} $$

  
and we will focus only on $\\mathrm{Ai}\\,(t)$ in today's post.

   
 

---

**Asymptotic form of Ai(t) in $\\mathbf{t \\gg 0}$ region**

---

First, we should figure out saddle points of $w$.   
$$ e^{w(z,t)} = e^{tz-\\frac{z^3}{3}} \\qquad \\Rightarrow \\qquad \\frac{dw}{dz}=t-z^2 \\qquad \\Rightarrow \\qquad \\text{saddle points of }  w(z,t)  \\text{  :  } \\;\\; z\_0 = \\pm \\sqrt{t} $$  
 

[##_Image|kage@QoEf7/btst6iYde9Z/gSxk6pPeGgQnxG7xh24eOK/img.png|CDM|1.3|{"originWidth":681,"originHeight":652,"style":"floatRight","width":279}_##]

i)  For $ z\_0 = -\\sqrt{t} $, $$ w''(z\_0,t) = 2\\sqrt{t} \\qquad \\Rightarrow \\qquad \\mathrm{arg}(w''\_0) = 0 $$ $\\; \\; \\;$ $\\therefore \\;\\; \\mathrm{Re}(w)$ decreases most rapidly when $\\theta = \\pi / 2 \\, , \\; 3\\pi / 2 $ as $z$ leaves $z\_0$.

ii)  For $ z\_0 = \\sqrt{t} $, $$ w''(z\_0,t) = -2\\sqrt{t} \\qquad \\Rightarrow \\qquad \\mathrm{arg}(w''\_0) = \\pi $$ $\\; \\; \\;$ $\\therefore \\;\\; \\mathrm{Re}(w)$ decreases most rapidly when $\\theta = 0 \\, , \\; \\pi $ as $z$ leaves $z\_0$.  
   
 

Let us definitize the integration contour. All we need to do is to find the level lines of $v$ that pass through each saddle points of $w$.

Let us plug $z=x+iy$ into $w(z)$. $$ w(z) = tz-\\frac{1}{3}z^3 = \\left\[ \\, tx-\\frac{1}{3}x^3 - xy^2 \\, \\right\] + i\\,\\left\[ \\, ty + \\frac{1}{3}y^3 - x^2 y \\, \\right\] $$  
Since $v(x,y)$ should be a level line, $$ v(x,y) = ty + \\frac{1}{3}y^3 - x^2 y = \\gamma \\qquad \\text{where} \\; \\gamma \\; \\text{is a real constant} $$ and, since $v(x,y)$ must pass through the saddle point(s), $$ v(z\_0) = v(\\pm \\sqrt{t}, 0) = 0 = \\gamma \\; . $$  
Then, we obtain some candidates for the integration contour $C$. $$ ty + \\frac{1}{3}y^3 - x^2 y = 0 \\qquad \\implies \\qquad C \\; : \\; \\begin{cases} \\quad  y=0 & \\mbox{:  real axis} \\\\ {} \\\\ \\quad x^2 - \\frac{1}{3}y^2 = t & \\mbox{:  hyperbola} \\end{cases} $$  
However, real axis cannot be an integration contour since its left-end is outside the gray color sectors !  
  
Hence, we must choose the hyperbola one as our integration contour. $$ C = \\left\\{ z=x+iy \\;\\; \\left| \\quad \\forall x<0 \\; , \\; \\forall y \\in \\mathbb{R} \\quad \\text{s.t.} \\quad x^2 - \\frac{1}{3}y^2 = t \\; \\right. \\right\\} $$ Notice that the hyperbola in positive $x$ region is neglected as well. Because its each end-point of $C$ are not inside the gray sectors.

Therefore, the integration contour for this case might be drawn as below.

[##_Image|kage@dvCB8j/btsubIQO9g1/dp3jw8DAm4dEkf0Qug3Ib1/img.png|CDM|1.3|{"originWidth":787,"originHeight":746,"style":"alignCenter","width":450,"height":427,"filename":"fig4.png"}_##]

 I chose the direction of the contour upward in order to make the asymptotic form match the conventional series form Airy function.  
 

  
Plugging the corresponding values $${ z\_0 = -\\sqrt{t} \\; , \\;\\; w\_0 = -\\frac{2}{3}t^{\\frac{3}{2}} \\; , \\;\\; w''\_0 = 2\\sqrt{t} \\; , \\;\\; \\theta = -\\frac{1}{2}\\mathrm{arg}(w''\_0) + \\frac{\\pi}{2} = \\frac{\\pi}{2} }$$ into the consequence of saddle point approximation $$ \\mathrm{Ai}\\,(t) \\sim \\frac{1}{2\\pi i} F(z\_0,t) \\, e^{i\\theta} \\sqrt{\\frac{2\\pi}{|w''(z\_0,t)|}} \\; , $$  
we obtain the asymptotic approximation of $\\mathrm{Ai}\\,(t)$ in $ t \\gg 0 $ region,

  
$$ \\therefore \\qquad \\mathrm{Ai}\\,(t) \\, \\overset{t \\to \\infty}{\\sim} \\, \\frac{1}{2\\sqrt{\\pi}\\, t^{\\frac{1}{4}}} \\, \\exp{\\left(-\\frac{2}{3} t^{\\frac{3}{2}}\\right)}  $$  
   
 

---

**Asymptotic form of Ai(t) in $\\mathbf{t \\ll 0}$ region**

---

 For this case, since $t$ is negative, saddle points are given by

$$ z\_0 = \\pm i \\sqrt{|t|} $$

[##_Image|kage@cuYhcv/btst7xILKiw/vgu71dBKcno7bvIieY3fRK/img.png|CDM|1.3|{"originWidth":711,"originHeight":697,"style":"floatRight","width":280,"filename":"fig5.png"}_##]

i)  For $ z\_0 = -i\\sqrt{|t|} $, $$ w''(z\_0,t) = 2i\\sqrt{|t|} \\qquad \\Rightarrow \\qquad \\mathrm{arg}(w''\_0) = \\frac{\\pi}{2} $$ $\\; \\; \\;$ $\\therefore \\;\\; \\mathrm{Re}(w)$ decreases most rapidly when $\\theta = \\pi / 4 \\, , \\; 5\\pi / 4 $ as $z$ leaves $z\_0$.

  
ii)  For $ z\_0 = i\\sqrt{|t|} $, $$ w''(z\_0,t) = -2i\\sqrt{|t|} \\qquad \\Rightarrow \\qquad \\mathrm{arg}(w''\_0) = -\\frac{\\pi}{2} $$ $\\; \\; \\;$ $\\therefore \\;\\; \\mathrm{Re}(w)$ decreases most rapidly when $\\theta = 3\\pi / 4 \\, , \\; 7\\pi / 4 $ as $z$ leaves $z\_0$.

   
  
 

For $z\_0 = i\\sqrt{|t|}$, the level line of $v$ passes through the saddle point $z\_0=i\\sqrt{|t|}$ is $$ v(x,y) = ty + \\frac{1}{3}y^3 - x^2 y = v(0, \\sqrt{|t|})  \\qquad \\Rightarrow \\qquad -|t|y + \\frac{1}{3}y^3 - x^2 y = -\\frac{2}{3} |t|^{\\frac{3}{2}} \\;\\; . $$ 

Similarly, for $z\_0 = -i\\sqrt{|t|}$, the level line of $v$ that passes through the saddle point $z\_0 = -i\\sqrt{|t|}$ is  $$ -|t|y + \\frac{1}{3}y^3 - x^2 y = \\frac{2}{3} |t|^{\\frac{3}{2}} \\;\\; . $$ 

By picking proper level lines (whose end-points are inside the gray sectors), and setting orientations of the picked level lines properly, the integration contours can be depicted as below.

[##_Image|kage@cFRLia/btsu0pWl1My/LJNmL2o8EKuu1TJvG3XgqK/img.png|CDM|1.3|{"originWidth":788,"originHeight":753,"style":"alignCenter","width":450,"height":430,"filename":"fig6.png"}_##]

Through the similar process as before, we can derieve the asymptotic form of the Airy function in $t \\ll 0$ region. 

$$ \\mathrm{Ai}\\,(t) \\;\\; \\sim \\;\\; \\frac{1}{2\\pi i} \\; \\left\[ \\, e^{\\frac{2\\,i}{3} |t|^{\\frac{3}{2}}} e^{\\frac{\\pi}{4} i} \\sqrt{\\frac{2\\pi}{\\left|2i \\sqrt{|t|}\\right|}} \\; + \\; e^{-\\frac{2\\,i}{3} |t|^{\\frac{3}{2}}} e^{\\frac{3\\pi}{4} i} \\sqrt{\\frac{2\\pi}{\\left|-2i \\sqrt{|t|}\\right|}} \\, \\right\] \\;\\; = \\;\\; \\frac{1}{\\sqrt{\\pi} \\, |t|^{\\frac{1}{4}}} \\; \\sin{\\left( \\frac{2}{3} |t|^{\\frac{3}{2}} + \\frac{\\pi}{4} \\right)} $$

$$ \\therefore \\qquad \\mathrm{Ai}\\,(t) \\;\\; \\overset{t \\to -\\infty}{\\sim} \\;\\;  \\frac{1}{\\sqrt{\\pi} \\, |t|^{\\frac{1}{4}}} \\;\\sin{\\left( \\frac{2}{3} |t|^{\\frac{3}{2}} + \\frac{\\pi}{4} \\right)} $$

Note that, if we included only a single saddle point or if we set the directions of contours to be opposite to each other, then we cannot make the $\\mathrm{Ai}\\,(t)$ to be a real valued function. Hence, we should take into account both saddle points, and set the orientations of the contours as the above figure! 

---

Asymptotic approximation이 exact Airy function을 얼마나 잘 따라가는지 구경 좀 해보려고 plot을 해봤다. 

[##_Image|kage@k5pRz/btsu2aSaHjr/0FwOfFb6bLmdSlc1pOfKKk/img.png|CDM|1.3|{"originWidth":794,"originHeight":600,"style":"alignCenter","width":650,"height":491,"filename":"graph.png"}_##]

approximation이 blow up 되어버리는 $|t|<<1$ 영역을 제외하면 상당히 잘 따라가는 것을 볼 수 있다.

신기하군.

---
