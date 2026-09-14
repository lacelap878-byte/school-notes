---
module: MAT01B1
topic: Volumes - Cylindrical Shells
session: S9
tags: [formula, worked-example]
---

# Volumes: Cylindrical Shells

Source: Dr K, §6.3 Volumes - Cylindrical shells (slides 1 to 22).

## Motivation (source, slides 2 to 3)

Consider rotating about the $y$-axis the region bounded by $y=2x^2-x^3$ and $y=0$. Slicing perpendicular to the $y$-axis gives washers, but finding their inner and outer radii means solving the cubic $y=2x^2-x^3$ for $x$ in terms of $y$, which is not easy. The **method of cylindrical shells** avoids this entirely by slicing *parallel* to the axis of rotation instead of perpendicular to it.

## Volume of a single shell (source, slides 3 to 5)

A cylindrical shell with inner radius $r_1$, outer radius $r_2$, and height $h$ has volume equal to the outer cylinder's volume minus the inner cylinder's:

$$
V=\pi r_2^2h-\pi r_1^2h=\pi(r_2^2-r_1^2)h=\pi(r_2+r_1)(r_2-r_1)h=2\pi\left(\frac{r_2+r_1}{2}\right)h(r_2-r_1).
$$

Writing $\Delta r=r_2-r_1$ (the shell's thickness) and $r=\tfrac12(r_2+r_1)$ (its average radius),

$$
V=2\pi r h\,\Delta r,
$$

remembered as $V=[\text{circumference}][\text{height}][\text{thickness}]$.

## Building the volume formula (source, slides 6 to 10)

Let $S$ be the solid from rotating about the $y$-axis the region bounded by $y=f(x)$ (with $f(x)\ge0$), $y=0$, $x=a$, $x=b$, where $b>a\ge0$. Dividing $[a,b]$ into $n$ subintervals of width $\Delta x$ with midpoints $\bar x_i$: rotating the rectangle over $[x_{i-1},x_i]$ with height $f(\bar x_i)$ produces a shell of average radius $\bar x_i$, height $f(\bar x_i)$, thickness $\Delta x$, so by the single-shell formula its volume is $V_i=2\pi\bar x_if(\bar x_i)\Delta x$. Summing and letting $n\to\infty$,

$$
V\approx\sum_{i=1}^n2\pi\bar x_if(\bar x_i)\Delta x\;\longrightarrow\;\int_a^b2\pi xf(x)\,dx.
$$

**Formula.** The volume of the solid obtained by rotating about the $y$-axis the region under $y=f(x)$ from $x=a$ to $x=b$ (with $0\le a<b$) is

$$
V=\int_a^b2\pi xf(x)\,dx.
$$

**Hypotheses**
- $f(x)\ge0$ on $[a,b]$
- $0\le a<b$

The formula is easiest to remember by picturing a single shell cut open and flattened out into a thin slab: radius $x$, circumference $2\pi x$, height $f(x)$, thickness $dx$,

$$
\int_a^b\underbrace{(2\pi x)}_{\text{circumference}}\underbrace{[f(x)]}_{\text{height}}\underbrace{dx}_{\text{thickness}}.
$$

This same reasoning (circumference times height times thickness) carries over directly to rotations about other lines, not just the $y$-axis, by re-reading "radius" and "height" off a diagram each time.

## Worked example: the motivating region, resolved with shells (source, slides 11 to 14)

Rotate about the $y$-axis the region bounded by $y=2x^2-x^3$, $y=0$. A typical shell has radius $x$, circumference $2\pi x$, height $f(x)=2x^2-x^3$.

$$
V=\int_0^2(2\pi x)(2x^2-x^3)\,dx=2\pi\int_0^2(2x^3-x^4)\,dx=2\pi\left[\frac{x^4}{2}-\frac{x^5}{5}\right]_0^2=\frac{16\pi}{5}.
$$

(source note) Comparing this with the motivation above: the shell method avoided both finding the local maximum and solving the cubic for $x$ in terms of $y$, which is exactly what made the washer method hard here. In other problems, though, the washer/disk method from [[MAT01B1_Notes_S8_Volumes]] can be the easier one, see the next example.

## Worked example: region between $y=x$ and $y=x^2$, about the $y$-axis (source, slides 15 to 16)

Shell radius $x$, circumference $2\pi x$, height $x-x^2$.

$$
V=\int_0^1(2\pi x)(x-x^2)\,dx=2\pi\int_0^1(x^2-x^3)\,dx=2\pi\left[\frac{x^3}{3}-\frac{x^4}{4}\right]_0^1=\frac{\pi}{6}.
$$

N.B This is the same two curves as the washer example in [[MAT01B1_Notes_S8_Volumes#Worked example: washer method]], but rotated about the $y$-axis here instead of the $x$-axis, so the two results ($\pi/6$ here versus $2\pi/15$ there) are not meant to match, they're different solids.

## Worked example: disk vs. shell for the same solid (source, slides 17 to 18)

Rotate about the $x$-axis the region under $y=\sqrt x$ from $0$ to $1$, this time with shells. Relabelling the curve as $x=y^2$, a shell (parallel to the $x$-axis, so built from $y$) has radius $y$, circumference $2\pi y$, height $1-y^2$.

$$
V=\int_0^1(2\pi y)(1-y^2)\,dy=2\pi\int_0^1(y-y^3)\,dy=2\pi\left[\frac{y^2}{2}-\frac{y^4}{4}\right]_0^1=\frac{\pi}{2}.
$$

Same answer as [[MAT01B1_Notes_S8_Volumes#Worked example: disk method, rotating about the $x$-axis]], which used the disk method on the identical solid. (source note) In this particular problem, the disk method was simpler, the shell method isn't automatically the better choice, it's a tool for when slicing perpendicular to the axis is the hard direction.

## Worked example: shells about a vertical line other than the axis (source, slides 19 to 20)

Rotate about the line $x=2$ the region bounded by $y=x-x^2$ and $y=0$. A shell now has radius $2-x$ (distance to the new axis), circumference $2\pi(2-x)$, height $x-x^2$.

$$
V=\int_0^1 2\pi(2-x)(x-x^2)\,dx=2\pi\int_0^1(x^3-3x^2+2x)\,dx=2\pi\left[\frac{x^4}{4}-x^3+x^2\right]_0^1=\frac{\pi}{2}.
$$

## Disks/washers vs cylindrical shells (source, slides 21 to 22)

Choosing a method comes down to which variable the region's boundaries are naturally written in terms of:

- Is the region more easily described by top/bottom boundaries $y=f(x)$, or by left/right boundaries $x=g(y)$?
- Which choice gives easier limits of integration? Does one variable need two separate integrals while the other needs only one?
- Can the resulting integral actually be evaluated with the chosen variable?

Practically: draw a sample rectangle in the region. Its thickness ($\Delta x$ or $\Delta y$) is the integration variable. Revolving that rectangle about the axis of rotation turns it into either a disk/washer (rectangle perpendicular to the axis) or a shell (rectangle parallel to the axis).

## See also
- [[MAT01B1_Notes_S8_Volumes]]
- [[MAT01B1_Notes_S7_AreaBetweenCurves]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (antiderivative formulas used throughout)
