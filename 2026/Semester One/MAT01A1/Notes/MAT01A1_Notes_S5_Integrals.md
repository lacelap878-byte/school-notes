---
module: MAT01A1
topic: Integrals
session: S5
tags: [definition, theorem, formula, worked-example, common-mistake, added]
---

# MAT01A1 Notes S5: Integrals

Source: the Moodle lecture notes for Stewart sections 4.9 and 5.1 to 5.5 (weeks 13 and 14). The notes pose most examples without answers, so the working is mine unless marked. Short revision notes, not from a teaching session.

Scope: the whole module was examined in the final (12 June 2026). The long Riemann sum calculations in the 5.1 examples are not covered in detail; the principle is.

Checked: every antiderivative and integral was checked in Python (SymPy, with a numerical check for the odd-function example) on 15 Nov 2026.

## Antiderivatives (source: section 4.9 notes)

> A function $F$ is an antiderivative of $f$ on an interval $I$ if $F'(x) = f(x)$ for all $x \in I$.

> **Theorem:** If $F$ is an antiderivative of $f$ on an interval $I$, then the most general antiderivative of $f$ on $I$ is $F(x) + C$ where $C$ is an arbitrary constant.

- Antiderivatives are not unique: $x^2$, $x^2 + 4$ and $x^2 + 7$ all have derivative $2x$.
- Given extra conditions ($f(0)$, $f'(0)$, a $y$-intercept), integrate step by step and use each condition to fix a constant.
- Reversing the chain rule: $2e^{2x}$ is $u'e^u$ with $u = 2x$, so its antiderivative is $e^{2x} + C$. The formal method is substitution (5.5).

Example (source: section 4.9 notes): find $f$ if $f''(x) = 12x^2 + 6x - 4$, $f(0) = 4$ and $f(1) = 1$.
   $f'(x) = 4x^3 + 3x^2 - 4x + C$, $f(x) = x^4 + x^3 - 2x^2 + Cx + D$. $f(0) = 4$ gives $D = 4$; $f(1) = 1$ gives $C = -3$. So $f(x) = x^4 + x^3 - 2x^2 - 3x + 4$.

## Area under a curve (source: section 5.1 notes)

- Approximate the area under $y = f(x) \ge 0$ from $a$ to $b$ by $n$ rectangles of width $\Delta x = \frac{b - a}{n}$. Heights from left endpoints, right endpoints or midpoints give different approximations; for an increasing $f$, left endpoints underestimate and right endpoints overestimate.
- As $n$ grows, $\Delta x \to 0$, every method gets closer to the true area, and the choice of point in each interval stops mattering.

$$A = \lim_{n \to \infty} \sum_{i=1}^{n} f(x_i^*)\,\Delta x$$

$x_i^*$ is any sample point in the $i$th interval.

Example (source: section 5.1 notes): area under $y = x^2$ from 0 to 1.
   Four rectangles: $L_4 = \frac{7}{32} = 0.21875 < A < R_4 = \frac{15}{32} = 0.46875$. With $n$ rectangles, $R_n = \frac{1}{n^3}\sum_{i=1}^{n} i^2 = \frac{(n + 1)(2n + 1)}{6n^2} \to \frac{1}{3}$.

## The definite integral (source: section 5.2 notes)

> Let $f$ be defined for $a \le x \le b$ and let $\Delta x = \frac{b - a}{n}$. Let $x_i^*$ be a sample point in the $i$th subinterval. The definite integral of $f$ from $a$ to $b$ is

$$\int_a^b f(x)\,dx = \lim_{n \to \infty}\left(\sum_{i=1}^{n} f(x_i^*)\,\Delta x\right)$$

> The definite integral of $f$ from $a$ to $b$ exists provided that the limit on the RHS exists. If the limit (and hence the integral) exists, we say that $f$ is integrable on $[a, b]$.

- $\sum f(x_i^*)\Delta x$ is a Riemann sum. $f(x)$ is the integrand, $a$ the lower and $b$ the upper limit. The integral is a number; the variable is a dummy ($\int_a^b f(t)\,dt$ is the same).
- If $f$ takes both signs, $\int_a^b f(x)\,dx = A_1 - A_2$, the net area: area above the $x$-axis minus area below.

> **Theorem:** If $f$ is continuous on $[a, b]$, or if $f$ has only a finite number of jump discontinuities, then $f$ is integrable on $[a, b]$; that is, the definite integral $\int_a^b f(x)\,dx$ exists.

> **Theorem:** If $f$ is integrable on $[a, b]$, then

$$\int_a^b f(x)\,dx = \lim_{n \to \infty}\sum_{i=1}^{n} f(x_i)\,\Delta x \qquad \text{where } \Delta x = \frac{b - a}{n} \text{ and } x_i = a + i\,\Delta x$$

- So right endpoints may be used. Reading a limit as an integral: $\lim \sum \frac{\cos x_i}{x_i}\Delta x$ on $[\pi, 2\pi]$ is $\int_\pi^{2\pi}\frac{\cos x}{x}\,dx$.

Properties (assume $f$ and $g$ continuous):

$$\int_b^a f(x)\,dx = -\int_a^b f(x)\,dx \qquad \int_a^a f(x)\,dx = 0 \qquad \int_a^b c\,dx = c(b - a)$$

$$\int_a^b [f(x) \pm g(x)]\,dx = \int_a^b f(x)\,dx \pm \int_a^b g(x)\,dx \qquad \int_a^b cf(x)\,dx = c\int_a^b f(x)\,dx \qquad \int_a^c f(x)\,dx + \int_c^b f(x)\,dx = \int_a^b f(x)\,dx$$

Comparison properties, for $a \le x \le b$:
6. If $f(x) \ge 0$, then $\int_a^b f(x)\,dx \ge 0$.
7. If $f(x) \ge g(x)$, then $\int_a^b f(x)\,dx \ge \int_a^b g(x)\,dx$.
8. If $m \le f(x) \le M$, then $m(b - a) \le \int_a^b f(x)\,dx \le M(b - a)$.

Examples (source: section 5.2 notes):
- $\int_0^1 \sqrt{1 - x^2}\,dx$ is a quarter of the unit circle: $\frac{\pi}{4}$.
- $\int_{-1}^{2}|x|\,dx$: two triangles, $\frac{1}{2} + 2 = \frac{5}{2}$.
- If $\int_0^8 f = 12$ and $\int_8^{10} f = 5$, then $\int_0^{10} f = 17$.

## The Fundamental Theorem of Calculus (source: section 5.3 notes)

- $g(x) = \int_a^x f(t)\,dt$ is the "area so far" function: the area under $f$ from $a$ up to $x$.

> **Fundamental Theorem of Calculus, Part 1:** If $f$ is continuous on $[a, b]$, then the function $g$ defined by $g(x) = \int_a^x f(t)\,dt$, $a \le x \le b$, is continuous on $[a, b]$ and differentiable on $(a, b)$ and $g'(x) = f(x)$. That is:

$$\frac{d}{dx}\int_a^x f(t)\,dt = f(x)$$

> **Part 2:** If $f$ is continuous on $[a, b]$, then

$$\int_a^b f(x)\,dx = F(b) - F(a)$$

> where $F$ is any antiderivative of $f$, that is $F' = f$.

- Hypothesis for both: $f$ continuous on $[a, b]$. Integration and differentiation are inverse processes.
- With a function as the upper limit, use the chain rule: $\frac{d}{dx}\int_a^{h(x)} f(t)\,dt = f(h(x))\,h'(x)$. With functions at both limits, split at a constant: $\frac{d}{dx}\int_{x^2}^{3x^3}\cos t\,dt = 9x^2\cos(3x^3) - 2x\cos(x^2)$.

> [!warning] Check continuity before using FTC2 (added)
> $\int_{-1}^{3}\frac{1}{x^2}\,dx \ne \left[-\frac{1}{x}\right]_{-1}^{3} = -\frac{4}{3}$. The integrand is positive, so a negative answer is impossible: $\frac{1}{x^2}$ is not continuous at 0, so FTC2 does not apply.

## Indefinite integrals (source: section 5.4 notes)

$$\int f(x)\,dx = F(x) \text{ means that } F'(x) = f(x)$$

- A definite integral is a number; an indefinite integral is a family of functions, always written with $+ C$.

| Integral | Result | Integral | Result |
|---|---|---|---|
| $\int k\,dx$ | $kx + C$ | $\int x^n\,dx$ ($n \ne -1$) | $\frac{x^{n+1}}{n + 1} + C$ |
| $\int \frac{1}{x}\,dx$ | $\ln\lvert x\rvert + C$ | $\int e^x\,dx$ | $e^x + C$ |
| $\int b^x\,dx$ | $\frac{b^x}{\ln b} + C$ | $\int \sin x\,dx$ | $-\cos x + C$ |
| $\int \cos x\,dx$ | $\sin x + C$ | $\int \sec^2 x\,dx$ | $\tan x + C$ |
| $\int \csc^2 x\,dx$ | $-\cot x + C$ | $\int \sec x\tan x\,dx$ | $\sec x + C$ |
| $\int \csc x\cot x\,dx$ | $-\csc x + C$ | $\int \frac{1}{x^2 + 1}\,dx$ | $\tan^{-1}x + C$ |
| $\int \frac{1}{\sqrt{1 - x^2}}\,dx$ | $\sin^{-1}x + C$ | $\int \sinh x\,dx$ | $\cosh x + C$ |
| $\int \cosh x\,dx$ | $\sinh x + C$ | | |

- Plus $\int cf\,dx = c\int f\,dx$ and $\int (f + g)\,dx = \int f\,dx + \int g\,dx$. Remember the absolute value in $\ln|x|$.
- Example (source): $\int \frac{\sin\theta}{\cos^2\theta}\,d\theta = \int \sec\theta\tan\theta\,d\theta = \sec\theta + C$.

## The substitution rule (source: section 5.5 notes)

> **The Substitution Rule:** If $u = g(x)$ is a differentiable function whose range is an interval $I$ and $f$ is continuous on $I$, then

$$\int f(g(x))\,g'(x)\,dx = \int f(u)\,du$$

- Look for an inner function $u$ whose derivative is also a factor of the integrand (up to a constant). Write $du = g'(x)\,dx$, replace everything in terms of $u$, integrate, then put $x$ back.
- Definite integrals: change the limits to $u$-values, or keep $x$-limits, write them as $x = \ldots$, and substitute back before evaluating.

Examples (source: section 5.5 notes):
- $\int 2x\sqrt{1 + x^2}\,dx$: $u = 1 + x^2$, $du = 2x\,dx$, so $\int \sqrt{u}\,du = \frac{2}{3}(1 + x^2)^{3/2} + C$.
- $\int \tan x\,dx = \int \frac{\sin x}{\cos x}\,dx$: $u = \cos x$, so $-\ln\lvert\cos x\rvert + C = \ln\lvert\sec x\rvert + C$.
- $\int_0^4\sqrt{2x + 1}\,dx$: $u = 2x + 1$ runs from 1 to 9, so $\frac{1}{2}\int_1^9 u^{1/2}\,du = \frac{1}{3}\left[u^{3/2}\right]_1^9 = \frac{26}{3}$.

> **Integrals of Symmetric Functions:** Suppose that $f$ is continuous on $[-a, a]$. Then,
> 1. If $f$ is even ($f(-x) = f(x)$), then $\int_{-a}^{a} f(x)\,dx = 2\int_0^a f(x)\,dx$
> 2. If $f$ is odd ($f(-x) = -f(x)$), then $\int_{-a}^{a} f(x)\,dx = 0$

- Example (source): $\int_{-\pi/4}^{\pi/4}(x^3 + x^4\tan x)\,dx = 0$, since $x^3$ is odd and $x^4\tan x$ (even times odd) is odd.

## Do not forget

- Indefinite integrals need $+ C$; definite integrals are numbers and do not.
- FTC2 needs $f$ continuous on the whole of $[a, b]$.
- $\frac{d}{dx}\int_a^{h(x)} f(t)\,dt = f(h(x))\,h'(x)$: do not forget the chain rule factor.
- In a definite substitution, change the limits too.

## See also

- [[MAT01A1_Notes_S4_Derivatives]]
- [[MAT01A1_Notes_S1_Sigma_Inequalities_Trig_and_Complex_Numbers]]

---
*CDG v13 | written S5 | 2026-11-15*
