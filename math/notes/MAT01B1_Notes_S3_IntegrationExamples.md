---
module: MAT01B1
topic: Integration Technique Examples
session: S3
tags: [worked-example]
---

# Integration Technique Examples

Formulas referenced here live in [[MAT01B1_Notes_S2_DerivativeIntegralReference]], this file is examples only.

## Integration by Parts

**(added) Worked example (composite).** $\displaystyle\int x e^x\,dx$. By LIATE, the algebraic factor $x$ outranks the exponential, so $u=x$, $dv=e^x\,dx$, giving $du=dx$, $v=e^x$:
$$
\int xe^x\,dx = xe^x - \int e^x\,dx = xe^x - e^x + c.
$$

## Trig Substitution

**(added) Worked example (composite).** $\displaystyle\int \frac{dx}{\sqrt{9-x^2}}$. Matches $\sqrt{a^2-b^2x^2}$ with $a=3$, $b=1$, so $x=3\sin\theta$, $dx=3\cos\theta\,d\theta$, and $\sqrt{9-x^2}=\sqrt{9-9\sin^2\theta}=3\cos\theta$:
$$
\int \frac{3\cos\theta\,d\theta}{3\cos\theta} = \int d\theta = \theta + c.
$$
Reading the triangle back ($x=3\sin\theta \Rightarrow \sin\theta = x/3$), $\theta = \sin^{-1}(x/3)$, so the answer is $\sin^{-1}(x/3)+c$.

## Partial Fractions

**(added) Worked example (composite).** $\displaystyle\int \frac{3x+5}{(x-1)(x+2)}\,dx$. Denominator is two distinct linear factors, so
$$
\frac{3x+5}{(x-1)(x+2)} = \frac{A}{x-1} + \frac{B}{x+2}.
$$
Multiplying through: $3x+5 = A(x+2) + B(x-1)$. Setting $x=1$: $8=3A \Rightarrow A=\tfrac{8}{3}$. Setting $x=-2$: $-1=-3B \Rightarrow B=\tfrac{1}{3}$. So
$$
\int \frac{3x+5}{(x-1)(x+2)}\,dx = \frac{8}{3}\ln|x-1| + \frac{1}{3}\ln|x+2| + c.
$$

## $\sin^n x \cos^m x$

**(added) Worked example (composite), $n$ odd case.** $\displaystyle\int \sin^3x\cos^2x\,dx$. Strip one sine: $\sin^3x=\sin x(1-\cos^2x)$. Let $u=\cos x$, $du=-\sin x\,dx$:
$$
\int \sin x(1-\cos^2x)\cos^2x\,dx = -\int(1-u^2)u^2\,du = -\frac{u^3}{3}+\frac{u^5}{5}+c = -\frac{\cos^3x}{3}+\frac{\cos^5x}{5}+c.
$$

## $\tan^n x \sec^m x$

Genuinely the hardest of this group, three cases sit far enough apart to each need their own worked example.

**(added) Worked example (composite), $n$ odd case.** $\displaystyle\int \tan^3x\sec^3x\,dx$. Strip one tangent and one secant together: $\tan^3x\sec^3x = \tan^2x\sec^2x\cdot(\sec x\tan x) = (\sec^2x-1)\sec^2x\cdot(\sec x\tan x)$. Let $u=\sec x$, $du=\sec x\tan x\,dx$:
$$
\int (u^2-1)u^2\,du = \frac{u^5}{5}-\frac{u^3}{3}+c = \frac{\sec^5x}{5}-\frac{\sec^3x}{3}+c.
$$

**(added) Worked example (composite), $m$ even case.** $\displaystyle\int \tan^2x\sec^4x\,dx$. Strip two secants: $\sec^4x=\sec^2x\cdot\sec^2x=(1+\tan^2x)\sec^2x$. Let $u=\tan x$, $du=\sec^2x\,dx$:
$$
\int \tan^2x(1+\tan^2x)\sec^2x\,dx = \int u^2(1+u^2)\,du = \frac{u^3}{3}+\frac{u^5}{5}+c = \frac{\tan^3x}{3}+\frac{\tan^5x}{5}+c.
$$

**(added) Worked example (composite), $n$ even and $m$ odd case, via the reduction formula.** $\displaystyle\int \tan^2x\sec^3x\,dx$. Replace $\tan^2x=\sec^2x-1$:
$$
\int \tan^2x\sec^3x\,dx = \int \sec^5x\,dx - \int \sec^3x\,dx.
$$
Apply the reduction formula (see: [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products and quotients of trig functions]]) with $k=5$:
$$
\int \sec^5x\,dx = \frac{\sec^3x\tan x}{4} + \frac{3}{4}\int \sec^3x\,dx.
$$
So
$$
\int \tan^2x\sec^3x\,dx = \frac{\sec^3x\tan x}{4} - \frac{1}{4}\int \sec^3x\,dx = \frac{\sec^3x\tan x}{4} - \frac{1}{8}\Big(\sec x\tan x + \ln|\sec x+\tan x|\Big) + c,
$$
using the table value $\int \sec^3x\,dx = \tfrac{1}{2}(\sec x\tan x + \ln|\sec x+\tan x|)+c$.

## Miscellaneous: mixing and matching strategies

The hard part in practice isn't executing a single technique, it's recognising which one applies, and sometimes stacking two of them. Three examples, each turning on that recognition step rather than the mechanics.

**(added) Worked example (composite) 1, u-sub then Integration by Parts.** $\displaystyle\int x^3 e^{x^2}\,dx$. A first glance suggests IBP directly, but $e^{x^2}$ has no elementary antiderivative on its own, so IBP can't start yet. Split off one power of $x$ to build a substitution first: let $w=x^2$, $dw=2x\,dx$, rewriting $x^3e^{x^2}\,dx = x^2e^{x^2}\cdot x\,dx = w e^w \cdot \tfrac{1}{2}dw$:
$$
\int x^3e^{x^2}\,dx = \frac{1}{2}\int w e^w\,dw.
$$
*Now* it's the plain IBP example from above, $u=w$, $dv=e^w\,dw$:
$$
\frac{1}{2}\int we^w\,dw = \frac{1}{2}\big(we^w-e^w\big)+c = \frac{1}{2}e^{x^2}(x^2-1)+c.
$$
The tell: a lone power of $x$ sitting next to something whose derivative also produces an $x$ (here $2x$ from $x^2$) is a substitution first, not an immediate IBP candidate.

**(added) Worked example (composite) 2, trig identity vs trig substitution, telling them apart.** $\displaystyle\int \sin^2x\cos^3x\,dx$ next to $\displaystyle\int \frac{dx}{\sqrt{4-x^2}}$. Both involve trig, but only one is a trig substitution problem. The first has no square root and no algebraic expression under one, it's a plain product of trig functions with a whole number power ($m=3$ odd), so it's the $\sin^n\cos^m$ family above: strip a cosine, substitute $u=\sin x$. The second has $\sqrt{a^2-x^2}$ sitting under an integral with $x$ as the *variable*, not an angle, that's the actual trigger for trig substitution ($x=2\sin\theta$). The test that separates them: is the variable already an angle inside trig functions (identity/reduction territory), or is it an algebraic variable trapped under a root (substitution territory)?

**(added) Worked example (composite) 3, partial fractions vs trig substitution, telling them apart by the denominator.** $\displaystyle\int \frac{dx}{x^2-1}$ next to $\displaystyle\int \frac{dx}{\sqrt{x^2-1}}$. Nearly identical on sight, opposite methods. The first has no root, $x^2-1=(x-1)(x+1)$ factors cleanly over the rationals, so it's partial fractions: $\frac{1}{x^2-1}=\frac{1/2}{x-1}-\frac{1/2}{x+1}$, integrating to $\tfrac{1}{2}\ln\left|\frac{x-1}{x+1}\right|+c$. The second has a root over the same expression, which partial fractions cannot touch (there's no polynomial numerator over polynomial denominator here), so it needs the $\sqrt{b^2x^2-a^2}$ trig substitution, $x=\sec\theta$. The presence or absence of the root, not the expression underneath it, is what decides which shelf to reach for.

## See also
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S1_CalculusApplications]]
