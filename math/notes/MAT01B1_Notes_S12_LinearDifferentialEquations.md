---
module: MAT01B1
topic: Linear Differential Equations
session: S12
tags: [definition, theorem, formula, worked-example]
---

# Linear Differential Equations

Source: Dr K, §9.5 Linear Differential Equations (slides 1 to 13).

## Standard form

**Definition.** A first order linear differential equation is one that can be written in the **standard form**

$$
\frac{dy}{dx}+P(x)y=Q(x),
$$

where $P$ and $Q$ are continuous functions on a given interval.

**Example (source, slide 2).** $xy'+y=2x$ is linear: for $x\ne0$ it rewrites as $y'+\dfrac1xy=2$, matching the standard form with $P(x)=1/x$, $Q(x)=2$. This equation is *not* separable, unlike everything in [[MAT01B1_Notes_S11_SeparableDifferentialEquations]], it needs a different technique entirely.

## Building the integrating factor (source, slides 3 to 7)

The method rests on the product rule. Notice $xy'+y=(xy)'$, so the example above becomes

$$
(xy)'=2x \;\Rightarrow\; xy=x^2+C \;\Rightarrow\; y=x+\frac{C}{x},
$$

just by integrating both sides directly, once the left side is recognised as a single derivative.

Every first order linear equation can be solved the same way, by multiplying by a function $I(x)$, an **integrating factor**, chosen so that the left side of the standard form collapses into $(I(x)y)'$:

$$
I(x)\big(y'+P(x)y\big)=\big(I(x)y\big)'.
$$

Multiplying the standard form by $I(x)$ then gives $\big(I(x)y\big)'=I(x)Q(x)$, and integrating both sides,

$$
I(x)y=\int I(x)Q(x)\,dx+C \;\Rightarrow\; y(x)=\frac{1}{I(x)}\left[\int I(x)Q(x)\,dx+C\right].
$$

**Finding $I$.** Expand the requirement $I(x)y'+I(x)P(x)y=\big(I(x)y\big)'=I'(x)y+I(x)y'$ and cancel the $I(x)y'$ term from both sides:

$$
I(x)P(x)=I'(x)=\frac{dI}{dx}.
$$

This is itself a separable equation ([[MAT01B1_Notes_S11_SeparableDifferentialEquations#Separable equations|separable equations]]):

$$
\frac{dI}{I}=P(x)\,dx \;\Rightarrow\; \int\frac{dI}{I}=\int P(x)\,dx \;\Rightarrow\; \ln|I|=\int P(x)\,dx \;\Rightarrow\; I=Ae^{\int P(x)\,dx},
$$

where $A=\pm e^C$. Taking $A=1$ (any nonzero $A$ works, so the simplest choice is used):

$$
I(x)=e^{\int P(x)\,dx}.
$$

## Method summary

**To solve $y'+P(x)y=Q(x)$:** multiply both sides by the integrating factor $I(x)=e^{\int P(x)\,dx}$, recognise the left side as $\big(I(x)y\big)'$, and integrate both sides with respect to $x$.

**Hypotheses**
- the equation is in standard form $y'+P(x)y=Q(x)$
- $P,Q$ continuous on the interval in question

## Worked example (source, slide 9)

**Solve $\dfrac{dy}{dx}+3x^2y=6x^2$.** Here $P(x)=3x^2$, $Q(x)=6x^2$, so $I(x)=e^{\int3x^2\,dx}=e^{x^3}$. Multiplying through:

$$
e^{x^3}\frac{dy}{dx}+3x^2e^{x^3}y=6x^2e^{x^3} \;\Rightarrow\; \frac{d}{dx}\big(e^{x^3}y\big)=6x^2e^{x^3}.
$$

Integrating both sides (right side by the substitution $u=x^3$):

$$
e^{x^3}y=\int6x^2e^{x^3}\,dx=2e^{x^3}+C \;\Rightarrow\; y=2+Ce^{-x^3}.
$$

## Worked example: an initial value problem (source, slides 10 to 11)

**Solve $x^2y'+xy=1$, $x>0$, $y(1)=2$.** Divide by $x^2$ to reach standard form:

$$
y'+\frac1xy=\frac{1}{x^2},\qquad x>0.
$$

$$
I(x)=e^{\int(1/x)\,dx}=e^{\ln x}=x.
$$

Multiplying by $x$: $xy'+y=\dfrac1x \Rightarrow (xy)'=\dfrac1x$, so

$$
xy=\int\frac1x\,dx=\ln x+C \;\Rightarrow\; y=\frac{\ln x+C}{x}.
$$

Applying $y(1)=2$: $2=\dfrac{\ln1+C}{1}=C$. The solution to the initial-value problem is

$$
y=\frac{\ln x+2}{x}.
$$

## Worked example: a non-elementary integral (source, slides 12 to 13)

**Solve $y'+2xy=1$.** Already in standard form, $P(x)=2x$, so $I(x)=e^{\int2x\,dx}=e^{x^2}$.

$$
e^{x^2}y'+2xe^{x^2}y=e^{x^2} \;\Rightarrow\; \big(e^{x^2}y\big)'=e^{x^2} \;\Rightarrow\; e^{x^2}y=\int e^{x^2}\,dx+C.
$$

$\displaystyle\int e^{x^2}\,dx$ cannot be expressed in terms of elementary functions, so the answer is left as

$$
y=e^{-x^2}\int e^{x^2}\,dx+Ce^{-x^2}.
$$

Using the Fundamental Theorem of Calculus, this can be written with a definite integral instead, choosing any convenient lower limit (here $0$):

$$
y=e^{-x^2}\int_0^{x}e^{t^2}\,dt+Ce^{-x^2}.
$$

N.B This is the same situation as $\displaystyle\int_1^\infty\frac1{x^2}\,dx$-type reasoning being about *evaluating* an integral even without an elementary antiderivative, compare [[MAT01B1_Notes_S1_CalculusApplications#Improper integrals (added)]]: here, the Fundamental Theorem of Calculus is used to name the antiderivative as a definite integral with a variable upper limit, rather than to evaluate a number.

## See also
- [[MAT01B1_Notes_S11_SeparableDifferentialEquations]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (Product Rule, basic integral formulas)
- [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7]] (why the $+C$ appears in each general solution)
