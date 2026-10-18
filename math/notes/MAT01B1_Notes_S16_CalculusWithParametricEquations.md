---
module: MAT01B1
topic: Calculus with Parametric Equations
session: S16
tags: [theorem, formula, worked-example]
---

# Calculus with Parametric Equations

Source: Dr K, §10.2 Calculus with Parametric Equations (slides 1 to 26).

## Tangents

Suppose $f,g$ are differentiable and $y$ is also a differentiable function of $x$ along the curve $x=f(t)$, $y=g(t)$. The [[MAT01B1_Notes_S2_DerivativeIntegralReference#Basic properties|Chain Rule]] gives $\dfrac{dy}{dt}=\dfrac{dy}{dx}\cdot\dfrac{dx}{dt}$, so if $dx/dt\ne0$,

$$
\frac{dy}{dx}=\frac{dy/dt}{dx/dt}.
$$

This finds the slope of the tangent to a parametric curve without eliminating $t$. The curve has a **horizontal tangent** where $dy/dt=0$ (provided $dx/dt\ne0$), and a **vertical tangent** where $dx/dt=0$ (provided $dy/dt\ne0$), useful for sketching.

**Second derivative.** Replacing $y$ by $dy/dx$ in the formula above,

$$
\frac{d^2y}{dx^2}=\frac{d}{dx}\left(\frac{dy}{dx}\right)=\frac{\dfrac{d}{dt}\left(\dfrac{dy}{dx}\right)}{dx/dt}.
$$

## Worked example: a self-crossing curve (source, slides 5 to 8)

$C$: $x=t^2$, $y=t^3-3t$.

**(a) Two tangents at $(3,0)$.** $y=t(t^2-3)=0$ at $t=0,\pm\sqrt3$. Since $x=t^2=3$ at $t=\pm\sqrt3$ (not at $t=0$), the point $(3,0)$ arises from *two* different parameter values, so $C$ crosses itself there.

$$
\frac{dy}{dx}=\frac{dy/dt}{dx/dt}=\frac{3t^2-3}{2t}=\frac32\left(t-\frac1t\right).
$$

At $t=\pm\sqrt3$: $dy/dx=\pm6/(2\sqrt3)=\pm\sqrt3$. The two tangents at $(3,0)$ are

$$
y=\sqrt3(x-3)\qquad\text{and}\qquad y=-\sqrt3(x-3).
$$

**(b) Horizontal and vertical tangents.** Horizontal: $dy/dt=3t^2-3=0\Rightarrow t=\pm1$ (points $(1,-2)$, $(1,2)$). Vertical: $dx/dt=2t=0\Rightarrow t=0$ (and $dy/dt\ne0$ there), point $(0,0)$.

**(c) Concavity.**

$$
\frac{d^2y}{dx^2}=\frac{\dfrac{d}{dt}\left(\dfrac32\left(t-\dfrac1t\right)\right)}{dx/dt}=\frac{\dfrac32\left(1+\dfrac1{t^2}\right)}{2t}=\frac{3(t^2+1)}{4t^3}.
$$

Concave up for $t>0$, concave down for $t<0$.

**(d)** Sketching $C$ uses the horizontal/vertical tangent points from (b) and the concavity split from (c) together.

## Worked example: tangent to the cycloid (source, slides 9 to 11)

$$
\frac{dy}{dx}=\frac{dy/d\theta}{dx/d\theta}=\frac{r\sin\theta}{r(1-\cos\theta)}=\frac{\sin\theta}{1-\cos\theta}.
$$

At $\theta=\pi/3$: $x=r\!\left(\dfrac\pi3-\dfrac{\sqrt3}2\right)$, $y=\dfrac r2$, and $\dfrac{dy}{dx}=\dfrac{\sqrt3/2}{1-1/2}=\sqrt3$. Tangent line:

$$
y-\frac r2=\sqrt3\left(x-\frac{r\pi}3+\frac{r\sqrt3}2\right)\quad\text{or}\quad\sqrt3x-y=r\left(\frac{\pi}{\sqrt3}-2\right).
$$

**Horizontal tangents:** $\sin\theta=0$ with $1-\cos\theta\ne0$, i.e. $\theta=(2n-1)\pi$, at points $\big((2n-1)\pi r,\,2r\big)$.

**Vertical tangents:** at $\theta=2n\pi$, both $dx/d\theta$ and $dy/d\theta$ are $0$, so [[MAT01B1_Notes_S1_CalculusApplications#L'Hospital's Rule and indeterminate forms|l'Hôpital's Rule]] is needed:

$$
\lim_{\theta\to2n\pi^+}\frac{dy}{dx}=\lim_{\theta\to2n\pi^+}\frac{\sin\theta}{1-\cos\theta}=\lim_{\theta\to2n\pi^+}\frac{\cos\theta}{\sin\theta}=\infty,
$$

and similarly $dy/dx\to-\infty$ as $\theta\to2n\pi^-$, confirming a vertical tangent at $\theta=2n\pi$, i.e. $x=2n\pi r$.

## Area under a parametric curve

If the curve $x=f(t)$, $y=g(t)$, $\alpha\le t\le\beta$, traces out $y=F(x)\ge0$ exactly once, the Substitution Rule turns the ordinary area formula into

$$
A=\int_a^by\,dx=\int_\alpha^\beta g(t)f'(t)\,dt.
$$

## Worked example: area under one arch of the cycloid (source, slide 13)

$0\le\theta\le2\pi$, $y=r(1-\cos\theta)$, $dx=r(1-\cos\theta)\,d\theta$:

$$
A=\int_0^{2\pi r}y\,dx=\int_0^{2\pi}r(1-\cos\theta)\cdot r(1-\cos\theta)\,d\theta=r^2\int_0^{2\pi}(1-\cos\theta)^2\,d\theta.
$$

Expanding and using $\cos^2\theta=\tfrac12(1+\cos2\theta)$:

$$
=r^2\int_0^{2\pi}\left[1-2\cos\theta+\frac12(1+\cos2\theta)\right]d\theta=r^2\left[\frac32\theta-2\sin\theta+\frac14\sin2\theta\right]_0^{2\pi}=r^2\left(\frac32\cdot2\pi\right)=3\pi r^2.
$$

## Arc length of a parametric curve

For $y=F(x)$, $a\le x\le b$ with $F'$ continuous, arc length is (from [[MAT01B1_Notes_S11_ArcLength#The Arc Length Formula (source, slides 7 to 9)|The Arc Length Formula]])

$$
L=\int_a^b\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx.
$$

If $C$ is also $x=f(t)$, $y=g(t)$, $\alpha\le t\le\beta$ with $dx/dt=f'(t)>0$ (so $C$ is traced once, left to right), substituting the tangent-slope formula and using the Substitution Rule gives

$$
L=\int_\alpha^\beta\sqrt{\left(\frac{dx}{dt}\right)^2+\left(\frac{dy}{dt}\right)^2}\,dt.
$$

**Why this still holds even when $C$ isn't of the form $y=F(x)$ (source, slides 16 to 19).** Divide $[\alpha,\beta]$ into $n$ subintervals of width $\Delta t$ with endpoints $t_0,\dots,t_n$; the points $P_i(x_i,y_i)=(f(t_i),g(t_i))$ form a polygon approximating $C$, and $L=\lim_{n\to\infty}\sum_{i=1}^n|P_{i-1}P_i|$. The [[MAT01B1_Proofs_ST1#Mean Value Theorem|Mean Value Theorem]], applied separately to $f$ and to $g$ on $[t_{i-1},t_i]$, gives numbers $t_i^*,t_i^{**}\in(t_{i-1},t_i)$ with

$$
\Delta x_i=f'(t_i^*)\Delta t,\qquad \Delta y_i=g'(t_i^{**})\Delta t,
$$

so $|P_{i-1}P_i|=\sqrt{[f'(t_i^*)]^2+[g'(t_i^{**})]^2}\,\Delta t$. The resulting sum resembles, but isn't exactly, a Riemann sum for $\sqrt{[f'(t)]^2+[g'(t)]^2}$, since in general $t_i^*\ne t_i^{**}$; when $f',g'$ are continuous, the limit is the same as if they were equal.

**Theorem.** If $C$ is described by $x=f(t)$, $y=g(t)$, $\alpha\le t\le\beta$, where $f',g'$ are continuous on $[\alpha,\beta]$ and $C$ is traversed exactly once as $t$ increases from $\alpha$ to $\beta$, then the length of $C$ is

$$
L=\int_\alpha^\beta\sqrt{\left(\frac{dx}{dt}\right)^2+\left(\frac{dy}{dt}\right)^2}\,dt.
$$

**Hypotheses**
- $f',g'$ continuous on $[\alpha,\beta]$
- $C$ traversed exactly once as $t$ runs from $\alpha$ to $\beta$

N.B "Traversed exactly once" is doing real work here, it's exactly the condition that failed in [[MAT01B1_Notes_S15_ParametricEquations#Worked example: the unit circle, traced twice (source, slide 9)|S15's second unit-circle parametrization]]; the next example shows what happens to $L$ when it's violated.

## Worked example: arc length of the unit circle, two parametrizations (source, slides 20 to 21)

**Traced once** ($x=\cos t$, $y=\sin t$, $0\le t\le2\pi$, from [[MAT01B1_Notes_S15_ParametricEquations#Worked example: the unit circle, traced once (source, slides 7 to 8)|S15]]): $dx/dt=-\sin t$, $dy/dt=\cos t$,

$$
L=\int_0^{2\pi}\sqrt{\sin^2t+\cos^2t}\,dt=\int_0^{2\pi}dt=2\pi,
$$

as expected for a unit circle.

**Traced twice** ($x=\sin2t$, $y=\cos2t$, $0\le t\le2\pi$, from [[MAT01B1_Notes_S15_ParametricEquations#Worked example: the unit circle, traced twice (source, slide 9)|S15]]): $dx/dt=2\cos2t$, $dy/dt=-2\sin2t$,

$$
L=\int_0^{2\pi}\sqrt{4\cos^22t+4\sin^22t}\,dt=\int_0^{2\pi}2\,dt=4\pi,
$$

double the true circumference, exactly because this parametrization goes around twice, the "traversed exactly once" hypothesis in the theorem above is violated, and the formula faithfully reports total distance travelled, not the length of the underlying set of points.

## Worked example: arc length of one arch of the cycloid (source, slides 22 to 24)

$dx/d\theta=r(1-\cos\theta)$, $dy/d\theta=r\sin\theta$:

$$
L=\int_0^{2\pi}\sqrt{r^2(1-\cos\theta)^2+r^2\sin^2\theta}\,d\theta=r\int_0^{2\pi}\sqrt{2(1-\cos\theta)}\,d\theta.
$$

Using $\sin^2x=\tfrac12(1-\cos2x)$ with $\theta=2x$, so $1-\cos\theta=2\sin^2(\theta/2)$: since $0\le\theta\le2\pi$ gives $0\le\theta/2\le\pi$, $\sin(\theta/2)\ge0$, so $\sqrt{2(1-\cos\theta)}=\sqrt{4\sin^2(\theta/2)}=2\sin(\theta/2)$.

$$
L=2r\int_0^{2\pi}\sin(\theta/2)\,d\theta=2r\Big[-2\cos(\theta/2)\Big]_0^{2\pi}=2r(2+2)=8r.
$$

## Surface area

Adapting the arc-length idea (the source refers to this as Formula 8.2.5; the $y=f(x)$ version it adapts is built up in [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution#Building the surface area formula (source, slides 7 to 10)|Building the surface area formula]]): for $C$: $x=f(t)$, $y=g(t)$, $\alpha\le t\le\beta$, with $f',g'$ continuous, $g(t)\ge0$, traversed once, rotated about the $x$-axis, the surface area is

$$
S=\int_\alpha^\beta2\pi y\sqrt{\left(\frac{dx}{dt}\right)^2+\left(\frac{dy}{dt}\right)^2}\,dt,
$$

matching the general symbolic form $S=\int2\pi y\,ds$ with $ds=\sqrt{(dx/dt)^2+(dy/dt)^2}\,dt$ for parametric curves.

## Worked example: surface area of a sphere (source, slides 25 to 26)

The sphere of radius $r$ is the semicircle $x=r\cos t$, $y=r\sin t$, $0\le t\le\pi$, rotated about the $x$-axis.

$$
S=\int_0^\pi2\pi r\sin t\sqrt{(-r\sin t)^2+(r\cos t)^2}\,dt=2\pi\int_0^\pi r\sin t\cdot r\,dt=2\pi r^2\big[-\cos t\big]_0^\pi=4\pi r^2.
$$

## See also
- [[MAT01B1_Notes_S15_ParametricEquations]]
- [[MAT01B1_Notes_S11_ArcLength]] (the arc length formula for $y=f(x)$ that the parametric version generalises)
- [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]] (the surface area formula for $y=f(x)$)
- [[MAT01B1_Proofs_ST1#Mean Value Theorem]] (used twice in the arc length derivation above, once for $f$, once for $g$)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (Chain Rule, Substitution Rule)
