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

## Strips, and why they become disks, washers or shells

This is the picture behind every volume formula that follows, and behind [[MAT01B1_Notes_S9_CylindricalShells]]. It is not new calculus, it is the reason the formulas look the way they do.

**A strip is a thin rectangle inside the region, and its thickness is the integration variable.**
- A strip of thickness $dx$ is **vertical**: thin in $x$, long in $y$. Its length is (top curve) minus (bottom curve), written in terms of $x$. Laying these strips side by side runs along the $x$-axis, which is why the limits are $x$-values.
- A strip of thickness $dy$ is **horizontal**: thin in $y$, long in $x$. Its length is (right curve) minus (left curve), written in terms of $y$, and the limits are $y$-values.

Area is strip length times thickness, added up: $\int(\text{top}-\text{bottom})\,dx$ or $\int(\text{right}-\text{left})\,dy$ (see [[MAT01B1_Notes_S7_AreaBetweenCurves]]).

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.6]
\draw[->] (0,0) -- (3.4,0) node[right] {$x$};
\draw[->] (0,0) -- (0,1.9) node[above] {$y$};
\draw[thick,domain=0:3,smooth,variable=\x] plot ({\x},{sqrt(\x)});
\draw (3,0) -- (3,1.732);
\fill[blue!30] (1.0,0) rectangle (1.2,1.05);
\draw (1.0,0) rectangle (1.2,1.05);
\fill[red!30] (1.6,1.2) rectangle (3,1.35);
\draw (1.6,1.2) rectangle (3,1.35);
\node[blue] at (1.1,-0.3) {\scriptsize $dx$ strip: vertical};
\node[red] at (2.2,1.6) {\scriptsize $dy$ strip: horizontal};
\end{tikzpicture}
\end{document}
```

The region under $y=\sqrt x$, with one vertical strip (thickness $dx$) and one horizontal strip (thickness $dy$).

**Now spin the region about an axis.** Each strip spins into a solid, and which solid depends only on whether the strip lies **across** the axis or **along** it.

- **Strip perpendicular to the axis: disk or washer.** The strip's thickness is measured along the axis, so spinning it gives a thin round slab. If the strip touches the axis the slab is a solid disk, with volume $\pi R^2\cdot(\text{thickness})$. If there is a gap between the strip and the axis it is a washer (a disk with a hole), with volume $\pi(R^2-r^2)\cdot(\text{thickness})$. Here $R$ is the distance from the axis to the far end of the strip and $r$ the distance to the near end. This is exactly the cross-sectional area $A$ from the Definition of Volume, times the thickness.
- **Strip parallel to the axis: cylindrical shell.** The strip's thickness is measured across, away from the axis, so spinning it gives a thin hollow tube, like a cardboard tube. Cut it open and flatten it into a thin rectangle: length $2\pi\cdot(\text{distance from axis})$, height equal to the strip's length, and the strip's thickness. Volume $2\pi\cdot(\text{radius})\cdot(\text{height})\cdot(\text{thickness})$.

N.B "Radius" always means the distance to the axis, not a coordinate. For the axis $x=2$, a strip at $x$ has radius $2-x$. For the axis $y=-1$, a point at height $y$ has radius $y+1$. This is why moving the axis changes the radii in the examples below and changes nothing else.

**Putting the two together.** A $dx$ strip is vertical and a $dy$ strip is horizontal, so:

| Axis | $dx$ strip (vertical) | $dy$ strip (horizontal) |
|---|---|---|
| horizontal ($x$-axis or $y=k$) | across the axis: disk or washer, radii are vertical distances, functions of $x$ | along the axis: shell, radius is the vertical distance to the strip (a function of $y$), height is the strip's length in $x$ |
| vertical ($y$-axis or $x=k$) | along the axis: shell, radius is the horizontal distance to the strip (a function of $x$), height is the strip's length in $y$ | across the axis: disk or washer, radii are horizontal distances, functions of $y$ |

You get to choose the strip direction, so you get to choose the method. Pick the direction in which the region's boundaries are already written as functions (no solving for the other variable) and the radii and heights are easy to read off. The standard case is in [[MAT01B1_Notes_S9_CylindricalShells#Motivation (source, slides 2 to 3)|S9's motivating example]]: $y=2x^2-x^3$ about the $y$-axis. Horizontal strips would be washers and need $x$ as a function of $y$ (a cubic), while vertical strips are shells and need only $y=f(x)$.

**Check against the examples below.**
- $y=\sqrt x$ about the $x$-axis: a vertical strip is across the axis and touches it, so a disk of radius $\sqrt x$.
- $y=x$ and $y=x^2$ about the $x$-axis: a vertical strip is across the axis but floats above it (its bottom is at $x^2$), so a washer with $R=x$ and $r=x^2$.
- The same region about $x=-1$: a horizontal strip is across the vertical axis, so a washer, with horizontal distances $R=1+\sqrt y$ and $r=1+y$.

**The same story gives the length and surface formulas.** Cut into tiny pieces, replace each piece by something whose size is known, add up, take the limit. For arc length and surface area the tiny piece is a bit of curve (see [[MAT01B1_Notes_S11_ArcLength#The idea in one picture]] and [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution#The idea in one picture]]).

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
