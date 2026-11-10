---
module: MAT01B1
topic: Area of a Surface of Revolution
session: S12
tags: [definition, formula, worked-example]
---

# Area of a Surface of Revolution

Source: Dr K, §8.2 Area of a Surface of Revolution (slides 1 to 21), plus the one-page handout "Applications of Calculus, Surface Area" (MAT01B1/MAT1B01).

## The idea in one picture

Take a tiny piece of the curve, of length $ds$ (see [[MAT01B1_Notes_S11_ArcLength#The idea in one picture]]). Spin it about the axis and it sweeps a thin band, like a label wrapped round a tin. Unroll the band: a thin rectangle as long as the circle the piece travels round, $2\pi\cdot(\text{radius})$, and as wide as the piece is long, $ds$. Its area is $2\pi\,r\,ds$, and adding up all the bands gives

$$
S=\int2\pi\,r\,ds.
$$

The radius $r$ is the distance from the piece of curve to the axis: $y$ for the $x$-axis, $x$ for the $y$-axis, and things like $2-x$ or $y+1$ for other lines. It is the same "radius is a distance" rule as for volumes (see [[MAT01B1_Notes_S8_Volumes#Strips, and why they become disks, washers or shells]]). Every formula below, including the four cases in the table, is this one formula with $ds$ written in terms of $dx$ or $dy$ and $r$ read off the picture. The sections that follow do it carefully: each band is really a slice of a cone (a frustum), and a limit removes the approximation.

## Simple surfaces (source, slides 2 to 3)

When a curve is rotated about an axis it generates a **surface of revolution**. Two simple surfaces fix the starting formulas.

**Cylinder.** The lateral surface area of a circular cylinder with radius $r$ and height $h$ is taken to be

$$
A=2\pi rh,
$$

because cutting the cylinder and unrolling it gives a rectangle with dimensions $2\pi r$ and $h$.

**Cone.** Take a circular cone with base radius $r$ and slant height $\ell$, cut it along a line running to the apex, and flatten it. The result is a sector of a circle with radius $\ell$ and central angle $\theta=\dfrac{2\pi r}{\ell}$. The area of a sector of radius $\ell$ and angle $\theta$ is $\tfrac12\ell^2\theta$, so

$$
A=\frac12\ell^2\left(\frac{2\pi r}{\ell}\right)=\pi r\ell.
$$

**Definition.** The lateral surface area of a cone is $A=\pi r\ell$.

## The band (frustum) formula (source, slides 4 to 6)

For a more complicated surface, follow the strategy used for arc length ([[MAT01B1_Notes_S11_ArcLength]]): approximate the curve by a polygon. Rotating the polygon about the axis gives a simpler surface made of a number of **bands**, each formed by rotating one line segment. Each band is a portion of a cone (a frustum), so its area can be found, and taking a limit gives the exact surface area.

A band with slant height $\ell$ and upper and lower radii $r_1$ and $r_2$ has area found by subtracting the areas of two cones. If $\ell_1$ is the slant height of the smaller (removed) cone,

$$
A=\pi r_2(\ell_1+\ell)-\pi r_1\ell_1=\pi\big[(r_2-r_1)\ell_1+r_2\ell\big].\qquad(1)
$$

Similar triangles give $\dfrac{\ell_1}{r_1}=\dfrac{\ell_1+\ell}{r_2}$, so $r_2\ell_1=r_1\ell_1+r_1\ell$, that is, $(r_2-r_1)\ell_1=r_1\ell$. Putting this into (1),

$$
A=\pi(r_1\ell+r_2\ell)\quad\text{or}\quad A=2\pi r\ell,\qquad(2)
$$

where $r=\tfrac12(r_1+r_2)$ is the **average radius** of the band.

N.B The band area is "circumference at the average radius times slant height", $2\pi r\cdot\ell$, exactly the way the cylinder formula is circumference times height. That is why the average radius appears.

## Building the surface area formula (source, slides 7 to 10)

Consider the surface obtained by rotating the curve $y=f(x)$, $a\le x\le b$, about the $x$-axis, where $f$ is positive and has a continuous derivative. Divide $[a,b]$ into $n$ subintervals with endpoints $x_0,\dots,x_n$ and equal width $\Delta x$, as for arc length. With $y_i=f(x_i)$, the point $P_i(x_i,y_i)$ lies on the curve. The part of the surface between $x_{i-1}$ and $x_i$ is approximated by rotating the segment $P_{i-1}P_i$ about the $x$-axis.

The result is a band with slant height $\ell=|P_{i-1}P_i|$ and average radius $r=\tfrac12(y_{i-1}+y_i)$, so by (2) its area is

$$
2\pi\,\frac{y_{i-1}+y_i}{2}\,\big|P_{i-1}P_i\big|.
$$

As in the derivation of the [[MAT01B1_Notes_S11_ArcLength#The Arc Length Formula (source, slides 7 to 9)|Arc Length Formula]],

$$
\big|P_{i-1}P_i\big|=\sqrt{1+\big[f'(x_i^*)\big]^2}\,\Delta x
$$

for some $x_i^*$ in $[x_{i-1},x_i]$. When $\Delta x$ is small, $y_i=f(x_i)\approx f(x_i^*)$ and $y_{i-1}=f(x_{i-1})\approx f(x_i^*)$, since $f$ is continuous. Therefore

$$
2\pi\,\frac{y_{i-1}+y_i}{2}\,\big|P_{i-1}P_i\big|\approx2\pi f(x_i^*)\sqrt{1+\big[f'(x_i^*)\big]^2}\,\Delta x,
$$

and an approximation to the whole surface is

$$
\sum_{i=1}^n2\pi f(x_i^*)\sqrt{1+\big[f'(x_i^*)\big]^2}\,\Delta x.\qquad(3)
$$

The approximation improves as $n\to\infty$. Sum (3) is a Riemann sum for $g(x)=2\pi f(x)\sqrt{1+[f'(x)]^2}$, so its limit is an integral.

**Definition.** For $f$ positive with a continuous derivative, the surface area of the surface obtained by rotating $y=f(x)$, $a\le x\le b$, about the $x$-axis is

$$
S=\int_a^b2\pi f(x)\sqrt{1+\big[f'(x)\big]^2}\,dx.\qquad(4)
$$

**Hypotheses**
- $f(x)>0$ on $[a,b]$ (the curve stays above the axis of rotation)
- $f'$ continuous on $[a,b]$

## The formulas in Leibniz notation and $ds$ form (source, slides 11 to 13)

In Leibniz notation, (4) becomes

$$
S=\int_a^b2\pi y\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx.\qquad(5)
$$

If the curve is described as $x=g(y)$, $c\le y\le d$, then for rotation about the $x$-axis

$$
S=\int_c^d2\pi y\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy.\qquad(6)
$$

Using the differential arc length $ds$ from [[MAT01B1_Notes_S11_ArcLength#Differential arc length (source, slide 18)|Differential arc length]], both (5) and (6) collapse to

$$
S=\int2\pi y\,ds\qquad(7)
$$

and for rotation about the $y$-axis

$$
S=\int2\pi x\,ds,\qquad(8)
$$

where, as before, $ds$ is either $\sqrt{1+\left(\dfrac{dy}{dx}\right)^2}\,dx$ or $\sqrt{1+\left(\dfrac{dx}{dy}\right)^2}\,dy$, whichever matches the variable being integrated.

N.B The memory device is that $2\pi y$ (about the $x$-axis) or $2\pi x$ (about the $y$-axis) is the circumference of the circle traced out by the point $(x,y)$ on the curve as it rotates. The radius of that circle is the distance from the point to the axis of rotation.

## The four cases (source: handout)

The handout lists every combination of axis and curve description:

| Axis of rotation | Curve | Surface area |
|---|---|---|
| $x$-axis | $y=f(x)$, $a\le x\le b$ | $\displaystyle S=\int_a^b2\pi f(x)\sqrt{1+[f'(x)]^2}\,dx=\int_a^b2\pi y\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx$ |
| $x$-axis | $x=g(y)$, $c\le y\le d$ | $\displaystyle S=\int_c^d2\pi y\sqrt{1+[g'(y)]^2}\,dy=\int_c^d2\pi y\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy$ |
| $y$-axis | $y=f(x)$, $a\le x\le b$ | $\displaystyle S=\int_a^b2\pi x\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx$ |
| $y$-axis | $x=g(y)$, $c\le y\le d$ | $\displaystyle S=\int_c^d2\pi g(y)\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy$ |

N.B In the last row the radius is $x=g(y)$, so the factor $2\pi g(y)$ replaces $2\pi y$. The handout is where the four combinations are all in one place.

## Worked example: a portion of a sphere (source, slides 14 to 16)

The curve $y=\sqrt{4-x^2}$, $-1\le x\le1$, is an arc of a circle. Find the area of the surface obtained by rotating it about the $x$-axis. (The surface is a portion of a sphere of radius $2$.)

$$
\frac{dy}{dx}=\frac12(4-x^2)^{-1/2}(-2x)=-\frac{x}{\sqrt{4-x^2}}.
$$

By (5),

$$
S=2\pi\int_{-1}^{1}\sqrt{4-x^2}\sqrt{1+\frac{x^2}{4-x^2}}\,dx=2\pi\int_{-1}^{1}\sqrt{4-x^2}\sqrt{\frac{4-x^2+x^2}{4-x^2}}\,dx=2\pi\int_{-1}^{1}\sqrt{4-x^2}\cdot\frac{2}{\sqrt{4-x^2}}\,dx.
$$

The square roots cancel:

$$
S=4\pi\int_{-1}^{1}1\,dx=4\pi(2)=8\pi.
$$

(added, sanity check) A zone of a sphere of radius $R$ cut by two parallel planes a distance $h$ apart has area $2\pi Rh$. Here $R=2$ and the planes $x=-1$ and $x=1$ are $h=2$ apart, so $2\pi(2)(2)=8\pi$, matching.

## Worked example: a parabola about the y-axis, two ways (source, slides 17 to 19)

The arc of $y=x^2$ from $(1,1)$ to $(2,4)$ is rotated about the $y$-axis. Find the area of the resulting surface.

**In $x$, using (8).** $\dfrac{dy}{dx}=2x$, so

$$
S=\int2\pi x\,ds=\int_1^22\pi x\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx=2\pi\int_1^2x\sqrt{1+4x^2}\,dx.
$$

Substitute $u=1+4x^2$, so $du=8x\,dx$, and change the limits ($x=1\Rightarrow u=5$, $x=2\Rightarrow u=17$):

$$
S=2\pi\int_5^{17}\sqrt u\cdot\frac18\,du=\frac\pi4\int_5^{17}u^{1/2}\,du=\frac\pi4\left[\frac23u^{3/2}\right]_5^{17}=\frac\pi6\left(17\sqrt{17}-5\sqrt5\right).
$$

**In $y$ (alternative solution).** Solve for $x=\sqrt y$, so $\dfrac{dx}{dy}=\dfrac{1}{2\sqrt y}$, and use (8) with the $dy$ form of $ds$:

$$
S=\int_1^42\pi x\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy=2\pi\int_1^4\sqrt y\sqrt{1+\frac{1}{4y}}\,dy=2\pi\int_1^4\sqrt{y+\frac14}\,dy=\pi\int_1^4\sqrt{4y+1}\,dy.
$$

With $u=1+4y$ ($y=1\Rightarrow u=5$, $y=4\Rightarrow u=17$), $\pi\displaystyle\int_1^4\sqrt{4y+1}\,dy=\frac\pi4\int_5^{17}\sqrt u\,du=\frac\pi6\left(17\sqrt{17}-5\sqrt5\right)$, the same value.

N.B Both routes reach $\tfrac\pi6(17\sqrt{17}-5\sqrt5)$. Choose the variable that gives the easier integral, and take the radius factor ($2\pi x$ here) from the axis of rotation, not from the variable you integrate in.

## Worked example: $y=e^x$ about the x-axis (source, slides 20 to 21)

Find the area of the surface generated by rotating $y=e^x$, $0\le x\le1$, about the $x$-axis. With $\dfrac{dy}{dx}=e^x$, (5) gives

$$
S=\int_0^12\pi y\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx=2\pi\int_0^1e^x\sqrt{1+e^{2x}}\,dx.
$$

Substitute $u=e^x$, so $du=e^x\,dx$ ($x=0\Rightarrow u=1$, $x=1\Rightarrow u=e$):

$$
S=2\pi\int_1^e\sqrt{1+u^2}\,du.
$$

Now a tangent substitution ([[MAT01B1_Notes_S2_DerivativeIntegralReference#Trig substitutions|Trig substitutions]]): $u=\tan\theta$, with $u=1\Rightarrow\theta=\tfrac\pi4$ and $u=e\Rightarrow\theta=\alpha=\tan^{-1}e$. Then $\sqrt{1+u^2}=\sec\theta$ and $du=\sec^2\theta\,d\theta$, so

$$
S=2\pi\int_{\pi/4}^{\alpha}\sec^3\theta\,d\theta=2\pi\cdot\frac12\Big[\sec\theta\tan\theta+\ln|\sec\theta+\tan\theta|\Big]_{\pi/4}^{\alpha}.
$$

Evaluating (at $\theta=\tfrac\pi4$, $\sec\theta=\sqrt2$ and $\tan\theta=1$),

$$
S=\pi\Big[\sec\alpha\tan\alpha+\ln(\sec\alpha+\tan\alpha)-\sqrt2-\ln\big(\sqrt2+1\big)\Big].
$$

Since $\tan\alpha=e$, $\sec^2\alpha=1+\tan^2\alpha=1+e^2$, so

$$
S=\pi\Big[e\sqrt{1+e^2}+\ln\big(e+\sqrt{1+e^2}\big)-\sqrt2-\ln\big(\sqrt2+1\big)\Big].
$$

The $\int\sec^3\theta\,d\theta$ value is the same one used in [[MAT01B1_Notes_S11_ArcLength#Worked example: parabola, trigonometric substitution (source, slides 14 to 15)|the arc length of a parabola]], from the table in [[MAT01B1_Notes_S2_DerivativeIntegralReference]].

## See also
- [[MAT01B1_Notes_S11_ArcLength]] (the arc length formula and $ds$ that this section builds on)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Surface area]] (the same surface area for a curve given parametrically, including the sphere of radius $r$)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (trig substitution and the $\sec^3$ integral)
- [[MAT01B1_Notes_S8_Volumes]], [[MAT01B1_Notes_S9_CylindricalShells]] (the other applications of rotating a curve or region about an axis)
