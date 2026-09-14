---
module: MAT01B1
topic: Separable Differential Equations
session: S11
tags: [definition, formula, worked-example]
---

# Separable Differential Equations

Source: Dr K, §9.3 Variable Separable Differential Equations (slides 1 to 24).

## What a differential equation is

**Definition.** A differential equation is an equation that contains an unknown function and one or more of its derivatives. The order of a differential equation is the order of the highest derivative that occurs in it.

Two examples fix the idea and show what "order" means in practice.

**Population growth (1st order).** If a population $P(t)$ grows at a rate proportional to its own size (a reasonable model under ideal conditions: unlimited space, adequate nutrition, no predators or disease), the rate of growth $dP/dt$ satisfies

$$
\frac{dP}{dt}=kP,
$$

where $k$ is the proportionality constant. Only a first derivative appears, so this is first order.

**Spring motion (2nd order).** A mass $m$ hangs on a vertical spring. Hooke's Law says a spring stretched or compressed $x$ units exerts a restoring force $-kx$ ($k>0$, the spring constant). Ignoring air resistance and friction, Newton's Second Law gives

$$
m\frac{d^2x}{dt^2}=-kx.
$$

A second derivative appears, so this is second order.

## Solutions of a differential equation

**Definition.** A function $f$ is a **solution** of a differential equation if the equation is satisfied when $y=f(x)$ and its derivatives are substituted in. "Solve the differential equation" means find *all* possible solutions.

## Worked example: verifying a family of solutions (source, slides 7 to 8)

Show every member of $y=\dfrac{1+ce^t}{1-ce^t}$ solves $y'=\tfrac12(y^2-1)$.

Differentiate with the Quotient Rule:

$$
y'=\frac{(1-ce^t)(ce^t)-(1+ce^t)(-ce^t)}{(1-ce^t)^2}=\frac{ce^t-c^2e^{2t}+ce^t+c^2e^{2t}}{(1-ce^t)^2}=\frac{2ce^t}{(1-ce^t)^2}.
$$

The right side of the equation:

$$
\frac12(y^2-1)=\frac12\left[\left(\frac{1+ce^t}{1-ce^t}\right)^2-1\right]=\frac12\left[\frac{(1+ce^t)^2-(1-ce^t)^2}{(1-ce^t)^2}\right]=\frac12\cdot\frac{4ce^t}{(1-ce^t)^2}=\frac{2ce^t}{(1-ce^t)^2}.
$$

Both sides match for every value of $c$, so the whole family is a solution.

## Worked example: picking out one solution with an initial condition (source, slide 9)

Find the solution of $y'=\tfrac12(y^2-1)$ satisfying $y(0)=2$, using the family found above. Substitute $t=0$, $y=2$:

$$
2=\frac{1+ce^0}{1-ce^0}=\frac{1+c}{1-c}\;\Rightarrow\;2-2c=1+c\;\Rightarrow\;c=\frac13.
$$

$$
y=\frac{1+\tfrac13e^t}{1-\tfrac13e^t}=\frac{3+e^t}{3-e^t}.
$$

N.B An **initial condition** (a value of $y$ at a specific point) picks a single curve out of a whole family of solutions. Every worked example below that includes one is doing exactly this.

## Separable equations

**Definition.** A first-order differential equation is **separable** if $dy/dx$ factors as a function of $x$ times a function of $y$:

$$
\frac{dy}{dx}=g(x)f(y),
$$

equivalently (when $f(y)\ne0$), writing $h(y)=1/f(y)$,

$$
\frac{dy}{dx}=\frac{g(x)}{h(y)}.
$$

**Method.** Rewrite in differential form, all $y$'s on one side, all $x$'s on the other, then integrate both sides:

$$
h(y)\,dy=g(x)\,dx \qquad\Longrightarrow\qquad \int h(y)\,dy=\int g(x)\,dx.
$$

This defines $y$ implicitly as a function of $x$; sometimes it can be solved explicitly for $y$, sometimes not.

**Why this works (source, slide 13).** If $h(y)\,dy=g(x)\,dx$ holds, differentiate both antiderivatives with respect to $x$:

$$
\frac{d}{dx}\left(\int h(y)\,dy\right)=\frac{d}{dx}\left(\int g(x)\,dx\right)\;\Rightarrow\;\frac{d}{dy}\left(\int h(y)\,dy\right)\frac{dy}{dx}=g(x)\;\Rightarrow\;h(y)\frac{dy}{dx}=g(x),
$$

using the [[MAT01B1_Notes_S2_DerivativeIntegralReference#Basic properties|Chain Rule]] on the left side, recovering the original equation. So integrating both sides really does produce a solution.

## Worked example: $y'=x^2/y^2$, with an initial condition (source, slides 14 to 15)

**Solve $\dfrac{dy}{dx}=\dfrac{x^2}{y^2}$.** Separate and integrate:

$$
y^2\,dy=x^2\,dx\;\Rightarrow\;\int y^2\,dy=\int x^2\,dx\;\Rightarrow\;\frac13y^3=\frac13x^3+C.
$$

Solving for $y$: $y=\sqrt[3]{x^3+3C}=\sqrt[3]{x^3+K}$, writing $K=3C$ (still an arbitrary constant).

**Find the solution with $y(0)=2$.** $y(0)=\sqrt[3]{K}$, so $\sqrt[3]K=2\Rightarrow K=8$, giving $y=\sqrt[3]{x^3+8}$.

## Worked example: an implicit solution (source, slide 16)

**Solve $\dfrac{dy}{dx}=\dfrac{6x^2}{2y+\cos y}$.**

$$
(2y+\cos y)\,dy=6x^2\,dx\;\Rightarrow\;\int(2y+\cos y)\,dy=\int6x^2\,dx\;\Rightarrow\;y^2+\sin y=2x^3+C.
$$

This gives the general solution implicitly; it's not possible to solve it explicitly for $y$ as a function of $x$ here, unlike the previous example.

## Worked example: $y'=x^2y$ (source, slides 17 to 18)

$$
\frac{dy}{dx}=x^2y.
$$

For $y\ne0$: $\dfrac{dy}{y}=x^2\,dx\;\Rightarrow\;\displaystyle\int\frac{dy}{y}=\int x^2\,dx\;\Rightarrow\;\ln|y|=\dfrac{x^3}{3}+C$.

Solving explicitly:

$$
|y|=e^{\ln|y|}=e^{x^3/3+C}=e^Ce^{x^3/3}\;\Rightarrow\;y=\pm e^Ce^{x^3/3}.
$$

$y=0$ can be checked directly not to satisfy the original equation, so the general solution is written

$$
y=Ae^{x^3/3},\qquad A=\pm e^C \text{ an arbitrary nonzero constant}.
$$

## Orthogonal trajectories

**Definition.** An orthogonal trajectory of a family of curves is a curve that meets every member of the family at right angles. Two families that are each other's orthogonal trajectories are called orthogonal.

(source example) Every line $y=mx$ through the origin is an orthogonal trajectory of the family of concentric circles $x^2+y^2=r^2$.

## Worked example: orthogonal trajectories of a family of parabolas (source, slides 21 to 23)

Find the orthogonal trajectories of $x=ky^2$ ($k$ arbitrary).

**Step 1, find a $k$-free differential equation for the family.** Differentiating $x=ky^2$: $1=2ky\,\dfrac{dy}{dx}\Rightarrow\dfrac{dy}{dx}=\dfrac{1}{2ky}$. This still has $k$ in it; eliminate $k$ using $k=x/y^2$ from the original equation:

$$
\frac{dy}{dx}=\frac{1}{2ky}=\frac{1}{2\left(\frac{x}{y^2}\right)y}=\frac{y}{2x}.
$$

**Step 2, take the negative reciprocal slope.** The orthogonal trajectories must have slope $-\dfrac{2x}{y}$ at each point (perpendicular to slope $y/2x$):

$$
\frac{dy}{dx}=-\frac{2x}{y}.
$$

**Step 3, solve the (now separable) equation.**

$$
y\,dy=-2x\,dx\;\Rightarrow\;\int y\,dy=-\int2x\,dx\;\Rightarrow\;\frac{y^2}{2}=-x^2+C\;\Rightarrow\;x^2+\frac{y^2}{2}=C.
$$

The orthogonal trajectories of the parabolas $x=ky^2$ are the family of ellipses $x^2+\tfrac{y^2}{2}=C$ ($C>0$).

```desmos-graph
left=-4; right=4;
top=3; bottom=-3;
---
x=0.3y^{2}
x=-0.3y^{2}
x=0.8y^{2}
x=-0.8y^{2}
x^{2}+\frac{y^{2}}{2}=1
x^{2}+\frac{y^{2}}{2}=2
x^{2}+\frac{y^{2}}{2}=4
```

(source aside) Orthogonal trajectories show up across physics: lines of force in an electrostatic field are orthogonal to lines of constant potential, and streamlines in aerodynamics are orthogonal to velocity-equipotential curves.

## See also
- [[MAT01B1_Notes_S12_LinearDifferentialEquations]] (the next technique, for equations that aren't separable)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (Chain Rule, Quotient Rule, antiderivative formulas used throughout)
- [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7]] (the reasoning behind the $+C$ appearing in every general solution above)
