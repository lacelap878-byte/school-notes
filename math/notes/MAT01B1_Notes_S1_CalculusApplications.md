---
module: MAT01B1
topic: Calculus Applications
session: S1
tags: [theorem, formula, worked-example]
---

# Calculus Applications

## Extremum values and what they let you do

A **local maximum** at a point $c$ means $f(c)$ is at least as large as $f(x)$ for every $x$ near $c$, not necessarily on the whole domain, just in a neighbourhood of $c$. A **local minimum** is the mirror image. A point where the derivative is zero or doesn't exist is called a **critical point**, and every local extremum of a differentiable function occurs at a critical point (that's Fermat's Theorem, full derivation in [[MAT01B1_Proofs_ST1#Fermat's Theorem]]). The reverse isn't true: a critical point doesn't have to be an extremum at all, $f(x)=x^3$ has a critical point at $x=0$ that's neither a max nor a min, just a flat spot the curve passes straight through.

Rolle's Theorem is the special case where the function starts and ends at the same height, $f(a)=f(b)$, over $[a,b]$. If it does, somewhere in between the curve has to level out, $f'(c)=0$ for some $c$ strictly inside the interval. It's really just Fermat's Theorem plus one observation: if $f$ isn't flat the whole way, it must climb above or dip below its starting height somewhere, and that peak or trough is an interior extremum. Full derivation in [[MAT01B1_Proofs_ST1#Rolle's Theorem]].

The **Mean Value Theorem** drops the requirement that the endpoints match. It says the instantaneous rate of change (the derivative) equals the average rate of change (the slope of the secant line joining the endpoints) at at least one point in between:

$$
f'(c) = \frac{f(b)-f(a)}{b-a}.
$$

The proof tilts the whole picture so the secant line becomes horizontal, which turns it back into Rolle's Theorem, full derivation in [[MAT01B1_Proofs_ST1#Mean Value Theorem]]. Concretely: if you drive 120 km in 2 hours, your average speed is 60 km/h, and the MVT guarantees that at some instant your speedometer actually read exactly 60 km/h, not more, not less.

**Theorem 5** and **Corollary 7** are the reason indefinite integrals carry a $+C$. If a function's derivative is zero everywhere on an interval, the function can't be doing anything but sitting still, it has to be constant, and that follows from the MVT applied to any two points. Stack that on top of Corollary 7 (two functions with the same derivative differ only by a constant) and you get the actual justification for writing $\int f(x)\,dx = F(x)+C$: any two antiderivatives of $f$ have equal derivatives (both equal $f$), so by Corollary 7 they differ by a constant. Full derivation in [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7]].

The **Increasing/Decreasing Test** converts the sign of $f'$ directly into the shape of $f$: positive derivative means climbing, negative means falling, and this too is just the MVT, since $f(x_2)-f(x_1)=f'(c)(x_2-x_1)$ forces the sign of the left side to match the sign of $f'(c)$. Full derivation in [[MAT01B1_Proofs_ST1#Increasing/Decreasing Test]].

## Curve sketching (added)

This section doesn't come from either source PDF, it's the standard way these results get used together in a first year course, gathered here because Abs Max/Min, MVT, and the Inc/Dec Test only really click once you use them on an actual curve.

**Reading a curve from $f'$ and $f''$.** Find the critical points (where $f'=0$ or is undefined), then use the Inc/Dec Test on the intervals between them to say where $f$ rises and falls. A critical point where $f'$ switches from positive to negative is a local maximum, negative to positive is a local minimum, no switch means neither (the $x^3$ situation from Fermat's Theorem above). **Concavity** describes which way the curve bends: $f''(x)>0$ means the curve bends upward (concave up, like a cup), $f''(x)<0$ means it bends downward (concave down, like a frown). A point where concavity switches is called an **inflection point**.

**(composite) Worked example.** Let $f(x) = x^3 - 3x^2$. Then $f'(x) = 3x^2-6x = 3x(x-2)$, zero at $x=0$ and $x=2$. Testing signs: $f'>0$ on $(-\infty,0)$, $f'<0$ on $(0,2)$, $f'>0$ on $(2,\infty)$. So $x=0$ is a local maximum ($f(0)=0$) and $x=2$ is a local minimum ($f(2)=-4$). $f''(x)=6x-6$, zero at $x=1$, negative before and positive after, so $x=1$ is an inflection point.

```desmos-graph
left=-2; right=4;
top=6; bottom=-6;
---
y=x^{3}-3x^{2}
```

## Integration techniques

All formulas referenced here (the exact statements of IBP, trig substitutions, partial fractions, and the reduction cases) live in [[MAT01B1_Notes_S2_DerivativeIntegralReference]], worked examples for each live in [[MAT01B1_Notes_S3_IntegrationExamples]], this section is about when and why to reach for each one, not the formulas or the worked mechanics.

**Integration by Parts** is the product rule run in reverse. It's the tool when the integrand is a product of two functions of different types (a polynomial times an exponential, a log by itself, an inverse trig function by itself) where no substitution collapses it into something simpler. See [[MAT01B1_Notes_S2_DerivativeIntegralReference#Integration by Parts]] for the formula and the LIATE guide for picking $u$.

**Trig substitution** is the tool specifically for a square root of a sum or difference of squares sitting under the integral sign, $\sqrt{a^2-b^2x^2}$, $\sqrt{b^2x^2-a^2}$, or $\sqrt{a^2+b^2x^2}$. The substitution turns the root into a single trig function via a Pythagorean identity, removing it entirely. See [[MAT01B1_Notes_S2_DerivativeIntegralReference#Trig substitutions]].

**Partial fractions** is for a rational function (one polynomial divided by another) where nothing simplifies directly. The idea: any such fraction can be broken back apart into the simpler fractions that would have been added together to make it, and each of those simpler pieces integrates using the log or arctan patterns already in the reference tables. See [[MAT01B1_Notes_S2_DerivativeIntegralReference#Partial fractions]] for the decomposition table, and [[MAT01B1_Notes_S3_IntegrationExamples#Partial Fractions]] for a worked example.

**Products and quotients of trig functions** ($\sin^n x\cos^m x$, $\tan^n x\sec^m x$) get handled by stripping one factor out to serve as the substitution's $du$, then converting everything else to match the remaining variable using a Pythagorean identity. The full case breakdown, including the case the original reference sheet left unexplained ($\tan^n x\sec^m x$ with $n$ even and $m$ odd, which needs the secant reduction formula), is in [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products and quotients of trig functions]].

## Improper integrals (added)

Every integral formula above assumes a finite interval and a function with no breaks in it. An **improper integral** is one where that assumption fails, either the interval runs out to infinity (**Type I**), or the function has a discontinuity, usually a vertical asymptote (a value the function shoots off to infinity near, without ever reaching it), somewhere in the interval (**Type II**).

**Type I: infinite interval.**

$$
\int_a^{\infty} f(x)\,dx = \lim_{t\to\infty} \int_a^t f(x)\,dx.
$$

If the limit exists (is a finite number), the integral is called **convergent** and that limit is its value. If the limit doesn't exist or is infinite, the integral is **divergent**. The same idea applies to $\int_{-\infty}^b f(x)\,dx$ with $t\to-\infty$, and $\int_{-\infty}^{\infty}f(x)\,dx$ is split at any point $c$ into $\int_{-\infty}^c + \int_c^{\infty}$, both pieces have to converge separately for the whole thing to converge.

**(composite) Worked example.** $\displaystyle\int_1^{\infty} \frac{1}{x^2}\,dx = \lim_{t\to\infty}\int_1^t x^{-2}\,dx = \lim_{t\to\infty}\left[-\frac{1}{x}\right]_1^t = \lim_{t\to\infty}\left(1-\frac{1}{t}\right) = 1.$ Convergent, value $1$, even though the region extends forever, the area under it is finite.

```desmos-graph
left=0; right=10;
top=3; bottom=-1;
---
y=1/x^{2}
```

**Type II: discontinuity in the interval.** If $f$ has a vertical asymptote at $b$ (or at $a$, or at an interior point $c\in(a,b)$), the integral is again defined as a limit approaching that point:

$$
\int_a^b f(x)\,dx = \lim_{t\to b^-} \int_a^t f(x)\,dx \quad \text{(asymptote at } b\text{)}.
$$

**(composite) Worked example.** $\displaystyle\int_0^1 \frac{1}{\sqrt{x}}\,dx = \lim_{t\to0^+}\int_t^1 x^{-1/2}\,dx = \lim_{t\to0^+}\Big[2\sqrt{x}\Big]_t^1 = \lim_{t\to0^+}\big(2-2\sqrt{t}\big) = 2.$ Convergent, value $2$, despite the function blowing up at $x=0$.

**The $p$-integral test.** Two families come up constantly enough to be worth memorising outright rather than re-deriving every time:

$$
\int_1^{\infty} \frac{1}{x^p}\,dx \text{ converges} \iff p>1, \qquad \int_0^1 \frac{1}{x^p}\,dx \text{ converges} \iff p<1.
$$

Notice these point in opposite directions: for the infinite interval, a *steeper* fall-off (larger $p$) is what saves it. For the interval shrinking toward a vertical asymptote, a *gentler* blow-up (smaller $p$) is what saves it.

**Comparison Test.** If $0\le g(x)\le f(x)$ on the interval, then $f$ convergent forces $g$ convergent (a smaller nonnegative function under a finite area is also finite), and $g$ divergent forces $f$ divergent (a bigger function above an infinite area is also infinite). This is useful exactly when the actual antiderivative is hard or impossible to find, but the integral can still be pinned between something easy and a known $p$-integral.

**(composite) Worked example.** Does $\displaystyle\int_1^{\infty} \frac{1}{\sqrt{x^3+1}}\,dx$ converge? The antiderivative isn't elementary, so compare instead: for $x\ge1$, $\sqrt{x^3+1} > \sqrt{x^3} = x^{3/2}$, so $\dfrac{1}{\sqrt{x^3+1}} < \dfrac{1}{x^{3/2}}$. Since $p=3/2>1$, $\int_1^\infty x^{-3/2}\,dx$ converges (by the $p$-integral test), and the original integrand is smaller and nonnegative, so by the Comparison Test the original integral converges too, without ever finding its actual value.

## See also
- [[MAT01B1_Proofs_ST1]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S3_IntegrationExamples]]
- [[MAT01B1_Notes_S5_OptimizationProblems]] (the extremum theory above applied directly to optimization problems)
- [[MAT01B1_Notes_S6_MVTForIntegrals]] (integral counterpart of the Mean Value Theorem)
- [[MAT01B1_Notes_S14_LinearDifferentialEquations]] (a different non-elementary integral, $\int e^{x^2}\,dx$, handled via the Fundamental Theorem of Calculus rather than the Comparison Test used above)
