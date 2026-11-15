---
module: MAT01A1
topic: Derivatives
session: S4
tags: [definition, theorem, formula, worked-example, exam-flagged, common-mistake, added]
---

# MAT01A1 Notes S4: Derivatives

Source: the Moodle lecture notes for Stewart sections 2.7, 2.8, 3.1 to 3.6, 3.11 and 4.4 (Parts 1 and 2), weeks 9 to 13. The handwritten proof PDFs in the Chapter 2.7 and 3.3 folders were not read; the proof outlines below follow the method the notes describe. Short revision notes, not from a teaching session.

Scope: the whole module was examined in the final (12 June 2026). Proofs flagged examinable by the notes: differentiable implies continuous, the product rule, the quotient rule, both special trig limits, and the derivatives of $\sin x$ and $\cos x$. Section 3.11 covers only p261 to Example 2 on p264 (no inverse hyperbolic functions). Sections 4.1 to 4.3, 4.5 and 4.7 belong to MAT01B1.

Checked: every derivative, limit and tangent line was checked in Python (SymPy) on 15 Nov 2026.

## The derivative at a point (source: section 2.7 notes)

> **Definition (The tangent line):** The tangent line to the curve $y = f(x)$ at the point $(a, f(a))$ is the line through $P(a, f(a))$ with slope

$$m = \lim_{x \to a} \frac{f(x) - f(a)}{x - a}$$

> provided that this limit exists.

> **Definition (The derivative):** The derivative of a function $f$ at a number $a$, denoted by $f'(a)$, is

$$f'(a) = \lim_{h \to 0} \frac{f(a + h) - f(a)}{h} = \lim_{x \to a} \frac{f(x) - f(a)}{x - a}$$

> if this limit exists.

- $f'(a)$ is the slope of the tangent at $(a, f(a))$. For a position function $s = f(t)$, $f'(a)$ is the instantaneous velocity $v(a)$, the limit of average velocities $\frac{f(a + h) - f(a)}{h}$.

Example (source: section 2.7 notes): tangent to $y = x^2 + 4x$ at $(4, 32)$.
   $f'(4) = \lim_{h \to 0} \frac{(4 + h)^2 + 4(4 + h) - 32}{h} = \lim_{h \to 0} (12 + h) = 12$, so $y = 12x - 16$.

## The derivative as a function (source: section 2.8 notes)

$$f'(x) = \lim_{h \to 0} \frac{f(x + h) - f(x)}{h} \qquad f'(x) = y' = \frac{dy}{dx} = \frac{df}{dx} = \frac{d}{dx}f(x) = Df(x) = D_x f(x)$$

- "Use first principles" or "use the definition" means this limit; otherwise the rules may be used.
- Second derivative $f'' = (f')' = \frac{d^2y}{dx^2}$, the rate of change of the slope. For $n \ge 4$ write $f^{(n)}$.

> **Theorem:** If a function $f$ is differentiable at $a$ then it is continuous at $a$. (Proof examinable.)

- Hypothesis: $f'(a)$ exists.
- Proof (added, standard; the lecturer's version is in "Differentiability implies continuity.pdf"): for $x \ne a$, $f(x) - f(a) = \frac{f(x) - f(a)}{x - a}\,(x - a)$. Taking $x \to a$ gives $f'(a) \cdot 0 = 0$, so $\lim_{x \to a} f(x) = f(a)$.
- The converse is false: $|x|$ is continuous at 0 but not differentiable there.
- A function fails to be differentiable at a corner ($|x|$ at 0), a discontinuity, or a vertical tangent ($\sqrt[3]{x}$ at 0).

Example (source: section 2.8 notes): $f(x) = x^2 - 2x$ for $x \ge 1$ and $x^2 - 4x + 2$ for $x < 1$. Show $f$ is continuous but not differentiable at 1.
   Both pieces give $-1$ at $x = 1$, so $f$ is continuous. The one-sided slopes are $2(1) - 2 = 0$ and $2(1) - 4 = -2$, which differ (a corner).

## Basic rules (source: section 3.1 notes)

$$\frac{d}{dx}(c) = 0 \qquad \frac{d}{dx}(x^n) = nx^{n-1} \ (n \in \mathbb{R}) \qquad \frac{d}{dx}[cf(x)] = c\frac{d}{dx}f(x) \qquad \frac{d}{dx}[f(x) \pm g(x)] = f'(x) \pm g'(x)$$

- Hypotheses: $c$ constant; $f$, $g$ differentiable. The power rule is proved here for $n \in \mathbb{Z}^+$ (using $x^n - a^n = (x - a)(x^{n-1} + x^{n-2}a + \cdots + a^{n-1})$, which gives $n$ terms each tending to $a^{n-1}$); the general version is proved in 3.6.
- The sum rule follows from the definition and Limit Law 1.

> **Definition:** $e$ is the number such that $\lim_{h \to 0} \frac{e^h - 1}{h} = 1$

$$\frac{d}{dx}(e^x) = e^x$$

- Why: $\frac{d}{dx}a^x = a^x \lim_{h \to 0}\frac{a^h - 1}{h} = a^x f'(0)$, and for $a = e$ that limit is 1.

## Product and quotient rules (source: section 3.2 notes)

> **The product rule:** If $f$ and $g$ are both differentiable, then

$$\frac{d}{dx}[f(x)g(x)] = f(x)\frac{d}{dx}g(x) + g(x)\frac{d}{dx}f(x) \qquad (fg)' = fg' + f'g$$

> **The quotient rule:**

$$\frac{d}{dx}\left[\frac{f(x)}{g(x)}\right] = \frac{g(x)\frac{d}{dx}[f(x)] - f(x)\frac{d}{dx}[g(x)]}{[g(x)]^2} \qquad \left(\frac{f}{g}\right)' = \frac{f'g - g'f}{g^2}$$

Proofs (source: section 3.2 notes, both examinable):
- Product: in the definition, add and subtract $f(x + h)g(x)$ in the numerator. Split into $f(x + h)\frac{g(x + h) - g(x)}{h} + g(x)\frac{f(x + h) - f(x)}{h}$, then use the limit laws and $\lim_{h \to 0} f(x + h) = f(x)$ ($f$ is continuous, being differentiable).
- Quotient: combine $\frac{f(x + h)}{g(x + h)} - \frac{f(x)}{g(x)}$ over the denominator $h\,g(x)g(x + h)$, add and subtract $f(x)g(x)$ in the numerator, split, and take limits (quotient, sum and product laws at once).

## Trigonometric derivatives (source: section 3.3 notes)

$$\lim_{\theta \to 0} \frac{\sin\theta}{\theta} = 1 \qquad \lim_{\theta \to 0} \frac{\cos\theta - 1}{\theta} = 0$$

Proofs (examinable):
- First limit (source): in the unit circle with $0 < \theta < \frac{\pi}{2}$, compare areas: big triangle $\frac{\tan\theta}{2}$ $\ge$ sector $\frac{\theta}{2}$ $\ge$ small triangle $\frac{\sin\theta}{2}$. Multiply by $\frac{2}{\sin\theta}$ to get $\frac{1}{\cos\theta} \ge \frac{\theta}{\sin\theta} \ge 1$, take reciprocals: $\cos\theta \le \frac{\sin\theta}{\theta} \le 1$. This also holds for $-\frac{\pi}{2} < \theta < 0$ (both sides are even). Squeeze: $\cos\theta \to 1$.
- Second limit (added, standard): multiply by $\frac{\cos\theta + 1}{\cos\theta + 1}$ to get $-\frac{\sin\theta}{\theta}\cdot\frac{\sin\theta}{\cos\theta + 1} \to -1 \cdot 0 = 0$.
- $\frac{d}{dx}\sin x$ (outline from the notes, steps added): $\frac{\sin(x + h) - \sin x}{h} = \sin x\,\frac{\cos h - 1}{h} + \cos x\,\frac{\sin h}{h} \to \sin x \cdot 0 + \cos x \cdot 1$. The same method gives $\cos x$.

| | | |
|---|---|---|
| $\frac{d}{dx}\sin x = \cos x$ | $\frac{d}{dx}\cos x = -\sin x$ | $\frac{d}{dx}\tan x = \sec^2 x$ |
| $\frac{d}{dx}\csc x = -\csc x\cot x$ | $\frac{d}{dx}\sec x = \sec x\tan x$ | $\frac{d}{dx}\cot x = -\csc^2 x$ |

- The last four come from the quotient rule. Derivatives of $\sin$ and $\cos$ repeat every 4, so $\frac{d^{27}}{dx^{27}}\cos x = \frac{d^3}{dx^3}\cos x = \sin x$.
- Limits: $\lim_{x \to 0}\frac{\sin 7x}{4x} = \frac{7}{4}\lim\frac{\sin 7x}{7x} = \frac{7}{4}$.

## The chain rule (source: section 3.4 notes)

> **The Chain Rule:** If $g$ is differentiable at $x$ and $f$ is differentiable at $g(x)$, then the composite function $F = f \circ g$ is differentiable at $x$ and $F'$ is given by the product

$$F'(x) = f'(g(x)) \cdot g'(x) \qquad \frac{dy}{dx} = \frac{dy}{du}\frac{du}{dx}$$

- Outside to inside: differentiate the outer function at the inner function, then multiply by the derivative of the inner function. Longer chains: $\frac{dy}{dt} = \frac{dy}{du}\frac{du}{dx}\frac{dx}{dt}$.

$$\frac{d}{dx}[g(x)]^n = n[g(x)]^{n-1}g'(x) \qquad \frac{d}{dx}(b^x) = b^x\ln b$$

- The second: $b^x = e^{(\ln b)x}$, then the chain rule.
- Example (source): $f(5) = 2$, $f'(6) = 8$, $g(3) = 6$, $g'(3) = 5$; then $F'(3) = f'(g(3))g'(3) = f'(6)(5) = 40$.

## Implicit differentiation and inverse trig derivatives (source: section 3.5 notes)

Steps: differentiate both sides with respect to $x$ (every $y$ term gets a factor $y'$ by the chain rule), collect the $y'$ terms on the left, factor out $y'$, solve.

Example (source: section 3.5 notes): for $x^3 + y^3 = 6xy$, find $y'$, the tangent at $(3, 3)$, and where the tangent is horizontal in quadrant 1.
   $3x^2 + 3y^2y' = 6y + 6xy'$, so $y' = \frac{2y - x^2}{y^2 - 2x}$. At $(3, 3)$: $y' = -1$, so $y = -x + 6$. Horizontal when $2y = x^2$: the point $(2^{4/3}, 2^{5/3})$.

- Inverse trig by implicit differentiation: $y = \cos^{-1}x \iff \cos y = x$ with $0 \le y \le \pi$, so $-\sin y\,y' = 1$ and $\sin y = \sqrt{1 - x^2}$ (positive on $[0, \pi]$).

$$\frac{d}{dx}\sin^{-1}x = \frac{1}{\sqrt{1 - x^2}} \qquad \frac{d}{dx}\cos^{-1}x = -\frac{1}{\sqrt{1 - x^2}} \qquad \frac{d}{dx}\tan^{-1}x = \frac{1}{1 + x^2}$$

$$\frac{d}{dx}\csc^{-1}x = -\frac{1}{x\sqrt{x^2 - 1}} \qquad \frac{d}{dx}\sec^{-1}x = \frac{1}{x\sqrt{x^2 - 1}} \qquad \frac{d}{dx}\cot^{-1}x = -\frac{1}{1 + x^2}$$

## Logarithmic functions (source: section 3.6 notes)

$$\frac{d}{dx}(\log_b x) = \frac{1}{x\ln b} \qquad \frac{d}{dx}(\ln x) = \frac{1}{x} \qquad \frac{d}{dx}(\ln|x|) = \frac{1}{x}$$

- From $b^y = x$ differentiated implicitly. With the chain rule: $\frac{d}{dx}\ln(x^3 + 1) = \frac{3x^2}{x^3 + 1}$.
- Logarithmic differentiation: take $\ln$ of both sides, simplify with the log laws, differentiate implicitly, solve for $y'$.

Derivative of $y = a^b$:
1. $a$, $b$ constants: $y' = 0$.
2. $a = f(x)$, $b$ constant: power and chain rule, $b[f(x)]^{b-1}f'(x)$.
3. $a$ constant, $b = g(x)$: $a^{g(x)}(\ln a)g'(x)$.
4. Both depend on $x$: logarithmic differentiation. $y = x^x$: $\ln y = x\ln x$, so $y' = x^x(\ln x + 1)$.

$$e = \lim_{x \to 0}(1 + x)^{1/x}$$

- From $f(x) = \ln x$ having $f'(1) = 1$, written as a limit, then the continuity of $e^x$.

## Hyperbolic functions (source: section 3.11 notes)

$$\sinh x = \frac{e^x - e^{-x}}{2} \quad \cosh x = \frac{e^x + e^{-x}}{2} \quad \tanh x = \frac{\sinh x}{\cosh x} \quad \text{csch}\,x = \frac{1}{\sinh x} \quad \text{sech}\,x = \frac{1}{\cosh x} \quad \coth x = \frac{\cosh x}{\sinh x}$$

- $\text{Ran}(\sinh) = (-\infty, \infty)$, $\text{Ran}(\cosh) = [1, \infty)$; $\cosh$ is the hanging chain shape. $\tanh x \to \pm 1$ as $x \to \pm\infty$.

$$\sinh(-x) = -\sinh x \quad \cosh(-x) = \cosh x \quad \cosh^2 x - \sinh^2 x = 1 \quad 1 - \tanh^2 x = \text{sech}^2 x$$

$$\sinh(x + y) = \sinh x\cosh y + \cosh x\sinh y \qquad \cosh(x + y) = \cosh x\cosh y + \sinh x\sinh y$$

- Proofs: substitute the definitions and expand. Note the $+$ in $\cosh(x + y)$, unlike $\cos(x + y)$.

| | | |
|---|---|---|
| $\frac{d}{dx}\sinh x = \cosh x$ | $\frac{d}{dx}\cosh x = \sinh x$ | $\frac{d}{dx}\tanh x = \text{sech}^2 x$ |
| $\frac{d}{dx}\text{csch}\,x = -\text{csch}\,x\coth x$ | $\frac{d}{dx}\text{sech}\,x = -\text{sech}\,x\tanh x$ | $\frac{d}{dx}\coth x = -\text{csch}^2 x$ |

- Unlike $\cos$, $\frac{d}{dx}\cosh x$ has no minus sign. Example: $\frac{d}{dx}\ln(\cosh x) = \tanh x$.

## L'Hospital's rule (source: section 4.4 notes, Parts 1 and 2)

> **L'Hospital's Rule:** Suppose $f$ and $g$ are differentiable and $g'(x) \ne 0$ when $x$ is near $a$. Suppose that $\lim_{x \to a} f(x) = 0$ and $\lim_{x \to a} g(x) = 0$ OR $\lim_{x \to a} f(x) = \pm\infty$ and $\lim_{x \to a} g(x) = \pm\infty$. Then

$$\lim_{x \to a} \frac{f(x)}{g(x)} = \lim_{x \to a} \frac{f'(x)}{g'(x)}$$

> if the RHS exists (or is $\infty$ or $-\infty$).

- Also for $x \to a^\pm$ and $x \to \pm\infty$, and may be used more than once. Differentiate top and bottom separately: this is not the quotient rule.
- Always check and name the indeterminate form, and mark where the rule is used.

| Type | What to do |
|---|---|
| $\frac{0}{0}$, $\frac{\infty}{\infty}$ | apply the rule directly |
| $0 \cdot \infty$ | write $fg = \frac{f}{1/g}$ or $\frac{g}{1/f}$; keep the harder reciprocal on top |
| $\infty - \infty$ | common denominator, rationalise or factorise into one fraction |
| $0^0$, $\infty^0$, $1^\infty$ | $y = f^g$, so $\ln y = g\ln f$; find $\lim \ln y$, then $\lim y = e^{\lim \ln y}$ |

Examples (source: section 4.4 notes):
- $\lim_{x \to 1}\frac{\ln x}{x - 1}$ ($\frac{0}{0}$) $= \lim_{x \to 1}\frac{1/x}{1} = 1$.
- $\lim_{x \to 0}\frac{\tan x - x}{x^3} = \frac{1}{3}$ ($\frac{0}{0}$, rule three times).
- $\lim_{x \to 0^+} x\ln x = \lim_{x \to 0^+}\frac{\ln x}{1/x}$ ($\frac{-\infty}{\infty}$) $= \lim_{x \to 0^+}\frac{1/x}{-1/x^2} = \lim_{x \to 0^+}(-x) = 0$.
- $\lim_{x \to 0^+} x^x$: $\ln y = x\ln x \to 0$, so the limit is $e^0 = 1$.
- $\lim_{x \to 0^+}(1 + \sin 4x)^{\cot x}$ ($1^\infty$): $\ln y = \frac{\ln(1 + \sin 4x)}{\tan x} \to \frac{4}{1} = 4$, so the limit is $e^4$.

## Do not forget

- Differentiable implies continuous, not the other way round ($|x|$ at 0).
- Chain rule: the outer derivative is evaluated at the inner function, then multiplied by the inner derivative.
- $\sin^{-1}x$ is $\arcsin x$, and its derivative is $\frac{1}{\sqrt{1 - x^2}}$; $\frac{d}{dx}\cosh x = +\sinh x$.
- For indeterminate powers, the limit of $\ln y$ is not the answer: exponentiate it.

## See also

- [[MAT01A1_Notes_S3_Functions_Limits_and_Continuity]]
- [[MAT01A1_Notes_S1_Sigma_Inequalities_Trig_and_Complex_Numbers]]

---
*CDG v13 | written S4 | 2026-11-15*
