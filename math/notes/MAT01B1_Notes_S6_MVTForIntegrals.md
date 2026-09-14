---
module: MAT01B1
topic: Mean Value Theorem for Integrals
session: S6
tags: [theorem, formula]
---

# Mean Value Theorem for Integrals

Source: lecture slides, Mean Value Theorem for Integrals (8 slides).

## Statement

**Theorem (Mean Value Theorem for Integrals).** If $f$ is continuous on $[a,b]$, then there exists a number $c$ in $[a,b]$ such that

$$
f(c) = f_{\text{avg}} = \frac{1}{b-a}\int_a^b f(x)\,dx.
$$

Equivalently,

$$
\int_a^b f(x)\,dx = f(c)(b-a).
$$

**Hypotheses**
- $f$ continuous on $[a,b]$

> [!note] Reading this next to the derivative MVT
> This is the integral counterpart of the [[MAT01B1_Proofs_ST1#Mean Value Theorem|Mean Value Theorem]] already on file: that one guarantees a point where the *instantaneous rate of change* equals the *average rate of change*; this one guarantees a point where the function's *actual value* equals its *average value* over the interval. Neither theorem says where $c$ is, only that one exists.

## Proof

**Case 1: $f$ is constant on $[a,b]$.**

Let $f(x)=z$ for all $x\in[a,b]$. Then

$$
f_{\text{avg}} = \frac{1}{b-a}\int_a^b f(x)\,dx = \frac{1}{b-a}\int_a^b z\,dx = \frac{1}{b-a}\big[zx\big]_a^b = z = f(c)
$$

for any $c\in[a,b]$.

**Case 2: $f$ is not constant on $[a,b]$.**

Since $f$ is continuous on $[a,b]$, the Extreme Value Theorem gives values $m,M\in[a,b]$ such that $f(m)$ is the absolute minimum and $f(M)$ the absolute maximum of $f$ on $[a,b]$. So for every $x\in[a,b]$,

$$
f(m)\le f(x)\le f(M).
$$

Integrating this inequality over $[a,b]$,

$$
\int_a^b f(m)\,dx \le \int_a^b f(x)\,dx \le \int_a^b f(M)\,dx,
$$

$$
\big[f(m)x\big]_a^b \le \int_a^b f(x)\,dx \le \big[f(M)x\big]_a^b,
$$

$$
f(m)(b-a) \le \int_a^b f(x)\,dx \le f(M)(b-a),
$$

$$
f(m) \le \frac{1}{b-a}\int_a^b f(x)\,dx \le f(M).
$$

$f$ is continuous on $[a,b]$, so it is continuous on the interval between $m$ and $M$, and $\dfrac{1}{b-a}\displaystyle\int_a^b f(x)\,dx$ lies between $f(m)$ and $f(M)$. By the Intermediate Value Theorem, there exists $c$ between $m$ and $M$ such that

$$
f(c) = \frac{1}{b-a}\int_a^b f(x)\,dx.
$$

Since $c$ lies between $m$ and $M$, and both $m,M\in[a,b]$, $c\in[a,b]$.

N.B The proof needs two separate existence theorems chained together, the Extreme Value Theorem to get $m$ and $M$, then the Intermediate Value Theorem to get $c$ itself, rather than the single algebraic identity that drives the [[MAT01B1_Proofs_ST1#Mean Value Theorem|derivative MVT proof]].

> [!note] (added, from §6.5) A second route to the same theorem
> [[MAT01B1_Notes_S10_AverageValueOfAFunction]] describes this theorem as a consequence of the [[MAT01B1_Proofs_ST1#Mean Value Theorem|Mean Value Theorem for derivatives]] together with the Fundamental Theorem of Calculus, an alternative to the Extreme-Value-Theorem-plus-Intermediate-Value-Theorem proof above. That source states the connection but doesn't carry out the derivation in full, so it isn't reproduced here either.

## See also
- [[MAT01B1_Proofs_ST1#Mean Value Theorem]]
- [[MAT01B1_Proofs_ST1#Rolle's Theorem]] (also leans on the Extreme Value Theorem)
- [[MAT01B1_Notes_S1_CalculusApplications#Improper integrals (added)]]
- [[MAT01B1_Notes_S10_AverageValueOfAFunction]] (defines $f_{\text{avg}}$, this theorem's $c$)
