---
module: MAT01B1
topic: Average Value of a Function
session: S10
tags: [definition, formula, worked-example]
---

# Average Value of a Function

Source: Dr K, §6.5 Average value of a function (slides 1 to 11).

## From finitely many numbers to a continuous function

The average of finitely many numbers $y_1,\dots,y_n$ is just $y_{\text{ave}}=\dfrac{y_1+\cdots+y_n}{n}$, but a continuous function $f$ on $[a,b]$ takes infinitely many values, so this needs extending. Divide $[a,b]$ into $n$ equal subintervals of width $\Delta x=(b-a)/n$, pick a point $x_i^*$ in each, and average the values $f(x_1^*),\dots,f(x_n^*)$:

$$
\frac{f(x_1^*)+\cdots+f(x_n^*)}{n}=\frac{1}{b-a}\sum_{i=1}^nf(x_i^*)\Delta x
$$

(using $n=(b-a)/\Delta x$ to rewrite the denominator). Letting $n\to\infty$ averages an ever-finer set of sample values, and by the definition of a definite integral,

$$
\lim_{n\to\infty}\frac{1}{b-a}\sum_{i=1}^nf(x_i^*)\Delta x=\frac{1}{b-a}\int_a^bf(x)\,dx.
$$

**Definition.** The average value of $f$ on $[a,b]$ is

$$
f_{\text{avg}}=\frac{1}{b-a}\int_a^bf(x)\,dx.
$$

## Worked example: average value of $1+x^2$ (source, slide 6)

$f(x)=1+x^2$ on $[-1,2]$.

$$
f_{\text{avg}}=\frac{1}{2-(-1)}\int_{-1}^2(1+x^2)\,dx=\frac13\left[x+\frac{x^3}{3}\right]_{-1}^2=\frac13\left[\left(2+\frac83\right)-\left(-1-\frac13\right)\right]=2.
$$

## Is there a point where $f$ actually equals its average?

For a temperature function $T(t)$, this asks whether the thermometer is ever exactly at the average temperature. The answer, for continuous functions, is the [[MAT01B1_Notes_S6_MVTForIntegrals|Mean Value Theorem for Integrals]]: there exists $c\in[a,b]$ with $f(c)=f_{\text{avg}}$. See that note for the full statement and proof (it isn't repeated here to avoid the same theorem living in two places); the source for this section adds one thing not in that proof, see the callout below.

> [!note] (added, from this source) Where the theorem comes from
> This section's slides describe the Mean Value Theorem for Integrals as a consequence of the [[MAT01B1_Proofs_ST1#Mean Value Theorem|Mean Value Theorem for derivatives]] together with the Fundamental Theorem of Calculus, a different route to the same result from the Extreme-Value-Theorem-plus-Intermediate-Value-Theorem proof already on file in [[MAT01B1_Notes_S6_MVTForIntegrals#Proof]]. The slides don't carry out this alternative derivation in full.

## Geometric interpretation (source, slide 9)

For $f\ge0$, the Mean Value Theorem for Integrals says there is a height $f(c)$ such that the rectangle with base $[a,b]$ and that height has exactly the same area as the region under the graph of $f$ from $a$ to $b$. Picture a two-dimensional mountain range: its top can always be chopped off at some height and used to fill in the valleys until the whole range is flattened to that one height, without changing the total area.

## Worked example: finding $c$ explicitly (source, slide 10)

For $f(x)=1+x^2$ on $[-1,2]$ (continuous, so the Mean Value Theorem for Integrals applies), $f_{\text{avg}}=2$ from the example above, so $c$ must satisfy

$$
f(c)=1+c^2=2 \;\Rightarrow\; c^2=1 \;\Rightarrow\; c=\pm1.
$$

Both $c=1$ and $c=-1$ lie in $[-1,2]$, so in this case there are two valid values of $c$, the theorem only guarantees at least one exists, not that it's unique.

## See also
- [[MAT01B1_Notes_S6_MVTForIntegrals]]
- [[MAT01B1_Proofs_ST1#Mean Value Theorem]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
