---
layout: post
title:  "Waves on Infinite Wires"
categories: math physics integration
---

## General Problem

Say you have some field which obeys the inverse square law, and an infinitely long wire. Let the time varying potential in the wire be $S(x, t)$, Where $x$ is distance along the wire and $t$ is the time. Say you are measuring the resulting field at a point whose orthogonal distance to the wire is $y$, and $x$ position is 0. Lets define $f(x,y)$ to be the contribution of a point along the wire at distance $x$ from the origin to the field measured at our point $(0, y)$. We will make the assumption that the propagation speed of our field is sufficiently high that any time delay can be ignored. Applying the inverse square law, 

$$f(x, y) = \frac{S(x,t)}{x^2 + y^2}$$

Adding up the contributions of each point along the wire yields the signal at the measured point, which we will call $s$.

$$s(y, t) = \int_{-\infty}^{\infty} f(x,y)dx=\int_{-\infty}^{\infty} \frac{S(x,t)}{x^2 + y^2}dx$$

These types of integrals can generally be solved by the residue theorem of complex analysis. The residue of $f(z)$ at a singularity $z=a$ is the value $R$ such that $f(z) - \frac{R}{z-a}$ has an analytic anti-derivative at $z=a$. Clearly our function only has two singularities, $x = iy$ and $x = -iy$. Using an algebra trick, we can separate the integrand into two term such that each only has a single singularity. 

$$\frac{S(x,t)}{x^2+y^2} = S(x,t)\left(\frac{1}{x^2 + y^2}\right) = S(x,t)\left(\frac{1}{2i(x-iy)} - \frac{1}{2i(x+iy)}\right) = \frac{S(x,t)}{2i(x-iy)} - \frac{S(x,t)}{2i(x+iy)}$$

This trick is essentially just the reverse of finding a common denominator, factoring the product into a sum rather than the usual direction, factoring a sum into a product. In order to remove the singularity at $x=-iy$,

$$\frac{S(x,t)}{2i(x+iy)} - \frac{R}{x+iy} \big |_{x=-iy}= 0$$

so

$$R = \frac{S(-iy,t)}{2i}$$

By the **residue theorem**, any closed path integral that incloses a single singularity with residual $R$ is

$$\oint f(x,y) dx = 2\pi iR$$

We can take our closed path to be a half circle, with the flat section traveling along the real axis from $-l$ to $l$, and the circular arc in the negative imaginary direction connecting the two ends.

$$\oint f(x,y) dx =\int_{\text{arc}}f(x,y)dx + \int^{l}_{-l}f(x,y)dx = \pi S(-iy,t)$$

Using the **ML inequality**, we can see what condition on $S$ is needed for $\lim_{l\to\infty} \int_{\text{arc}}f(x,y)dx = 0$. 
Along the semicircular arc, $x = le^{i\theta}$ for $-\pi\leq\theta\leq 0$, so

$$\left|\int_{\text{arc}} f(x,y)dx\right|\leq \pi l \sup_{-\pi\leq\theta\leq 0}\left|\frac{S(le^{i\theta},y)}{l^2e^{2i\theta}+y^2}\right|$$

By the reverse triangle inequality, and using the fact that $y,l\in\mathbb{R}$,

$$\pi l \sup_{-\pi\leq\theta\leq 0}\left|\frac{S(le^{i\theta},y)}{l^2e^{2i\theta}+y^2}\right|\leq\pi l \frac{\sup_{-\pi\leq\theta\leq 0}|S(le^{i\theta},y)|}{|l^2-y^2|}$$

Then in order for  

$$\lim_{l\to\infty} \int_{\text{arc}}f(x,y)dx = 0, \ \ \lim_{l\to\infty} \frac{\sup_{-\pi\leq\theta\leq 0}|S(le^{i\theta},t)|}{l}  = 0$$ 

If this condition is met, then we have our desired solution,

$$s(t,y)= \int_{-\infty}^{\infty} \frac{S(x,t)}{x^2+y^2}dx=\pi S(-iy, t)$$

## Sinusoidal Potential

Lets consider a sinusoidal potential with angular frequency $\omega$ that travels down our wire at speed $c$, with real positive amplitude $A(x): \ \mathbb{C}\to\mathbb{R}$.

$$S(x, t) = A(x)\sin(\omega (t - x/c) + \varphi)$$

In order to simplify some of the work, note that

$$\int_{-\infty}^{\infty} \frac{A(x)\sin(z(x))}{x^2 + y^2}dx = \int_{-\infty}^{\infty}\frac{A(x)\Im(e^{iz(x)})}{x^2+y^2} = \Im\left(\int_{-\infty}^{\infty}\frac{A(x)e^{iz(x)}}{x^2+y^2}\right)$$

Where $z(x) = \omega (t - x/c) + \varphi$. So let

$$S'(x,t) = A(x)e^{i(\omega (t - x/c) + \varphi)}$$

then 

$$|S'(le^{i\theta},t)|=|A(le^{i\theta})e^{-ile^{i\theta}}e^{i(\omega t+\varphi)}|=|A(le^{i\theta})||e^{-il\cos(\theta) + l\sin(\theta)}|=A(le^{i\theta})e^{l\sin(\theta)}$$

For $-\pi\leq\theta\leq0$, $\sin(\theta)\leq 0$, 
so $|S'(le^{i\theta},t)|\leq\sup_{-\pi\leq\theta\leq 0}A(le^{i\theta})$. If we then require that $A(x)$ is bounded above by some finite value $A_0$, we have that

$$\lim_{l\to\infty} \frac{\sup_{0\leq\theta\leq\pi}|S(le^{i\theta},t)|}{l} \leq \lim_{l\to\infty} \frac{A_0}{l} = 0$$

and therefore 

$$s(t,y)= \Im\left(\int_{-\infty}^{\infty} \frac{S'(x,t)}{x^2+y^2}dx\right)=\Im(\pi S'(-iy, t))$$

so our solution is then

$$s(t,y) = \Im\left(A(-iy)e^{i(\omega (t + iy/c) + \varphi)}\right) = A(-iy)e^{-\omega y /c}\Im\left(e^{i(\omega t + \varphi)}\right)$$

$$s(t,y) =A(-iy)e^{-\omega y /c}\sin(\omega t + \varphi)$$

For example, let the potential amplitude be exponentially decaying from some source on the wire a distance $d$ away. Then,

$$A(z) = A_0e^{-\alpha|x-d|}= A_0e^{-\alpha\sqrt{(x-d)^*(x-d)}}$$

so 

$$A(-iy) = A_0e^{-\alpha\sqrt{y^2+d^2}}$$ 

and 

$$s(t,y) = A_0e^{-\left(\omega y / c +\alpha\sqrt{y^2+d^2}\right)}\sin(\omega t + \varphi)$$

Interestingly, the phase of the signal observed at the measurement point is the same as the closest point on the wire, but the amplitude depends on the frequency of the wave as well as the traveling speed, distance from the wire and potential source.


