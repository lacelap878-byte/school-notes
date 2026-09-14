---
module: MAT01B1
topic: Polar Coordinates
session: S15
tags: [definition, formula, worked-example]
---

# Polar Coordinates

Source: Dr K, §10.3 Polar Coordinates (slides 1 to 19).

## Polar coordinates

A coordinate system represents a point by an ordered pair of numbers. Cartesian coordinates use directed distances from two perpendicular axes, and every point corresponds to a unique pair $(x,y)$.

**Definition.** Fix a point $O$ (the **pole**) and a ray from $O$ (the **polar axis**). For any point $P$, let $r$ be the distance from $O$ to $P$ and $\theta$ the angle (usually in radians) between the polar axis and $OP$, measured positive counterclockwise, negative clockwise. Then $P$ is represented by the ordered pair $(r,\theta)$, its **polar coordinates**. If $P=O$, then $r=0$ and $(0,\theta)$ represents the pole for *every* value of $\theta$.

**Negative $r$.** Extend the meaning of $(r,\theta)$ to negative $r$ by agreeing that $(-r,\theta)$ and $(r,\theta)$ lie on the same line through $O$, at the same distance $|r|$ from $O$, but on opposite sides of $O$. If $r>0$, $(r,\theta)$ lies in the same quadrant as $\theta$; if $r<0$, the opposite quadrant. Consequently $(r,\theta)$ and $(r,\theta+\pi)$ represent the same point.

## Worked example: plotting points (source, slide 5)

Plot $(1,5\pi/4)$, $(2,3\pi)$, $(2,-2\pi/3)$, $(-3,3\pi/4)$. For the last one: the angle $3\pi/4$ points into the second quadrant, but $r=-3$ is negative, so the point $(-3,3\pi/4)$ actually lies three units from the pole in the **fourth** quadrant, on the opposite side of $O$ from where the angle points.

## Multiple representations

Unlike Cartesian coordinates, every point in the polar system has infinitely many representations. Since a full counterclockwise rotation is $2\pi$, the point $(r,\theta)$ is also represented by

$$
(r,\theta+2n\pi)\qquad\text{and}\qquad(-r,\theta+(2n+1)\pi)\qquad\text{for any integer }n.
$$

For instance, $(1,5\pi/4)$ can equally be written $(1,-3\pi/4)$, $(1,13\pi/4)$, or $(-1,\pi/4)$.

## Converting between polar and Cartesian

With the pole at the Cartesian origin and the polar axis along the positive $x$-axis, a point with Cartesian coordinates $(x,y)$ and polar coordinates $(r,\theta)$ satisfies $\cos\theta=x/r$, $\sin\theta=y/r$, so

$$
x=r\cos\theta,\qquad y=r\sin\theta.
$$

These were read off a diagram for $r>0$, $0<\theta<\pi/2$, but hold for *all* values of $r$ and $\theta$.

To go the other way (find $r,\theta$ from $x,y$):

$$
r^2=x^2+y^2,\qquad \tan\theta=\frac{y}{x}\ (x\ne0).
$$

N.B These equations don't uniquely determine $\theta$ from $x,y$: as $\theta$ ranges over $0\le\theta<2\pi$, each value of $\tan\theta$ occurs twice (once in each of two opposite quadrants). Converting Cartesian to polar therefore also requires checking which quadrant $(x,y)$ is actually in, not just solving the equations.

## Worked example: polar to Cartesian (source, slide 10)

Convert $(2,\pi/3)$. $x=2\cos(\pi/3)=1$, $y=2\sin(\pi/3)=\sqrt3$. Cartesian point: $(1,\sqrt3)$.

## Worked example: Cartesian to polar (source, slide 11)

Represent $(1,-1)$ in polar coordinates. Taking $r>0$: $r=\sqrt{1^2+(-1)^2}=\sqrt2$, $\tan\theta=-1$. Since $(1,-1)$ is in the fourth quadrant, $\theta=-\pi/4$ (or equivalently $7\pi/4$). So $(\sqrt2,-\pi/4)$ or $(\sqrt2,7\pi/4)$ are both valid answers, consistent with the multiple-representations rule above.

## Polar curves

**Definition.** The graph of a polar equation $r=f(\theta)$ (or more generally $F(r,\theta)=0$) consists of every point that has at least one polar representation $(r,\theta)$ satisfying the equation.

## Worked example: $r=2$ (source, slide 13)

All points at distance $2$ from the pole, i.e. the circle centered at $O$ with radius $2$. In general, $r=a$ represents a circle centered at $O$ with radius $|a|$.

## Worked example: $\theta=1$ (source, slide 14)

All points with polar angle exactly $1$ radian: the straight line through $O$ making angle $1$ with the polar axis. Points $(r,1)$ with $r>0$ lie in the first quadrant; those with $r<0$ lie in the third quadrant (opposite side of $O$).

## Worked example: $r=2\cos\theta$ (source, slides 15 to 17)

**(a) Sketch.** Tabulating $r$ for $\theta$ from $0$ to $\pi$ and plotting suggests a circle; values of $\theta$ beyond $\pi$ retrace the same points.

**(b) Cartesian equation.** From $x=r\cos\theta$, $\cos\theta=x/r$, so $r=2\cos\theta$ becomes $r=2x/r$, giving $2x=r^2=x^2+y^2$, i.e. $x^2+y^2-2x=0$. Completing the square:

$$
(x-1)^2+y^2=1,
$$

a circle centered at $(1,0)$ with radius $1$.

## Worked example: $r=\cos2\theta$, the four-leaved rose (source, slides 18 to 19)

(source note) The slides describe this by first sketching $r=\cos2\theta$ as an ordinary Cartesian graph (with $\theta$ on the horizontal axis and $r$ on the vertical), the way "Example 7" is said to have done just before it, though that particular example's own content isn't included in these slides. Reading that Cartesian graph tells you how $r$ behaves in each interval of $\theta$, which is then converted into the polar picture piece by piece:

As $\theta$ increases from $0$ to $\pi/4$, $r$ decreases from $1$ to $0$, tracing one petal in the region near the polar axis. As $\theta$ increases from $\pi/4$ to $\pi/2$, $r$ goes from $0$ back up to $1$ in magnitude, but since $r$ is negative on this stretch, that portion of the curve is drawn on the *opposite* side of the pole, in the third quadrant rather than the first. Continuing this analysis around the rest of $0\le\theta\le2\pi$ traces out the remaining petals. The resulting curve has four loops and is called a **four-leaved rose**.

## See also
- [[MAT01B1_Notes_S13_ParametricEquations]] (another way of describing curves outside the $y=f(x)$ framework)
- [[MAT01B1_Notes_S14_CalculusWithParametricEquations]]
