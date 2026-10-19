---
module: MAT01B1
topic: Optimization Problems
session: S5
tags: [theorem, formula, worked-example]
---

# Optimization Problems

Source: Dr K, §4.7 Optimization Problems (slides 1 to 26).

## Why this is just extremum theory in disguise

An optimization problem asks for the best way of doing something. That always reduces to finding the absolute maximum or minimum of some function on some domain, which means every tool built for extrema (critical points, the [[MAT01B1_Notes_S1_CalculusApplications#Curve sketching (added)|Inc/Dec Test]], [[MAT01B1_Proofs_ST1#Fermat's Theorem|Fermat's Theorem]]) applies directly. The real difficulty in this section is almost never the calculus, it's turning a written description into a single-variable function in the first place.

## Steps in Solving Optimization Problems (source, slides 3 to 5)

1. **Understand the problem.** Read carefully, identify the unknown, the given quantities, and the given conditions.
2. **Draw a diagram**, to organize relationships.
3. **Introduce notation.** Name the quantity to be optimized (say $Q$) and every other variable involved.
4. **Express $Q$** in terms of the other variables.
5. If $Q$ depends on more than one variable, find a relationship between them (from the geometry of the problem) that lets you write $Q=f(x)$, a function of one variable, and state the domain of $f$ in context.
6. Determine the absolute maximum or minimum of $f$ on its domain, using the extremum theory already developed.

N.B Step 5 is where the actual work happens: reducing $Q$ from several variables down to one, using whatever geometric constraint the problem hands you.

## First Derivative Test for Absolute Extreme Values (source, slide 16)

**Statement.** Suppose $c$ is a critical number of a continuous function $f$ defined on an interval.
(a) If $f'(x)>0$ for all $x<c$ and $f'(x)<0$ for all $x>c$, then $f(c)$ is the absolute maximum value of $f$.
(b) If $f'(x)<0$ for all $x<c$ and $f'(x)>0$ for all $x>c$, then $f(c)$ is the absolute minimum value of $f$.

**Hypotheses**
- $f$ continuous on an interval
- $c$ a critical number of $f$
- the sign of $f'$ is known on the whole of each side of $c$

> [!note] Global version of the Inc/Dec Test
> This is the [[MAT01B1_Notes_S1_CalculusApplications#Curve sketching (added)|Inc/Dec Test]] applied across an *entire* domain rather than a small neighbourhood of $c$: one sign change over the whole interval is what upgrades a local extremum into an absolute one. It earns its own name because it's exactly the tool needed when the domain is unbounded, where the Closed Interval Method below has no endpoints to fall back on.

## The Closed Interval Method (source, §4.1)

When the domain of $Q=f(x)$ is a closed, bounded interval $[a,b]$: find the critical numbers in $(a,b)$, evaluate $f$ at each of them and at both endpoints, and the largest and smallest of those values are the absolute maximum and minimum. The §4.7 slides use the name without spelling it out, and the three-step statement, with a worked test question, is in Dr K's §4.1 (see: [[MAT01B1_Notes_S1_CalculusApplications#Fermat's Theorem, critical numbers and the Closed Interval Method]]).

## Worked example: rectangular field along a river (source, slides 6 to 9)

1200 m of fencing encloses a rectangular field bordering a river (no fence needed along the river). Maximize the area.

Let $x$ = depth, $y$ = width. $A=xy$. Fencing used: $2x+y=1200\Rightarrow y=1200-2x$, so

$$
A(x)=x(1200-2x)=1200x-2x^2,\qquad x\in[0,600].
$$

Closed Interval Method: $A'(x)=1200-4x=0\Rightarrow x=300$. $A(0)=0$, $A(300)=180\,000$, $A(600)=0$. Maximum at $x=300$: depth 300 m, width 600 m. $A''(x)=-4<0$ confirms the graph is concave down, consistent with $x=300$ being an absolute maximum.

```desmos-graph
left=-50; right=650;
top=200000; bottom=-20000;
---
y=1200x-2x^{2}\left\{0\le x\le600\right\}
(300,180000)
```

## Worked example: minimum-surface-area can (source, slides 10 to 14)

A cylindrical can must hold 1 L ($1000\text{ cm}^3$); minimize the total surface area (top, bottom, side).

$$
A=2\pi r^2+2\pi rh,\qquad \pi r^2h=1000\Rightarrow h=\frac{1000}{\pi r^2}.
$$

$$
A(r)=2\pi r^2+\frac{2000}{r},\qquad r>0.
$$

$$
A'(r)=4\pi r-\frac{2000}{r^2}=\frac{4(\pi r^3-500)}{r^2}=0 \;\Rightarrow\; r_0=\left(\frac{500}{\pi}\right)^{1/3}.
$$

The domain $(0,\infty)$ has no endpoints, so the Closed Interval Method doesn't apply here. Sign analysis (source, slide 15): since $r^2>0$ always, $A'(r)<0 \iff \pi r^3<500 \iff r<r_0$, and $A'(r)>0$ for $r>r_0$. By the First Derivative Test for Absolute Extreme Values above, $A(r_0)$ is the absolute minimum. Substituting back, $h=\dfrac{1000}{\pi r_0^2}=2r_0$, so the minimizing can has height equal to twice its radius.

N.B This example is exactly why the First Derivative Test for Absolute Extreme Values exists as a tool separate from the Closed Interval Method.

## Worked example: closest point on a parabola (source, slides 17 to 19)

Find the point on $y^2=2x$ closest to $(1,4)$.

$$
d=\sqrt{(x-1)^2+(y-4)^2},\qquad x=\frac{1}{2}y^2 \text{ (on the parabola)}.
$$

Minimizing $d$ is equivalent to minimizing $d^2$ (easier to differentiate, same minimizer since $d\ge0$):

$$
f(y)=d^2=\left(\frac{1}{2}y^2-1\right)^2+(y-4)^2,\qquad f'(y)=y^3-8.
$$

$f'(y)=0$ at $y=2$; $f'(y)<0$ for $y<2$ and $f'(y)>0$ for $y>2$, so by the First Derivative Test the absolute minimum is at $y=2$. Then $x=\tfrac{1}{2}(2)^2=2$. Closest point: $(2,2)$, distance $d=\sqrt{f(2)}=\sqrt5$.

(source aside) The geometry of the problem makes it clear there's a closest point but no farthest one, which is consistent with the one-sided sign change found above.

## Worked example: fastest route across a river (source, slides 20 to 23)

A man rows from $A$ across a 3 km river, then runs to $B$, 8 km downstream on the far bank. He rows 6 km/h, runs 8 km/h. $x$ = distance from the point directly opposite $A$ to his landing point.

$$
T(x)=\frac{\sqrt{x^2+9}}{6}+\frac{8-x}{8},\qquad x\in[0,8].
$$

$$
T'(x)=\frac{x}{6\sqrt{x^2+9}}-\frac{1}{8}=0 \;\Rightarrow\; 4x=3\sqrt{x^2+9}\;\Rightarrow\;16x^2=9(x^2+9)\;\Rightarrow\;7x^2=81\;\Rightarrow\;x=\frac{9}{\sqrt7}\ (x\ge0).
$$

Domain is closed, so Closed Interval Method: $T(0)=1.5$, $T\!\left(\tfrac{9}{\sqrt7}\right)=1+\tfrac{\sqrt7}{8}\approx1.33$, $T(8)=\tfrac{\sqrt{73}}{6}\approx1.42$. Smallest at $x=\tfrac{9}{\sqrt7}\approx3.4$ km downstream, land there.

## Worked example: largest rectangle inscribed in a semicircle (source, slides 24 to 26)

Semicircle $x^2+y^2=r^2$ (upper half). Rectangle with two vertices on the semicircle, two on the $x$-axis; $(x,y)$ is the vertex in the first quadrant, so the rectangle has sides $2x$ and $y$.

$$
A=2xy,\qquad y=\sqrt{r^2-x^2}\ \text{(on the circle)} \;\Rightarrow\; A=2x\sqrt{r^2-x^2},\qquad x\in[0,r].
$$

$$
A'(x)=\frac{2(r^2-2x^2)}{\sqrt{r^2-x^2}}=0 \;\Rightarrow\; x=\frac{r}{\sqrt2}\ (x\ge0).
$$

Closed Interval Method: $A(0)=0$, $A(r)=0$, so the interior critical point is the maximum: $A\!\left(\tfrac{r}{\sqrt2}\right)=r^2$.

(source note) The textbook gives a second, non-calculus solution to this problem; it isn't reproduced here since it isn't shown in the slides.

## See also
- [[MAT01B1_Notes_S1_CalculusApplications#Extremum values and what they let you do]]
- [[MAT01B1_Proofs_ST1#Fermat's Theorem]]
- [[MAT01B1_Notes_S4_RelatedRates]]
