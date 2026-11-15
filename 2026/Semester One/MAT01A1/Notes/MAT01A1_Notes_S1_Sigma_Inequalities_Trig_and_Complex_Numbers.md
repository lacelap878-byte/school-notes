---
module: MAT01A1
topic: Sigma Notation, Inequalities, Trigonometry and Complex Numbers
session: S1
tags: [definition, theorem, formula, worked-example, added]
---

# MAT01A1 Notes S1: Sigma Notation, Inequalities, Trigonometry and Complex Numbers

Source: the Moodle lecture notes for Stewart Appendix E, Appendix A, Appendix D and Complex Numbers (8th edition Appendix H), weeks 1 and 2; glanced at the two additional Monday lectures, which repeat this material with more examples. The notes pose examples without answers, so every worked answer here is mine. Short revision notes, not from a teaching session.

Scope: the whole module was examined in the final (12 June 2026). Complex exponentials (end of the Appendix H PDF) are not covered in MAT01A1.

Checked: every worked answer was checked in Python (SymPy) on 15 Nov 2026.

## Sigma notation (source: Appendix E notes)

> **Definition:** If $a_m, a_{m+1}, \ldots, a_n$ are real numbers and $m$ and $n$ are integers such that $m \le n$, then

$$\sum_{i=m}^{n} a_i = a_m + a_{m+1} + a_{m+2} + \cdots + a_{n-1} + a_n$$

> **Theorem:** If $c$ is any constant (it does not depend on $i$), then:

$$\sum_{i=m}^{n} c a_i = c\sum_{i=m}^{n} a_i \qquad \sum_{i=m}^{n} (a_i + b_i) = \sum_{i=m}^{n} a_i + \sum_{i=m}^{n} b_i \qquad \sum_{i=m}^{n} (a_i - b_i) = \sum_{i=m}^{n} a_i - \sum_{i=m}^{n} b_i$$

- Hypothesis: $c$ does not depend on $i$.
- Proof: expand the sum and factor out $c$; for the second, regroup using the associative and commutative laws.

> **Theorem:** Let $c$ be a constant and $n$ a positive integer. Then:

$$\sum_{i=1}^{n} 1 = n \qquad \sum_{i=1}^{n} c = nc \qquad \sum_{i=1}^{n} i = \frac{n(n+1)}{2}$$

$$\sum_{i=1}^{n} i^2 = \frac{n(n+1)(2n+1)}{6} \qquad \sum_{i=1}^{n} i^3 = \left[\frac{n(n+1)}{2}\right]^2$$

- Proofs use a telescoping sum: a sum that looks long but collapses, because each term cancels part of the next. For $\sum i^2$ (added, the notes leave the working to the lecture), add up $(1 + i)^3 - i^3 = 3i^2 + 3i + 1$ for $i = 1$ to $n$; the left side collapses to $(1 + n)^3 - 1$, then solve for $\sum i^2$.

Example (source: Appendix E notes)
Find $\displaystyle\lim_{n \to \infty} \sum_{i=1}^{n} \frac{3}{n}\left[\left(\frac{i}{n}\right)^2 + 1\right]$.

WORKING
$= \lim \left[\dfrac{3}{n^3}\sum i^2 + \dfrac{3}{n}\sum 1\right] = \lim \left[\dfrac{3}{n^3}\cdot\dfrac{n(n+1)(2n+1)}{6} + 3\right] = \lim \left[\dfrac{(n+1)(2n+1)}{2n^2} + 3\right] = 1 + 3 = 4$.

## Numbers, sets and intervals (source: Appendix A notes)

- $\mathbb{N} = \{0, 1, 2, \ldots\}$ (these notes include 0), $\mathbb{Z}$ the integers, $\mathbb{Q}$ the rationals $\frac{m}{n}$ with $m, n \in \mathbb{Z}$ and $n \ne 0$, $\mathbb{R}$ the rationals together with the irrationals ($\sqrt{2}$, $\pi$, $\log_{10} 2$). $\mathbb{N} \subseteq \mathbb{Z} \subseteq \mathbb{Q} \subseteq \mathbb{R} \subseteq \mathbb{C}$.
- A rational number has a repeating decimal; an irrational number does not.
- $a < b$ means $b - a$ is positive.
- Sets: $a \in S$ (element of), $A \cup B$ (in $A$ or $B$ or both), $A \cap B$ (in both), $A \subseteq B$ (every element of $A$ is in $B$). The empty set $\emptyset$ is a subset of every set. Set-builder: $\{x \in \mathbb{Z} \mid 0 < x < 7\}$.
- Intervals: round bracket excludes the endpoint (open dot), square bracket includes it (solid dot). $(a, b) = \{x \in \mathbb{R} \mid a < x < b\}$, $[a, b] = \{x \in \mathbb{R} \mid a \le x \le b\}$, $(a, \infty) = \{x \in \mathbb{R} \mid x > a\}$. $\infty$ is not a number, so it always gets a round bracket.

## Inequalities (source: Appendix A notes)

Rules for inequalities:
> 1. If $a < b$, then $a + c < b + c$.
> 2. If $a < b$ and $c < d$, then $a + c < b + d$.
> 3. If $a < b$ and $c > 0$, then $ac < bc$.
> 4. If $a < b$ and $c < 0$, then $ac > bc$.
> 5. If $0 < a < b$, then $\frac{1}{a} > \frac{1}{b}$.

- Polynomial or rational inequality: get 0 on one side, factor, find where each factor is 0, and use a sign table.

> [!warning] Never multiply by an expression whose sign you do not know (added)
> For $\frac{x-1}{x-4} > 1$, multiplying by $x - 4$ breaks rule 4 when $x < 4$. Subtract 1 instead: $\frac{x - 1}{x - 4} - 1 = \frac{3}{x - 4} > 0$, so $x > 4$.

Example (source: Appendix A notes): solve $x^3 + 3x^2 > 4x$.
   $x(x + 4)(x - 1) > 0$. Sign table on $-4, 0, 1$: the solution is $(-4, 0) \cup (1, \infty)$.

## Absolute values (source: Appendix A notes)

$$|a| = \begin{cases} a & \text{if } a \ge 0 \\ -a & \text{if } a < 0 \end{cases}$$

$|a|$ is the distance from $a$ to 0, so $|a| \ge 0$. Since $\sqrt{\ }$ means the positive square root, $\sqrt{a^2} = |a|$ for all $a$ (not $a$).

> **Properties:** Suppose $a$ and $b$ are any real numbers and $n$ is an integer. Then:
> 1. $|ab| = |a||b|$
> 2. $\left|\frac{a}{b}\right| = \frac{|a|}{|b|}$ ($b \ne 0$)
> 3. $|a^n| = |a|^n$
>
> Suppose $a > 0$. Then:
> 4. $|x| = a$ if and only if $x = \pm a$
> 5. $|x| < a$ if and only if $-a < x < a$
> 6. $|x| > a$ if and only if $x > a$ or $x < -a$

> **The Triangle Inequality:** If $a$ and $b$ are any real numbers, then $|a + b| \le |a| + |b|$.

Example (source: Appendix A notes): solve $|2x + 3| \ge 5$.
   $2x + 3 \ge 5$ or $2x + 3 \le -5$, so $x \ge 1$ or $x \le -4$.

Example (source: Appendix A notes): if $|x - 4| < 0.1$ and $|y - 7| < 0.2$, estimate $|(x + y) - 11|$.
   $|(x - 4) + (y - 7)| \le |x - 4| + |y - 7| < 0.1 + 0.2 = 0.3$.

## Radians (source: Appendix D notes)

$$\theta = \frac{a}{r} \qquad a = r\theta$$

$a$ is the arc length and $r$ the radius; valid only when $\theta$ is in radians.

- $360^\circ = 2\pi$ radians, so $1^\circ = \frac{\pi}{180}$ radians and 1 radian $= \frac{180}{\pi} \approx 57.3^\circ$.
- Common angles: $30^\circ = \frac{\pi}{6}$, $45^\circ = \frac{\pi}{4}$, $60^\circ = \frac{\pi}{3}$, $90^\circ = \frac{\pi}{2}$, $120^\circ = \frac{2\pi}{3}$, $135^\circ = \frac{3\pi}{4}$, $180^\circ = \pi$, $270^\circ = \frac{3\pi}{2}$.
- Positive angles turn anticlockwise from the positive $x$-axis, negative angles clockwise.

## Trigonometric functions (source: Appendix D notes)

For a point $P(x, y)$ at distance $r$ from the origin, at angle $\theta$:

$$\sin\theta = \frac{y}{r} \quad \cos\theta = \frac{x}{r} \quad \tan\theta = \frac{y}{x} \quad \csc\theta = \frac{r}{y} \quad \sec\theta = \frac{r}{x} \quad \cot\theta = \frac{x}{y}$$

- Signs (CAST): all positive in quadrant 1, sin in 2, tan in 3, cos in 4.
- Special triangles: sides $1, 1, \sqrt{2}$ for $\frac{\pi}{4}$; sides $1, \sqrt{3}, 2$ for $\frac{\pi}{6}$ and $\frac{\pi}{3}$.
- Graphs: $-1 \le \sin x \le 1$ and $|\cos x| \le 1$, both with period $2\pi$. $\tan x$ has vertical asymptotes at $x = \pm\frac{\pi}{2}$ and passes through $(\frac{\pi}{4}, 1)$. $\csc x$ and $\sec x$ are undefined where $\sin x$ or $\cos x$ is 0; $\cot x = 0$ wherever $\tan x$ has an asymptote.

Example (source: Appendix D notes): exact ratios for $\theta = \frac{2\pi}{3}$.
   Quadrant 2, reference angle $\frac{\pi}{3}$: $\sin = \frac{\sqrt{3}}{2}$, $\cos = -\frac{1}{2}$, $\tan = -\sqrt{3}$.

## Trigonometric identities (source: Appendix D notes)

$$\csc\theta = \frac{1}{\sin\theta} \quad \sec\theta = \frac{1}{\cos\theta} \quad \tan\theta = \frac{\sin\theta}{\cos\theta} \quad \cot\theta = \frac{1}{\tan\theta} = \frac{\cos\theta}{\sin\theta}$$

$$\sin^2\theta + \cos^2\theta = 1 \qquad \tan^2\theta + 1 = \sec^2\theta \qquad 1 + \cot^2\theta = \csc^2\theta$$

- The first comes from $x^2 + y^2 = r^2$; divide it by $\cos^2\theta$ or $\sin^2\theta$ for the other two.

$$\sin(x \pm y) = \sin x\cos y \pm \cos x\sin y \qquad \cos(x \pm y) = \cos x\cos y \mp \sin x\sin y$$

$$\sin 2x = 2\sin x\cos x \qquad \cos 2x = \cos^2 x - \sin^2 x = 2\cos^2 x - 1 = 1 - 2\sin^2 x$$

$$\cos^2 x = \frac{1 + \cos 2x}{2} \qquad \sin^2 x = \frac{1 - \cos 2x}{2}$$

- The minus versions come from $\sin(-\theta) = -\sin\theta$ and $\cos(-\theta) = \cos\theta$.
- To prove an identity, work on the left side and the right side separately; never move terms across.

Example (source: Appendix D notes): find all $x \in [0, 2\pi]$ with $\sin x = \sin 2x$.
   $\sin x - 2\sin x\cos x = \sin x(1 - 2\cos x) = 0$. So $\sin x = 0$ ($x = 0, \pi, 2\pi$) or $\cos x = \frac{1}{2}$ ($x = \frac{\pi}{3}, \frac{5\pi}{3}$).

## Complex numbers, rectangular form (source: Complex Numbers notes)

$$z = a + bi \qquad a, b \in \mathbb{R}, \quad i^2 = -1$$

$a$ is the real part, $b$ the imaginary part; $z$ is the point $(a, b)$ in the complex (Argand) plane.

- Add or subtract real and imaginary parts separately. Multiply out and use $i^2 = -1$: $(a + bi)(c + di) = (ac - bd) + (ad + bc)i$.
- Conjugate $\bar{z} = a - bi$ (reflection in the real axis). Divide by multiplying top and bottom by the conjugate of the bottom:

$$\frac{a + bi}{c + di} = \frac{ac + bd}{c^2 + d^2} + \frac{bc - ad}{c^2 + d^2}\,i$$

- $\overline{z + w} = \bar{z} + \bar{w}$, $\overline{zw} = \bar{z}\,\bar{w}$, $\overline{z^n} = \bar{z}^n$.
- Modulus $|z| = \sqrt{a^2 + b^2}$, the distance from the origin, and $z\bar{z} = |z|^2$.
- With $\sqrt{-y} = \sqrt{y}\,i$ for $y > 0$, the quadratic formula always works. $x^2 + x + 1 = 0$ gives $x = -\frac{1}{2} \pm \frac{\sqrt{3}}{2}i$.

> **Theorem (Fundamental Theorem of Algebra):** Every polynomial of degree $n$ has $n$ complex roots.

- Hypothesis: degree $n$. The roots may repeat ($x^2 = 0$ has the root 0 twice).

## Complex numbers, polar form (source: Complex Numbers notes)

$$z = r(\cos\theta + i\sin\theta) \qquad r = |z| = \sqrt{a^2 + b^2}, \quad \tan\theta = \frac{b}{a}$$

$\theta = \arg(z)$ is the argument. It is not unique: $\theta + 2k\pi$ works for any $k \in \mathbb{Z}$.

- Plot $z$ before choosing $\theta$: $\tan\theta = \frac{b}{a}$ has two solutions in $[0, 2\pi]$. For $z = -1 - i$, $\tan\theta = 1$ but $\theta = \frac{5\pi}{4}$, not $\frac{\pi}{4}$ (third quadrant).
- Multiply: multiply the moduli and add the arguments. Divide: divide the moduli and subtract the arguments.

$$z_1 z_2 = r_1 r_2\left[\cos(\theta_1 + \theta_2) + i\sin(\theta_1 + \theta_2)\right] \qquad \frac{z_1}{z_2} = \frac{r_1}{r_2}\left[\cos(\theta_1 - \theta_2) + i\sin(\theta_1 - \theta_2)\right]$$

- Proof of the product: multiply out, use $i^2 = -1$, then the addition formulas for $\cos$ and $\sin$.

> **De Moivre's Theorem:** For $z = r(\cos\theta + i\sin\theta)$ and $n \in \mathbb{Z}^+$

$$z^n = r^n(\cos n\theta + i\sin n\theta)$$

> **Roots:** Let $z = r(\cos\theta + i\sin\theta)$ and let $n$ be any positive integer. Then $z$ has $n$ distinct $n$th roots. For $k = 0, 1, 2, \ldots, n - 1$ the roots are

$$w_k = r^{1/n}\left[\cos\left(\frac{\theta + 2k\pi}{n}\right) + i\sin\left(\frac{\theta + 2k\pi}{n}\right)\right]$$

- All roots lie on the circle of radius $r^{1/n}$. The first has argument $\frac{\theta}{n}$; each next one is rotated $\frac{2\pi}{n}$ anticlockwise. $k = n$ just repeats $w_0$.

Example (source: Complex Numbers notes): find $(1 + \sqrt{3}i)^4$.
   $r = 2$, $\theta = \frac{\pi}{3}$, so $2^4\left(\cos\frac{4\pi}{3} + i\sin\frac{4\pi}{3}\right) = 16\left(-\frac{1}{2} - \frac{\sqrt{3}}{2}i\right) = -8 - 8\sqrt{3}i$.

Example (source: Complex Numbers notes): find the cube roots of $z = i$.
   $r = 1$, $\theta = \frac{\pi}{2}$, arguments $\frac{\pi}{6}, \frac{5\pi}{6}, \frac{3\pi}{2}$: $w_0 = \frac{\sqrt{3}}{2} + \frac{1}{2}i$, $w_1 = -\frac{\sqrt{3}}{2} + \frac{1}{2}i$, $w_2 = -i$.

## Do not forget

- $\sqrt{a^2} = |a|$, not $a$.
- Multiplying an inequality by a negative number reverses it; never multiply by an expression of unknown sign.
- Radians in every formula from now on; $a = r\theta$ needs radians.
- Plot $z$ before finding $\arg(z)$; an $n$th root question always has $n$ answers.

---
*CDG v13 | written S1 | 2026-11-15*
