---
module: MAT01B1
topic: Calculus Applications
session: S1
tags: [definition, theorem, formula, worked-example, common-mistake]
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

## L'Hospital's Rule and indeterminate forms

Source: Dr K, §4.4 Indeterminate Forms and L'Hospital's Rule, Part 1 (slides 1 to 34). Part 2 of that lecture (the forms $\infty-\infty$, $0^0$, $\infty^0$, $1^\infty$) isn't in the vault yet.

<span style="color:#f08c00">Exam: L'Hospital's Rule is examined in the final exam.</span> #exam-flagged

**Why it exists.** Some limits can't be settled by the usual limit laws because the answer depends on how fast each piece moves. In $\displaystyle\lim_{x\to1}\frac{\ln x}{x-1}$ the numerator and denominator both go to $0$, so the quotient could end up as anything. That is an **indeterminate form**, here of type $\tfrac00$. The other two types handled in this lecture are $\tfrac{\infty}{\infty}$ and $0\cdot\infty$. (added) The idea behind the rule: if $f(a)=g(a)=0$, then near $a$ we have $f(x)\approx f'(a)(x-a)$ and $g(x)\approx g'(a)(x-a)$, so the ratio $f/g$ behaves like $f'(a)/g'(a)$. This is only a heuristic for the friendliest case, not a proof (the source doesn't prove the rule).

**Statement (source).** Suppose $f$ and $g$ are differentiable and $g'(x)\neq0$ when $x$ is near $a$. Suppose that $\lim_{x\to a}f(x)=0$ and $\lim_{x\to a}g(x)=0$, or $\lim_{x\to a}f(x)=\pm\infty$ and $\lim_{x\to a}g(x)=\pm\infty$. Then

$$
\lim_{x\to a}\frac{f(x)}{g(x)}=\lim_{x\to a}\frac{f'(x)}{g'(x)}
$$

if the limit on the right exists (or is $\pm\infty$).

**Hypotheses**
- $f$ and $g$ differentiable
- $g'(x)\neq0$ near $a$
- the limit has the form $\tfrac00$ or $\tfrac{\pm\infty}{\pm\infty}$

The rule also holds for one-sided limits ($x\to a^+$, $x\to a^-$) and for limits at infinity ($x\to\infty$, $x\to-\infty$).

N.B Differentiate the numerator and the denominator **separately**. This is not the Quotient Rule.

N.B Every solution needs two visible steps: first check that the limit really is $\tfrac00$ or $\tfrac{\pm\infty}{\pm\infty}$ and write down the type, then write L'H over the equals sign where the rule is applied.

> [!warning] Check the form before using the rule
> $\displaystyle\lim_{x\to\pi^-}\frac{\sin x}{1-\cos x}$: the numerator goes to $\sin\pi=0$ but the denominator goes to $1-\cos\pi=2$, so this is not indeterminate and the rule must not be used. Plug in directly: $\dfrac{0}{2}=0$. (source) <span style="color:#e03131">Wrong:</span> differentiating anyway gives $\cos x/\sin x\to-\infty$ as $x\to\pi^-$ (added). <span style="color:#2f9e44">Right:</span> the limit is $0$. #common-mistake

**Worked example (source, §4.4 Part 1).** $\displaystyle\lim_{x\to1}\frac{\ln x}{x-1}$, type $\tfrac00$:

$$
\lim_{x\to1}\frac{\ln x}{x-1}\overset{\text{L'H}}{=}\lim_{x\to1}\frac{1/x}{1}=1.
$$

**Worked example (source, §4.4 Part 1), applying the rule twice.** $\displaystyle\lim_{x\to\infty}\frac{e^x}{x^2}$, type $\tfrac\infty\infty$, and still $\tfrac\infty\infty$ after one step:

$$
\lim_{x\to\infty}\frac{e^x}{x^2}\overset{\text{L'H}}{=}\lim_{x\to\infty}\frac{e^x}{2x}\overset{\text{L'H}}{=}\lim_{x\to\infty}\frac{e^x}{2}=\infty.
$$

**Worked example (source, §4.4 Part 1), simplify before going again.** $\displaystyle\lim_{x\to\infty}\frac{\ln x}{\sqrt[3]{x}}$, type $\tfrac\infty\infty$:

$$
\lim_{x\to\infty}\frac{\ln x}{x^{1/3}}\overset{\text{L'H}}{=}\lim_{x\to\infty}\frac{1/x}{\tfrac13x^{-2/3}}=\lim_{x\to\infty}\frac{3}{x^{1/3}}=0.
$$

Here the fraction was tidied after one step and the limit read off, so no second application was needed.

**Worked example (source, §4.4 Part 1), three applications.** $\displaystyle\lim_{x\to0}\frac{\tan x-x}{x^3}$, type $\tfrac00$:

$$
\lim_{x\to0}\frac{\tan x-x}{x^3}\overset{\text{L'H}}{=}\lim_{x\to0}\frac{\sec^2x-1}{3x^2}\overset{\text{L'H}}{=}\lim_{x\to0}\frac{2\sec^2x\tan x}{6x}=\lim_{x\to0}\frac{\sec^2x\tan x}{3x}
$$

$$
\overset{\text{L'H}}{=}\lim_{x\to0}\frac{2\sec^2x\tan^2x+\sec^4x}{3}=\frac13.
$$

The source needs $\tan0=0$, $\sec0=1$, $\frac{d}{dx}\tan x=\sec^2x$ and $\frac{d}{dx}\sec x=\sec x\tan x$ at every step.

**Type $0\cdot\infty$ (source).** If $\lim_{x\to a}f(x)=0$ and $\lim_{x\to a}g(x)=\pm\infty$, the product $f\cdot g$ is an indeterminate form of type $0\cdot\infty$. Turn it into a quotient first, which is plain algebra and not yet the rule:

$$
f\cdot g=\frac{f}{1/g}\qquad\text{or}\qquad f\cdot g=\frac{g}{1/f}.
$$

That gives $\tfrac00$ or $\tfrac\infty\infty$, and now the rule applies. N.B The choice matters: first try leaving the function with the more complicated reciprocal in the numerator.

**Worked example (source, §4.4 Part 1).** $\displaystyle\lim_{x\to0^+}x\ln x$. Put $1/x$ in the denominator, since $1/x$ is much easier to differentiate than $1/\ln x$:

$$
\lim_{x\to0^+}x\ln x=\lim_{x\to0^+}\frac{\ln x}{1/x}\overset{\text{L'H}}{=}\lim_{x\to0^+}\frac{1/x}{-1/x^2}=\lim_{x\to0^+}(-x)=0.
$$

<span style="color:#e03131">Wrong:</span> the other choice, $\dfrac{x}{1/\ln x}$, leads after one step to $\lim_{x\to0^+}-x(\ln x)^2$, which is again of type $0\cdot\infty$ and no closer to an answer. <span style="color:#2f9e44">Right:</span> $\dfrac{\ln x}{1/x}$.

**Where the rule is used elsewhere in this vault.** Two improper integral examples below need it for the boundary term, $\int_{-\infty}^0xe^x\,dx$ and $\int_0^1\ln x\,dx$ (see: Worked examples from the lecture, section 7.8). The vertical tangents of the cycloid in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: tangent to the cycloid (source, slides 9 to 11)|S16]] also need it.

## Curve sketching (added)

This section doesn't come from either source PDF, it's the standard way these results get used together in a first year course, gathered here because Abs Max/Min, MVT, and the Inc/Dec Test only really click once you use them on an actual curve.

**Reading a curve from $f'$ and $f''$.** Find the critical points (where $f'=0$ or is undefined), then use the Inc/Dec Test on the intervals between them to say where $f$ rises and falls. A critical point where $f'$ switches from positive to negative is a local maximum, negative to positive is a local minimum, no switch means neither (the $x^3$ situation from Fermat's Theorem above). **Concavity** describes which way the curve bends: $f''(x)>0$ means the curve bends upward (concave up, like a cup), $f''(x)<0$ means it bends downward (concave down, like a frown). A point where concavity switches is called an **inflection point**. Limits at the ends of the domain (to find asymptotes) sometimes need [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]], for example $\lim_{x\to-\infty}xe^x=0$ gives the $x$-axis as a horizontal asymptote of $y=xe^x$ (source, §4.5 summary of curve sketching).

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

Source: the Comparison Theorem and every example marked (source, §7.8) are from Dr K, §7.8 Improper Integrals. The rest of this section is added context.

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

If the asymptote is at the left endpoint $a$, use $\lim_{t\to a^+}\int_t^b f(x)\,dx$ instead. If it sits at an interior point $c$ with $a<c<b$, split the integral at $c$ and treat each piece as its own limit:

$$
\int_a^b f(x)\,dx=\int_a^c f(x)\,dx+\int_c^b f(x)\,dx.
$$

The whole integral converges only if **both** pieces converge (source, §7.8).

> [!warning] Spot the asymptote before integrating
> $\displaystyle\int_0^3\frac{dx}{x-1}$ has a vertical asymptote at $x=1$, inside the interval. <span style="color:#e03131">Wrong:</span> treating it as an ordinary integral gives $\ln|x-1|\Big|_0^3=\ln2-\ln1=\ln2$. <span style="color:#2f9e44">Right:</span> split at $1$. Already $\displaystyle\int_0^1\frac{dx}{x-1}=\lim_{t\to1^-}\ln|t-1|=-\infty$, so the integral is divergent. (source, §7.8, Example 7 and its warning) #common-mistake


**(composite) Worked example.** $\displaystyle\int_0^1 \frac{1}{\sqrt{x}}\,dx = \lim_{t\to0^+}\int_t^1 x^{-1/2}\,dx = \lim_{t\to0^+}\Big[2\sqrt{x}\Big]_t^1 = \lim_{t\to0^+}\big(2-2\sqrt{t}\big) = 2.$ Convergent, value $2$, despite the function blowing up at $x=0$.

**The $p$-integral test.** Two families come up constantly enough to be worth memorising outright rather than re-deriving every time:

$$
\int_1^{\infty} \frac{1}{x^p}\,dx \text{ converges} \iff p>1, \qquad \int_0^1 \frac{1}{x^p}\,dx \text{ converges} \iff p<1.
$$

Notice these point in opposite directions: for the infinite interval, a *steeper* fall-off (larger $p$) is what saves it. For the interval shrinking toward a vertical asymptote, a *gentler* blow-up (smaller $p$) is what saves it. For $p>1$ the value is $\int_1^\infty\frac{1}{x^p}\,dx=\frac{1}{p-1}$, and for $p=1$ it is $\lim_{t\to\infty}\ln t=\infty$, divergent (source, §7.8, Examples 1 and 4).

### Worked examples from the lecture, section 7.8

**Type I.** $\displaystyle\int_1^\infty\frac{dx}{x}=\lim_{t\to\infty}\ln t=\infty$, divergent (source, §7.8, Example 1). Compare $\int_1^\infty\frac{dx}{x^2}=1$ above: both integrands go to $0$, but $1/x^2$ goes to $0$ fast enough and $1/x$ doesn't.

$\displaystyle\int_{-\infty}^0xe^x\,dx=\lim_{t\to-\infty}\int_t^0xe^x\,dx=\lim_{t\to-\infty}\big(-te^t-1+e^t\big)=-1$ (source, §7.8, Example 2). Integration by parts with $u=x$, $dv=e^x\,dx$ gives the antiderivative, and $te^t\to0$ comes from rewriting $te^t=\dfrac{t}{e^{-t}}$ and using [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]] (type $\tfrac\infty\infty$).

$\displaystyle\int_{-\infty}^{\infty}\frac{dx}{1+x^2}=\pi$ (source, §7.8, Example 3). Split at $0$: each half is $\lim\tan^{-1}$ and equals $\tfrac\pi2$, and both converge.

**Type II.** $\displaystyle\int_2^5\frac{dx}{\sqrt{x-2}}=\lim_{t\to2^+}2\big(\sqrt3-\sqrt{t-2}\big)=2\sqrt3$, convergent (source, §7.8, Example 5). The asymptote is at the left endpoint, so the limit is $t\to2^+$.

$\displaystyle\int_0^{\pi/2}\sec x\,dx=\lim_{t\to(\pi/2)^-}\ln|\sec t+\tan t|=\infty$, divergent (source, §7.8, Example 6).

$\displaystyle\int_0^1\ln x\,dx=\lim_{t\to0^+}\big(-t\ln t-1+t\big)=-1$ (source, §7.8, Example 8). Integration by parts with $u=\ln x$, $dv=dx$, and $t\ln t\to0$ from the $0\cdot\infty$ case of [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]].

### Comparison Theorem

**Comparison Theorem (source, §7.8)**, also called the Comparison Test. Suppose $f$ and $g$ are continuous with $f(x)\ge g(x)\ge0$ for $x\ge a$.

(a) If $\displaystyle\int_a^\infty f(x)\,dx$ is convergent, then $\displaystyle\int_a^\infty g(x)\,dx$ is convergent.

(b) If $\displaystyle\int_a^\infty g(x)\,dx$ is divergent, then $\displaystyle\int_a^\infty f(x)\,dx$ is divergent.

**Hypotheses**
- $f$ and $g$ continuous
- $f(x)\ge g(x)\ge0$ for $x\ge a$

The source states it for Type I integrals and says a similar theorem holds for Type II. It omits the proof and gives only the picture: if the area under the top curve $y=f(x)$ is finite, so is the area under the bottom curve $y=g(x)$, and if the area under the bottom curve is infinite, so is the area under the top. This is useful exactly when the actual antiderivative is hard or impossible to find, but the integral can still be pinned between something easy and a known $p$-integral.

> [!warning] Only two directions work
> <span style="color:#2f9e44">Right:</span> a smaller nonnegative function under a convergent bigger one converges, and a bigger function over a divergent smaller one diverges. <span style="color:#e03131">Wrong:</span> concluding $\int f$ converges because $\int g$ does, or that $\int g$ diverges because $\int f$ does. If $\int_a^\infty g$ converges, $\int_a^\infty f$ may or may not; if $\int_a^\infty f$ diverges, $\int_a^\infty g$ may or may not. (source) #common-mistake

**Worked example (source, §7.8, Example 9), convergence.** Show $\displaystyle\int_0^\infty e^{-x^2}\,dx$ is convergent. The antiderivative of $e^{-x^2}$ isn't elementary, so split:

$$
\int_0^\infty e^{-x^2}\,dx=\int_0^1e^{-x^2}\,dx+\int_1^\infty e^{-x^2}\,dx.
$$

The first integral is an ordinary definite integral. For the second, $x\ge1$ gives $x^2\ge x$, so $-x^2\le-x$ and $e^{-x^2}\le e^{-x}$. Also

$$
\int_1^\infty e^{-x}\,dx=\lim_{t\to\infty}\big(-e^{-t}+e^{-1}\big)=e^{-1},
$$

convergent. Taking $f(x)=e^{-x}$ and $g(x)=e^{-x^2}$ in the Comparison Theorem, $\int_1^\infty e^{-x^2}\,dx$ converges, so $\int_0^\infty e^{-x^2}\,dx$ converges. (added) The split at $1$ is not optional: on $(0,1)$ we have $x^2<x$, so $e^{-x^2}>e^{-x}$ and the inequality needed for the theorem points the wrong way there.

**Worked example (source, §7.8, Example 10), divergence.** Show $\displaystyle\int_1^\infty\frac{1+e^{-x}}{x}\,dx$ is divergent. For $x\ge1$, $\dfrac{1+e^{-x}}{x}>\dfrac1x$, and $\displaystyle\int_1^\infty\frac{dx}{x}$ is divergent (the $p$-integral test with $p=1$). By part (b) with $g(x)=\dfrac1x$ and $f(x)=\dfrac{1+e^{-x}}{x}$, the given integral is divergent.

**(composite) Worked example.** Does $\displaystyle\int_1^{\infty} \frac{1}{\sqrt{x^3+1}}\,dx$ converge? The antiderivative isn't elementary, so compare instead: for $x\ge1$, $\sqrt{x^3+1} > \sqrt{x^3} = x^{3/2}$, so $\dfrac{1}{\sqrt{x^3+1}} < \dfrac{1}{x^{3/2}}$. Since $p=3/2>1$, $\int_1^\infty x^{-3/2}\,dx$ converges (by the $p$-integral test), and the original integrand is smaller and nonnegative, so by the Comparison Theorem the original integral converges too, without ever finding its actual value.

## See also
- [[MAT01B1_Proofs_ST1]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S3_IntegrationExamples]]
- [[MAT01B1_Notes_S5_OptimizationProblems]] (the extremum theory above applied directly to optimization problems)
- [[MAT01B1_Notes_S6_MVTForIntegrals]] (integral counterpart of the Mean Value Theorem)
- [[MAT01B1_Notes_S14_LinearDifferentialEquations]] (a different non-elementary integral, $\int e^{x^2}\,dx$, handled via the Fundamental Theorem of Calculus rather than the Comparison Theorem used above)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: tangent to the cycloid (source, slides 9 to 11)]] (L'Hospital's Rule applied to the cycloid's vertical tangents)
