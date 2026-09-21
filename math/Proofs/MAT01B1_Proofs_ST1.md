---
module: MAT01B1
topic: Extremum Value Theorems
test: ST1
tags: [theorem]
---

# Fermat, Rolle, MVT and their consequences

Source: user-transcribed calculus proof sheet (Fermat's Theorem, Rolle's Theorem, the Mean Value Theorem, Theorem 5, Corollary 7, the Increasing/Decreasing Test).

## Fermat's Theorem

**Statement.** If $f$ has a local maximum or minimum at $c$, and $f'(c)$ exists, then $f'(c) = 0$.

**Proof.** Assume $f$ has a local maximum at $c$. By definition,

$$
f'(c) = \lim_{h \to 0} \frac{f(c+h) - f(c)}{h}.
$$

For $h$ small, $f(c+h) \le f(c)$.

If $h > 0$:
$$
\frac{f(c+h) - f(c)}{h} \le 0 \quad \Rightarrow \quad f'(c) = \lim_{h \to 0^+} (\cdots) \le 0.
$$

If $h < 0$:
$$
\frac{f(c+h) - f(c)}{h} \ge 0 \quad \Rightarrow \quad f'(c) = \lim_{h \to 0^-} (\cdots) \ge 0.
$$

Since $f'(c)$ exists, both one sided limits are equal, so $0 \le f'(c) \le 0$, giving $f'(c) = 0$. The local minimum case is symmetric.

> [!note] Converse is false
> $f'(c) = 0$ does not imply an extremum. For example $f(x) = x^3$ at $c = 0$ is an inflection point (a point where the curve changes concavity), not an extremum.

## Rolle's Theorem

**Statement.** Let $f$ be continuous on $[a,b]$, differentiable on $(a,b)$, with $f(a) = f(b)$. Then there exists $c \in (a,b)$ such that $f'(c) = 0$.

**Hypotheses**
- $f$ continuous on $[a,b]$
- $f$ differentiable on $(a,b)$
- $f(a) = f(b)$

**Proof.**

*Case I: $f$ is constant on $[a,b]$.* Then $f'(x) = 0$ for every $x$, so any $c \in (a,b)$ works.

*Case II: $f(x) > f(a)$ for some $x \in (a,b)$.* By the Extreme Value Theorem (a continuous function on a closed interval attains a maximum and minimum on that interval), $f$ attains a maximum on $[a,b]$. Since that maximum exceeds $f(a) = f(b)$, it cannot occur at either endpoint, so it occurs at some $c \in (a,b)$. Then $c$ is a local maximum, and Fermat's Theorem gives $f'(c) = 0$.

*Case III: $f(x) < f(a)$ for some $x \in (a,b)$.* Symmetric to Case II using the minimum: $f'(c) = 0$ for some $c \in (a,b)$.

-> feeds directly into the Mean Value Theorem (see: Mean Value Theorem), which is Rolle's Theorem applied to a tilted helper function.

## Mean Value Theorem

**Statement.** Let $f$ be continuous on $[a,b]$ and differentiable on $(a,b)$. Then there exists $c \in (a,b)$ such that

$$
f'(c) = \frac{f(b) - f(a)}{b-a}.
$$

**Hypotheses**
- $f$ continuous on $[a,b]$
- $f$ differentiable on $(a,b)$

**Proof.** Define

$$
h(x) = f(x) - \left[ f(a) + \frac{f(b)-f(a)}{b-a}(x-a) \right],
$$

the vertical gap between $f$ and the secant line (the straight line joining the two endpoints) through $(a, f(a))$ and $(b, f(b))$.

Since $f$ is continuous on $[a,b]$ and differentiable on $(a,b)$, and the bracketed term is linear (continuous and differentiable everywhere), $h$ is continuous on $[a,b]$ and differentiable on $(a,b)$.

$$
h(a) = f(a) - [f(a) + 0] = 0,
$$
$$
h(b) = f(b) - \left[ f(a) + \frac{f(b)-f(a)}{b-a}(b-a) \right] = f(b) - f(b) = 0.
$$

So $h(a) = h(b)$, and Rolle's Theorem (see: Rolle's Theorem) gives $c \in (a,b)$ with $h'(c) = 0$. Since

$$
h'(x) = f'(x) - \frac{f(b)-f(a)}{b-a},
$$

setting $h'(c) = 0$ gives

$$
f'(c) = \frac{f(b)-f(a)}{b-a}.
$$

-> the constant helper function trick above is reused directly in Theorem 5 (see: Theorem 5 and Corollary 7). The integral counterpart of this theorem, guaranteeing a point where a function's value equals its average value rather than a point where its rate equals its average rate, is in [[MAT01B1_Notes_S6_MVTForIntegrals]].

## Theorem 5 and Corollary 7

**Theorem 5.** If $f'(x) = 0$ for all $x$ in $(a,b)$, then $f$ is constant on $(a,b)$.

**Proof.** Let $x_1 < x_2$ be any two points in $(a,b)$. By the Mean Value Theorem on $[x_1, x_2]$ (see: Mean Value Theorem), there exists $c \in (x_1, x_2)$ with

$$
f(x_2) - f(x_1) = f'(c)(x_2 - x_1).
$$

Since $f' \equiv 0$ on $(a,b)$, $f'(c) = 0$, so $f(x_2) - f(x_1) = 0$, i.e. $f(x_1) = f(x_2)$. As $x_1, x_2$ were arbitrary, $f$ is constant on $(a,b)$.

**Corollary 7.** If $f'(x) = g'(x)$ for all $x$ in $(a,b)$, then $f(x) = g(x) + c$ for some constant $c$.

**Proof.** Let $F(x) = f(x) - g(x)$. Then $F'(x) = f'(x) - g'(x) = 0$ on $(a,b)$. By Theorem 5, $F$ is constant, say $F(x) = c$. Hence $f(x) = g(x) + c$.

> [!note] Why every antiderivative carries a $+C$
> Any two antiderivatives of the same $f$ have equal derivatives, so by Corollary 7 they differ only by a constant. This is the actual reason the indefinite integral always carries a $+C$, it isn't a formatting convention, it's a direct consequence of this corollary.

## Increasing/Decreasing Test

**Statement.**
(a) If $f'(x) > 0$ on an interval, $f$ is increasing there.
(b) If $f'(x) < 0$ on an interval, $f$ is decreasing there.

**Proof.**

(a) Let $x_1 < x_2$ be any two points in the interval. By the Mean Value Theorem, there exists $c$ between $x_1, x_2$ with

$$
f(x_2) - f(x_1) = f'(c)(x_2 - x_1).
$$

Since $f'(c) > 0$ and $x_2 - x_1 > 0$, the product is positive, so $f(x_2) - f(x_1) > 0$, i.e. $f(x_1) < f(x_2)$. As $x_1, x_2$ were arbitrary, $f$ is increasing.

(b) Identical argument with $f'(c) < 0$: the product $f'(c)(x_2-x_1)$ is negative, so $f(x_1) > f(x_2)$, meaning $f$ is decreasing.

## Summary table

| Theorem | Conclusion | Key tool used |
|---|---|---|
| Fermat's | $f'(c)=0$ at local extremum | Definition of derivative, one sided limits |
| Rolle's | $f'(c)=0$ somewhere in $(a,b)$ | Extreme Value Theorem + Fermat's |
| MVT | $f'(c) = \dfrac{f(b)-f(a)}{b-a}$ | Rolle's Theorem on a helper function |
| Theorem 5 | $f' \equiv 0 \Rightarrow f$ constant | MVT |
| Corollary 7 | $f' = g' \Rightarrow f = g + c$ | Theorem 5 |
| Inc/Dec Test | Sign of $f' \Rightarrow$ monotonicity | MVT |

## Derivatives of inverse trig functions (added, absent from the source entirely)

All six follow the same move: set $y$ equal to the inverse function, rewrite as a plain trig equation, differentiate implicitly, then convert the result back to $x$ using a Pythagorean identity and the domain restriction that made the inverse function well defined in the first place.

**$\dfrac{d}{dx}\big[\sin^{-1}x\big] = \dfrac{1}{\sqrt{1-x^2}}$.** Let $y=\sin^{-1}x$, so $\sin y = x$ with $y\in[-\pi/2,\pi/2]$. Differentiating implicitly: $\cos y \cdot y' = 1$, so $y'=\dfrac{1}{\cos y}$. On $[-\pi/2,\pi/2]$, $\cos y\ge0$, so $\cos y = \sqrt{1-\sin^2y}=\sqrt{1-x^2}$, giving $y'=\dfrac{1}{\sqrt{1-x^2}}$.

**$\dfrac{d}{dx}\big[\cos^{-1}x\big] = -\dfrac{1}{\sqrt{1-x^2}}$.** Uses the complementary identity $\cos^{-1}x = \dfrac{\pi}{2}-\sin^{-1}x$ (true because $\sin$ and $\cos$ are complements of each other). Differentiating both sides: $\dfrac{d}{dx}\big[\cos^{-1}x\big] = -\dfrac{d}{dx}\big[\sin^{-1}x\big] = -\dfrac{1}{\sqrt{1-x^2}}$.

**$\dfrac{d}{dx}\big[\tan^{-1}x\big] = \dfrac{1}{1+x^2}$.** Let $y=\tan^{-1}x$, so $\tan y = x$. Differentiating implicitly: $\sec^2y\cdot y'=1$, so $y'=\dfrac{1}{\sec^2y}=\dfrac{1}{1+\tan^2y}=\dfrac{1}{1+x^2}$, using $\sec^2y=1+\tan^2y$.

**$\dfrac{d}{dx}\big[\cot^{-1}x\big] = -\dfrac{1}{1+x^2}$.** Same complementary move: $\cot^{-1}x=\dfrac{\pi}{2}-\tan^{-1}x$, so the derivative is the negative of the previous result.

**$\dfrac{d}{dx}\big[\sec^{-1}x\big] = \dfrac{1}{|x|\sqrt{x^2-1}}$.** Let $y=\sec^{-1}x$, so $\sec y=x$ with $y\in[0,\pi/2)\cup(\pi/2,\pi]$. Differentiating implicitly: $\sec y\tan y\cdot y'=1$, so $y'=\dfrac{1}{\sec y\tan y} = \dfrac{1}{x\tan y}$. From $\tan^2y=\sec^2y-1=x^2-1$, $\tan y = \pm\sqrt{x^2-1}$. On $y\in[0,\pi/2)$, $x=\sec y>0$ and $\tan y\ge0$; on $y\in(\pi/2,\pi]$, $x=\sec y<0$ and $\tan y\le0$. So $\tan y$ always carries the same sign as $x$, meaning $x\tan y = |x|\cdot|\tan y| = |x|\sqrt{x^2-1}$. Hence $y'=\dfrac{1}{|x|\sqrt{x^2-1}}$.

**$\dfrac{d}{dx}\big[\csc^{-1}x\big] = -\dfrac{1}{|x|\sqrt{x^2-1}}$.** Same complementary move: $\csc^{-1}x=\dfrac{\pi}{2}-\sec^{-1}x$, so the derivative is the negative of the previous result.

## Derivatives of inverse hyperbolic functions (added, absent from the source entirely)

Same implicit differentiation approach as the inverse trig set, but using the hyperbolic identity $\cosh^2y-\sinh^2y=1$ in place of the Pythagorean identity, and no domain-driven sign cases, since $\cosh y\ge1$ and $\operatorname{sech} y>0$ always, which removes the absolute-value subtlety that showed up for $\sec^{-1}$ above.

**$\dfrac{d}{dx}\big[\sinh^{-1}x\big] = \dfrac{1}{\sqrt{x^2+1}}$.** Let $y=\sinh^{-1}x$, so $\sinh y=x$. Differentiating implicitly: $\cosh y\cdot y'=1$, so $y'=\dfrac{1}{\cosh y}$. Since $\cosh y = \sqrt{1+\sinh^2y}$ (always $\ge1$, no sign ambiguity), $\cosh y=\sqrt{1+x^2}$, giving $y'=\dfrac{1}{\sqrt{x^2+1}}$.

**$\dfrac{d}{dx}\big[\cosh^{-1}x\big] = \dfrac{1}{\sqrt{x^2-1}}$, $x>1$.** Let $y=\cosh^{-1}x$, so $\cosh y=x$ with $y\ge0$. Differentiating implicitly: $\sinh y\cdot y'=1$, so $y'=\dfrac{1}{\sinh y}$. Since $y\ge0$, $\sinh y\ge0$, so $\sinh y=\sqrt{\cosh^2y-1}=\sqrt{x^2-1}$, giving $y'=\dfrac{1}{\sqrt{x^2-1}}$.

**$\dfrac{d}{dx}\big[\tanh^{-1}x\big] = \dfrac{1}{1-x^2}$, $|x|<1$.** Let $y=\tanh^{-1}x$, so $\tanh y=x$. Differentiating implicitly: $\operatorname{sech}^2y\cdot y'=1$, so $y'=\dfrac{1}{\operatorname{sech}^2y}=\dfrac{1}{1-\tanh^2y}=\dfrac{1}{1-x^2}$, using $\operatorname{sech}^2y=1-\tanh^2y$.

> [!note] The remaining three follow the identical pattern
> $\coth^{-1}x$ mirrors $\tanh^{-1}x$ exactly (same identity, same working, only the domain differs, $|x|>1$ instead of $|x|<1$), and $\operatorname{sech}^{-1}x$, $\operatorname{csch}^{-1}x$ mirror $\cosh^{-1}x$ and $\sinh^{-1}x$ the same way $\sec^{-1}$ and $\csc^{-1}$ mirrored $\cos^{-1}$ and $\sin^{-1}$ above, reciprocal identity first, then the same implicit differentiation. Not repeated here since the working is line for line the same as their non-reciprocal partner.

## See also
- [[MAT01B1_Notes_S1_CalculusApplications]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S5_OptimizationProblems]] (Fermat's Theorem used to justify the First Derivative Test for Absolute Extreme Values)
- [[MAT01B1_Notes_S6_MVTForIntegrals]] (Mean Value Theorem, integral counterpart)
- [[MAT01B1_Notes_S11_ArcLength#The Arc Length Formula (source, slides 7 to 9)|MAT01B1_Notes_S11_ArcLength]] (Mean Value Theorem used to derive the Arc Length Formula for $y=f(x)$)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations]] (Mean Value Theorem applied twice, once to each of two functions, to derive parametric arc length)
