---
module: MAT01B1
topic: Arc Length
session: S11
tags: [definition, theorem, formula, worked-example]
---

# Arc Length

Source: Dr K, §8.1 Arc Length (slides 1 to 20).

## What arc length means (source, slides 2 to 3)

The obvious way to measure a curve is to lay a piece of string along it and straighten the string against a ruler. That is hard to do accurately for a complicated curve, so a precise definition is needed, in the same spirit as the definitions already built for area ([[MAT01B1_Notes_S7_AreaBetweenCurves]]) and volume ([[MAT01B1_Notes_S8_Volumes#Definition of Volume (source, slide 8)|Definition of Volume]]).

If the curve is a polygon, its length is easy: add up the lengths of the line segments, each found with the distance formula. The plan is to approximate a general curve by a polygon and then take a limit as the number of segments grows. This is already familiar for a circle, whose circumference is the limit of the lengths of inscribed polygons.

## Definition of arc length (source, slides 4 to 6)

Let $C$ be the curve $y=f(x)$, $a\le x\le b$, with $f$ continuous. Divide $[a,b]$ into $n$ subintervals with endpoints $x_0,x_1,\dots,x_n$ and equal width $\Delta x$. With $y_i=f(x_i)$, each point $P_i(x_i,y_i)$ lies on $C$, and the polygon with vertices $P_0,P_1,\dots,P_n$ approximates $C$. The approximation improves as $n$ increases.

**Definition.** The length $L$ of the curve $C$ is the limit of the lengths of these inscribed polygons, if the limit exists:

$$
L=\lim_{n\to\infty}\sum_{i=1}^n\big|P_{i-1}P_i\big|.
$$

**Hypotheses**
- $f$ continuous on $[a,b]$

N.B The procedure is the same three moves as for area and volume: cut into many small parts, approximate each part, add up, then take the limit as $n\to\infty$.

## The Arc Length Formula (source, slides 7 to 9)

The definition is not convenient for computing. When $f$ has a continuous derivative (such an $f$ is called **smooth**, because a small change in $x$ produces a small change in $f'(x)$), it can be turned into an integral.

**Derivation.** Write $\Delta y_i=y_i-y_{i-1}$. The distance formula gives

$$
\big|P_{i-1}P_i\big|=\sqrt{(x_i-x_{i-1})^2+(y_i-y_{i-1})^2}=\sqrt{(\Delta x)^2+(\Delta y_i)^2}.
$$

Apply the [[MAT01B1_Proofs_ST1#Mean Value Theorem|Mean Value Theorem]] to $f$ on $[x_{i-1},x_i]$: there is a number $x_i^*$ between $x_{i-1}$ and $x_i$ with $f(x_i)-f(x_{i-1})=f'(x_i^*)(x_i-x_{i-1})$, that is,

$$
\Delta y_i=f'(x_i^*)\,\Delta x.
$$

Substituting, and using $\Delta x>0$,

$$
\big|P_{i-1}P_i\big|=\sqrt{(\Delta x)^2+\big[f'(x_i^*)\Delta x\big]^2}=\sqrt{1+\big[f'(x_i^*)\big]^2}\,\Delta x.
$$

By the definition,

$$
L=\lim_{n\to\infty}\sum_{i=1}^n\sqrt{1+\big[f'(x_i^*)\big]^2}\,\Delta x,
$$

which is the definition of the definite integral of $\sqrt{1+[f'(x)]^2}$. That integral exists because $g(x)=\sqrt{1+[f'(x)]^2}$ is continuous.

**Theorem (The Arc Length Formula).** If $f'$ is continuous on $[a,b]$, the length of the curve $y=f(x)$, $a\le x\le b$, is

$$
L=\int_a^b\sqrt{1+\big[f'(x)\big]^2}\,dx.
$$

In Leibniz notation,

$$
L=\int_a^b\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx.
$$

**Hypotheses**
- $f'$ continuous on $[a,b]$

N.B The definition only needed $f$ continuous, but the integral formula needs the stronger hypothesis that $f'$ is continuous. Both the continuity of $g$ (so the integral exists) and the Mean Value Theorem step in the derivation rely on it.

## Curves written as x in terms of y (source, slide 13)

If the curve is $x=g(y)$, $c\le y\le d$, with $g'$ continuous, interchange the roles of $x$ and $y$:

$$
L=\int_c^d\sqrt{1+\big[g'(y)\big]^2}\,dy=\int_c^d\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy.
$$

## Worked example: semicubical parabola (source, slides 10 to 12)

Find the length of $y^2=x^3$ between $(1,1)$ and $(4,8)$. For the top half, $y=x^{3/2}$ and $\dfrac{dy}{dx}=\dfrac32x^{1/2}$, so

$$
L=\int_1^4\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx=\int_1^4\sqrt{1+\frac94x}\,dx.
$$

Substitute $u=1+\tfrac94x$, so $du=\tfrac94\,dx$. When $x=1$, $u=\tfrac{13}4$; when $x=4$, $u=10$:

$$
L=\frac49\int_{13/4}^{10}\sqrt u\,du=\frac49\cdot\frac23\Big[u^{3/2}\Big]_{13/4}^{10}=\frac{8}{27}\left[10^{3/2}-\left(\frac{13}{4}\right)^{3/2}\right]=\frac{1}{27}\left(80\sqrt{10}-13\sqrt{13}\right).
$$

(added, arithmetic) $\left(\tfrac{13}{4}\right)^{3/2}=\tfrac{13\sqrt{13}}{8}$, so $\tfrac{8}{27}\cdot\tfrac{13\sqrt{13}}{8}=\tfrac{13\sqrt{13}}{27}$, and $L\approx7.634$.

```desmos-graph
left=-0.5; right=5;
top=9; bottom=-1;
---
y=x^{3/2}\left\{1\le x\le4\right\}
(1,1)
(4,8)
```

## Worked example: parabola, trigonometric substitution (source, slides 14 to 15)

Find the length of the arc of $y^2=x$ from $(0,0)$ to $(1,1)$. Since $x=y^2$, $\dfrac{dx}{dy}=2y$, and the $x=g(y)$ formula gives

$$
L=\int_0^1\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy=\int_0^1\sqrt{1+4y^2}\,dy.
$$

This is the $\sqrt{a^2+b^2x^2}$ pattern, so use the tangent substitution ([[MAT01B1_Notes_S2_DerivativeIntegralReference#Trig substitutions|Trig substitutions]]): $y=\tfrac12\tan\theta$, $dy=\tfrac12\sec^2\theta\,d\theta$, and $\sqrt{1+4y^2}=\sqrt{1+\tan^2\theta}=\sec\theta$. When $y=0$, $\tan\theta=0$, so $\theta=0$; when $y=1$, $\tan\theta=2$, so $\theta=\tan^{-1}2=\alpha$, say. Then

$$
L=\int_0^\alpha\sec\theta\cdot\frac12\sec^2\theta\,d\theta=\frac12\int_0^\alpha\sec^3\theta\,d\theta.
$$

The value of $\int\sec^3\theta\,d\theta$ is on the reference sheet ([[MAT01B1_Notes_S2_DerivativeIntegralReference]]); the source cites its Example 7.2.8 and Formula 21 in the Table of Integrals:

$$
L=\frac12\cdot\frac12\Big[\sec\theta\tan\theta+\ln|\sec\theta+\tan\theta|\Big]_0^\alpha=\frac14\Big(\sec\alpha\tan\alpha+\ln|\sec\alpha+\tan\alpha|\Big).
$$

Since $\tan\alpha=2$, $\sec^2\alpha=1+\tan^2\alpha=5$, so $\sec\alpha=\sqrt5$, and

$$
L=\frac{\sqrt5}{2}+\frac{\ln\big(\sqrt5+2\big)}{4}.
$$

(added) The same $\int\sec^3\theta\,d\theta$ value also comes from the secant reduction formula with $k=3$, derived in [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products and quotients of trig functions]].

(source note) The deck numbers this one Example 2, and the arc length function example below is Example 4. There is no Example 3 in these slides.

```desmos-graph
left=-0.3; right=1.5;
top=1.3; bottom=-0.3;
---
x=y^{2}\left\{0\le y\le1\right\}
(0,0)
(1,1)
```

## The arc length function (source, slides 16 to 17)

It is useful to have a function that measures the arc length of a curve from a fixed starting point to any other point. If the smooth curve $C$ is $y=f(x)$, $a\le x\le b$, let $s(x)$ be the distance along $C$ from the initial point $P_0(a,f(a))$ to the point $Q(x,f(x))$. Then $s$ is called the **arc length function**, and by the Arc Length Formula

$$
s(x)=\int_a^x\sqrt{1+\big[f'(t)\big]^2}\,dt.
$$

The variable of integration is renamed $t$ so that $x$ does not have two meanings. The integrand is continuous, so Part 1 of the Fundamental Theorem of Calculus differentiates it:

$$
\frac{ds}{dx}=\sqrt{1+\big[f'(x)\big]^2}=\sqrt{1+\left(\frac{dy}{dx}\right)^2}.
$$

This says the rate of change of $s$ with respect to $x$ is always at least $1$, and equals $1$ exactly when the slope $f'(x)$ is $0$. Written as a differential, the **differential arc length** is

$$
ds=\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx.
$$

## Differential arc length (source, slide 18)

The last equation is sometimes written in the symmetric form

$$
(ds)^2=(dx)^2+(dy)^2.
$$

Figure 7 in the source shows why: a small piece of the curve, its horizontal change $dx$, its vertical change $dy$, and the segment $ds$ form a right triangle with $ds$ as the hypotenuse.

It doubles as a mnemonic for both length formulas. Write $L=\int ds$. Solving $(ds)^2=(dx)^2+(dy)^2$ for $ds$ in terms of $dx$ gives the $dx$ form above, and hence the formula in $x$. Solving it the other way gives

$$
ds=\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy,
$$

and hence the formula for $x=g(y)$.

-> This same $ds$ is the factor that turns a rotated curve into a surface: see [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]], where the surface area integrals are $\int2\pi y\,ds$ and $\int2\pi x\,ds$.

## Worked example: arc length function (source, slides 19 to 20)

Find the arc length function for $y=x^2-\tfrac18\ln x$, taking $P_0(1,1)$ as the starting point. With $f(x)=x^2-\tfrac18\ln x$, $f'(x)=2x-\dfrac{1}{8x}$, so

$$
1+\big[f'(x)\big]^2=1+\left(2x-\frac{1}{8x}\right)^2=1+4x^2-\frac12+\frac{1}{64x^2}=4x^2+\frac12+\frac{1}{64x^2}=\left(2x+\frac{1}{8x}\right)^2.
$$

Since $x>0$, $\sqrt{1+[f'(x)]^2}=2x+\dfrac{1}{8x}$. Then

$$
s(x)=\int_1^x\left(2t+\frac{1}{8t}\right)dt=\Big[t^2+\tfrac18\ln t\Big]_1^x=x^2+\frac18\ln x-1.
$$

For instance, the arc length along the curve from $(1,1)$ to $(3,f(3))$ is

$$
s(3)=3^2+\frac18\ln3-1=8+\frac{\ln3}{8}\approx8.1373.
$$

N.B The whole example turns on noticing that $1+[f'(x)]^2$ collapses to a perfect square, which removes the square root. Arc length integrals are usually only doable when that happens (or when a substitution such as the ones above rescues them), so it is worth checking for a perfect square early.

## See also
- [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]] (the surface generated by rotating these curves, built on the same $ds$)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Arc length of a parametric curve]] (arc length for curves given parametrically, the same idea with $dx/dt$ and $dy/dt$)
- [[MAT01B1_Proofs_ST1#Mean Value Theorem]] (used in the derivation above)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (trig substitution and the $\sec^3$ integral)
- [[MAT01B1_Notes_S7_AreaBetweenCurves]], [[MAT01B1_Notes_S8_Volumes]] (the same divide, approximate, sum, limit procedure applied to area and volume)
