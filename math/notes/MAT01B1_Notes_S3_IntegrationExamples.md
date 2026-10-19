---
module: MAT01B1
topic: Integration Technique Examples
session: S3
tags: [worked-example, formula, common-mistake]
---

# Integration Technique Examples

Formulas referenced here live in [[MAT01B1_Notes_S2_DerivativeIntegralReference]], this file is examples only.

## Integration by Parts

**(added) Worked example (composite).** $\displaystyle\int x e^x\,dx$. By LIATE, the algebraic factor $x$ outranks the exponential, so $u=x$, $dv=e^x\,dx$, giving $du=dx$, $v=e^x$:
$$
\int xe^x\,dx = xe^x - \int e^x\,dx = xe^x - e^x + c.
$$

### Worked examples from the lecture, section 7.1

**Worked example (source, §7.1), choosing $u$.** $\displaystyle\int x\sin x\,dx$. Take $u=x$, $dv=\sin x\,dx$, so $du=dx$, $v=-\cos x$:

$$
\int x\sin x\,dx=-x\cos x+\int\cos x\,dx=-x\cos x+\sin x+C.
$$

Differentiating the answer returns $x\sin x$, which is the quick check. <span style="color:#e03131">Wrong:</span> $u=\sin x$, $dv=x\,dx$ gives $\tfrac{x^2}{2}\sin x-\tfrac12\int x^2\cos x\,dx$, which is true but harder than the integral you started with. <span style="color:#2f9e44">Right:</span> pick $u$ so that $v\,du$ is simpler than $u\,dv$. #common-mistake

**Worked example (source, §7.1), a single function.** $\displaystyle\int\ln x\,dx$. Take $u=\ln x$, $dv=dx$, so $du=\frac{dx}{x}$, $v=x$:

$$
\int\ln x\,dx=x\ln x-\int dx=x\ln x-x+C.
$$

There is no real alternative here: $dv=\ln x\,dx$ would need $\int\ln x\,dx$, the problem itself.

**Worked example (source, §7.1), applying the rule twice.** $\displaystyle\int t^2e^t\,dt$. Take $u=t^2$, $dv=e^t\,dt$, so $du=2t\,dt$, $v=e^t$:

$$
\int t^2e^t\,dt=t^2e^t-2\int te^t\,dt.
$$

Again with $u=t$, $dv=e^t\,dt$: $\int te^t\,dt=te^t-e^t+C$. Substituting back,

$$
\int t^2e^t\,dt=t^2e^t-2te^t+2e^t+C.
$$

N.B $dv=t^2\,dt$ instead would raise the power of $t$ to $t^3$ and make the integral more complex (source).

**Worked example (source, §7.1), the integral comes back.** $\displaystyle\int e^x\sin x\,dx$. Take $u=e^x$, $dv=\sin x\,dx$, so $du=e^x\,dx$, $v=-\cos x$:

$$
\int e^x\sin x\,dx=-e^x\cos x+\int e^x\cos x\,dx.
$$

The new integral is no simpler but no harder. Apply the rule again with $u=e^x$, $dv=\cos x\,dx$: $\int e^x\cos x\,dx=e^x\sin x-\int e^x\sin x\,dx$. Substituting,

$$
\int e^x\sin x\,dx=-e^x\cos x+e^x\sin x-\int e^x\sin x\,dx.
$$

The original integral now appears on both sides, so solve for it:

$$
\int e^x\sin x\,dx=\tfrac12e^x(\sin x-\cos x)+C.
$$

N.B (added) Use $u=e^x$ both times. Swapping the roles in the second round undoes the first round and returns $\int e^x\sin x\,dx=\int e^x\sin x\,dx$, which says nothing.

**Worked example (source, §7.1), a definite integral.** $\displaystyle\int_0^1\tan^{-1}x\,dx$. Take $u=\tan^{-1}x$, $dv=dx$, so $du=\frac{dx}{1+x^2}$, $v=x$, and use the definite form of the formula:

$$
\int_0^1\tan^{-1}x\,dx=x\tan^{-1}x\Big|_0^1-\int_0^1\frac{x}{1+x^2}\,dx=\frac\pi4-\int_0^1\frac{x}{1+x^2}\,dx.
$$

For the leftover integral substitute $t=1+x^2$ (the letter $u$ is already taken), so $x\,dx=\tfrac12dt$, and the limits become $x=0\Rightarrow t=1$, $x=1\Rightarrow t=2$:

$$
\int_0^1\frac{x}{1+x^2}\,dx=\frac12\int_1^2\frac{dt}{t}=\frac12\ln2,\qquad\text{so}\qquad\int_0^1\tan^{-1}x\,dx=\frac\pi4-\frac{\ln2}{2}.
$$

N.B Once you substitute, change the limits too (source).

**Worked example (source, §7.1), a reduction formula.** For an integer $n\ge2$,

$$
\int\sin^nx\,dx=-\frac1n\cos x\sin^{n-1}x+\frac{n-1}{n}\int\sin^{n-2}x\,dx.
$$

Take $u=\sin^{n-1}x$, $dv=\sin x\,dx$, so $du=(n-1)\sin^{n-2}x\cos x\,dx$, $v=-\cos x$:

$$
\int\sin^nx\,dx=-\cos x\sin^{n-1}x+(n-1)\int\sin^{n-2}x\cos^2x\,dx.
$$

Replace $\cos^2x=1-\sin^2x$:

$$
\int\sin^nx\,dx=-\cos x\sin^{n-1}x+(n-1)\int\sin^{n-2}x\,dx-(n-1)\int\sin^nx\,dx.
$$

Move the last term to the left, where it combines with the original to give $n\int\sin^nx\,dx$:

$$
n\int\sin^nx\,dx=-\cos x\sin^{n-1}x+(n-1)\int\sin^{n-2}x\,dx,
$$

and dividing by $n$ gives the formula. (added) This is the same idea as the secant reduction formula derived in [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products and quotients of trig functions]].

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
