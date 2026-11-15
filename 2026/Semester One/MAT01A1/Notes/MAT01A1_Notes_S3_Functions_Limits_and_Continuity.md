---
module: MAT01A1
topic: Functions, Limits and Continuity
session: S3
tags: [definition, theorem, formula, worked-example, common-mistake, added]
---

# MAT01A1 Notes S3: Functions, Limits and Continuity

Source: the Moodle lecture notes for Stewart sections 1.1 to 1.5 and 2.1 to 2.6 (weeks 5 to 8). The notes pose most examples without answers, so the working is mine unless marked. Short revision notes, not from a teaching session.

Scope: the whole module was examined in the final (12 June 2026). For the precise definition of a limit, only linear functions are covered; the proofs of the limit laws (Appendix F) are not examinable.

Checked: every limit and worked answer was checked in Python (SymPy) on 15 Nov 2026.

## Functions (source: section 1.1 notes)

> A function $f$ is a rule which assigns to each element $x$ in a set $D$ exactly one element, $f(x)$, in a set $E$. The set $D$ is the domain of $f$. The range of $f$ is the set of all possible values of $f(x)$ as $x$ varies through the domain.

- Notation $\text{Dom}(f)$, $\text{Ran}(f)$. $x$ is the independent variable, $f(x)$ the dependent variable. The graph is $\{(x, f(x)) \mid x \in D\}$.
- Vertical line test: a curve is a function of $x$ if and only if no vertical line meets it more than once. $x^2 + y^2 = 4$ fails; $y = \sqrt{4 - x^2}$ passes.
- Domain hunting: no negative under an even root, no zero denominator. $\sqrt{x + 2}$ has domain $[-2, \infty)$; $\frac{1}{1 - 2\cos x}$ needs $\cos x \ne \frac{1}{2}$, so $x \ne \pm\frac{\pi}{3} + 2n\pi$.

> If a function $f$ satisfies $f(-x) = f(x)$ for all $x \in D$ then $f$ is an even function (symmetric about the $y$-axis). A function $f$ is odd if $f(-x) = -f(x)$ for all $x \in D$ (symmetric about the origin).

- Even: $x^2$, $|x|$, $\cos x$. Odd: $x^3$, $\sin x$. Neither: $x^2 + x$.
- If $f$ is odd and 0 is in its domain, then $f(0) = 0$. Proof: $f(0) = f(-0) = -f(0)$, so $2f(0) = 0$.

> A function $f$ is increasing on an interval $I$ if whenever $x_1 < x_2$, we have $f(x_1) < f(x_2)$. It is decreasing on $I$ if whenever $x_1 < x_2$, we have $f(x_1) > f(x_2)$.

## Essential functions (source: section 1.2 notes)

| Function | Form | Domain | Range |
|---|---|---|---|
| Power, $n$ even | $x^n$ | $\mathbb{R}$ | $[0, \infty)$ |
| Power, $n$ odd | $x^n$ | $\mathbb{R}$ | $\mathbb{R}$ |
| Sine, cosine | $\sin x$, $\cos x$ | $\mathbb{R}$ | $[-1, 1]$, period $2\pi$ |
| Tangent | $\tan x$ | $x \ne \frac{\pi}{2} + n\pi$, $n \in \mathbb{Z}$ | $\mathbb{R}$, period $\pi$ |
| Exponential | $a^x$, $a > 0$ | $\mathbb{R}$ | $(0, \infty)$ |
| Logarithmic | $\log_a x$, $a > 0$ | $(0, \infty)$ | $\mathbb{R}$ |

- Polynomial: $a_n x^n + \cdots + a_1 x + a_0$, degree $n$ if $a_n \ne 0$. Rational: $\frac{P(x)}{Q(x)}$ with $P$, $Q$ polynomials. Algebraic: built with $+, -, \times, \div$, powers and roots (every rational function is algebraic).
- Four ways to represent a function: in words, a table, a graph, a formula. A mathematical model describes a real-world problem with a function or equation.

## New functions from old (source: section 1.3 notes)

For $c > 0$: $f(x) + c$ shifts up, $f(x - c)$ shifts right, $f(x + c)$ shifts left. For $c > 1$: $c f(x)$ stretches vertically, $f(cx)$ squashes horizontally, $f(x/c)$ stretches horizontally. $-f(x)$ reflects in the $x$-axis; $f(-x)$ reflects in the $y$-axis.

- $\text{Dom}(f \pm g) = \text{Dom}(fg) = \text{Dom} f \cap \text{Dom} g$; for $\frac{f}{g}$, also need $g(x) \ne 0$.

> If $f(x)$ and $g(x)$ are functions, we consider the composite function defined for $x \in \mathbb{R}$ by $(f \circ g)(x) = f(g(x))$. Note, in general $f \circ g \ne g \circ f$.

$$\text{Dom}(f \circ g) = \text{Dom}(g) \cap \{x \in \mathbb{R} \mid g(x) \in \text{Dom}(f)\}$$

Example (source: section 1.3 notes): $f(x) = x^2$, $g(x) = x - 3$.
   $f \circ g = (x - 3)^2$ but $g \circ f = x^2 - 3$.

## Exponential functions (source: section 1.4 notes)

- $a^x$ with $a > 0$: built up from positive integers, $a^0 = 1$, rational powers $a^{p/q} = \sqrt[q]{a^p} = (\sqrt[q]{a})^p$, and irrational powers as the common bound of rational approximations.
- $a > 1$: increasing. $0 < a < 1$: decreasing. $a = 1$: constant. $(\frac{1}{b})^x = b^{-x}$ is $b^x$ reflected in the $y$-axis.

> **Laws of Exponents:** If $a$ and $b$ are positive numbers and $x$ and $y$ are any real numbers, then

$$a^x a^y = a^{x+y} \qquad \frac{a^x}{a^y} = a^{x-y} \qquad (a^x)^y = a^{xy} = (a^y)^x \qquad (ab)^x = a^x b^x$$

- $(a + b)^x \ne a^x + b^x$ in general.
- $e \approx 2.71828$ is the number for which the tangent to $y = e^x$ at $x = 0$ has gradient 1.

## Inverse functions and logarithms (source: section 1.5 notes)

> A function $f$ is called a one-to-one function if it never takes on the same value twice, that is, $f(x_1) \ne f(x_2)$ whenever $x_1 \ne x_2$. Equivalently (contrapositive), $f(x_1) = f(x_2)$ implies that $x_1 = x_2$.

- Horizontal line test: one-to-one if and only if no horizontal line meets the graph more than once. $x^3$ passes, $x^2$ fails.

> Let $f$ be a one-to-one function with domain $A$ and range $B$. Then its inverse function $f^{-1}$ has domain $B$ and range $A$ and is defined by $f^{-1}(y) = x \iff f(x) = y$ for any $y \in B$.

- $f^{-1}(x) \ne \frac{1}{f(x)}$. Cancellation: $f^{-1}(f(x)) = x$ on $A$ and $f(f^{-1}(x)) = x$ on $B$. The graph of $f^{-1}$ is $f$ reflected in $y = x$.
- To find $f^{-1}$: write $y = f(x)$, solve for $x$, then swap $x$ and $y$.

Example (source: section 1.5 notes): find the inverse of $f(x) = \frac{x - 2}{x + 2}$.
   $y(x + 2) = x - 2 \Rightarrow x(y - 1) = -2y - 2 \Rightarrow x = \frac{-2y - 2}{y - 1}$, so $f^{-1}(x) = \frac{-2x - 2}{x - 1}$.

> **Log laws:** If $x, y > 0$ then

$$\log_a(xy) = \log_a x + \log_a y \qquad \log_a\left(\frac{x}{y}\right) = \log_a x - \log_a y \qquad \log_a(x^r) = r\log_a x \ (r \in \mathbb{R})$$

- $\log_a 1 = 0$, $\log_a a = 1$, $\log_a a^x = x$, $a^{\log_a x} = x$. $\ln x = \log_e x$, so $\ln x = y \iff e^y = x$, $\ln(e^x) = x$, $e^{\ln x} = x$ for $x > 0$.

$$\log_a x = \frac{\ln x}{\ln a} \qquad (a > 0, \ a \ne 1)$$

Example (source: section 1.5 notes): solve $\log_{10} 5 + \log_{10}(5x + 1) = \log_{10}(x + 5) + 1$.
   $\log_{10}(25x + 5) = \log_{10}(10x + 50)$, so $15x = 45$ and $x = 3$ (both logs defined at 3).

Inverse trig functions (domains restricted so the function is one-to-one):

| | Input $t$ | Output $\theta$ |
|---|---|---|
| $\sin^{-1} t = \theta \iff \sin\theta = t$ | $[-1, 1]$ | $[-\frac{\pi}{2}, \frac{\pi}{2}]$ |
| $\cos^{-1} t = \theta \iff \cos\theta = t$ | $[-1, 1]$ | $[0, \pi]$ |
| $\tan^{-1} t = \theta \iff \tan\theta = t$ | $(-\infty, \infty)$ | $(-\frac{\pi}{2}, \frac{\pi}{2})$ |

- $\sin^{-1} x = \arcsin x$, not $\frac{1}{\sin x} = \csc x$. A trig function takes an angle and gives a ratio; an inverse trig function takes a ratio and gives an angle. Every inverse trig graph must pass the vertical line test.
- Examples: $\arcsin(-\frac{\sqrt{3}}{2}) = -\frac{\pi}{3}$. $\cos(\arcsin t) = \sqrt{1 - t^2}$, positive because $\arcsin t \in [-\frac{\pi}{2}, \frac{\pi}{2}]$.

## Limits and one-sided limits (source: sections 2.1 and 2.2 notes)

- Tangent and velocity problems both need a limit: the slope of secants $PQ$ as $Q \to P$. The tangent to $y = x^2$ at $(1, 1)$ has slope 2: $y = 2x - 1$.

> **Intuitive Definition of a Limit:** Suppose $f(x)$ is defined for $x$ near $a$. We write $\lim_{x \to a} f(x) = L$ and say "the limit of $f(x)$, as $x$ approaches $a$, equals $L$" if we can make the values of $f(x)$ as close to $L$ as we like by taking $x$ to be sufficiently close to $a$ (on either side of $a$), but not equal to $a$.

- "Near" means defined on an open interval around $a$, possibly not at $a$. The value $f(a)$ plays no part in the limit.
- Left-hand limit $\lim_{x \to a^-}$ uses only $x < a$; right-hand limit $\lim_{x \to a^+}$ uses only $x > a$.

$$\lim_{x \to a} f(x) = L \iff \lim_{x \to a^-} f(x) = L \text{ and } \lim_{x \to a^+} f(x) = L$$

- $\lim_{x \to a} f(x) = \infty$ means $f(x)$ can be made as large as we like by taking $x$ close to $a$, $x \ne a$. The limit still does not exist; $\infty$ is not a number.

> **Vertical Asymptotes:** The line $x = a$ is called a vertical asymptote of the curve $y = f(x)$ if at least one of the following statements is true: $\lim_{x \to a} f(x) = \pm\infty$, $\lim_{x \to a^-} f(x) = \pm\infty$, $\lim_{x \to a^+} f(x) = \pm\infty$.

- $f$ may still be defined at a vertical asymptote.

## Limit laws (source: section 2.3 notes)

> Suppose that $c$ is a constant and the limits $\lim_{x \to a} f(x)$ and $\lim_{x \to a} g(x)$ exist. Then:
> 1. $\lim [f(x) + g(x)] = \lim f(x) + \lim g(x)$
> 2. $\lim [f(x) - g(x)] = \lim f(x) - \lim g(x)$
> 3. $\lim [c f(x)] = c\lim f(x)$
> 4. $\lim [f(x)g(x)] = \lim f(x) \cdot \lim g(x)$
> 5. $\lim \frac{f(x)}{g(x)} = \frac{\lim f(x)}{\lim g(x)}$ if $\lim g(x) \ne 0$
> 6. $\lim [f(x)]^n = [\lim f(x)]^n$
> 7. $\lim c = c$
> 8. $\lim x = a$
> 9. $\lim x^n = a^n$ where $n \in \mathbb{Z}^+$
> 10. $\lim \sqrt[n]{x} = \sqrt[n]{a}$ where $n \in \mathbb{Z}^+$
> 11. $\lim \sqrt[n]{f(x)} = \sqrt[n]{\lim f(x)}$ ($n \in \mathbb{Z}^+$; if $n$ is even, assume $\lim f(x) \ge 0$)

> **Direct Substitution Property:** If $f$ is a polynomial or a rational function and $a$ is in the domain of $f$, then $\lim_{x \to a} f(x) = f(a)$.

> If $f(x) = g(x)$ when $x \ne a$, then $\lim_{x \to a} f(x) = \lim_{x \to a} g(x)$, provided that both limits exist.

- So cancel, then substitute: factorise, multiply by the conjugate radical, or use a common denominator.

> **Theorem:** If $f(x) \le g(x)$ when $x$ is near $a$ (except possibly at $a$) and the limits of $f$ and $g$ both exist as $x$ approaches $a$, then $\lim_{x \to a} f(x) \le \lim_{x \to a} g(x)$.

> **The Squeeze Theorem:** If $f(x) \le g(x) \le h(x)$ when $x$ is near $a$ (except possibly at $a$) and $\lim_{x \to a} f(x) = \lim_{x \to a} h(x) = L$, then $\lim_{x \to a} g(x) = L$.

Examples (source: section 2.3 notes):
- $\lim_{x \to 1} \frac{x^2 - 1}{x - 1} = \lim_{x \to 1} (x + 1) = 2$.
- $\lim_{h \to 0} \frac{(3 + h)^2 - 9}{h} = \lim_{h \to 0} (6 + h) = 6$.
- $\lim_{t \to 0} \frac{\sqrt{t^2 + 9} - 3}{t^2} = \lim_{t \to 0} \frac{1}{\sqrt{t^2 + 9} + 3} = \frac{1}{6}$ (conjugate).
- $\lim_{x \to 0} \frac{|x|}{x}$ does not exist: the right limit is 1, the left limit is $-1$.
- (composite) $-x^2 \le x^2\cos\frac{1}{x} \le x^2$ and both bounds go to 0, so $\lim_{x \to 0} x^2\cos\frac{1}{x} = 0$ by the Squeeze Theorem.

## The precise definition of a limit (source: section 2.4 notes)

> **Definition:** Let $f$ be a function defined on some open interval containing $a$ (except possibly at $a$ itself) and let $L \in \mathbb{R}$. We say that the limit of $f(x)$ as $x$ approaches $a$ is $L$, and write $\lim_{x \to a} f(x) = L$ if for every number $\varepsilon > 0$ there exists a $\delta > 0$ such that

$$|f(x) - L| < \varepsilon \quad \text{whenever} \quad 0 < |x - a| < \delta$$

- In words: the distance from $f(x)$ to $L$ can be made as small as we like by taking $x$ close enough to $a$ (but not equal to it).
- Two steps: (1) guess $\delta$ by working backwards from $|f(x) - L| < \varepsilon$ to a statement about $|x - a|$; (2) let $\varepsilon > 0$, assume $0 < |x - a| < \delta$, and work forwards to $|f(x) - L| < \varepsilon$.

Example (source: section 2.4 notes): prove $\lim_{x \to -2}(3x + 5) = -1$.
   Step 1: $|(3x + 5) + 1| < \varepsilon \iff |3(x + 2)| < \varepsilon \iff |x + 2| < \frac{\varepsilon}{3}$. Guess $\delta = \frac{\varepsilon}{3}$.
   Step 2: let $\varepsilon > 0$ and $0 < |x + 2| < \frac{\varepsilon}{3}$. Then $|3x + 6| < \varepsilon$, that is $|(3x + 5) - (-1)| < \varepsilon$.

> **Definition:** Let $f$ be a function defined on some open interval that contains $a$, except possibly at $a$ itself. Then $\lim_{x \to a} f(x) = \infty$ means that for every positive number $M$ there is a $\delta > 0$ such that if $0 < |x - a| < \delta$ then $f(x) > M$. (For $-\infty$: every negative $N$, and $f(x) < N$.)

- Example: for $\lim_{x \to 0} \frac{1}{x^2} = \infty$, take $\delta = \frac{1}{\sqrt{M}}$.

## Continuity (source: section 2.5 notes)

> **Definition:** A function $f$ is continuous at a number $a \in \mathbb{R}$ if $\lim_{x \to a} f(x) = f(a)$.

Three conditions: (1) $f(a)$ is defined, (2) $\lim_{x \to a} f(x)$ exists, (3) they are equal.

- Removable discontinuity: the limit exists but $f(a)$ is missing or wrong; redefine $f(a)$ to remove it. $\frac{x^2 - x - 2}{x - 2}$ at 2: define $f(2) = 3$.
- Infinite discontinuity: an infinite limit. Jump discontinuity: left and right limits differ (the greatest integer function $[\![x]\!]$ at every integer).

> **Definition:** A function $f$ is continuous from the right at $a$ if $\lim_{x \to a^+} f(x) = f(a)$, and continuous from the left at $a$ if $\lim_{x \to a^-} f(x) = f(a)$. A function $f$ is continuous on an interval if it is continuous at every number in the interval (one-sided at an endpoint).

> **Theorem:** If $f$ and $g$ are continuous at $a$ and $c$ is a constant, then $f + g$, $f - g$, $cf$, $fg$ and $\frac{f}{g}$ (if $g(a) \ne 0$) are also continuous at $a$.

> **Theorem:** The following types of functions are continuous at every number in their domains: polynomials, rational functions, root functions, trig functions, inverse trig functions, exponential functions, logarithmic functions.

> **Theorem:** If $f$ is continuous at $b$ and $\lim_{x \to a} g(x) = b$, then $\lim_{x \to a} f(g(x)) = f(b)$. In other words $\lim_{x \to a} f(g(x)) = f\left(\lim_{x \to a} g(x)\right)$.

> **Theorem:** If $g$ is continuous at $a$ and $f$ is continuous at $g(a)$, then the composite function $f \circ g$ given by $(f \circ g)(x) = f(g(x))$ is continuous at $a$.

> **The Intermediate Value Theorem:** Suppose that $f$ is continuous on the closed interval $[a, b]$ and let $N$ be any number between $f(a)$ and $f(b)$, where $f(a) \ne f(b)$. Then there exists a number $c \in (a, b)$ such that $f(c) = N$.

- Hypotheses: $f$ continuous on the closed interval $[a, b]$ (say why: what it is built from), $f(a) \ne f(b)$, $N$ between them. There may be more than one $c$.

Example (source: section 2.5 notes): find $a$, $b$ so that $f$ is continuous everywhere, where $f(x) = 2x + 8a$ for $x < 0$, $ax^2 - 4b$ for $0 \le x \le 2$, and $-3x + 18$ for $x > 2$.
   At 0: $8a = -4b$. At 2: $4a - 4b = 12$. So $a = 1$, $b = -2$.

Example (source: section 2.5 notes): show $4x^3 - 6x^2 + 3x - 2 = 0$ has a root in $(1, 2)$.
   $f$ is a polynomial, so continuous on $[1, 2]$. $f(1) = -1 < 0 < 12 = f(2)$, so by the IVT some $c \in (1, 2)$ has $f(c) = 0$.

## Limits at infinity (source: section 2.6 notes)

> Let $f$ be a function defined on some interval $(a, \infty)$. Then $\lim_{x \to \infty} f(x) = L$ means that the values of $f(x)$ can be made arbitrarily close to $L$ by requiring $x$ to be sufficiently large. (For $x \to -\infty$: defined on $(-\infty, a)$, $x$ a sufficiently large negative number.)

> **Definition:** the line $y = L$ is called a horizontal asymptote of the curve $y = f(x)$ if either $\lim_{x \to \infty} f(x) = L$ or $\lim_{x \to -\infty} f(x) = L$.

- A curve may touch or cross a horizontal asymptote ($\frac{\sin x}{x}$ crosses $y = 0$). $\lim_{x \to \pm\infty} \arctan x = \pm\frac{\pi}{2}$; $\lim_{x \to -\infty} e^x = 0$.
- The limit laws hold at $\pm\infty$, except Laws 9 and 10, and only when each limit used exists.

> **Theorem:** If $r > 0$ is rational, then $\lim_{x \to \infty} \frac{1}{x^r} = 0$. Also, if $r > 0$ is a rational number such that $x^r$ is defined for all $x$, then $\lim_{x \to -\infty} \frac{1}{x^r} = 0$.

- Method: divide top and bottom by the highest power of $x$ in the denominator (under a root, $\sqrt{x^4}$ counts as $x^2$). For $x < 0$, $\sqrt{x^2} = |x| = -x$, so $x = -\sqrt{x^2}$.
- Never "substitute $\infty$": $\infty - \infty$ is not 0. Use the conjugate radical instead.

> **Precise definitions:** $\lim_{x \to \infty} f(x) = L$ means that for every $\varepsilon > 0$ there exists a corresponding $N$ such that if $x > N$ then $|f(x) - L| < \varepsilon$. For $x \to -\infty$: if $x < N$ then $|f(x) - L| < \varepsilon$. $\lim_{x \to \infty} f(x) = \infty$ means that for every positive number $M$, there exists $N$ such that if $x > N$ then $f(x) > M$.

Examples (source: section 2.6 notes):
- $\lim_{x \to \infty} \frac{3x^2 - x - 2}{5x^2 + 4x + 1} = \frac{3}{5}$ (divide by $x^2$).
- $f(x) = \frac{\sqrt{2x^2 + 1}}{3x - 5}$: horizontal asymptotes $y = \frac{\sqrt{2}}{3}$ (as $x \to \infty$) and $y = -\frac{\sqrt{2}}{3}$ (as $x \to -\infty$, using $x = -\sqrt{x^2}$); vertical asymptote $x = \frac{5}{3}$.
- $\lim_{x \to \infty}(\sqrt{x^2 + 1} - x) = \lim_{x \to \infty} \frac{1}{\sqrt{x^2 + 1} + x} = 0$.

## Do not forget

- $\lim_{x \to a} f(x)$ ignores $f(a)$; continuity is exactly when the two agree.
- A limit of $\pm\infty$ means the limit does not exist.
- IVT needs continuity on the closed interval, stated with a reason, and $f(a) \ne f(b)$.
- For $x \to -\infty$ with roots: $\sqrt{x^2} = -x$.

## See also

- [[MAT01A1_Notes_S1_Sigma_Inequalities_Trig_and_Complex_Numbers]]
- [[MAT01A1_Notes_S2_Logic_and_Proof_Techniques]]

---
*CDG v13 | written S3 | 2026-11-15*
