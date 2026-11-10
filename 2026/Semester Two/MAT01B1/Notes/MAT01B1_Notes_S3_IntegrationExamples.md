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

### Worked examples from the lecture, section 7.3

**Worked example (source, §7.3).** $\displaystyle\int\frac{\sqrt{9-x^2}}{x^2}\,dx$. Let $x=3\sin\theta$ with $-\frac\pi2\le\theta\le\frac\pi2$, so $dx=3\cos\theta\,d\theta$ and $\sqrt{9-x^2}=3\cos\theta$ (since $\cos\theta\ge0$ on that range):

$$
\int\frac{3\cos\theta}{9\sin^2\theta}\,3\cos\theta\,d\theta=\int\cot^2\theta\,d\theta=\int(\csc^2\theta-1)\,d\theta=-\cot\theta-\theta+C.
$$

Back to $x$ with a right triangle ($\sin\theta=\frac x3$, so the adjacent side is $\sqrt{9-x^2}$): $\cot\theta=\frac{\sqrt{9-x^2}}{x}$ and $\theta=\sin^{-1}\frac x3$, so

$$
\int\frac{\sqrt{9-x^2}}{x^2}\,dx=-\frac{\sqrt{9-x^2}}{x}-\sin^{-1}\frac x3+C.
$$

**Worked example (source, §7.3), area of an ellipse.** The first-quadrant part of $\frac{x^2}{a^2}+\frac{y^2}{b^2}=1$ is $y=\frac ba\sqrt{a^2-x^2}$, so $A=4\cdot\frac ba\displaystyle\int_0^a\sqrt{a^2-x^2}\,dx$. Let $x=a\sin\theta$, $dx=a\cos\theta\,d\theta$, and change the limits: $x=0\Rightarrow\theta=0$, $x=a\Rightarrow\theta=\frac\pi2$.

$$
A=4ab\int_0^{\pi/2}\cos^2\theta\,d\theta=2ab\int_0^{\pi/2}(1+\cos2\theta)\,d\theta=2ab\left[\theta+\tfrac12\sin2\theta\right]_0^{\pi/2}=\pi ab.
$$

With $a=b=r$ this is the circle's $\pi r^2$. N.B The integral is definite and the limits were changed, so there is no converting back to $x$.

**Worked example (source, §7.3).** $\displaystyle\int\frac{dx}{x^2\sqrt{x^2+4}}$. Let $x=2\tan\theta$, $dx=2\sec^2\theta\,d\theta$, $\sqrt{x^2+4}=2\sec\theta$:

$$
\int\frac{2\sec^2\theta}{4\tan^2\theta\cdot2\sec\theta}\,d\theta=\frac14\int\frac{\sec\theta}{\tan^2\theta}\,d\theta=\frac14\int\frac{\cos\theta}{\sin^2\theta}\,d\theta.
$$

Put $u=\sin\theta$: $\frac14\int\frac{du}{u^2}=-\frac{1}{4\sin\theta}=-\frac{\csc\theta}{4}$. From the triangle ($\tan\theta=\frac x2$, hypotenuse $\sqrt{x^2+4}$), $\csc\theta=\frac{\sqrt{x^2+4}}{x}$:

$$
\int\frac{dx}{x^2\sqrt{x^2+4}}=-\frac{\sqrt{x^2+4}}{4x}+C.
$$

**Worked example (source, §7.3), when not to use it.** $\displaystyle\int\frac{x}{\sqrt{x^2+4}}\,dx$ has the same root, but $u=x^2+4$, $du=2x\,dx$ is simpler: $\frac12\int u^{-1/2}\,du=\sqrt{x^2+4}+C$. N.B Even when an integrand contains a root of this form, a direct $u$-substitution can beat trig substitution.

**Worked example (source, §7.3), two solutions.** $\displaystyle\int\frac{dx}{\sqrt{x^2-a^2}}$, $a>0$. *Solution 1.* Let $x=a\sec\theta$, $dx=a\sec\theta\tan\theta\,d\theta$, $\sqrt{x^2-a^2}=a\tan\theta$:

$$
\int\sec\theta\,d\theta=\ln|\sec\theta+\tan\theta|+C=\ln\left|\frac xa+\frac{\sqrt{x^2-a^2}}{a}\right|+C=\ln\left|x+\sqrt{x^2-a^2}\right|+C_1,
$$

with $C_1=C-\ln a$. *Solution 2* (for $x>0$). Let $x=a\cosh t$, so $\sqrt{x^2-a^2}=a\sinh t$ and $dx=a\sinh t\,dt$: the integral is $\int dt=t+C=\cosh^{-1}\frac xa+C$. This is formula 20 in the table (see: Other standard integrals in [[MAT01B1_Notes_S2_DerivativeIntegralReference]]).

**Worked example (source, §7.3), a preliminary substitution.** $\displaystyle\int_0^{3\sqrt3/2}\frac{x^3}{(4x^2+9)^{3/2}}\,dx$. The expression $4x^2+9$ isn't quite in the table, but $u=2x$ makes it $u^2+9$. Combined with the tangent substitution, $x=\frac32\tan\theta$, $dx=\frac32\sec^2\theta\,d\theta$, $(4x^2+9)^{3/2}=27\sec^3\theta$. Limits: $x=0\Rightarrow\theta=0$, $x=\frac{3\sqrt3}{2}\Rightarrow\tan\theta=\sqrt3\Rightarrow\theta=\frac\pi3$.

$$
\int_0^{\pi/3}\frac{\frac{27}{8}\tan^3\theta\cdot\frac32\sec^2\theta}{27\sec^3\theta}\,d\theta=\frac3{16}\int_0^{\pi/3}\frac{\tan^3\theta}{\sec\theta}\,d\theta=\frac3{16}\int_0^{\pi/3}\frac{1-\cos^2\theta}{\cos^2\theta}\sin\theta\,d\theta.
$$

With $u=\cos\theta$ (limits $1$ to $\frac12$): $\frac3{16}\int_{1/2}^{1}(u^{-2}-1)\,du=\frac3{16}\left[-\frac1u-u\right]_{1/2}^{1}=\frac3{16}\cdot\frac12=\frac{3}{32}$.

**Worked example (source, §7.3), completing the square.** $\displaystyle\int\frac{x}{\sqrt{3-2x-x^2}}\,dx$. First $3-2x-x^2=4-(x+1)^2$. Let $u=x+1$, so $x=u-1$:

$$
\int\frac{u-1}{\sqrt{4-u^2}}\,du.
$$

Then $u=2\sin\theta$, $du=2\cos\theta\,d\theta$, $\sqrt{4-u^2}=2\cos\theta$:

$$
\int(2\sin\theta-1)\,d\theta=-2\cos\theta-\theta+C=-\sqrt{4-u^2}-\sin^{-1}\frac u2+C=-\sqrt{3-2x-x^2}-\sin^{-1}\frac{x+1}{2}+C.
$$

## Partial Fractions

**(added) Worked example (composite).** $\displaystyle\int \frac{3x+5}{(x-1)(x+2)}\,dx$. Denominator is two distinct linear factors, so
$$
\frac{3x+5}{(x-1)(x+2)} = \frac{A}{x-1} + \frac{B}{x+2}.
$$
Multiplying through: $3x+5 = A(x+2) + B(x-1)$. Setting $x=1$: $8=3A \Rightarrow A=\tfrac{8}{3}$. Setting $x=-2$: $-1=-3B \Rightarrow B=\tfrac{1}{3}$. So
$$
\int \frac{3x+5}{(x-1)(x+2)}\,dx = \frac{8}{3}\ln|x-1| + \frac{1}{3}\ln|x+2| + c.
$$

### Worked examples from the lecture, section 7.4

**Worked example (source, §7.4), long division first.** $\displaystyle\int\frac{x^3+x}{x-1}\,dx$. The numerator's degree is not less than the denominator's, so divide: $x^3+x=(x-1)(x^2+x+2)+2$.

$$
\int\left(x^2+x+2+\frac{2}{x-1}\right)dx=\frac{x^3}{3}+\frac{x^2}{2}+2x+2\ln|x-1|+C.
$$

**Worked example (source, §7.4), Case I, two methods.** $\displaystyle\int\frac{x^2+2x-1}{2x^3+3x^2-2x}\,dx$. The denominator is $x(2x-1)(x+2)$, so

$$
\frac{x^2+2x-1}{x(2x-1)(x+2)}=\frac Ax+\frac{B}{2x-1}+\frac{C}{x+2},\qquad x^2+2x-1=A(2x-1)(x+2)+Bx(x+2)+Cx(2x-1).
$$

*Method 1, equate coefficients.* Expanding the right side gives $(2A+B+2C)x^2+(3A+2B-C)x-2A$, so $2A+B+2C=1$, $3A+2B-C=2$, $-2A=-1$. *Method 2, choose values of $x$.* $x=0$: $-1=-2A$, so $A=\frac12$. $x=\frac12$: $\frac14=\frac54B$, so $B=\frac15$. $x=-2$: $-1=10C$, so $C=-\frac1{10}$. Both give

$$
\int\frac{x^2+2x-1}{2x^3+3x^2-2x}\,dx=\frac12\ln|x|+\frac1{10}\ln|2x-1|-\frac1{10}\ln|x+2|+K.
$$

The middle term uses the mental substitution $u=2x-1$, which brings a factor $\frac12$ (that is why it is $\frac1{10}$, not $\frac15$).

**Worked example (source, §7.4).** $\displaystyle\int\frac{dx}{x^2-a^2}$. Write $\frac{1}{(x-a)(x+a)}=\frac{A}{x-a}+\frac{B}{x+a}$, so $A(x+a)+B(x-a)=1$. $x=a$ gives $A=\frac1{2a}$ and $x=-a$ gives $B=-\frac1{2a}$:

$$
\int\frac{dx}{x^2-a^2}=\frac1{2a}\big(\ln|x-a|-\ln|x+a|\big)+C=\frac{1}{2a}\ln\left|\frac{x-a}{x+a}\right|+C.
$$

**Worked example (source, §7.4), Case II.** $\displaystyle\int\frac{x^4-2x^2+4x+1}{x^3-x^2-x+1}\,dx$. Divide first: the quotient is $x+1$ with remainder $4x$. The denominator factors as $(x-1)^2(x+1)$ (since $Q(1)=0$), so

$$
\frac{4x}{(x-1)^2(x+1)}=\frac{A}{x-1}+\frac{B}{(x-1)^2}+\frac{C}{x+1},\qquad 4x=A(x-1)(x+1)+B(x+1)+C(x-1)^2.
$$

Equating coefficients: $A+C=0$, $B-2C=4$, $-A+B+C=0$, giving $A=1$, $B=2$, $C=-1$:

$$
\int\left(x+1+\frac{1}{x-1}+\frac{2}{(x-1)^2}-\frac{1}{x+1}\right)dx=\frac{x^2}{2}+x+\ln|x-1|-\frac{2}{x-1}-\ln|x+1|+K.
$$

**Worked example (source, §7.4), Case III.** $\displaystyle\int\frac{2x^2-x+4}{x^3+4x}\,dx$. Since $x^3+4x=x(x^2+4)$ and $x^2+4$ is irreducible,

$$
\frac{2x^2-x+4}{x(x^2+4)}=\frac Ax+\frac{Bx+C}{x^2+4},\qquad 2x^2-x+4=(A+B)x^2+Cx+4A,
$$

so $A=1$, $B=1$, $C=-1$. Split $\frac{x-1}{x^2+4}$ into $\frac{x}{x^2+4}-\frac{1}{x^2+4}$ (the first by $u=x^2+4$, the second by the arctangent formula with $a=2$):

$$
\int\frac{2x^2-x+4}{x^3+4x}\,dx=\ln|x|+\frac12\ln(x^2+4)-\frac12\tan^{-1}\frac x2+K.
$$

**Worked example (source, §7.4), an irreducible quadratic after dividing.** $\displaystyle\int\frac{4x^2-3x+2}{4x^2-4x+3}\,dx$. Divide: $1+\frac{x-1}{4x^2-4x+3}$. The quadratic is irreducible ($b^2-4ac=-32<0$), so complete the square: $4x^2-4x+3=(2x-1)^2+2$. Let $u=2x-1$, so $x=\frac12(u+1)$ and $dx=\frac12du$:

$$
\int\frac{x-1}{4x^2-4x+3}\,dx=\frac14\int\frac{u-1}{u^2+2}\,du=\frac18\ln(u^2+2)-\frac{1}{4\sqrt2}\tan^{-1}\frac{u}{\sqrt2}.
$$

$$
\int\frac{4x^2-3x+2}{4x^2-4x+3}\,dx=x+\frac18\ln(4x^2-4x+3)-\frac{1}{4\sqrt2}\tan^{-1}\frac{2x-1}{\sqrt2}+C.
$$

**Worked example (source, §7.4), Case IV, form only.** Writing out the decomposition without finding the constants:

$$
\frac{x^3+x^2+1}{x(x-1)(x^2+x+1)(x^2+1)^3}=\frac Ax+\frac B{x-1}+\frac{Cx+D}{x^2+x+1}+\frac{Ex+F}{x^2+1}+\frac{Gx+H}{(x^2+1)^2}+\frac{Ix+J}{(x^2+1)^3}.
$$

**Worked example (source, §7.4), Case IV, evaluated.** $\displaystyle\int\frac{1-x+2x^2-x^3}{x(x^2+1)^2}\,dx$. The form is $\frac Ax+\frac{Bx+C}{x^2+1}+\frac{Dx+E}{(x^2+1)^2}$. Equating coefficients gives $A+B=0$, $C=-1$, $2A+B+D=2$, $C+E=-1$, so $A=1$, $B=-1$, $C=-1$, $D=1$, $E=0$:

$$
\int\left(\frac1x-\frac{x+1}{x^2+1}+\frac{x}{(x^2+1)^2}\right)dx=\ln|x|-\frac12\ln(x^2+1)-\tan^{-1}x-\frac{1}{2(x^2+1)}+K.
$$

N.B This worked out nicely because $E=0$. In general a leftover $\frac{1}{(x^2+1)^2}$ term needs $x=\tan\theta$.

**Worked example (source, §7.4), avoiding partial fractions.** $\displaystyle\int\frac{x^2+1}{x(x^2+3)}\,dx$. Case III would work, but $u=x(x^2+3)=x^3+3x$ gives $du=(3x^2+3)\,dx$ directly:

$$
\int\frac{x^2+1}{x(x^2+3)}\,dx=\frac13\ln|x^3+3x|+C.
$$

**Worked example (source, §7.4), a rationalizing substitution.** $\displaystyle\int\frac{\sqrt{x+4}}{x}\,dx$. Let $u=\sqrt{x+4}$, so $x=u^2-4$ and $dx=2u\,du$:

$$
\int\frac{2u^2}{u^2-4}\,du=2\int\left(1+\frac{4}{u^2-4}\right)du=2u+8\cdot\frac14\ln\left|\frac{u-2}{u+2}\right|+C=2\sqrt{x+4}+2\ln\left|\frac{\sqrt{x+4}-2}{\sqrt{x+4}+2}\right|+C.
$$

The step $\int\frac{du}{u^2-4}$ is the $\frac1{2a}\ln\left|\frac{u-a}{u+a}\right|$ result above with $a=2$.

## $\sin^n x \cos^m x$

**(added) Worked example (composite), $n$ odd case.** $\displaystyle\int \sin^3x\cos^2x\,dx$. Strip one sine: $\sin^3x=\sin x(1-\cos^2x)$. Let $u=\cos x$, $du=-\sin x\,dx$:
$$
\int \sin x(1-\cos^2x)\cos^2x\,dx = -\int(1-u^2)u^2\,du = -\frac{u^3}{3}+\frac{u^5}{5}+c = -\frac{\cos^3x}{3}+\frac{\cos^5x}{5}+c.
$$

### Worked examples from the lecture, section 7.2, sine and cosine

**Worked example (source, §7.2), odd power of cosine.** $\displaystyle\int\cos^3x\,dx$. Saving one cosine and using $\cos^2x=1-\sin^2x$, then $u=\sin x$, $du=\cos x\,dx$:

$$
\int(1-\sin^2x)\cos x\,dx=\int(1-u^2)\,du=\sin x-\frac{\sin^3x}{3}+C.
$$

**Worked example (source, §7.2), odd power of sine with an even cosine.** $\displaystyle\int\sin^5x\cos^2x\,dx$. Converting $\cos^2x$ to sines would leave no extra $\cos x$ factor. Instead save a sine: $\sin^5x\cos^2x=(1-\cos^2x)^2\cos^2x\sin x$. With $u=\cos x$, $du=-\sin x\,dx$:

$$
-\int(1-u^2)^2u^2\,du=-\int(u^2-2u^4+u^6)\,du=-\frac{\cos^3x}{3}+\frac{2\cos^5x}{5}-\frac{\cos^7x}{7}+C.
$$

**Worked example (source, §7.2), both powers even.** $\displaystyle\int_0^\pi\sin^2x\,dx$. Writing $\sin^2x=1-\cos^2x$ gets nowhere, so use the half-angle identity:

$$
\int_0^\pi\sin^2x\,dx=\frac12\int_0^\pi(1-\cos2x)\,dx=\frac12\left[x-\frac12\sin2x\right]_0^\pi=\frac\pi2.
$$

**Worked example (source, §7.2), half-angle twice.** $\displaystyle\int\sin^4x\,dx$. Write $\sin^4x=(\sin^2x)^2=\frac14(1-\cos2x)^2=\frac14\left(1-2\cos2x+\cos^22x\right)$. The $\cos^22x$ needs another half-angle step, $\cos^22x=\frac12(1+\cos4x)$:

$$
\int\sin^4x\,dx=\frac14\int\left(\frac32-2\cos2x+\frac12\cos4x\right)dx=\frac{3x}{8}-\frac{\sin2x}{4}+\frac{\sin4x}{32}+C.
$$

N.B The source points out that this and the previous example also follow from the $\sin^n$ reduction formula derived in [[#Worked examples from the lecture, section 7.1]].

**Worked example (source, §7.2), a product of different angles.** $\displaystyle\int\sin4x\cos5x\,dx$. Parts would work, but the identity $\sin A\cos B=\frac12[\sin(A-B)+\sin(A+B)]$ (see: Products of sines and cosines of different angles in [[MAT01B1_Notes_S2_DerivativeIntegralReference]]) is easier:

$$
\int\sin4x\cos5x\,dx=\frac12\int(-\sin x+\sin9x)\,dx=\frac12\left(\cos x-\frac19\cos9x\right)+C.
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

### Worked examples from the lecture, section 7.2, tangent and secant

**Worked example (source, §7.2), even power of secant.** $\displaystyle\int\tan^6x\sec^4x\,dx$. Separate one $\sec^2x$ and write the other as $1+\tan^2x$. With $u=\tan x$, $du=\sec^2x\,dx$:

$$
\int\tan^6x(1+\tan^2x)\sec^2x\,dx=\int(u^6+u^8)\,du=\frac{\tan^7x}{7}+\frac{\tan^9x}{9}+C.
$$

**Worked example (source, §7.2), odd power of tangent.** $\displaystyle\int\tan^5\theta\sec^7\theta\,d\theta$. Keep $\sec\theta\tan\theta$ as the differential, so the remaining powers are both even and the square identity applies. With $u=\sec\theta$, $du=\sec\theta\tan\theta\,d\theta$:

$$
\int\tan^4\theta\sec^6\theta\,\sec\theta\tan\theta\,d\theta=\int(u^2-1)^2u^6\,du=\int(u^{10}-2u^8+u^6)\,du=\frac{\sec^{11}\theta}{11}-\frac{2\sec^9\theta}{9}+\frac{\sec^7\theta}{7}+C.
$$

**Worked example (source, §7.2), $\int\sec^3x\,dx$ by parts.** Neither $u=\sec x$ nor $u=\tan x$ works directly. Use integration by parts with $u=\sec x$, $dv=\sec^2x\,dx$, so $du=\sec x\tan x\,dx$, $v=\tan x$:

$$
\int\sec^3x\,dx=\sec x\tan x-\int\sec x\tan^2x\,dx=\sec x\tan x-\int\sec^3x\,dx+\int\sec x\,dx.
$$

The original integral appears on both sides. Using $\int\sec x\,dx=\ln|\sec x+\tan x|+C$ and solving,

$$
\int\sec^3x\,dx=\frac12\left(\sec x\tan x+\ln|\sec x+\tan x|\right)+C.
$$

This is the table value used in S2 and in the arc length and surface area examples.

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
