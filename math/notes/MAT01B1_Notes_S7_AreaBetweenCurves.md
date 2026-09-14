---
module: MAT01B1
topic: Area Between Curves
session: S7
tags: [formula, worked-example]
---

# Area Between Curves

Source: Dr K, §6.1 Areas between curves (slides 1 to 20).

## From area under one curve to area between two

The area-under-a-curve idea from Chapter 5 extends directly: slice the region between $y=f(x)$ and $y=g(x)$ (with $f(x)\ge g(x)$ on $[a,b]$) into $n$ thin vertical strips of width $\Delta x$. Each strip is approximated by a rectangle of height $f(x_i^*)-g(x_i^*)$ rather than just $f(x_i^*)$, since the strip now sits between the two curves instead of between one curve and the axis. Summing the rectangles and letting $n\to\infty$ turns the sum into a definite integral of $f-g$.

**Formula.** If $f$ and $g$ are continuous and $f(x)\ge g(x)$ for all $x\in[a,b]$, the area of the region bounded by $y=f(x)$, $y=g(x)$, $x=a$, and $x=b$ is

$$
A=\int_a^b\big[f(x)-g(x)\big]\,dx.
$$

**Hypotheses**
- $f,g$ continuous on $[a,b]$
- $f(x)\ge g(x)$ for all $x\in[a,b]$

The special case $g(x)=0$ recovers the plain area-under-a-curve formula, and when both $f,g\ge0$ the formula is just [area under $f$] minus [area under $g$].

## When the curves cross

If $f(x)\ge g(x)$ on part of $[a,b]$ but $f(x)\le g(x)$ elsewhere, split the region at each crossing into pieces $S_1,S_2,\dots$ and add their areas. Since $|f(x)-g(x)|$ automatically picks out whichever curve is on top on each piece, the area is

$$
A=\int_a^b\big|f(x)-g(x)\big|\,dx.
$$

In practice this means: find where $f=g$, work out which curve is on top on each sub-interval, then integrate $(\text{top}-\text{bottom})$ separately over each piece and add the results, rather than trying to integrate the absolute value directly.

## Strips along $y$ instead of $x$

Some regions are more naturally bounded by curves written as $x=f(y)$ and $x=g(y)$ (left and right boundaries) than as functions of $x$. If $f(y)\ge g(y)$ for $c\le y\le d$, the same slicing argument run sideways gives

$$
A=\int_c^d\big[f(y)-g(y)\big]\,dy.
$$

N.B Whether to slice vertically ($dx$) or horizontally ($dy$) is a choice made for convenience: pick whichever way the boundary curves are already naturally written as functions, so you avoid solving for the other variable. The same "which variable is easier" judgement call comes up again, in a bigger way, when choosing between disks/washers and cylindrical shells for volumes (see: [[MAT01B1_Notes_S9_CylindricalShells#Disks/washers vs cylindrical shells]]).

## Worked example: region between $e^x$ and $x$ (source, slides 7 to 8)

Area bounded above by $y=e^x$, below by $y=x$, between $x=0$ and $x=1$.

$$
A=\int_0^1(e^x-x)\,dx=\left[e^x-\tfrac12x^2\right]_0^1=\left(e-\tfrac12\right)-1=e-1.5.
$$

## Worked example: region between two parabolas (source, slides 9 to 10)

Area enclosed by $y=x^2$ and $y=2x-x^2$. Intersections: $x^2=2x-x^2\Rightarrow 2x^2-2x=0\Rightarrow x=0,1$.

$$
A=\int_0^1\big[(2x-x^2)-x^2\big]\,dx=2\int_0^1(x-x^2)\,dx=2\left[\frac{x^2}{2}-\frac{x^3}{3}\right]_0^1=2\left(\frac12-\frac13\right)=\frac13.
$$

## Worked example: curves with no exact intersection point (source, slides 11 to 13)

Area between $y=\dfrac{x}{\sqrt{x^2+1}}$ and $y=x^4-x$. Solving for the exact intersection is not possible algebraically, so a graphing device is used to locate it numerically: one intersection is at the origin, the other at $x\approx1.18$.

$$
A\approx\int_0^{1.18}\left[\frac{x}{\sqrt{x^2+1}}-(x^4-x)\right]dx.
$$

For the first term, substitute $u=x^2+1$, $du=2x\,dx$ ($u\approx1$ to $u\approx2.39$):

$$
A\approx\frac12\int_1^{2.39}\frac{du}{\sqrt u}-\int_0^{1.18}(x^4-x)\,dx=\Big[\sqrt u\Big]_1^{2.39}-\left[\frac{x^5}{5}-\frac{x^2}{2}\right]_0^{1.18}\approx0.785.
$$

N.B This example is the reminder that "solve algebraically" isn't always available; numerical root-finding plus the same area formula still gets a (approximate) answer.

## Worked example: region between $\sin x$ and $\cos x$ (source, slides 16 to 17)

Area bounded by $y=\sin x$, $y=\cos x$, $x=0$, $x=\pi/2$. They cross at $x=\pi/4$ (the only crossing in $[0,\pi/2]$), with $\cos x\ge\sin x$ on $[0,\pi/4]$ and $\sin x\ge\cos x$ on $[\pi/4,\pi/2]$.

$$
A=\int_0^{\pi/2}|\cos x-\sin x|\,dx=\int_0^{\pi/4}(\cos x-\sin x)\,dx+\int_{\pi/4}^{\pi/2}(\sin x-\cos x)\,dx=2\sqrt2-2.
$$

```desmos-graph
left=-0.3; right=2;
top=1.3; bottom=-0.3;
---
y=\sin(x)
y=\cos(x)
```

(source aside) The region is symmetric about $x=\pi/4$, so the whole area could have been found faster as $A=2\displaystyle\int_0^{\pi/4}(\cos x-\sin x)\,dx$, halving the work.

## Worked example: area via $y$-strips (source, slides 19 to 20)

Area enclosed by the line $y=x-1$ and the parabola $y^2=2x+6$. Solving simultaneously gives intersection points $(-1,-2)$ and $(5,4)$. Solving the parabola for $x$: the left and right boundaries are $x=\tfrac12y^2-3$ (parabola) and $x=y+1$ (line), naturally functions of $y$ rather than $x$, so integrate in $y$ from $y=-2$ to $y=4$:

$$
A=\int_{-2}^{4}\left[(y+1)-\left(\frac12y^2-3\right)\right]dy=\int_{-2}^4\left(-\frac12y^2+y+4\right)dy=18.
$$

## See also
- [[MAT01B1_Notes_S8_Volumes]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (antiderivative formulas used throughout)
