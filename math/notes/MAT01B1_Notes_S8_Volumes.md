---
module: MAT01B1
topic: Volumes
session: S8
tags: [definition, formula, worked-example]
---

# Volumes

Source: Dr K, §6.2 Volumes (slides 1 to 34).

## From cylinders to arbitrary solids

A (right) cylinder is a solid swept out by a plane region (the base, area $A$) moved a distance $h$ perpendicular to itself; its volume is simply $V=Ah$. A circular cylinder ($V=\pi r^2h$) and a rectangular box ($V=lwh$) are the two special cases used constantly below.

For a solid $S$ that isn't a cylinder, slice it with planes perpendicular to the $x$-axis. Each slice through the point $x$ has some cross-sectional area $A(x)$, and dividing $S$ into $n$ thin slabs of width $\Delta x$, the $i$th slab is approximated by a cylinder of base area $A(x_i^*)$ and height $\Delta x$, giving $V(S_i)\approx A(x_i^*)\Delta x$. Summing over all slabs and letting $n\to\infty$ turns the Riemann sum into a definite integral, exactly the same limiting argument used for area under a curve (Chapter 5) and area between curves ([[MAT01B1_Notes_S7_AreaBetweenCurves]]).

## Definition of Volume (source, slide 8)

**Definition.** Let $S$ be a solid that lies between $x=a$ and $x=b$. If the cross-sectional area of $S$ in the plane $P_x$, through $x$ and perpendicular to the $x$-axis, is $A(x)$, where $A$ is a continuous function, then the volume of $S$ is

$$
V=\lim_{n\to\infty}\sum_{i=1}^n A(x_i^*)\Delta x=\int_a^b A(x)\,dx.
$$

**Hypotheses**
- $S$ lies between $x=a$ and $x=b$
- $A(x)$, the cross-sectional area at $x$, is a continuous function of $x$

When using $V=\int_a^b A(x)\,dx$, $A(x)$ is the area of a *moving* cross-section, re-measured at each $x$, not a fixed shape.

## Finding $A(x)$ for a solid of revolution

Solids of revolution (obtained by rotating a plane region about a line) are the main application. The cross-sectional area is found one of two ways:

- **Disk.** If a cross-section is a full disk, find its radius (in terms of $x$ or $y$) and use $A=\pi(\text{radius})^2$.
- **Washer.** If a cross-section is an annular ring (a disk with a hole), find the inner radius $r_{\text{in}}$ and outer radius $r_{\text{out}}$ from a sketch and use $A=\pi(\text{outer radius})^2-\pi(\text{inner radius})^2$.

N.B Which axis a solid is rotated about decides which variable to slice perpendicular to, and therefore whether $V=\int_a^b A(x)\,dx$ or $V=\int_c^d A(y)\,dy$ is the one that actually has a continuous, easy-to-write $A$.

## Worked example: volume of a sphere (source, slides 9 to 10)

Show $V=\dfrac43\pi r^3$ for a sphere of radius $r$. Centering the sphere at the origin, the plane $P_x$ cuts it in a disk of radius $y=\sqrt{r^2-x^2}$ (Pythagoras), so $A(x)=\pi(r^2-x^2)$.

$$
V=\int_{-r}^{r}\pi(r^2-x^2)\,dx=2\pi\int_0^r(r^2-x^2)\,dx=2\pi\left[r^2x-\frac{x^3}{3}\right]_0^r=\frac43\pi r^3.
$$

## Worked example: disk method, rotating about the $x$-axis (source, slides 13 to 14)

Rotate the region under $y=\sqrt x$ from $x=0$ to $x=1$ about the $x$-axis. Each slice is a disk of radius $\sqrt x$, so $A(x)=\pi x$.

$$
V=\int_0^1\pi x\,dx=\pi\left[\frac{x^2}{2}\right]_0^1=\frac{\pi}{2}.
$$

## Worked example: disk method, rotating about the $y$-axis (source, slides 15 to 16)

Rotate the region bounded by $y=x^3$, $y=8$, $x=0$ about the $y$-axis. Slicing perpendicular to the $y$-axis, a disk at height $y$ has radius $x=\sqrt[3]y$, so $A(y)=\pi y^{2/3}$.

$$
V=\int_0^8\pi y^{2/3}\,dy=\pi\left[\frac35 y^{5/3}\right]_0^8=\frac{96\pi}{5}.
$$

## Worked example: washer method (source, slides 17 to 18)

Region enclosed by $y=x$ and $y=x^2$ (intersecting at $(0,0)$ and $(1,1)$), rotated about the $x$-axis. Each cross-section is a washer with outer radius $x$, inner radius $x^2$:

$$
A(x)=\pi x^2-\pi(x^2)^2=\pi(x^2-x^4),\qquad V=\int_0^1\pi(x^2-x^4)\,dx=\pi\left[\frac{x^3}{3}-\frac{x^5}{5}\right]_0^1=\frac{2\pi}{15}.
$$

## Worked example: washer method, axis shifted off the boundary (source, slides 19 to 20)

Same region ($y=x$, $y=x^2$), now rotated about $y=2$ instead of the $x$-axis. The distances to the axis change: outer radius $2-x^2$, inner radius $2-x$.

$$
A(x)=\pi(2-x^2)^2-\pi(2-x)^2,\qquad V=\pi\int_0^1(x^4-5x^2+4x)\,dx=\pi\left[\frac{x^5}{5}-\frac{5x^3}{3}+2x^2\right]_0^1=\frac{8\pi}{15}.
$$

N.B Shifting the axis of rotation off the region's own boundary doesn't change the method, only the expressions for the inner and outer radii; both are measured as distance to the *new* axis, not to $y=0$.

## Worked example: washer method, rotating about a vertical line, sliced in $y$ (source, slides 24 to 26)

Same region again, rotated about $x=-1$. This time a horizontal slice (perpendicular to the axis of rotation, so perpendicular to $x=-1$, meaning the natural variable is $y$) is a washer with inner radius $1+y$ and outer radius $1+\sqrt y$:

$$
A(y)=\pi(1+\sqrt y)^2-\pi(1+y)^2,\qquad V=\pi\int_0^1\big(2\sqrt y-y-y^2\big)\,dy=\pi\left[\frac{4y^{3/2}}{3}-\frac{y^2}{2}-\frac{y^3}{3}\right]_0^1=\frac{\pi}{2}.
$$

## Worked example: non-circular cross-sections, equilateral triangles (source, slides 27 to 29)

A solid has a circular base of radius 1 ($x^2+y^2=1$); cross-sections perpendicular to the base are equilateral triangles. At distance $x$ from the origin, the base of the triangle is a chord of the circle, $|AB|=2y=2\sqrt{1-x^2}$, and since the triangle is equilateral its height is $\sqrt3\,y=\sqrt3\sqrt{1-x^2}$.

$$
A(x)=\frac12\big(2\sqrt{1-x^2}\big)\big(\sqrt3\sqrt{1-x^2}\big)=\sqrt3(1-x^2).
$$

$$
V=\int_{-1}^{1}\sqrt3(1-x^2)\,dx=2\sqrt3\int_0^1(1-x^2)\,dx=2\sqrt3\left[x-\frac{x^3}{3}\right]_0^1=\frac{4\sqrt3}{3}.
$$

N.B The cross-sections here aren't disks or washers at all, the "slice, find $A(x)$, integrate" method from the Definition of Volume applies regardless of the cross-section's shape; disks and washers are just the shape that shows up for solids of revolution specifically.

## Worked example: pyramid with a square base (source, slides 30 to 31)

Pyramid, square base of side $L$, height $h$, apex at the origin with the $x$-axis along the central axis. By similar triangles, a cross-section at distance $x$ from the apex is a square of side $s=Lx/h$.

$$
A(x)=s^2=\frac{L^2}{h^2}x^2,\qquad V=\int_0^h\frac{L^2}{h^2}x^2\,dx=\frac{L^2}{h^2}\left[\frac{x^3}{3}\right]_0^h=\frac{L^2h}{3}.
$$

## Worked example: wedge cut from a cylinder (source, slides 32 to 34)

A wedge is cut from a circular cylinder of radius 4 by a plane perpendicular to the cylinder's axis and a second plane meeting the first at $30°$ along a diameter. Placing the $x$-axis along that diameter, the base is a semicircle $y=\sqrt{16-x^2}$, $-4\le x\le4$. A cross-section perpendicular to the $x$-axis is a right triangle with base $y=\sqrt{16-x^2}$ and height $|BC|=y\tan30°=\sqrt{16-x^2}/\sqrt3$.

$$
A(x)=\frac12\sqrt{16-x^2}\cdot\frac{\sqrt{16-x^2}}{\sqrt3}=\frac{16-x^2}{2\sqrt3}.
$$

$$
V=\int_{-4}^{4}\frac{16-x^2}{2\sqrt3}\,dx=\frac{1}{\sqrt3}\int_0^4(16-x^2)\,dx=\frac{1}{\sqrt3}\left[16x-\frac{x^3}{3}\right]_0^4=\frac{128}{3\sqrt3}.
$$

## See also
- [[MAT01B1_Notes_S7_AreaBetweenCurves]]
- [[MAT01B1_Notes_S9_CylindricalShells]] (an alternative method for the same solids of revolution)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (antiderivative formulas used throughout)
