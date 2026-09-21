---
module: MAT01B1
topic: Curves Defined by Parametric Equations
session: S15
tags: [definition, formula, worked-example]
---

# Curves Defined by Parametric Equations

Source: Dr K, §10.1 Curves defined by Parametric equations (slides 1 to 12).

## Why parametric equations

A curve $C$ that fails the Vertical Line Test (loops back on itself, crosses itself, and so on) cannot be written as $y=f(x)$. But if a particle traces $C$ over time, its $x$- and $y$-coordinates are each separately functions of time, $x=f(t)$ and $y=g(t)$.

**Definition.** If $x$ and $y$ are both given as functions of a third variable $t$ (the **parameter**) by $x=f(t)$, $y=g(t)$ (**parametric equations**), each value of $t$ determines a point $(x,y)$. As $t$ varies, $(x,y)=(f(t),g(t))$ traces out a **parametric curve**. $t$ needn't represent time and needn't be called $t$, but in many applications it does denote time, and $(f(t),g(t))$ is a particle's position at time $t$.

If $t$ is restricted to $a\le t\le b$, the curve $x=f(t)$, $y=g(t)$ has **initial point** $(f(a),g(a))$ and **terminal point** $(f(b),g(b))$.

## Worked example: identifying a curve by eliminating the parameter (source, slides 3 to 6)

Sketch and identify $x=t^2-2t$, $y=t+1$.

Plotting points for several values of $t$ suggests a parabola. Consecutive points at equal time intervals are *not* equally spaced along the curve, the particle slows down then speeds up as $t$ increases. To confirm the shape, eliminate $t$: from the second equation, $t=y-1$, substitute into the first:

$$
x=t^2-2t=(y-1)^2-2(y-1)=y^2-4y+3.
$$

So the curve is the parabola $x=y^2-4y+3$.

If $t$ is restricted to $0\le t\le4$, the curve is only the piece of this parabola from the initial point $(0,1)$ to the terminal point $(8,5)$, traced in the direction of increasing $t$.

## Worked example: the unit circle, traced once (source, slides 7 to 8)

$x=\cos t$, $y=\sin t$, $0\le t\le2\pi$. Eliminating $t$:

$$
x^2+y^2=\cos^2t+\sin^2t=1,
$$

so $(x,y)$ moves on the unit circle. Here $t$ is literally the angle shown in the standard picture of the unit circle: as $t$ increases from $0$ to $2\pi$, the point moves once around the circle counterclockwise, starting at $(1,0)$.

## Worked example: the unit circle, traced twice (source, slide 9)

$x=\sin2t$, $y=\cos2t$, $0\le t\le2\pi$. Again $x^2+y^2=\sin^22t+\cos^22t=1$, the same unit circle. But now, as $t$ increases from $0$ to $2\pi$, the point starts at $(0,1)$ and goes around the circle **twice**, in the **clockwise** direction.

N.B Two different parametrizations traced out the identical set of points here, only the starting point, direction, and number of times around differ. This matters: a curve's *shape* and its *parametrization* are genuinely different pieces of information, and this exact pair of examples is reused in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: arc length of the unit circle, two parametrizations (source, slides 20 to 21)|S16's arc length section]] to show why the distinction matters for calculus done on the curve.

## Worked example: the cycloid (source, slides 10 to 12)

**Definition.** A **cycloid** is the curve traced by a point $P$ on the circumference of a circle as the circle rolls along a straight line.

**Setting up parametric equations.** Let a circle of radius $r$ roll along the $x$-axis, with $P$ at the origin when the rotation angle $\theta=0$. Take $\theta$ (the angle the circle has rotated through) as the parameter. Since the circle has rolled without slipping, the distance rolled equals the arc length in contact with the line:

$$
|OT|=\text{arc }PT=r\theta,
$$

so the circle's center is $C(r\theta,r)$. Reading the coordinates of $P=(x,y)$ off the rolling-circle diagram,

$$
x=|OT|-|PQ|=r\theta-r\sin\theta=r(\theta-\sin\theta),
$$
$$
y=|TC|-|QC|=r-r\cos\theta=r(1-\cos\theta).
$$

**Parametric equations for the cycloid:**

$$
x=r(\theta-\sin\theta),\qquad y=r(1-\cos\theta),\qquad\theta\in\mathbb R.
$$

One full arch (one complete rotation of the circle) corresponds to $0\le\theta\le2\pi$. The derivation above was carried out for $0<\theta<\pi/2$, but the resulting equations are valid for every value of $\theta$.

```desmos-graph
left=-1; right=14;
top=3; bottom=-0.5;
---
(t-\sin(t),1-\cos(t))\left\{0\le t\le4\pi\right\}
```

## See also
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations]] (tangents, area, arc length, surface area for these curves)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
