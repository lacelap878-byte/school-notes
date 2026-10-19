---
module: MAT01B1
topic: Derivative and Integral Reference
session: S2
tags: [formula, definition]
---

# Derivative and Integral Reference

Source: Common Derivatives and Integrals (Paul Dawkins, Lamar University), reference sheet. Kept in the same concise table style as the original. Anything filled in beyond the source is marked `(added)`.

## Derivatives

### Basic properties

$$
\frac{d}{dx}\big[c f(x)\big] = c f'(x), \quad c \text{ any constant}
$$
$$
\frac{d}{dx}\big[f(x) \pm g(x)\big] = f'(x) \pm g'(x)
$$
$$
\frac{d}{dx}\big[x^n\big] = n x^{n-1}, \quad n \text{ any number}
$$
$$
\frac{d}{dx}\big[c\big] = 0, \quad c \text{ any constant}
$$
$$
\big[f(x)g(x)\big]' = f'(x)g(x) + f(x)g'(x) \quad \text{(Product Rule)}
$$
$$
\frac{d}{dx}\big[e^{g(x)}\big] = g'(x)e^{g(x)}
$$
$$
\left[\frac{f(x)}{g(x)}\right]' = \frac{f'(x)g(x) - f(x)g'(x)}{g(x)^2} \quad \text{(Quotient Rule)}
$$
$$
\frac{d}{dx}\ln\big(g(x)\big) = \frac{g'(x)}{g(x)}
$$
$$
\frac{d}{dx}\Big[f\big(g(x)\big)\Big] = f'\big(g(x)\big)\, g'(x) \quad \text{(Chain Rule)}
$$

> [!note] (added) Reading the Chain Rule
> $g(x)$ is called the **inner function** and $f$ the **outer function**. "Derivative of the outer, evaluated at the inner, times derivative of the inner" is the phrase worth keeping. Every one of the rules below that has a plain $x$ version and a $g(x)$ version (e.g. $\sin(x)$ vs a general $\sin(g(x))$ pattern) is just the Chain Rule applied to that basic derivative.

### Polynomials

$$
\frac{d}{dx}[c] = 0, \qquad \frac{d}{dx}[x] = 1, \qquad \frac{d}{dx}[cx] = c
$$
$$
\frac{d}{dx}\big[x^n\big] = n x^{n-1}, \qquad \frac{d}{dx}\big[cx^n\big] = ncx^{n-1}
$$

### Trig functions

$$
\frac{d}{dx}[\sin x] = \cos x \qquad \frac{d}{dx}[\cos x] = -\sin x
$$
$$
\frac{d}{dx}[\tan x] = \sec^2 x \qquad \frac{d}{dx}[\csc x] = -\csc x \cot x
$$
$$
\frac{d}{dx}[\sec x] = \sec x \tan x \qquad \frac{d}{dx}[\cot x] = -\csc^2 x
$$

> [!note] (added) Pattern worth noticing
> Every "co" function (cosine, cosecant, cotangent) has a derivative with a minus sign. That's the fastest way to check you haven't swapped a sign under exam pressure.

### Inverse trig functions

$$
\frac{d}{dx}\big[\sin^{-1}x\big] = \frac{1}{\sqrt{1-x^2}} \qquad \frac{d}{dx}\big[\cos^{-1}x\big] = -\frac{1}{\sqrt{1-x^2}}
$$
$$
\frac{d}{dx}\big[\tan^{-1}x\big] = \frac{1}{1+x^2} \qquad \frac{d}{dx}\big[\cot^{-1}x\big] = -\frac{1}{1+x^2}
$$
$$
\frac{d}{dx}\big[\sec^{-1}x\big] = \frac{1}{|x|\sqrt{x^2-1}} \qquad \frac{d}{dx}\big[\csc^{-1}x\big] = -\frac{1}{|x|\sqrt{x^2-1}}
$$

> [!note] (added) $\sin^{-1}x$ means arcsine
> $\sin^{-1}x$ (also written $\arcsin x$) is the **inverse sine function**: the angle whose sine is $x$. It is not $\frac{1}{\sin x}$, that would be written $\csc x$ or $(\sin x)^{-1}$. Same convention for all six inverse trig functions above.
>
> Full derivations of all six are in [[MAT01B1_Proofs_ST1#Derivatives of inverse trig functions (added, absent from the source entirely)|derivatives of inverse trig functions]].

### Exponential and logarithm functions

$$
\frac{d}{dx}\big[a^x\big] = a^x \ln(a) \qquad \frac{d}{dx}\big[e^x\big] = e^x
$$
$$
\frac{d}{dx}\big[\ln x\big] = \frac{1}{x}, \; x>0 \qquad \frac{d}{dx}\big[\ln|x|\big] = \frac{1}{x}, \; x \ne 0
$$
$$
\frac{d}{dx}\big[\log_a x\big] = \frac{1}{x \ln a}, \; x>0
$$

### Hyperbolic functions

$$
\frac{d}{dx}[\sinh x] = \cosh x \qquad \frac{d}{dx}[\cosh x] = \sinh x
$$
$$
\frac{d}{dx}[\tanh x] = \operatorname{sech}^2 x \qquad \frac{d}{dx}[\operatorname{csch} x] = -\operatorname{csch} x \coth x
$$
$$
\frac{d}{dx}[\operatorname{sech} x] = -\operatorname{sech} x \tanh x \qquad \frac{d}{dx}[\coth x] = -\operatorname{csch}^2 x
$$

> [!note] (added) Hyperbolic functions, in one line
> $\sinh x = \dfrac{e^x - e^{-x}}{2}$ and $\cosh x = \dfrac{e^x + e^{-x}}{2}$, built from $e^x$ directly, which is why none of their derivatives carry a minus sign the way the "co" trig functions do (except $\operatorname{sech}$ and $\operatorname{csch}$'s derivatives, by direct analogy with $\sec$ and $\csc$).

### Inverse hyperbolic functions (added, absent from the source entirely)

$$
\sinh^{-1}x = \ln\!\left(x+\sqrt{x^2+1}\right), \; x \in \mathbb{R} \qquad \frac{d}{dx}\big[\sinh^{-1}x\big] = \frac{1}{\sqrt{x^2+1}}
$$
$$
\cosh^{-1}x = \ln\!\left(x+\sqrt{x^2-1}\right), \; x \ge 1 \qquad \frac{d}{dx}\big[\cosh^{-1}x\big] = \frac{1}{\sqrt{x^2-1}}, \; x>1
$$
$$
\tanh^{-1}x = \frac{1}{2}\ln\!\left(\frac{1+x}{1-x}\right), \; |x|<1 \qquad \frac{d}{dx}\big[\tanh^{-1}x\big] = \frac{1}{1-x^2}, \; |x|<1
$$
$$
\coth^{-1}x = \frac{1}{2}\ln\!\left(\frac{x+1}{x-1}\right), \; |x|>1 \qquad \frac{d}{dx}\big[\coth^{-1}x\big] = \frac{1}{1-x^2}, \; |x|>1
$$
$$
\operatorname{sech}^{-1}x = \ln\!\left(\frac{1}{x}+\sqrt{\frac{1}{x^2}-1}\right), \; 0<x\le1 \qquad \frac{d}{dx}\big[\operatorname{sech}^{-1}x\big] = -\frac{1}{x\sqrt{1-x^2}}, \; 0<x<1
$$
$$
\operatorname{csch}^{-1}x = \ln\!\left(\frac{1}{x}+\sqrt{\frac{1}{x^2}+1}\right), \; x\ne0 \qquad \frac{d}{dx}\big[\operatorname{csch}^{-1}x\big] = -\frac{1}{|x|\sqrt{x^2+1}}, \; x\ne0
$$

> [!note] (added) Same formula, two different domains
> $\tanh^{-1}x$ and $\coth^{-1}x$ have the identical derivative formula $\frac{1}{1-x^2}$, the split is entirely in where each is defined: $\tanh^{-1}$ lives strictly inside $(-1,1)$, $\coth^{-1}$ strictly outside $[-1,1]$. Neither one covers $|x|=1$, where both blow up.
>
> Full derivations of all six are in [[MAT01B1_Proofs_ST1#Derivatives of inverse hyperbolic functions (added, absent from the source entirely)|derivatives of inverse hyperbolic functions]].

## Integrals

### Basic properties

$$
\int cf(x)\,dx = c\int f(x)\,dx, \quad c \text{ constant}
$$
$$
\int \big[f(x) \pm g(x)\big]\,dx = \int f(x)\,dx \pm \int g(x)\,dx
$$
$$
\int_a^b f(x)\,dx = F(x)\Big|_a^b = F(b) - F(a), \quad \text{where } F(x) = \int f(x)\,dx
$$
$$
\int_a^b cf(x)\,dx = c\int_a^b f(x)\,dx \qquad \int_a^b \big[f(x)\pm g(x)\big]\,dx = \int_a^b f(x)\,dx \pm \int_a^b g(x)\,dx
$$
$$
\int_a^a f(x)\,dx = 0 \qquad \int_a^b f(x)\,dx = -\int_b^a f(x)\,dx
$$
$$
\int_a^b f(x)\,dx = \int_a^c f(x)\,dx + \int_c^b f(x)\,dx \qquad \int_a^b c\,dx = c(b-a)
$$

If $f(x) \ge 0$ on $[a,b]$ then $\displaystyle\int_a^b f(x)\,dx \ge 0$.
If $f(x) \ge g(x)$ on $[a,b]$ then $\displaystyle\int_a^b f(x)\,dx \ge \int_a^b g(x)\,dx$.

### Polynomials

$$
\int dx = x + c \qquad \int k\,dx = kx + c \qquad \int x^n\,dx = \frac{1}{n+1}x^{n+1} + c, \; n \ne -1
$$
$$
\int \frac{1}{x}\,dx = \ln|x| + c \qquad \int \frac{1}{ax+b}\,dx = \frac{1}{a}\ln|ax+b| + c
$$
$$
\int x^{p/q}\,dx = \frac{q}{p+q}x^{\frac{p+q}{q}} + c
$$

### Trig functions

$$
\int \cos u\,du = \sin u + c \qquad \int \sin u\,du = -\cos u + c
$$
$$
\int \sec^2 u\,du = \tan u + c \qquad \int \csc^2 u\,du = -\cot u + c
$$
$$
\int \sec u \tan u\,du = \sec u + c \qquad \int \csc u \cot u\,du = -\csc u + c
$$
$$
\int \tan u\,du = \ln|\sec u| + c \qquad \int \cot u\,du = \ln|\sin u| + c
$$
$$
\int \sec u\,du = \ln|\sec u + \tan u| + c \qquad \int \csc u\,du = \ln|\csc u - \cot u| + c
$$
$$
\int \sec^3 u\,du = \tfrac{1}{2}\big(\sec u \tan u + \ln|\sec u + \tan u|\big) + c
$$
$$
\int \csc^3 u\,du = \tfrac{1}{2}\big(-\csc u \cot u + \ln|\csc u - \cot u|\big) + c
$$

> [!note] (added) Where $\int \tan u\,du = \ln|\sec u|+c$ actually comes from
> Write $\tan u = \dfrac{\sin u}{\cos u}$ and substitute $w = \cos u$, $dw = -\sin u\,du$. Then $\int \tan u\,du = -\int \frac{dw}{w} = -\ln|w| + c = -\ln|\cos u| + c = \ln|\sec u| + c$, using $-\ln|\cos u| = \ln|\cos u|^{-1} = \ln|\sec u|$. This is the same substitution pattern used throughout the trig product/quotient section below (see: Products and quotients of trig functions), it isn't a separate trick.

### Other standard integrals (source, §7.1 table)

$$
\int \sinh x\,dx = \cosh x \qquad \int \cosh x\,dx = \sinh x
$$
$$
\int \frac{dx}{x^2+a^2} = \frac{1}{a}\tan^{-1}\!\left(\frac{x}{a}\right) \qquad \int \frac{dx}{\sqrt{a^2-x^2}} = \sin^{-1}\!\left(\frac{x}{a}\right),\; a>0
$$
$$
\int \frac{dx}{x^2-a^2} = \frac{1}{2a}\ln\left|\frac{x-a}{x+a}\right| \qquad \int \frac{dx}{\sqrt{x^2\pm a^2}} = \ln\left|x+\sqrt{x^2\pm a^2}\right|
$$

The last two need not be memorised, because they are easily derived: the first by partial fractions, the second by a trigonometric substitution (source).

> [!note] (added) The source table omits one answer
> The slide lists $\int\sinh x\,dx$ with no result. It is $\cosh x$, the reverse of $\frac{d}{dx}[\cosh x]=\sinh x$ (see: Hyperbolic functions).

## Integration by Parts

$$
\int u\,dv = uv - \int v\,du \qquad \int_a^b u\,dv = uv\Big|_a^b - \int_a^b v\,du
$$

Choose $u$ and $dv$ from the integral, compute $du$ by differentiating $u$, and compute $v = \int dv$. The lecture's rule of thumb: choose $u$ to be a function that becomes simpler when differentiated (or at least not more complicated), as long as $dv=g'(x)\,dx$ can be integrated readily to give $v$ (source, §7.1). Worked examples, including the repeated, cyclic and definite cases and the $\sin^n$ reduction formula, are in [[MAT01B1_Notes_S3_IntegrationExamples#Integration by Parts]].

> [!note] (added) Choosing $u$: the LIATE guide
> When more than one factor could plausibly be $u$, this rough priority order tends to work: **L**ogarithmic, **I**nverse trig, **A**lgebraic (polynomials), **T**rigonometric, **E**xponential. Whichever type appears first in that list is the better choice for $u$. Reason: $u$ should be the factor that gets *simpler* when differentiated (a log or an inverse trig function collapses into an algebraic expression), and $dv$ should be the factor that stays easy to integrate.

## Trig substitutions

If the integral contains the given root, use the matching substitution.

$$
\sqrt{a^2 - b^2x^2} \;\Rightarrow\; x = \frac{a}{b}\sin\theta, \quad \cos^2\theta = 1 - \sin^2\theta
$$
$$
\sqrt{b^2x^2 - a^2} \;\Rightarrow\; x = \frac{a}{b}\sec\theta, \quad \tan^2\theta = \sec^2\theta - 1
$$
$$
\sqrt{a^2 + b^2x^2} \;\Rightarrow\; x = \frac{a}{b}\tan\theta, \quad \sec^2\theta = 1 + \tan^2\theta
$$

Each substitution is used with $\theta$ restricted so that $x=g(\theta)$ is one-to-one (the Substitution Rule run in reverse needs an inverse). The restriction is also what lets the root simplify without an absolute value (source, §7.3, where the table is the case $b=1$):

$$
x=\frac{a}{b}\sin\theta,\ -\frac\pi2\le\theta\le\frac\pi2\qquad x=\frac{a}{b}\tan\theta,\ -\frac\pi2<\theta<\frac\pi2\qquad x=\frac{a}{b}\sec\theta,\ 0\le\theta<\frac\pi2\ \text{or}\ \pi\le\theta<\frac{3\pi}{2}
$$

For example, with $x=a\sin\theta$ and $-\frac\pi2\le\theta\le\frac\pi2$: $\sqrt{a^2-x^2}=\sqrt{a^2\cos^2\theta}=a|\cos\theta|=a\cos\theta$, because $\cos\theta\ge0$ on that range.

N.B This is not an ordinary $u$-substitution. There the new variable is a function of the old one ($u=a^2-x^2$). Here the old variable is a function of the new one ($x=a\sin\theta$), the Substitution Rule used in reverse (source, §7.3).

Practical points (source, §7.3):
- Check for a plain $u$-substitution first. $\int\frac{x}{\sqrt{x^2+4}}\,dx$ looks like a trig substitution but $u=x^2+4$ is simpler.
- If the expression under the root isn't in the table's form, complete the square ($3-2x-x^2=4-(x+1)^2$, then $u=x+1$) or make a preliminary substitution ($4x^2+9$ with $u=2x$).
- For a definite integral, change the limits to $\theta$ and there is no need to convert back to $x$.
- A hyperbolic substitution can replace the trigonometric one: for $\sqrt{x^2-a^2}$, $x=a\cosh t$ with $\cosh^2t-\sinh^2t=1$ gives $\cosh^{-1}(x/a)$. Trig substitutions are usually preferred because the identities are more familiar.

> [!note] (added) Why these three and not others
> Each substitution is chosen so the expression under the root collapses via a Pythagorean identity into a perfect square, which is what removes the root. All three come from the same right triangle idea: label the sides so that $a$ is the hypotenuse or a leg matching the constant under the root, and $bx$ the other leg, then $\theta$ is the angle between them. After integrating in $\theta$, that same triangle is what lets you convert the answer back to $x$ (read $\sin\theta$, $\cos\theta$, etc. straight off the triangle's side ratios) instead of leaving the answer in terms of $\theta$.

## Partial fractions

For $\displaystyle\int \frac{P(x)}{Q(x)}\,dx$ where $\deg P < \deg Q$: factor $Q(x)$ completely, find the partial fraction decomposition (P.F.D.), then integrate term by term.

| Factor of $Q(x)$ | Term in P.F.D. | Factor of $Q(x)$ | Term in P.F.D. |
|---|---|---|---|
| $ax+b$ | $\dfrac{A}{ax+b}$ | $(ax+b)^k$ | $\dfrac{A_1}{ax+b} + \dfrac{A_2}{(ax+b)^2} + \cdots + \dfrac{A_k}{(ax+b)^k}$ |
| $ax^2+bx+c$ | $\dfrac{Ax+B}{ax^2+bx+c}$ | $(ax^2+bx+c)^k$ | $\dfrac{A_1x+B_1}{ax^2+bx+c} + \cdots + \dfrac{A_kx+B_k}{(ax^2+bx+c)^k}$ |

> [!note] (added) $\deg P < \deg Q$ means what, exactly
> $\deg P$ ("degree of $P$") is the highest power of $x$ appearing in that polynomial. The condition $\deg P < \deg Q$ (numerator's highest power smaller than denominator's) is what makes the fraction "proper." If it isn't, do polynomial long division first, split off a polynomial plus a proper remainder fraction, and only the remainder gets a P.F.D.

**The four cases (source, §7.4).** Any polynomial denominator can be factored into linear factors $ax+b$ and irreducible quadratic factors $ax^2+bx+c$ with $b^2-4ac<0$. The decomposition of a proper fraction then depends on the case:

- **Case I.** Distinct linear factors: one term $\dfrac{A}{ax+b}$ for each.
- **Case II.** A repeated linear factor $(ax+b)^r$: one term for each power from $1$ to $r$.
- **Case III.** Irreducible quadratic factors, none repeated: one term $\dfrac{Ax+B}{ax^2+bx+c}$ for each.
- **Case IV.** A repeated irreducible quadratic $(ax^2+bx+c)^r$: $\dfrac{A_1x+B_1}{ax^2+bx+c}+\cdots+\dfrac{A_rx+B_r}{(ax^2+bx+c)^r}$.

The table above holds the same information. The cases are how the lecture names them.

**Finding the coefficients (source).** Multiply both sides by the common denominator, then either expand and equate coefficients of like powers of $x$ (a linear system), or substitute convenient values of $x$ (roots of the denominator's factors) that make most terms vanish. Repeated or quadratic factors usually need the coefficient method, or a mix of both.

**Integrating a quadratic-factor term (source).** For $\dfrac{Ax+B}{ax^2+bx+c}$ with $b^2-4ac<0$, complete the square in the denominator, substitute $u$ for the resulting linear expression, and split into $\displaystyle\int\frac{u}{u^2+a^2}\,du$ (a logarithm) plus $\displaystyle\int\frac{du}{u^2+a^2}=\frac1a\tan^{-1}\frac ua$ (an arctangent). A leftover $\dfrac{1}{(x^2+1)^2}$ term from Case IV is handled by $x=\tan\theta$.

N.B Partial fractions can sometimes be avoided. $\displaystyle\int\frac{x^2+1}{x(x^2+3)}\,dx$ looks like Case III, but with $u=x^3+3x$, $du=(3x^2+3)\,dx$, the integral is $\tfrac13\ln|x^3+3x|+C$ (source, §7.4).

**Rationalizing substitutions (source, §7.4 and §7.5).** If the integrand contains $\sqrt[n]{g(x)}$, for instance $\sqrt[n]{ax+b}$, try $u=\sqrt[n]{g(x)}$. This can turn a non-rational integrand into a rational one, which partial fractions then handles. It doesn't always lead somewhere simple (see: Strategy for integration in S1).

## Products and quotients of trig functions

### $\int \sin^n x \cos^m x\,dx$

1. **$n$ odd.** Strip one sine out, convert the rest to cosines using $\sin^2 x = 1-\cos^2 x$, then substitute $u=\cos x$.
2. **$m$ odd.** Strip one cosine out, convert the rest to sines using $\cos^2 x = 1 - \sin^2 x$, then substitute $u = \sin x$.
3. **$n$ and $m$ both odd.** Use either 1. or 2.
4. **$n$ and $m$ both even.** Use double angle ($\sin 2x = 2\sin x\cos x$) and/or half angle ($\sin^2 x = \tfrac{1-\cos 2x}{2}$, $\cos^2 x = \tfrac{1+\cos 2x}{2}$) formulas to reduce the integral into an integrable form.

### $\int \tan^n x \sec^m x\,dx$ (added: expanded well beyond the source, this is where the original sheet stayed thin)

The whole family runs on two Pythagorean identities and the fact that $\dfrac{d}{dx}[\tan x]=\sec^2x$ and $\dfrac{d}{dx}[\sec x]=\sec x\tan x$. Those two derivatives are exactly the two "extraction" moves used below, everything else is bookkeeping with $\tan^2x=\sec^2x-1$.

1. **$n$ odd.** Strip one tangent *and* one secant out together (since $\sec x\tan x\,dx$ is the derivative of $\sec x$, this pair is the substitution engine), convert the remaining (even) power of tangent to secants using $\tan^2x=\sec^2x-1$, then substitute $u=\sec x$, $du=\sec x\tan x\,dx$.
2. **$m$ even.** Strip two secants out (since $\sec^2x\,dx$ is the derivative of $\tan x$), convert the rest to tangents using $\sec^2x=1+\tan^2x$, then substitute $u=\tan x$, $du=\sec^2x\,dx$.
3. **$n$ odd and $m$ even.** Either method works; case 1 is usually shorter if $n$ is small, case 2 if $m$ is small.
4. **$n$ even and $m$ odd.** Neither extraction move is available ($n$ even means no lone tangent to strip with a secant partner, $m$ odd means no even pair of secants to strip). This is the case the source sheet left as "dealt with differently," here is the actual method.

**(added) Case 4 in full: $n$ even, $m$ odd.**

Since $n$ is even, write every tangent in terms of secant using $\tan^2x=\sec^2x-1$, turning the whole integrand into a polynomial in $\sec x$ alone, an odd power sum of secants. What remains is a sum of integrals of the form $\displaystyle\int \sec^k x\,dx$ for various odd $k$, handled by the **secant reduction formula**:

$$
\int \sec^k x\,dx = \frac{\sec^{k-2}x\tan x}{k-1} + \frac{k-2}{k-1}\int \sec^{k-2}x\,dx.
$$

*(added) Derivation of the reduction formula, by Integration by Parts (see: Integration by Parts).* Write $\sec^k x = \sec^{k-2}x \cdot \sec^2x$ and set $u=\sec^{k-2}x$, $dv=\sec^2x\,dx$, so $du=(k-2)\sec^{k-2}x\tan x\,dx$ and $v=\tan x$:

$$
\int \sec^k x\,dx = \sec^{k-2}x\tan x - (k-2)\int \sec^{k-2}x\tan^2x\,dx.
$$

Replace $\tan^2x = \sec^2x - 1$:

$$
\int \sec^k x\,dx = \sec^{k-2}x\tan x - (k-2)\int \sec^k x\,dx + (k-2)\int \sec^{k-2}x\,dx.
$$

The unknown integral $\int \sec^k x\,dx$ now appears on both sides. Collecting it:

$$
(k-1)\int \sec^k x\,dx = \sec^{k-2}x\tan x + (k-2)\int \sec^{k-2}x\,dx,
$$

which rearranges to the boxed formula above. Applied repeatedly, it drops the power by 2 each time until it reaches $\int \sec x\,dx = \ln|\sec x+\tan x|+c$ (odd $k$, matches case 4) or $\int \sec^0x\,dx = \int dx = x+c$ (even $k$, doesn't arise in case 4 since $k$ stays odd throughout, but is the base case for the general formula).

**(added) The $\int \cot^nx\csc^mx\,dx$ family** works identically to $\tan^n\sec^m$, symmetrically, using $\cot^2x=\csc^2x-1$, $\dfrac{d}{dx}[\cot x]=-\csc^2x$, and $\dfrac{d}{dx}[\csc x]=-\csc x\cot x$. Every case above transfers directly with the sign changes those two derivatives bring.

### Products of sines and cosines of different angles (source, §7.2)

To integrate $\int\sin mx\cos nx\,dx$, $\int\sin mx\sin nx\,dx$ or $\int\cos mx\cos nx\,dx$, use the matching identity to turn the product into a sum:

$$
\sin A\cos B=\tfrac12\big[\sin(A-B)+\sin(A+B)\big]
$$
$$
\sin A\sin B=\tfrac12\big[\cos(A-B)-\cos(A+B)\big]
$$
$$
\cos A\cos B=\tfrac12\big[\cos(A-B)+\cos(A+B)\big]
$$

The source notes the integral could be done by parts, but the identity is easier. Worked example in [[MAT01B1_Notes_S3_IntegrationExamples#Worked examples from the lecture, section 7.2, sine and cosine]].

## See also
- [[MAT01B1_Notes_S1_CalculusApplications]]
- [[MAT01B1_Notes_S3_IntegrationExamples]]
- [[MAT01B1_Proofs_ST1]]
- [[MAT01B1_Notes_S7_AreaBetweenCurves]], [[MAT01B1_Notes_S8_Volumes]], [[MAT01B1_Notes_S9_CylindricalShells]] (basic integral formulas applied to areas and volumes)
- [[MAT01B1_Notes_S13_SeparableDifferentialEquations]], [[MAT01B1_Notes_S14_LinearDifferentialEquations]] (Chain Rule and Product Rule underlying both solution methods)
- [[MAT01B1_Notes_S11_ArcLength]], [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]] (trig substitution and the $\sec^3$ integral applied to arc length and surface area)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations]] (Chain Rule for parametric tangents, Substitution Rule for parametric area and arc length)
