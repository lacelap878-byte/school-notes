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

-> the constant helper function trick above is reused directly in Theorem 5 (see: Theorem 5 and Corollary 7).

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

## See also
- [[MAT01B1_Notes_S1_CalculusApplications]]
