---
module: APM01B1
topic: Polar and Intrinsic Coordinates, Vector Kinematics
session: S1
tags: [definition, formula, theorem, worked-example, common-mistake, added]
---

# APM01B1 — Polar and Intrinsic Coordinates, Vector Kinematics

Position, velocity and acceleration are vector-valued functions of time. This note builds the two moving-basis frames used to describe motion, polar $(\hat r, \hat\theta)$ and tangential-normal $(\hat T, \hat n)$, from first principles, then applies Newton's second law to recover the path equation.

## Position, velocity, acceleration

Given a path equation $\vec r(t)$:

$$\vec v(t) = \dot{\vec r}(t) = \frac{d\vec r}{dt}, \qquad \vec a(t) = \dot{\vec v}(t) = \frac{d\vec v}{dt} = \frac{d^2\vec r}{dt^2}$$

Kinematics studies this path equation itself, it does not ask how the motion came about, that question is dynamics (see: Newton's second law and the path equation, below).

> [!note] N.B
> $\vec r(t)$ is the position at time $t$, not merely a curve in space. The parameter $t$ carries timing information a bare curve does not.

## Average vs instantaneous velocity

Average velocity over an interval needs only the position at the endpoints:

$$\vec v_{ave} = \frac{\Delta \vec r}{\Delta t} = \frac{\vec r(t_1) - \vec r(t_0)}{t_1 - t_0}$$

This is not the mean of the instantaneous velocities at the endpoints:

$$\vec v_{mean} = \frac{\vec v_1 + \vec v_2}{2} \neq \vec v_{ave}$$

$\vec v_{mean}$ requires instantaneous velocity (a derivative) at each endpoint. $\vec v_{ave}$ requires only instantaneous position, i.e. the path equation.

Example ($r(t)=\sin(\omega t)$, $\omega = 2\pi$):

$$v(t) = 2\pi\cos(2\pi t), \qquad v(0) = 2\pi, \quad v(3) = 2\pi$$

$$v_{mean} = \frac{v(0)+v(3)}{2} = 2\pi \qquad \text{(averaging the two endpoint speeds)}$$

Over $[t_0,t_1]=[0,3]$, since $r(0)=r(3)=0$:

$$v_{ave} = \frac{r(3)-r(0)}{3-0} = \frac{0-0}{3} = 0$$

> [!note] N.B
> $v_{ave}=0$ here because the particle returned to its starting position, not because its instantaneous speed was ever small. $v_{ave}$ and $v_{mean}$ answer different questions and there is no general reason for them to agree.

## Vector differentiation rules

For two vectors written in the fixed Cartesian basis, $\vec a(t) = a_x(t)\hat x + a_y(t)\hat y + a_z(t)\hat z$ and similarly for $\vec b(t)$:

$$\frac{d\vec a}{dt} = \frac{da_x}{dt}\hat x + \frac{da_y}{dt}\hat y + \frac{da_z}{dt}\hat z$$

Since $\hat x,\hat y,\hat z$ are constant, they need not be differentiated (no product rule on them).

**Linearity:**

$$\frac{d}{dt}\big(\alpha\vec a(t) + \beta\vec b(t)\big) = \alpha\frac{d\vec a}{dt} + \beta\frac{d\vec b}{dt}$$

This follows immediately by differentiating componentwise and factoring the constants $\alpha,\beta$ back out.

**Product rule for the dot product:**

$$\frac{d}{dt}(\vec a\cdot\vec b) = \frac{d\vec a}{dt}\cdot\vec b + \vec a\cdot\frac{d\vec b}{dt}$$

*Proof.* Write $\vec a\cdot\vec b = a_xb_x+a_yb_y+a_zb_z$, a sum of ordinary scalar products. Differentiate term by term with the ordinary product rule:

$$\frac{d(\vec a\cdot\vec b)}{dt} = \frac{da_x}{dt}b_x + a_x\frac{db_x}{dt} + \dots = \frac{d\vec a}{dt}\cdot\vec b + \vec a\cdot\frac{d\vec b}{dt} \qquad \blacksquare$$

**Product rule for scalar-times-vector**, used repeatedly below:

$$\frac{d}{dt}\big(f(t)\,\vec a(t)\big) = \frac{df}{dt}\vec a + f\frac{d\vec a}{dt}$$

## Parametric motion, 2D vs 1D graphs

A path in the plane, $\vec r(t) = x(t)\hat x + y(t)\hat y$, is a parametric plot. Projectile motion is normally drawn as $y$ against $x$ (a "normal" $y(x)$ graph), which looks identical in shape to the $y$-vs-$t$ curve. This is not a coincidence.

For a projectile under gravity, $\vec F = (0,-mg)$ and $\vec F = m\vec a$ give

$$x''(t) = 0, \qquad y''(t) = -mg/m = -g$$

Integrating:

$$x = x_0 + v_0^x t, \qquad y = -\tfrac12 g t^2 + v_0^y t + y_0$$

Since $x$ is linear in $t$, solving for $t = \dfrac{x-x_0}{v_0^x}$ and substituting into $y(t)$ gives $y = ax^2+bx+c$, a parabola in $x$ exactly as $y(t)$ is a parabola in $t$. The 2D and 1D graphs look alike because $x(t)$ is linear, a straight rescaling of the time axis into the $x$ axis, not a general property of parametric plots.

> [!note] N.B
> Parametric plots are not, in general, univariate scalar functions ($y$ as a single-valued function of $x$). Circular motion is the standard counterexample, the same $x$ corresponds to two different $y$ values.

## Galilean invariance

Comparing Newton's second law in two frames, "my frame" ($x_1 = \vec x(t)$) and "your frame" (shifted by $\vec x_1$, i.e. position $\vec x_1(t) + \vec x(t)$ in my coordinates):

$$\vec F = m\ddot{\vec x}_1 \qquad \vec f_1 = m(\vec a_1+\vec a) = m\frac{d^2}{dt^2}(\vec x_1+\vec x) = m\left(\frac{d^2\vec x_1}{dt^2} + \frac{d^2\vec x}{dt^2}\right)$$

The only way $\vec F = \vec f_1 = m\vec a$ holds in both frames is if the extra term vanishes, i.e. if $\vec x_1(t) = \vec x_0 + \vec v_0 t$: the second frame moves at constant velocity relative to the first (no relative acceleration). This is Galilean invariance, Newton's second law keeps the same form under a constant-velocity change of frame.

-> This sets up why $\vec F = m\vec a$ is called a coordinate-independent statement, see Newton's second law below.

## Polar coordinates: why $\hat r, \hat\theta$ are needed

Cartesian $\hat x,\hat y$ are fixed, $\dfrac{d\hat x}{dt}=\dfrac{d\hat y}{dt}=0$. Polar coordinates instead co-move with the particle, but they still remember the Cartesian origin.

We want $\hat r,\hat\theta$ to behave like $\hat x,\hat y$ in one respect: $\hat r\cdot\hat r = \hat\theta\cdot\hat\theta = 1$ and $\hat r\cdot\hat\theta = 0$ (orthonormal). Unlike $\hat x,\hat y$, they are not constant.

**Constructing $\hat r$.** From $\vec r = r_x\hat x + r_y\hat y$ with $r_x=r\cos\theta,\ r_y=r\sin\theta$:

$$\hat r = \frac{\vec r}{|\vec r|} = \cos\theta\,\hat x + \sin\theta\,\hat y$$

**Constructing $\hat\theta$.** We need $\hat\theta$ orthogonal to $\hat r$, i.e. $\hat r\cdot\hat\theta=0$. By inspection of $\hat r$:

$$\hat\theta = -\sin\theta\,\hat x + \cos\theta\,\hat y$$

Related quantities:

$$r = \sqrt{x^2+y^2}, \qquad \theta = \arctan(y/x), \qquad x=r\cos\theta,\ y=r\sin\theta$$

$\hat r$ is the unit vector pointing away from the origin at the particle. $\hat\theta$ points perpendicular to $\hat r$, in the direction of increasing $\theta$.

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.2]
  \draw[->] (-0.5,0) -- (4,0) node[right] {$x$};
  \draw[->] (0,-0.5) -- (0,3.5) node[above] {$y$};
  \draw[->, thick] (0,0) -- (2.5,2);
  \node at (1.4,0.9) {$r$};
  \draw (0.6,0) arc (0:38.7:0.6);
  \node at (0.9,0.22) {$\theta$};
  \draw[->, thick, blue] (2.5,2) -- (3.13,2.5) node[right] {$\hat r$};
  \draw[->, thick, red] (2.5,2) -- (2.0,2.63) node[above] {$\hat\theta$};
  \filldraw (2.5,2) circle (1.5pt);
\end{tikzpicture}
\end{document}
```

> [!note] N.B
> Since $\hat x,\hat y$ are fixed but $\hat r,\hat\theta$ move with the particle, $\dfrac{d\hat r}{dt}\neq 0$ in general, even though $\dfrac{d\hat x}{dt}=0$. If $\theta$ happens to be constant, then $\dfrac{d\hat r}{dt}=0$ too, since $\hat r$ only changes because $\theta$ changes.

### Time derivatives of $\hat r$ and $\hat\theta$

For $\theta = \theta(t)$, differentiate with the chain rule:

$$\frac{d}{dt}(\cos\theta\,\hat x + \sin\theta\,\hat y) = -\dot\theta\sin\theta\,\hat x + \dot\theta\cos\theta\,\hat y = \dot\theta(-\sin\theta\,\hat x+\cos\theta\,\hat y) = \dot\theta\,\hat\theta$$

$$\frac{d}{dt}(-\sin\theta\,\hat x + \cos\theta\,\hat y) = -\dot\theta\cos\theta\,\hat x - \dot\theta\sin\theta\,\hat y = -\dot\theta(\cos\theta\,\hat x+\sin\theta\,\hat y) = -\dot\theta\,\hat r$$

$$\boxed{\dfrac{d\hat r}{dt} = \dot\theta\,\hat\theta} \qquad\qquad \boxed{\dfrac{d\hat\theta}{dt} = -\dot\theta\,\hat r}$$

This extends to 3D as cylindrical polar coordinates, adding a fixed $\hat z$ with $\hat r\times\hat\theta=\hat z$.

## Velocity and acceleration in polar coordinates

Starting from $\vec r = r(t)\,\hat r(\theta(t))$ and applying the product rule plus the boxed results above:

$$\vec v = \frac{d\vec r}{dt} = \dot r\,\hat r + r\dot\theta\,\hat\theta = v_r\hat r + v_\theta\hat\theta$$

Differentiating again:

$$\vec a = \frac{d\vec v}{dt} = \ddot r\,\hat r + \dot r\dot\theta\,\hat\theta + \dot r\dot\theta\,\hat\theta + r\ddot\theta\,\hat\theta - r\dot\theta^2\hat r$$

$$\boxed{\vec a = \big(\ddot r - r\dot\theta^2\big)\hat r + \big(r\ddot\theta + 2\dot r\dot\theta\big)\hat\theta}$$

Four named terms:

1. $\ddot r$: radial acceleration
2. $r\ddot\theta$: angular acceleration
3. $-r\dot\theta^2$: centripetal acceleration
4. $2\dot r\dot\theta$: Coriolis acceleration

## Worked example: circular spiral

$r(\theta) = R\theta$ (radius grows linearly with angle, an outward spiral, radius increases as $\theta$ increases).

```desmos-graph
left=-12; right=12; top=12; bottom=-12;
---
r=\theta\left\{0\le\theta\le4\pi\right\}
```

Extension example, $\vec r(t) = t\cos t\,\hat x + t\sin t\,\hat y$:

$$\vec v(t) = \cos t\,\hat x + \sin t\,\hat y + (t\cos t\,\hat y - t\sin t\,\hat x)$$

$$\frac{\vec r}{r} = \cos t\,\hat x + \sin t\,\hat y \quad\Rightarrow\quad \theta(t) = \arctan\!\left(\frac{t\sin t}{t\cos t}\right) = \arctan(\tan t) = t$$

$$\hat\theta = -\sin\theta\,\hat x+\cos\theta\,\hat y = -\sin t\,\hat x + \cos t\,\hat y$$

Then, using $\vec r = r(\theta)\hat r$ with the chain rule $\dfrac{d\vec r}{dt} = \dfrac{dr}{d\theta}\dfrac{d\theta}{dt}\hat r + r\dot\theta\,\hat\theta$ (setting up the general form used again in the Coriolis section below):

$$\frac{d\vec r}{dt} = \frac{dr}{dt}\hat r + r\frac{d\hat r}{dt}$$

-> This chain-rule form is exactly what produces the Coriolis breakdown in the next section.

## Worked example: $\hat r(t), \hat\theta(t)$ for a non-circular path

For $\vec r(t) = \sin t\,\hat x + \sin(2t)\,\hat y$:

```desmos-graph
left=-1.5; right=1.5; top=1.5; bottom=-1.5;
---
(\sin(t),\sin(2t))\left\{0\le t\le2\pi\right\}
```

$$\hat r(t) = \frac{\vec r}{|\vec r|} = \frac{\sin t\,\hat x + \sin(2t)\,\hat y}{\sqrt{\sin^2 t+\sin^2 2t}} = \frac{\hat x + 2\cos t\,\hat y}{\sqrt{1+4\cos^2 t}}$$

(added) The last step divides top and bottom by $\sin t$, so it holds where $\sin t>0$. Where $\sin t<0$ the whole vector flips sign.

$$\hat\theta(t) = -\sin\theta\,\hat x+\cos\theta\,\hat y = \hat z\times\hat r = \frac{-2\cos t\,\hat x + \hat y}{\sqrt{1+(2\cos t)^2}}$$

Transverse speed by projection:

$$v_\theta = r\dot\theta = \vec v\cdot\hat\theta = (\cos t\,\hat x + 2\cos 2t\,\hat y)\cdot\frac{-2\cos t\,\hat x+\hat y}{\sqrt{1+(2\cos t)^2}} = \frac{-2\cos^2 t+2\cos 2t}{\sqrt{1+(2\cos t)^2}}$$

then $\dot\theta = v_\theta/r$, and radial acceleration follows from $a_r = \vec a\cdot\hat r = \ddot r - r\dot\theta^2$.

## Tangential-normal (intrinsic) coordinates

### Motivation

$\hat r = \vec r/r$ depends on the origin: shifting the origin changes $\hat r$ even though the path itself is unchanged. We want a frame that is independent of this choice.

The first such vector is the velocity, $\vec v = \dfrac{d\vec r}{dt}$, since it depends only on the shape of the path, not on where the origin sits. Normalising gives the **tangent vector**:

$$\hat T = \frac{\vec v}{\|\vec v\|}$$

We then need something orthonormal to $\hat T$, call it $\hat n$. Recall $\hat x\times\hat y=\hat z$, and similarly $\hat y\times\hat z=\hat x$, $\hat z\times\hat x=\hat y$. Introduce $\hat z$ orthogonal to $\hat T$ and $\hat n$ (out of the page). Then by the same right-handed convention:

$$\hat T\times\hat n = \hat z, \qquad \hat n\times\hat z=\hat T, \qquad \hat z\times\hat T=\hat n$$

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.2]
  \draw[->] (-0.5,0) -- (4,0) node[right] {$x$};
  \draw[->] (0,-0.5) -- (0,3) node[above] {$y$};
  \draw[thick] (0,0.3) to[out=20,in=200] (3.5,2.2);
  \filldraw (2.2,1.5) circle (1.5pt);
  \draw[->, thick, blue] (2.2,1.5) -- (2.9,1.95) node[right] {$\hat T$};
  \draw[->, thick, red] (2.2,1.5) -- (1.75,2.15) node[above] {$\hat n$};
  \draw (2.2,1.5) -- (2.9,1.5);
  \draw (2.55,1.5) arc (0:35:0.35);
  \node at (2.75,1.62) {$\psi$};
\end{tikzpicture}
\end{document}
```

> [!warning] Common mistake
> Despite the structural similarity, $(\hat T,\hat n)$ are **not the same** as $(\hat r,\hat\theta)$. $\hat T$ is fixed by the direction of motion, not by direction from the origin, and $\hat n$ points toward the concave side of the path, not necessarily perpendicular to a position vector.

### Time derivatives of $\hat T$ and $\hat n$

Let $\psi$ be the angle $\hat T$ makes with the $x$-axis:

$$\hat T = \cos\psi\,\hat x + \sin\psi\,\hat y, \qquad \hat n = -\sin\psi\,\hat x + \cos\psi\,\hat y$$

With respect to the tangent angle $\psi$ (not time):

$$\frac{d\hat T}{d\psi} = \hat n, \qquad \frac{d\hat n}{d\psi} = -\hat T$$

For a general path, can $\Delta s$ (arc length) be treated as the arc of a circle as $\Delta\psi\to0$? Not in general. But define the radius of curvature $\rho$ (curvature itself is $1/\rho$) by

$$\frac{d\psi}{ds} = \frac{1}{\rho}$$

Then by the chain rule (spatial differentiation denoted by primes here, temporal by dots):

$$\frac{d\hat T}{dt} = \frac{d\hat T}{d\psi}\cdot\frac{d\psi}{ds}\cdot\frac{ds}{dt} = \hat n\cdot\frac{1}{\rho}\cdot v$$

$$\frac{d\hat n}{dt} = \frac{d\hat n}{d\psi}\cdot\frac{d\psi}{ds}\cdot\frac{ds}{dt} = -\hat T\cdot\frac{1}{\rho}\cdot v$$

$$\boxed{\dfrac{d\hat T}{dt} = \dfrac{v}{\rho}\hat n} \qquad\qquad \boxed{\dfrac{d\hat n}{dt} = -\dfrac{v}{\rho}\hat T}$$

### Acceleration in tangential-normal coordinates

Since $\vec v = v\hat T$:

$$\vec a = \frac{d\vec v}{dt} = \dot v\,\hat T + v\frac{d\hat T}{dt} = \dot v\,\hat T + \frac{v^2}{\rho}\hat n$$

$$\boxed{\vec a = \dot v\,\hat T + \dfrac{v^2}{\rho}\hat n}$$

Given $\vec v$, the tangent, normal, and tangential acceleration component can be recovered by:

$$\hat T = \frac{\vec v}{v}, \qquad \hat n = \hat z\times\hat T, \qquad a_T = \vec a\cdot\hat T$$

> [!note] N.B
> $\hat n$ is always perpendicular to the path (to $\hat T$), by construction, not by any relation to the origin.

## Worked example: straight line into a circle

A driver moves at constant speed $v_0$, path straight then curving into a circle then straight again:

$$\vec r = \begin{cases} v_0 t\,\hat x & 0<t<t_1 \\ v_0\cos\psi\,\hat x+v_0\sin\psi\,\hat y & t_1<t<t_2 \\ v_0 t\,\hat y & t>t_2\end{cases}
\qquad
\hat T = \begin{cases} \hat x & 0<t<t_1 \\ \cos\psi\,\hat x+\sin\psi\,\hat y & t_1<t<t_2 \\ \hat y & t>t_2\end{cases}$$

$$\vec v = v_0\hat T$$

Speed is constant ($\dot v=0$) throughout, so on the straight sections $\vec a=0$. The interesting part is $t_1<t<t_2$, the circular arc, where

$$\vec a = \dot v\,\hat T + \frac{v^2}{\rho}\hat n = \frac{v^2}{\rho}\hat n \quad\Rightarrow\quad \|\vec a\| = \frac{v^2}{\rho}$$

-> This connects directly to Newton's second law below: knowing $\vec a(t)$ from the path is what lets us ask what force produced it.

## Newton's second law and the path equation

The general form of Newton's second law, valid even for changing mass, is momentum-based:

$$\frac{d\vec p}{dt} = \vec F, \qquad \vec p = m\vec v$$

For constant mass:

$$\frac{d(m\vec v)}{dt} = \vec F \;\Rightarrow\; m\frac{d\vec v}{dt} = \vec F \;\Rightarrow\; m\vec a = \vec F$$

Treating Newton's second law as an equation to solve for the path equation $\vec r(t)$ given $\vec a(t) = \vec F/m$: integrate twice.

$$\int\vec a(t)\,dt = \vec v(t) + \vec A, \qquad \int\vec v(t)\,dt = \vec r(t) + \vec A t + \vec B$$

Rephrased as a second-order ODE (system of 2nd order ordinary differential equations, since it applies componentwise to $x,y,z$):

$$m\frac{d^2\vec r}{dt^2} = \vec F \quad(\text{constant mass})$$

### Worked example: constant force, $\vec F = -mg\hat z$

Given $\vec r(0)=\vec 0$, $\vec v(0) = \hat x+2\hat y+3\hat z$, find $\vec r(t)$.

Componentwise, $m\ddot x=0,\ m\ddot y=0,\ m\ddot z=-mg$, i.e. $m\ddot{\vec r}=\vec F$.

Integrating once:

$$m\int\ddot{\vec r}\,dt = \int\vec F_{const}\,dt \;\Rightarrow\; \dot{\vec r} = \frac{\vec Ft}{m}+\vec c$$

$\vec c$ is the constant of integration; setting $t=0$ shows $\vec c = \dot{\vec r}(0) = \vec v(0)$, so

$$\vec v(t) = \frac{\vec F t}{m} + \vec v(0)$$

Integrating a second time, from $t=0$:

$$\vec r(t) - \vec r(0) = \frac{\vec F t^2}{2m} + \vec v(0)\,t$$

Substituting $\vec F=-mg\hat z$, $\vec r(0)=\vec 0$, $\vec v(0)=\hat x+2\hat y+3\hat z$:

$$\vec r(t) = \frac{-mg\hat z\,t^2}{2m} + (\hat x+2\hat y+3\hat z)\,t = t\,\hat x + 2t\,\hat y + \left(3t-\tfrac12 g t^2\right)\hat z$$

## Two edge cases for solving $m\ddot{\vec r}=\vec F$

1. **Constant force.** Specify $\vec r(0)$ and $\vec v(0)$, then ask for $\vec r(t)$.
2. **Time-dependent force.** Specify $\vec r(0)$ and $\vec r(1)$ (two position conditions, not a position and a velocity), then ask for $\vec v(0)$.

Setup only (source did not carry this to completion): a person applies a force to an object on an incline at angle $\theta$ to the horizontal. This is presented as a scaffold for setting up $\vec F=m\vec a$ with resolved components along the incline, not as a finished example.

## (added) Deriving the Q4-style angle identity from $\hat r,\hat\theta$ projections

> [!note] Added, not from source
> This derivation was intentionally left for students to build using the projection technique already taught (see: Velocity and acceleration in polar coordinates). It is included here for completeness, but it is not a lecturer-supplied derivation, see `APM01B1_Proofs_ST1.md` for the exact sourcing distinction.

For $\vec v = a\hat x+b\hat y$, projecting onto $\hat r,\hat\theta$ gives $\dot r = a\cos\theta+b\sin\theta$ and $r\dot\theta=-a\sin\theta+b\cos\theta$. Scaling and combining to cancel the cross term:

$$a\dot r + b\,r\dot\theta = (a^2+b^2)\cos\theta \;\Rightarrow\; \theta = \arccos\!\left(\frac{a\dot r+b\,r\dot\theta}{v^2}\right)$$

$$b\dot r - a\,r\dot\theta = (a^2+b^2)\sin\theta \;\Rightarrow\; \theta = \arcsin\!\left(\frac{b\dot r-a\,r\dot\theta}{v^2}\right)$$

with $v^2=a^2+b^2$.

## Do not forget

- $\dfrac{d\hat r}{dt}=\dot\theta\hat\theta$ and $\dfrac{d\hat\theta}{dt}=-\dot\theta\hat r$, this single pair builds both $\vec v$ and $\vec a$ in polar form.
- $(\hat T,\hat n)$ are not $(\hat r,\hat\theta)$, despite the same construction pattern.
- $\vec v_{ave}$ needs only endpoint positions, $\vec v_{mean}$ needs instantaneous velocity at each endpoint, they are not generally equal.
- The two edge cases for $m\ddot{\vec r}=\vec F$ are told apart by which pair of conditions is given: $(\vec r(0),\vec v(0))$ for constant force, $(\vec r(0),\vec r(1))$ for time-dependent force.
- Galilean invariance: $\vec F=m\vec a$ keeps its form under a frame change only if the two frames differ by a constant velocity.

## Amendments
- Final pass (27 Oct 2026): spiral example chain rule corrected to $\dfrac{d\vec r}{dt}=\dfrac{dr}{d\theta}\dot\theta\,\hat r+r\dot\theta\,\hat\theta$ (it was written as $d\hat r/dt$ with a wrong second term).
- Final pass (27 Oct 2026): non-circular path example, $\hat\theta$ sign fixed to $-\sin\theta\,\hat x+\cos\theta\,\hat y$; $\vec v$ typo fixed to $\cos t\,\hat x+2\cos 2t\,\hat y$ (the final $v_\theta$ was already right); added the $\sin t>0$ condition on the simplified $\hat r$.
- Final pass (27 Oct 2026): $d\hat T/d\psi$ is with respect to the tangent angle $\psi$, not arc length; $\rho$ named as the radius of curvature. Em dashes removed from the Coriolis term list (R8).
