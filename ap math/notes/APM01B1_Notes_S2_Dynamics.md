---
module: APM01B1
topic: Dynamics of a Particle
session: S2
tags: [definition, formula, theorem, worked-example, common-mistake, added]
---

# APM01B1 — Dynamics of a Particle

Kinematics describes motion; dynamics asks what force produced it, or, given a force, what motion follows. Every example in this chapter solves the same equation, $m\ddot{\vec r}=\vec F$, or its momentum form $\dfrac{d\vec p}{dt}=\vec F$ (defined in: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Newton's second law and the path equation]]), the differences between examples are entirely in what kind of object $\vec F$ is: a constant, a function of $t$, a function of $v$, or a function of $r$. That classification, taken directly from the source's own end-of-chapter recap, is the map for this whole chapter:

> [!note] Roadmap
> - $\vec F = \text{const}$ or $\vec F=\vec F(t)$ -> direct integration (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Two edge cases for solving $m\ddot{\vec r}=\vec F$]], and Time-dependent force below)
> - $\vec F=\vec F(v)$ -> use $a=\dfrac{dv}{dt}=v\dfrac{dv}{dr}$, gives an exponential or power-law solution (see: Speed-dependent force below)
> - $\vec F=\vec F(r)$ -> ansatz/guess a solution and verify it, e.g. $r=\sin\omega t$ (see: Position-dependent force below)
> - Not every $\vec F=m\vec a$ is solvable analytically.

Also carried forward without repetition: inertial systems. A frame is inertial exactly when $\vec F=m\vec a$ holds in it without correction terms, which is precisely the Galilean-invariance condition already derived (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Galilean invariance]]): two frames related by a constant relative velocity are both inertial or both not.

## Time-dependent force: an incline worked example

A person pushes an object up a ramp inclined at angle $\theta$ to the horizontal, with a force that decays over time:

$$\vec F = F_0e^{-t}\,\hat x$$

where $\hat x$ points up the slope. Gravity resolves into a component down the slope and a component into the slope:

$$\vec F_{net} = F_0e^{-t}\,\hat x - mg\sin\theta\,\hat x - mg\cos\theta\,\hat y$$

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.1]
  \draw[thick] (0,0) -- (4,0) -- (4,2.2) -- cycle;
  \draw (0.5,0) arc (0:28.6:0.5);
  \node at (0.85,0.18) {$\theta$};
  \filldraw (1.6,0.88) circle (2pt);
  \draw[->,thick,blue] (1.6,0.88) -- (3.1,1.71) node[right] {$\hat x$};
  \draw[->,thick,red] (1.6,0.88) -- (2.24,-0.18) node[below] {$\hat y$};
  \draw[->,thick] (1.6,0.88) -- (2.35,1.32) node[above] {$\vec F_0e^{-t}$};
\end{tikzpicture}
\end{document}
```

Because the object stays on the ramp, the perpendicular ($\hat y$) component of gravity is exactly balanced by the normal force, so only the $\hat x$ equation carries any motion:

$$m\ddot x = F_0e^{-t} - mg\sin\theta \;\Rightarrow\; \ddot x = \frac{F_0}{m}e^{-t} - g\sin\theta$$

Integrating once:

$$\dot x = -\frac{F_0}{m}e^{-t} - (g\sin\theta)t + v_0$$

where $v_0$ is the constant of integration (it is not automatically the initial speed; setting $t=0$ gives $\dot x(0) = -F_0/m + v_0$, so $v_0$ is only the initial speed once the $-F_0/m$ offset is accounted for). Integrating again:

$$x(t) = \frac{F_0}{m}e^{-t} - \tfrac12(g\sin\theta)t^2 + v_0t + r_0$$

with $r_0$ the second constant of integration, fixing where on the ramp the object starts.

For a general time-dependent force $\vec F=\vec F(t)$ this pattern always gives:

$$\vec x(t) = \frac{1}{m}\int\!\left(\int\vec F(t)\,dt\right)dt + \vec v_0t + \vec r_0$$

> [!note] N.B
> The trick that makes multi-dimensional problems collapse to one equation is checking which components of $\vec F_{net}$ are cancelled by a constraint force (here, the normal force). Always isolate the *unbalanced* component before integrating.

## Speed-dependent force: friction and terminal velocity

### Setup and terminal velocity

A body falling under gravity with linear drag experiences a resistive force opposing its velocity, $\vec F_{fric}=-k\vec v$. For a vertical fall (downward $\hat z$):

$$\vec F_{net} = -mg\hat z - kv\hat z \;\Rightarrow\; m\ddot z = -mg - k\dot z$$

At terminal velocity the acceleration vanishes, $\ddot z=0$:

$$0 = -mg - k\dot z_{term} \;\Rightarrow\; \dot z_{term} = -\frac{mg}{k}$$

> [!note] N.B
> Terminal velocity is found by setting acceleration to zero directly in the force balance, it never requires solving the full differential equation.

### Solving for $z(t)$: separation of variables

Integrating $m\ddot z=-mg-k\dot z$ once directly (every term is either already a derivative or trivially antidifferentiable in $t$):

$$m\dot z = -mgt - kz + C \;\Rightarrow\; \frac{dz}{dt} = -gt - \frac{k}{m}z + C$$

This can't be integrated again as it stands: the right-hand side depends on the unknown $z$ itself, not only on $t$. As a warm-up in separating variables, ignore the $-gt$ term for a moment (pure mathematics, not the physical equation):

$$\frac{dz}{dt} = -kz + C \;\Rightarrow\; dz = (-kz+C)\,dt \;\Rightarrow\; \frac{dz}{-kz+C} = dt$$

Now the variables are separated, $z$ terms on the left, $t$ on the right, so both sides can be integrated. Substitute $Z=-kz+C$, $dZ=-k\,dz$:

$$-\frac1k\int\frac{dZ}{Z} = \int dt \;\Rightarrow\; -\frac1k\ln Z = t + C_2 \;\Rightarrow\; Z = Ke^{-kt}$$

$$-kz + C = Ke^{-kt} \;\Rightarrow\; z(t) = \frac{C}{k} - \frac{K}{k}e^{-kt}$$

> [!note] N.B
> Morale of the story: **any** equation of the shape $\dot z = -kz + (\text{const})$ produces an $e^{-kt}$ solution. Recognising this pattern (defined in: Position-dependent force, ansatz method below) saves re-deriving it from scratch every time it appears.

### Solving for $v(z)$: the $v\,dv/dz$ trick

The equation with gravity restored, $\ddot z = -g - \dfrac{k}{m}\dot z$, is more useful rewritten in terms of displacement rather than time, using the same chain-rule substitution as $v_f^2=v_i^2+2a\Delta s$ in kinematics:

$$a = \frac{d^2z}{dt^2} = \frac{d\dot z}{dt} = \frac{d\dot z}{dz}\cdot\frac{dz}{dt} = \dot z\frac{d\dot z}{dz}$$

Writing $\dot z = v$:

$$a = v\frac{dv}{dz}$$

so Newton's second law becomes

$$v\frac{dv}{dz} = -g - \frac{k}{m}v$$

This is now separable in $v$ and $z$:

$$\int_{v_0}^{v}\frac{v'\,dv'}{g+\frac{k}{m}v'} = \int_{z_0}^{z}(-1)\,dz'$$

Let $u = g+\dfrac{k}{m}v$, so $du = \dfrac{k}{m}dv$ and $v = \dfrac{m}{k}(u-g)$:

$$\int\frac{v\,dv}{g+\frac km v} = \frac mk\int\frac{u-g}{u}\,du = \frac mk\int\left(1-\frac gu\right)du = \frac mk\big(u - g\ln u\big)$$

$$\Rightarrow\; \frac mk\left[g+\frac km v - g\ln\!\left(g+\frac km v\right)\right]_{v_0}^{v} = -(z-z_0)$$

> [!note] N.B
> Not every $\vec F=m\vec a$ is solvable analytically in closed form for $z(t)$ directly, this result is an *implicit* relation between $v$ and $z$, and is exactly as much of a solution as the equation admits.

## Position-dependent force: springs and simple harmonic motion

### Setup

Hooke's law gives the spring force

$$\vec F = -k(x-x_0)\,\hat x$$

```tikz
\begin{document}
\begin{tikzpicture}[scale=1]
  \draw (0,0) -- (0,1.2);
  \draw (0,0.6) -- (0.25,0.6) -- (0.5,0.9) -- (0.75,0.3) -- (1.0,0.9) -- (1.25,0.3) -- (1.5,0.9) -- (1.75,0.3) -- (2,0.6);
  \draw (2,0) rectangle (3,1.2);
  \node at (2.5,0.6) {$m$};
\end{tikzpicture}
\end{document}
```

Newton's second law, $\vec F=m\vec a$, gives

$$\ddot x = -\frac{k}{m}(x-x_0)$$

### The ansatz method

This can't be integrated by the earlier methods (it is neither constant, nor a function of $t$ alone, nor separable in $\dot x$). Shift the origin to $x_0$: let $\xi(t)=x(t)-x_0$, so $\dot x=\dot\xi$, $\ddot x=\ddot\xi$, and

$$\ddot\xi = -\frac km\xi$$

**Guess** a solution (an ansatz):

$$\xi(t) = A\cos\omega t + B\sin\omega t$$

Check that it actually solves the equation:

$$\ddot\xi = -A\omega^2\cos\omega t - B\omega^2\sin\omega t = -\omega^2\xi$$

Substituting into $\ddot\xi=-\frac km\xi$:

$$-\omega^2(A\cos\omega t+B\sin\omega t) = -\frac km(A\cos\omega t+B\sin\omega t) \;\Rightarrow\; \frac km-\omega^2=0$$

$$\boxed{\omega = \sqrt{\frac km}}$$

> [!note] N.B
> The ansatz only works for this specific $\omega$. Guessing a solution and verifying it is a legitimate solving method precisely because the verification step pins down every free parameter the guess did not already fix; $A$ and $B$ themselves are then found from initial or boundary conditions.

So the general position-dependent-force solution is

$$x(t) = A\cos\!\left(\sqrt{\tfrac km}\,t\right) + B\sin\!\left(\sqrt{\tfrac km}\,t\right) + x_0$$

**Equivalent complex-exponential form.** Using $e^{i\theta}=\cos\theta+i\sin\theta$, the same ansatz can be written $\xi(t)=Ae^{i\omega t}+Be^{-i\omega t}$. Differentiating twice, $\ddot\xi = -A\omega^2e^{i\omega t}+\dots = -\omega^2\xi$, the same condition $\omega=\sqrt{k/m}$ falls out. This is the same result reached by a different route, useful when the driving or damping terms make the exponential form easier to manipulate.

### (added) Worked example: two masses coupled by a spring

> [!note] Added, not from primary source
> Not present in the photographed handwritten notes or `Notes_-_Chapter_4.pdf`; included because a tutorial question (Tutorial 8) requires it and it reuses the ansatz method above rather than introducing new machinery.

Two particles of mass $m_1,m_2$, connected by a spring of stiffness $k$ and natural length $L_0$, rest on a smooth horizontal surface with $x_2>x_1$.

```tikz
\begin{document}
\begin{tikzpicture}[scale=1]
  \draw (0,0) rectangle (1,0.8);
  \node at (0.5,0.4) {$m_1$};
  \draw (1,0.4) -- (1.25,0.4) -- (1.5,0.7) -- (1.75,0.1) -- (2.0,0.7) -- (2.25,0.1) -- (2.5,0.7) -- (2.75,0.1) -- (3,0.4);
  \draw (3,0) rectangle (4,0.8);
  \node at (3.5,0.4) {$m_2$};
  \draw (-0.3,0) -- (4.3,0);
\end{tikzpicture}
\end{document}
```

Newton's second law on each mass separately (the spring pulls each toward the other when stretched):

$$m_1\ddot x_1 = k(x_2-x_1-L_0), \qquad m_2\ddot x_2 = -k(x_2-x_1-L_0)$$

Introduce the **relative displacement** $x_d=x_2-x_1$ and the **centre of mass** $x_c=\dfrac{m_1x_1+m_2x_2}{m_1+m_2}$.

**Centre of mass equation.** Adding the two equations of motion directly:

$$m_1\ddot x_1+m_2\ddot x_2 = k(x_2-x_1-L_0)-k(x_2-x_1-L_0) = 0 \;\Rightarrow\; \ddot x_c = 0$$

The centre of mass moves at constant velocity, exactly as expected since the spring is an internal force with no external force on the two-body system (see: Momentum, and Law of Conservation of Momentum, below).

**Relative equation.** Subtracting the $m_1$ equation (divided by $m_1$) from the $m_2$ equation (divided by $m_2$):

$$\ddot x_d = \ddot x_2-\ddot x_1 = -\frac{k}{m_2}(x_2-x_1-L_0)-\frac{k}{m_1}(x_2-x_1-L_0) = -k\left(\frac1{m_1}+\frac1{m_2}\right)(x_d-L_0)$$

Defining the **reduced mass** $\mu=\dfrac{m_1m_2}{m_1+m_2}$, so $\dfrac1\mu=\dfrac1{m_1}+\dfrac1{m_2}$:

$$\ddot x_d = -\frac{k}{\mu}(x_d-L_0)$$

This is exactly the SHM equation solved above (shift origin to $L_0$, same ansatz), so the two masses oscillate relative to each other with

$$\boxed{\omega=\sqrt{\frac{k}{\mu}} = \sqrt{\frac{k(m_1+m_2)}{m_1m_2}}, \qquad T=\frac{2\pi}{\omega}=2\pi\sqrt{\frac{m_1m_2}{k(m_1+m_2)}}}$$

> [!note] N.B
> The problem separates cleanly into two independent one-body problems (centre of mass moving freely, relative coordinate oscillating) only because $x_c$ and $x_d$ were chosen to decouple the two original equations. This centre-of-mass/relative-coordinate split is a standard technique whenever two particles interact only with each other.

### (added) Worked example: a tunnel through the earth

> [!note] Added, not from primary source
> Not present in the photographed handwritten notes; `Notes_-_Chapter_4.pdf` poses this as a problem and explicitly hints that the position-dependent-force analysis above is applicable, without carrying out the derivation, so it is worked here in full.

By spherical symmetry (shell theorem), a particle at radius $r$ inside a uniform-density earth (radius $R$, mass $M$) feels gravity only from the mass enclosed within radius $r$, $M(r)=M(r/R)^3$:

$$F(r) = -\frac{GM(r)m}{r^2} = -\frac{GMm}{R^3}r$$

This is a **linear restoring force**, the same functional form as the spring force above, with effective stiffness $k_{eff}/m = GM/R^3$. Using $g=GM/R^2$ at the surface, $GM=gR^2$, so

$$\ddot r = -\frac{g}{R}r \;\Rightarrow\; \omega=\sqrt{\frac gR}$$

Dropped from rest at the surface ($r=R$), the particle executes SHM about the centre with amplitude $R$. It reaches the centre ($r=0$) after a quarter period:

$$t_{centre} = \frac T4 = \frac{\pi}{2\omega} = \frac\pi2\sqrt{\frac Rg}$$

and, since $r=0$ is the equilibrium point of the oscillation (where speed is maximal, $v=\omega\times\text{amplitude}$):

$$v_{centre} = \omega R = \sqrt{\frac gR}\,R = \sqrt{gR}$$

> [!note] N.B
> Recognising $F(r)\propto -r$ as "the spring equation with a different constant" is what makes this solvable with zero new machinery, this is the same recognition the chapter's own recap page ("$\vec F=\vec F(r)\to$ ansatz, e.g. $r=\sin\omega t$") is pointing at.

### Worked example: spring pendulum (gravity plus a spring, in polar coordinates)

A mass hangs from a spring of natural length $r_0$, free to swing at angle $\theta$ from the vertical:

```tikz
\begin{document}
\begin{tikzpicture}[scale=1]
  \draw (0,1.2) -- (-1.5,1.2);
  \begin{scope}[shift={(0,1.2)}, rotate=-60.64]
    \draw (0,0) -- (0.23,0) -- (0.46,0.15) -- (0.69,-0.15) -- (0.92,0.15) -- (1.15,-0.15) -- (1.38,0.15) -- (1.61,-0.15) -- (1.836,0);
  \end{scope}
  \filldraw (0.9,-0.4) circle (2.5pt);
  \draw[dashed] (0,1.2) -- (0,-1);
  \draw (0,0.5) arc (270:305:0.7);
  \node at (0.35,0.35) {$\theta$};
\end{tikzpicture}
\end{document}
```

The resultant force is spring plus gravity, $\vec F_{res}=\vec F_{spring}+\vec F_g=-k(r-r_0)\hat r+mg\hat y$. Before applying $\vec F=m\vec a$, $\hat y$ must be written in terms of the moving basis $\hat r,\hat\theta$: from $\hat r=\cos\theta\hat x+\sin\theta\hat y$ and $\hat\theta=-\sin\theta\hat x+\cos\theta\hat y$ (defined in: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Polar coordinates: why $\hat r, \hat\theta$ are needed]]),

$$\sin\theta\,\hat r+\cos\theta\,\hat\theta = \hat y$$

so

$$\vec F_{res} = -k(r-r_0)\hat r + mg(\sin\theta\,\hat r+\cos\theta\,\hat\theta) = \big(mg\sin\theta - k(r-r_0)\big)\hat r + mg\cos\theta\,\hat\theta$$

Equating to $m\vec a$ in polar coordinates (defined in: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Velocity and acceleration in polar coordinates]]) and dividing by $m$:

$$\text{in }\hat r:\quad \ddot r - r\dot\theta^2 = g\sin\theta - \frac km(r-r_0)$$

$$\text{in }\hat\theta:\quad r\ddot\theta+2\dot r\dot\theta = g\cos\theta$$

> [!note] N.B
> This is the general pattern for every polar-coordinates dynamics problem: resolve every force into $\hat r,\hat\theta$, write $\vec F=m\vec a$ using the boxed acceleration from [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Velocity and acceleration in polar coordinates|Kinematics]], then split into two scalar equations by matching components.

### Worked example: central (inverse-square) force

A central force always points along $\hat r$: $\vec F=-\dfrac{k}{r^n}\hat r$. Specialising to gravity ($n=2$, $k=GMm$, force per unit mass $-GM/r^2$):

$$(\ddot r-r\dot\theta^2)\hat r + (r\ddot\theta+2\dot r\dot\theta)\hat\theta = -\frac{GM}{r^2}\hat r$$

$$\text{(1) } \ddot r - r\dot\theta^2 = -\frac{GM}{r^2} \qquad\qquad \text{(2) } r\ddot\theta+2\dot r\dot\theta = 0 \quad(\text{note: zero force in }\hat\theta)$$

**Equation (2)** looks like a product rule run backwards: $\dfrac{d}{dt}(r^2\dot\theta) = r^2\ddot\theta+2r\dot r\dot\theta = r(r\ddot\theta+2\dot r\dot\theta) = 0$, so

$$\boxed{r^2\dot\theta = h = \text{const}} \qquad (\text{angular momentum per unit mass})$$

**Substituting into equation (1)**, using $\dot\theta=h/r^2$:

$$\ddot r - \frac{h^2}{r^3} = -\frac{GM}{r^2}$$

Multiply by $\dot r$ and use the same $v\,dv/dr$ device as in Speed-dependent force above ($\dot r\ddot r = v\,dv/dr$ with $v\equiv\dot r$):

$$\dot r\ddot r = \frac{h^2\dot r}{r^3} - \frac{GM\dot r}{r^2} \;\Rightarrow\; \frac{d}{dr}\!\left(\frac{v^2}{2}\right) = \frac{h^2}{r^3}-\frac{GM}{r^2} \;\Rightarrow\; \frac12v^2 = -\frac{h^2}{2r^2}+\frac{GM}{r}+C$$

Multiplying through by $m$ and regrouping the two kinetic pieces (radial $\dot r$ and tangential, rewritten via $h$) against the gravitational potential energy:

$$\boxed{\left(\frac12mv^2+\frac{h^2m}{2r^2}\right) - \frac{GMm}{r} = E}$$

$$\underbrace{\phantom{\frac12mv^2+\frac{h^2m}{2r^2}}}_{\text{kinetic energy}} \qquad\qquad \underbrace{\phantom{-\frac{GMm}{r}}}_{\text{potential energy}}$$

> [!note] N.B
> $r^2\dot\theta=h$ (conservation of angular momentum) and the energy equation above are both *constants of motion*: quantities that stay fixed along the trajectory even though $r(t)$ and $\theta(t)$ individually change. Deriving a conserved quantity is often more useful than solving the ODE outright, see Rotational motion below for the general theorem behind this.

> [!note] N.B
> Reading $\ddot r = h^2/r^3-GM/r^2$ physically: $h^2/r^3$ behaves like an outward centrifugal acceleration (fictitious, an artefact of the rotating description) while $-GM/r^2$ is the real, inward gravitational acceleration.

## Further examples in polar coordinates: circular motion in a magnetic field

The Lorentz (magnetic) force on a charge $q$ moving with velocity $\vec v$ in a field $\vec B=B\hat z$ is

$$\vec F = q(\vec v\times\vec B)$$

Using polar coordinates for $\vec v=\dot r\hat r+r\dot\theta\hat\theta$:

$$\vec F = q(\dot r\hat r+r\dot\theta\hat\theta)\times B\hat z = Bq\big[\dot r(\hat r\times\hat z)+r\dot\theta(\hat\theta\times\hat z)\big] = -Bq\dot r\,\hat\theta+Bqr\dot\theta\,\hat r$$

(using $\hat r\times\hat z=-\hat\theta$ and $\hat\theta\times\hat z=\hat r$, both consequences of $\hat r\times\hat\theta=\hat z$).

### Via the torque and angular momentum

The moment (torque) of this force about the origin is

$$\vec M = \vec r\times\vec F = r\hat r\times(Bqr\dot\theta\,\hat r-Bq\dot r\,\hat\theta) = -Bqr\dot r\,(\hat r\times\hat\theta) = -Bqr\dot r\,\hat z$$

From the general theorem $\dfrac{d\vec H}{dt}=\vec M$ (defined in: Rotational motion below), and $\vec H=\vec r\times m\vec v = mr^2\dot\theta\,\hat z$ (so $H_r=H_\theta=0$, only $H_z$ is nonzero):

$$\frac{d}{dt}(mr^2\dot\theta) = -Bqr\dot r$$

Using $r\dot r=\tfrac12\dfrac{d}{dt}(r^2)$ on the right:

$$\frac{d}{dt}(mr^2\dot\theta) = -\frac{Bq}{2}\frac{d}{dt}(r^2) \;\Rightarrow\; mr^2\dot\theta + \frac{Bqr^2}{2} = C$$

### Cross-check: direct application of $\vec F=m\vec a$

Equating $\vec F=m\vec a$ in polar coordinates component by component:

$$\text{in }\hat r:\quad \ddot r-r\dot\theta^2 = \frac{Bqr\dot\theta}{m}$$

$$\text{in }\hat\theta:\quad r\ddot\theta+2\dot r\dot\theta = -\frac{Bq\dot r}{m}$$

Both routes, the angular-momentum theorem and the direct component equations, describe the same motion (a charged particle curving in a magnetic field); the angular-momentum route reaches a first integral of the motion directly, the direct route gives the full pair of second-order equations.

> [!note] Aside on classification
> This example is grouped here because it uses the same polar-coordinates $\vec F=m\vec a$ machinery as the spring-pendulum and central-force examples above, and because the source notebook itself works it as a further polar-coordinates application. It does not correspond to any of the specific worked examples in the module's official Chapter 4 notes (which illustrate "further applications of N2" with coupled/constrained systems: pulleys, rotating platforms, beams), so treat the heading as descriptive rather than a citation to a numbered subsection.

## Momentum

Newton's second law in its most general form (already introduced, see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Newton's second law and the path equation]]) is

$$\vec F = \frac{d\vec p}{dt}, \qquad \vec p=m\vec v$$

> [!note] Added, not from source
> **Law of Conservation of Momentum.** If $\vec F=\vec 0$ then $\dfrac{d\vec p}{dt}=\vec 0$, so $\vec p$ is constant: the momentum of a force-free particle never changes. This is the formal statement behind the variable-mass example below, where $\vec F\neq\vec 0$ so $\vec p$ is *not* conserved, and the whole point is tracking how it changes.

### (added) Conservation of momentum for a system of two particles, and collisions

> [!note] Added, not from primary source
> Not present in the photographed handwritten notes or `Notes_-_Chapter_4.pdf`'s momentum/impulse sections; included because a tutorial question (Tutorial 9) requires it directly.

For two particles interacting only with each other (no external force), Newton's third law makes the force each exerts on the other equal and opposite, $\vec F_{12}=-\vec F_{21}$:

$$m_1\dot{\vec v}_1 = \vec F_{12}, \qquad m_2\dot{\vec v}_2 = \vec F_{21} = -\vec F_{12}$$

Adding these:

$$\frac{d}{dt}(m_1\vec v_1+m_2\vec v_2) = \vec 0 \;\Rightarrow\; \boxed{m_1\vec v_1+m_2\vec v_2 = \text{const}}$$

Total momentum of the two-particle system is conserved, regardless of what the internal force $\vec F_{12}$ actually is, even during a collision where it is large, complicated, and short-lived (see: Impulse, above). This single vector equation is not, on its own, enough to find both final velocities after a collision; a second equation comes from the type of collision.

**Elastic collision** (particle 1 with initial speed $u$ strikes stationary particle 2; kinetic energy is also conserved):

$$m_1u = m_1v_1+m_2v_2 \qquad\qquad m_1u^2 = m_1v_1^2+m_2v_2^2$$

Factor the energy equation as a difference of squares and divide by the momentum equation (both rearranged as $m_1(u-v_1)=m_2v_2$ and $m_1(u-v_1)(u+v_1)=m_2v_2^2$):

$$u+v_1 = v_2$$

Substituting back into the momentum equation:

$$\boxed{v_1 = \frac{m_1-m_2}{m_1+m_2}u, \qquad v_2 = \frac{2m_1}{m_1+m_2}u}$$

**Perfectly inelastic collision** (the particles stick together, common final velocity $v_f$, kinetic energy is *not* conserved):

$$m_1u = (m_1+m_2)v_f \;\Rightarrow\; \boxed{v_f = \frac{m_1}{m_1+m_2}u}$$

$$\Delta KE = \tfrac12m_1u^2 - \tfrac12(m_1+m_2)v_f^2 < 0$$

the lost kinetic energy is converted to heat, sound, and deformation, which is precisely what "inelastic" means.

> [!note] N.B
> Momentum conservation holds for **every** collision (elastic or not), because it only assumes $\vec F_{12}=-\vec F_{21}$. Kinetic energy conservation is the *extra* assumption that makes a collision elastic; it is never automatic.

### Worked example: rocket with exponentially decaying mass

A rocket of time-varying mass $m(t)$ rises under gravity alone, $\vec F=-mg\hat y$. Because $m$ is not constant, the momentum form must be used directly, not $\vec F=m\vec a$:

$$\frac{dp}{dt} = -m(t)g, \qquad y(0)=0,\ \dot y(0)=v_0, \qquad \text{suppose } m(t)=m_0e^{-\lambda t}$$

$$\frac{d}{dt}\big(m(t)v(t)\big) = -m(t)g$$

**Approach 1: differentiate the product first.**

$$m(t)\dot v(t) + \dot m(t)v(t) = -m(t)g$$

Dividing by $m(t)$ and using $\dot m/m=-\lambda$ (from $m=m_0e^{-\lambda t}$):

$$\dot v = -\frac{\dot m}{m}v - g = \lambda v - g$$

**Approach 2: integrate directly.**

$$\frac{d}{dt}(mv) = -mg \;\Rightarrow\; m_0e^{-\lambda t}v = -\int m_0e^{-\lambda t}g\,dt = \frac{m_0g}{\lambda}e^{-\lambda t}+C$$

$$\Rightarrow\; v = \frac{g}{\lambda} + Ce^{\lambda t}, \qquad v(0)=v_0 \;\Rightarrow\; C=v_0-\frac{g}{\lambda}$$

Both approaches describe the same linear first-order ODE for $v$ (approach 1 gives the equation, approach 2 solves it): $\dot v-\lambda v=-g$, solved with integrating factor $e^{-\lambda t}$, giving $v(t)=\dfrac g\lambda+\left(v_0-\dfrac g\lambda\right)e^{\lambda t}$.

> [!note] N.B
> With mass strictly decreasing and no thrust force beyond gravity, $\vec F=-mg\hat y$ alone, the momentum equation still allows $v$ to grow, because $p=mv$ can stay consistent with a shrinking $m$ only if $v$ changes to compensate. This is why the momentum form, not $\vec F=m\vec a$, is the correct starting point whenever mass is not constant.

## Impulse

For a force acting over a finite time interval, integrate the momentum form:

$$\Delta\vec p = \int_{t_0}^{t}\vec F(t')\,dt' \qquad(\text{impulse: short-lasting, transient, non-repetitive})$$

For a **constant** force this simplifies to $\Delta\vec p=\vec F\,\Delta t$, and, for constant mass, $\Delta\vec v = \dfrac{1}{m}\vec F\,\Delta t$.

### Worked example: force applied briefly

What is the change in momentum of a particle experiencing $10\,\text{N}$ of force for $3\,\text{ns}$?

$$\Delta p = (10)(3\times10^{-9}) = 3\times10^{-8}\ \text{kg m s}^{-1}$$

> [!warning] Common mistake (added, corrected)
> The source computed this using $3\times10^{-6}$ (microseconds) rather than $3\times10^{-9}$ (nanoseconds) for "$3\,\text{ns}$", giving $3\times10^{-5}\,\text{kg m s}^{-1}$. The method (impulse equals force times time interval, for constant force) is correct; only the unit conversion of "ns" was off by three orders of magnitude. Always double check that the power of ten attached to a unit prefix (n, $\mu$, m) matches the prefix actually written.

### Worked example: rebound (particle accelerator)

A particle travels with momentum $\vec p_0$ and rebounds with momentum $-3\vec p_0$ in $4\,\text{ns}$. What force is required?

$$\Delta\vec p = -3\vec p_0 - \vec p_0 = -4\vec p_0$$

$$\Delta\vec p = \vec F\,\Delta t \;\Rightarrow\; \vec F = \frac{4\vec p_0}{4\times10^{-9}\,\text{s}}$$

which, taking $p_0$ to be of order $1\,\text{kg m s}^{-1}$, is of order $10^9\,\text{N}$: over nanosecond timescales even a modest change in momentum demands an enormous instantaneous force, which is exactly why impulsive forces are treated as short, transient events rather than integrated over their full (unknown) time profile.

## Rotational motion

### Angular momentum and the rotational form of N2

Recall from statics the moment of a force about the origin, $\vec M=\vec r\times\vec F$. Define the **angular momentum** of a particle about the origin the same way, with momentum in place of force:

$$\vec H = \vec r\times\vec p$$

Differentiating,

$$\frac{d\vec H}{dt} = \dot{\vec r}\times\vec p + \vec r\times\dot{\vec p} = (\vec r\times m\dot{\vec r}) + \vec r\times\vec F$$

The first term vanishes ($\dot{\vec r}\times\dot{\vec r}=\vec 0$ for any vector crossed with itself), leaving

$$\boxed{\frac{d\vec H}{dt} = \vec r\times\vec F = \vec M}$$

> [!note] N.B
> This is not new physics, it is a reformulation of $\vec F=d\vec p/dt$ (compare: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Newton's second law and the path equation]]). $\vec H$ and $\vec M$ must always be measured about the *same* fixed reference point; the point can be any fixed point, not only the origin.

**Conservation of angular momentum** follows immediately: if $\vec M=\vec 0$ about some fixed point, then $\vec H$ is constant about that point. This is exactly what happened for the central force above, $\vec M=\vec 0$ in equation (2) there gave $r^2\dot\theta=h=$ const, i.e. $\vec H=mh\hat z=$ const (see: Worked example central inverse-square force, above).

### (added) Worked example: the simple pendulum

> [!note] Added, not from primary source
> Not present in the photographed handwritten notes; included from the module's official Chapter 4 notes because it is the standard textbook application of $d\vec H/dt=\vec M$ and connects directly back to the ansatz method already derived above.

A particle of mass $m$ hangs from a weightless rope of length $l$, free to swing in a vertical plane, origin $O$ at the fixed suspension point.

```tikz
\begin{document}
\begin{tikzpicture}[scale=1]
  \draw (0,1.2) -- (-1.5,1.2);
  \filldraw (0,1.2) circle (1pt) node[above] {$O$};
  \draw[thick] (0,1.2) -- (0.9,-0.4);
  \filldraw (0.9,-0.4) circle (2.5pt);
  \draw[dashed] (0,1.2) -- (0,-0.6);
  \draw (0,0.5) arc (270:305:0.7);
  \node at (0.32,0.35) {$\theta$};
  \draw[->] (0.9,-0.4) -- (0.9,-1.1) node[below] {$m\vec g$};
\end{tikzpicture}
\end{document}
```

Two forces act: weight $m\vec g$ and rope tension $\vec T$. Because $\vec T$ is always directed toward $O$, it contributes no moment about $O$, so only gravity matters for $\vec M_O$:

$$\vec M_O = \vec r\times m\vec g = mgl\sin\theta\,(-\hat z)$$

Since the particle moves on a circle of radius $l$, $\vec v$ is perpendicular to $\vec r$ with magnitude $l\dot\theta$, so

$$\vec H_O = \vec r\times m\vec v = l\big(ml\dot\theta\big)\hat z = ml^2\dot\theta\,\hat z$$

Applying $\vec M_O=d\vec H_O/dt$ and matching $\hat z$ components:

$$ml^2\ddot\theta = -mgl\sin\theta \;\Rightarrow\; \boxed{\ddot\theta = -\frac{g}{l}\sin\theta}$$

This cannot be solved in closed form in general (it requires numerical methods), but for small oscillations $\sin\theta\approx\theta$:

$$\ddot\theta \approx -\frac gl\theta$$

which is exactly the simple-harmonic-motion equation solved by the ansatz method above (see: Position-dependent force springs and simple harmonic motion), with

$$\omega = \sqrt{\frac gl} \;\Rightarrow\; T = \frac{2\pi}{\omega} = 2\pi\sqrt{\frac lg}$$

> [!note] N.B
> $\vec M_O=d\vec H_O/dt$ is not new information beyond $\vec F=m\vec a$, but choosing $O$ at the pivot makes the unknown tension $\vec T$ drop out of the moment equation entirely, whereas a direct $\vec F=m\vec a$ resolution would need to eliminate $\vec T$ by hand.

## Angular impulse

### (added) Definition

> [!note] Added, not from primary source
> Not present in the photographed handwritten notes; included from the module's official Chapter 4 notes for completeness, it is the direct rotational analogue of the impulse already derived above from the primary source.

Integrating $\vec M_O=d\vec H_O/dt$ between two times, exactly as impulse was obtained from $\vec F=d\vec p/dt$:

$$\int_{t_1}^{t_2}\vec M_O\,dt = \vec H_O(t_2)-\vec H_O(t_1)$$

Defining the **angular impulse** $\vec J_O=\displaystyle\int_{t_1}^{t_2}\vec M_O\,dt$:

$$\boxed{\vec J_O = \Delta\vec H_O}$$

directly analogous to $\Delta\vec p=\int\vec F\,dt$ above.

## Do not forget (Dynamics)

- Classify the force first: const/$F(t)$ integrate directly; $F(v)$ use $v\,dv/dr$; $F(r)$ guess-and-verify (ansatz). Not every case is solvable in closed form.
- On an incline or any constrained surface, isolate the unbalanced force component before integrating, the constraint force cancels the rest.
- Terminal velocity comes from setting $\ddot z=0$ in the force balance directly, never from solving the full ODE.
- The SHM ansatz $A\cos\omega t+B\sin\omega t$ only solves $\ddot\xi=-\frac km\xi$ for the specific $\omega=\sqrt{k/m}$, verification is what pins that down.
- Central force in polar coordinates always splits into a zero-torque $\hat\theta$ equation (giving $r^2\dot\theta=h=$ const) and a radial equation that becomes solvable once $h$ is substituted in.
- Momentum form $\vec F=d\vec p/dt$, not $\vec F=m\vec a$, is required whenever mass is not constant.
- $\vec H=\vec r\times\vec p$ and $d\vec H/dt=\vec r\times\vec F=\vec M$ is a reformulation of N2, not new physics; choosing the reference point to kill an unknown force's moment (as with pendulum tension) is the main reason to use it.
- Impulse $\Delta\vec p=\int\vec F\,dt$ and angular impulse $\Delta\vec H=\int\vec M\,dt$ are directly analogous.
- Total momentum of a two-particle system is conserved whenever they interact only with each other, elastic vs inelastic is about whether kinetic energy is *also* conserved, never automatic.
- $F(r)\propto -r$ (a spring, or gravity inside a uniform sphere) is always SHM; recognising the functional form avoids re-deriving the ansatz from scratch.
- Two particles interacting only via an internal force (e.g. a connecting spring) decouple into a freely-moving centre of mass and a relative coordinate that obeys the one-body equation with the reduced mass $\mu=m_1m_2/(m_1+m_2)$ in place of $m$.

## See also

- [[APM01B1_Notes_S1_PolarIntrinsicCoordinates]] (Session 1, Kinematics — required background: polar and intrinsic coordinates, vector differentiation, Newton's second law and the path equation, the two edge cases)
- `APM01B1_Proofs_ST1.md`, `APM01B1_Summary_ST1.md` (scope-locked to the ST1 kinematics test, unaffected by this session)
