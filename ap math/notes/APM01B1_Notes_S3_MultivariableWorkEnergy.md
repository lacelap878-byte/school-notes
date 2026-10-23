---
module: APM01B1
topic: Multivariable Functions, Line Integrals, Work and Energy
session: S3
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# APM01B1 S3: Multivariable Functions, Line Integrals, Work and Energy

This note covers the last block of the module. First come the multivariable tools: partial derivatives, the gradient, line integrals and the curl test. Then those tools are used to build work, kinetic and potential energy, conservation of energy, and a run of worked examples (escape speed, a bullet and block on a slope, a particle on a sphere, a tunnel through the Earth, the Moon's orbit). It closes with a short look at systems of particles and with the revision pages on solving Newton's second law, which sit here because they feed straight into the energy results.

Notation: $T$ is kinetic energy and $V$ is potential energy, both in joules (J). The lecturer's pages also write $K$ and $U$ for the same two things. Newton's second law is written NII.

## What the final covers

#exam-flagged

As noted from the lecturer:

- Chapters 5 and 6: the tools of chapter 5 are used to do the things of chapter 6.
- Chapters 3 and 4: chapter 3 is the tools, chapter 4 is the work.
- Particularly: coordinate systems (Cartesian, polar, tangential-normal).
- Particularly: path equations (easy in 3D, medium in 2D).
- Particularly: solving NII in its four cases (direct integration, the substitution $dv/dt = v\,dv/dx$, separation of variables).
- Particularly: work-energy, $W = \int \vec{F}\cdot d\vec{r} = \Delta T = -\Delta V$, and so on.
- Particularly: impulse and momentum conservation.
- Being asked to formulate NII in different coordinate systems.
- Sample question flagged: a hole is drilled through the centre of the Earth (see: Tunnel through the Earth).

## Functions of several variables and the gradient

### Functions of several variables

A quantity often depends on more than one independent variable. Examples from the pages:

- A wave on an elastic material.
- Health depends on age, exercise, environment.
- Risk depends on age, health, income.
- The volume of a prism, $V = \Delta x\,\Delta y\,\Delta z$ or $xyz$.
- Temperature depends on position and time.
- BMI depends on mass and height.

With two inputs the picture is a surface. $z = f(x,y)$ assigns a height $z$ to each point $(x,y)$ of the plane (the domain). It is a surface because there are only two inputs, $x$ and $y$.

Example: $z = x^2 + y^2 = r^2$ is a bowl (a paraboloid) opening upward.

Why this changes differentiation: along a curve there is one slope at a point, but on a surface the slope depends on which direction you step. The fix is to differentiate with respect to one input at a time.

### Partial derivatives

#definition

$$\frac{\partial f}{\partial x} = \lim_{h\to 0}\frac{f(x+h,y)-f(x,y)}{h}$$

Here $f$ is the function, $h$ is a small step in $x$ only, and $y$ is held fixed.

Practical rule: differentiate with respect to one variable and treat every other variable as a constant.

Example 1: $f(x,y) = \sin x\, e^{-y^2}$

$$\frac{\partial f}{\partial x} = \cos x\, e^{-y^2}, \qquad \frac{\partial f}{\partial y} = -2y\sin x\, e^{-y^2}$$

Example 2: $f(x,y) = \cos(x+y) + \sin(x-y) + x^2 + y^3$

$$\frac{\partial f}{\partial x} = -\sin(x+y) + \cos(x-y) + 2x$$

$$\frac{\partial f}{\partial y} = -\sin(x+y) - \cos(x-y) + 3y^2$$

The chain rule on the inside functions gives the $-\cos(x-y)$ in the $y$ derivative, since $\frac{\partial}{\partial y}(x-y) = -1$.

### Gradient of a scalar function

#definition #formula

$$\vec{\nabla}f = \frac{\partial f}{\partial x}\hat{x} + \frac{\partial f}{\partial y}\hat{y}$$

In three variables a third term $\dfrac{\partial f}{\partial z}\hat{z}$ is added. $\vec{\nabla}f$ (also written grad $f$) is the vector built from the partial derivatives of the scalar $f$, in the unit vectors $\hat{x},\hat{y},\hat{z}$.

Why bother: two separate partial derivatives become one vector, and a vector can be projected onto a path (see: Chain rule along a path and the directional derivative).

**N.B** $\vec{\nabla}f$ is a genuine vector. Its meaning does not depend on the coordinate system chosen.

Example: $f(x,y) = x^2 + 2xy - y^2$

$$\vec{\nabla}f = (2x+2y)\hat{x} + (2x-2y)\hat{y}$$

Example: $g(x,y,z) = x\sin(yz) + z\,e^{-xy}$

$$\vec{\nabla}g = \big[\sin(yz) - yz\,e^{-xy}\big]\hat{x} + \big[xz\cos(yz) - xz\,e^{-xy}\big]\hat{y} + \big[xy\cos(yz) + e^{-xy}\big]\hat{z}$$

### Nabla, divergence and curl

The operator is

$$\vec{\nabla} = \hat{x}\frac{\partial}{\partial x} + \hat{y}\frac{\partial}{\partial y} + \hat{z}\frac{\partial}{\partial z}$$

It can be applied in three ways:

| Operation | Acts on | Gives | What it tells you |
|---|---|---|---|
| $\vec{\nabla}f$ (gradient) | scalar field $f$ | vector | how $f$ changes with position, perpendicular to level surfaces |
| $\vec{\nabla}\cdot\vec{V}$ (divergence, div) | vector field | scalar | inflow or outflow |
| $\vec{\nabla}\times\vec{V}$ (curl) | vector field | vector | rotation |

<span style="color:#f08c00">Open: the gradient acts on a scalar, so "grad cross F" does not exist. The curl is nabla crossed with a vector field. The divergence is nabla dotted with a vector field. For conservative-force tests the one you need is the curl.</span> #struggle

#### Gradient of a vector field

For a vector field $\vec{V}(\vec{r}) = V_x\hat{x} + V_y\hat{y} + V_z\hat{z}$, the gradient $\vec{\nabla}\vec{V}$ is the table of all nine partial derivatives:

$$\vec{\nabla}\vec{V} = \begin{pmatrix} \partial V_x/\partial x & \partial V_x/\partial y & \partial V_x/\partial z \\ \partial V_y/\partial x & \partial V_y/\partial y & \partial V_y/\partial z \\ \partial V_z/\partial x & \partial V_z/\partial y & \partial V_z/\partial z \end{pmatrix}$$

Each row is one component of $\vec{V}$ differentiated with respect to each of $x,y,z$.

### Chain rule along a path and the directional derivative

Take a path in the $xy$-plane, $\vec{r}(s) = x(s)\hat{x} + y(s)\hat{y}$. Along it, $f$ becomes a function of $s$ alone: $f(s) = f(x(s),y(s))$. The rate of change along the path is $df/ds$. There are two ways to get it.

The obvious way: substitute $x(s)$ and $y(s)$ into $f$, then differentiate $f(s)$.

The exciting way (to understand conceptually): start from the total change

$$df = \frac{\partial f}{\partial x}dx + \frac{\partial f}{\partial y}dy$$

and divide by $ds$:

$$\frac{df}{ds} = \frac{\partial f}{\partial x}\frac{dx}{ds} + \frac{\partial f}{\partial y}\frac{dy}{ds} = \vec{\nabla}f\cdot\frac{d\vec{r}}{ds}$$

Here $d\vec{r}/ds$ is the tangent (velocity-like) vector of the path. This is the projection of the gradient onto the path taken: only the part of $\vec{\nabla}f$ along the path changes $f$.

The directional derivative, in the form the pages use: write the surface as $F(x,y,z) = c$ and pick a path $\vec{r}(s)$ on it, then

$$\frac{dF}{ds} = \vec{\nabla}F\cdot\frac{d\vec{r}}{ds}$$

where $F$ is the function, $s$ the parameter along the path, and $\vec{r}(s)$ the path.

(added) For a straight path in the direction of a unit vector $\hat{u}$, this reads $\vec{\nabla}F\cdot\hat{u}$.

Example (source): $F = xyz$ along $\vec{r}(s) = s\hat{x} + s^2\hat{y} + \hat{z}$.

$$\vec{\nabla}F = yz\,\hat{x} + xz\,\hat{y} + xy\,\hat{z}, \qquad \frac{d\vec{r}}{ds} = \hat{x} + 2s\,\hat{y}$$

On the path $x = s$, $y = s^2$, $z = 1$, so

$$\vec{\nabla}F\cdot\frac{d\vec{r}}{ds} = yz + 2s(xz) = s^2 + 2s(s) = 3s^2$$

> *I checked this the obvious way: on the path $F(s) = s\cdot s^2\cdot 1 = s^3$, and $dF/ds = 3s^2$. The two methods agree.*

### Level surfaces and the gradient

An equation $F(x,y,z) = c$ with $c$ constant defines a surface. $\vec{\nabla}F$ is not necessarily zero there.

Pick a path $\vec{r}(s)$ that stays on the surface. $F$ never changes along it, so $dF/ds = 0$, and by the chain rule above

$$\vec{\nabla}F\cdot\frac{d\vec{r}}{ds} = 0$$

$d\vec{r}/ds$ is tangent to the surface, and the path was arbitrary, so in general $\vec{\nabla}F$ is perpendicular to the surface.

Pictures from the pages:

- On the circle $x^2 + y^2 = 1$ starting at $(0,1)$, a step of $0.5$ in $x$ forces a change in $y$ to stay on the circle.
- In 3D on the sphere $x^2 + y^2 + z^2 = 1$, a change in $x$ forces a change in $y$ and/or $z$.
- $x^2 + y^2 = r^2$ is a circle. The function $x^2 + y^2$ itself has concentric circles as its contours, and $\vec{\nabla}F$ points across them.
- $F = x^2 + y^2 + z^2$ with $F$ constant gives a family of spheres, and

$$\vec{\nabla}F = 2x\,\hat{x} + 2y\,\hat{y} + 2z\,\hat{z}$$

which points radially, perpendicular to each sphere.

## Line integrals

### Arc length of a path

In one dimension, integration usually means area under a curve, and

$$\int_a^b f(x)\,dx = F(b) - F(a)$$

where $F$ is an antiderivative of $f$.

How long is a piece of string? Describe it by a path $\vec{r}(s)$. Then $L = \int ds$, but the string changes direction, so the step $ds$ must be measured along the path:

$$L = \int ds = \int (d\vec{r}\cdot d\vec{r})^{1/2} = \int\left[\left(\frac{dx}{ds}\right)^2 + \left(\frac{dy}{ds}\right)^2\right]^{1/2}ds = \int\left|\frac{d\vec{r}}{ds}\right|ds$$

Given $\vec{r}(s)$ you can find the length, and this is essentially a path integral.

### Integrating a vector function along a path

Can we integrate functions that are vectors? Yes, but only along a path. Take, for example, the vector $\vec{p} = s^2\hat{x} + s^2\hat{y}$. Along a path $\vec{r}(s)$, the integral of $\vec{p}$ is

$$\int_\Gamma \vec{p}\cdot d\vec{r}$$

and the path $\Gamma$ is directly associated with $\vec{r}$. Since $d\vec{r} = \dfrac{d\vec{r}}{ds}\,ds$:

$$I = \int_\Gamma \left(\vec{p}\cdot\frac{d\vec{r}}{ds}\right)ds$$

### Line integral as a limit of sums

#definition

$$\int_\Gamma \vec{F}\cdot d\vec{r} = \lim_{\substack{N\to\infty\\ \Delta r_i\to 0}}\sum_{i=1}^{N}\vec{F}(\vec{r}_i)\cdot\Delta\vec{r}_i$$

$\Gamma$ is the path, $\vec{F}$ the field, $\Delta\vec{r}_i$ the $i$-th small step along $\Gamma$ and $\vec{r}_i$ the point where the field is sampled. The dot product keeps only the part of $\vec{F}$ along each step.

### Computing a line integral in four steps

1. Define the path by a parametrisation, $\vec{r} \to \vec{r}(s)$.
2. Recognise that $d\vec{r}$ is just $\dfrac{d\vec{r}}{ds}\,ds$.
3. Substitute in and compute $\vec{F}\cdot\dfrac{d\vec{r}}{ds}$, expressing $\vec{F}$ in terms of $s$.
4. Integrate the resulting function $f(s) = \vec{F}\cdot\dfrac{d\vec{r}}{ds}$.

$$\int_\Gamma \vec{F}\cdot d\vec{r} = \int_{s_0}^{s_1}\vec{F}(\vec{r}(s))\cdot\frac{d\vec{r}}{ds}\,ds$$

#worked-example

Example (source): $\vec{F} = x\,\hat{x} + y^2\,\hat{y}$ along the curve $y = x^2$ from $(1,1)$ to $(2,4)$.

Step 1. Parametrise $y = x^2$ by $\vec{r}(s) = s\,\hat{x} + s^2\,\hat{y}$ with $s\in[1,2]$.

Step 2. $d\vec{r} = (\hat{x} + 2s\,\hat{y})\,ds$.

Step 3. On the path $\vec{F}(s) = s\,\hat{x} + s^4\,\hat{y}$, so

$$\vec{F}\cdot d\vec{r} = \vec{F}\cdot\frac{d\vec{r}}{ds}\,ds = (s + 2s^5)\,ds$$

Step 4.

$$\int_1^2 (s + 2s^5)\,ds = \left[\tfrac12 s^2 + \tfrac13 s^6\right]_1^2 = \left(2 + \tfrac{64}{3}\right) - \left(\tfrac12 + \tfrac13\right) = \tfrac{135}{6} = \tfrac{45}{2}$$

> *I redid this arithmetic and it gives $135/6$. If your page shows $155/6$, that is a slip on the page.*

### Closed paths and non-smooth paths

A path that ends where it started is closed. For a closed path the integral is written with a circle:

$$\oint_\Gamma \vec{F}\cdot d\vec{r}$$

A path need not even be a smooth line (a square, for example). To handle a non-smooth path, perform piecewise integration on each continuous (smooth) piece and add the results.

### Integral of a gradient along a path

#theorem

Consider the path integral of the gradient of a scalar $\psi$, going from $A$ to $B$. Recall that for $\psi = \psi(x,y,z)$ the total change is

$$d\psi = \frac{\partial\psi}{\partial x}dx + \frac{\partial\psi}{\partial y}dy + \frac{\partial\psi}{\partial z}dz = \vec{\nabla}\psi\cdot d\vec{r}$$

so the line integral collapses to an ordinary integral of $d\psi$:

$$\int_A^B \vec{\nabla}\psi\cdot d\vec{r} = \int_A^B d\psi = \psi(\vec{r}_B) - \psi(\vec{r}_A)$$

$\psi$ is the scalar function, and $\vec{r}_A,\vec{r}_B$ are the start and end points. Only the endpoints matter, not the route.

If the path is closed ($A = B$) this is zero.

## Conservative fields

### Conservative vector fields and the scalar potential

#definition

A conservative field is one that can be written as $\vec{\nabla}f$. Here $f$ is called the scalar potential, and $\vec{\nabla}f$ is a conservative vector field.

If the force can be written as a scalar gradient, it is said to be conservative, and all path integrals are path independent. Gravity and electrostatics are examples. For the closed path:

$$\oint_\Gamma \vec{\nabla}\psi\cdot d\vec{r} = \psi(\vec{r}_A) - \psi(\vec{r}_A) = 0$$

Given a field $\vec{F}$, two tasks follow: (1) check whether $\vec{F}$ is conservative, (2) if so, find $f$.

> [!warning] ⚠️ Sign convention changes between chapters
> The multivariable pages write $\vec{F} = \vec{\nabla}f$, so the potential is $f$. The energy pages write $\vec{F} = -\vec{\nabla}V$, so the potential energy is $V$. The two are related by $V = -f$ (up to a constant). The minus sign is the one that gets forgotten.

### Testing for a conservative field with the curl

#theorem

For every scalar $f$, the curl of a gradient is zero identically:

$$\vec{\nabla}\times\left(\vec{\nabla}f\right) = \vec{0}$$

So if we do not know that $\vec{F}$ is conservative, we check its curl:

$$\vec{\nabla}\times\vec{F} = \vec{0}$$

If the curl is zero, $\vec{F}$ is conservative and there exists $f$ with $\vec{F} = \vec{\nabla}f$. If the curl is not zero, $\vec{F}$ cannot be a gradient.

Example (source): $\vec{F} = x\,\hat{x} + y\,\hat{y}$

$$\vec{\nabla}\times\vec{F} = \left(\hat{x}\frac{\partial}{\partial x} + \hat{y}\frac{\partial}{\partial y} + \hat{z}\frac{\partial}{\partial z}\right)\times\left(x\,\hat{x} + y\,\hat{y} + 0\,\hat{z}\right) = 0\,\hat{x} + 0\,\hat{y} + 0\,\hat{z} = \vec{0}$$

so $\vec{F}$ is conservative.

Example (source): $\vec{F} = y\,\hat{x} - x\,\hat{y}$

$$\vec{\nabla}\times\vec{F} = -\frac{\partial x}{\partial x}(\hat{x}\times\hat{y}) + \frac{\partial y}{\partial y}(\hat{y}\times\hat{x}) = -2\,\hat{z}$$

The curl is not zero, so this $\vec{F}$ is not conservative.

(added) In 2D, with $F_z = 0$ and nothing depending on $z$, only the $\hat{z}$ component survives and the test reduces to one equation:

$$\frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y} = 0$$

(added) A zero curl is always necessary, and is sufficient when the region has no holes (simply connected). All the fields on the pages are defined on the whole plane or space, so this is not an issue there.

### Finding the scalar potential by partial integration

#formula

If $\vec{F} = \vec{\nabla}f$, then $f$ can only be determined up to an arbitrary constant, because adding a constant does not change any partial derivative.

Example (source): $\vec{F} = x\,\hat{x} + y\,\hat{y}$, assumed conservative so that $\vec{F} = \vec{\nabla}f$. Comparing components:

$$\frac{\partial f}{\partial x} = x, \qquad \frac{\partial f}{\partial y} = y$$

Integrate each one. Because $f$ has two variables, each integral picks up an arbitrary function of the other variable:

$$\int\frac{\partial f}{\partial x}\,dx = \tfrac12 x^2 + g(y), \qquad \int\frac{\partial f}{\partial y}\,dy = \tfrac12 y^2 + h(x)$$

Why $g(y)$: integrating with respect to $x$ treats $y$ as a constant, and anything depending only on $y$ would vanish under $\partial/\partial x$, so it could be hiding in $f$. Both results describe the same $f$, so $g(y)$ must be $\tfrac12 y^2$ plus a constant and $h(x)$ must be $\tfrac12 x^2$ plus a constant:

$$f(x,y) = \tfrac12 x^2 + \tfrac12 y^2 + c$$

<span style="color:#f08c00">Open: this is partial integration and matching, not separation of variables. You integrate one partial derivative, keep the unknown function of the other variable ($g(y)$), then use the other partial derivative to pin that function down.</span> #struggle

#worked-example #added

(added) Second example, worked step by step: $\vec{F} = 2xy\,\hat{x} + x^2\,\hat{y}$ with $\vec{F} = \vec{\nabla}f$.

Check first: $\dfrac{\partial F_y}{\partial x} = 2x$ and $\dfrac{\partial F_x}{\partial y} = 2x$, so the curl is zero.

Integrate $\dfrac{\partial f}{\partial x} = 2xy$ with respect to $x$, treating $y$ as constant:

$$f = x^2 y + g(y)$$

Differentiate that with respect to $y$ and match $\dfrac{\partial f}{\partial y} = x^2$:

$$x^2 + g'(y) = x^2 \;\Rightarrow\; g'(y) = 0 \;\Rightarrow\; g = \text{constant}$$

So $f = x^2 y + c$. In the energy convention $\vec{F} = -\vec{\nabla}V$ the same field has $V = -x^2 y + c$.

### Picturing the gradient as arrows

$\vec{\nabla}f$ is a vector field, so it can be pictured as a box of arrows, one at each point. For $f = \tfrac12 x^2 + \tfrac12 y^2 + c$ the partial derivatives are $\partial f/\partial x = x$ and $\partial f/\partial y = y$.

The page then writes a slope of the arrows, $dy/dx$, and ends on $x/y$. The arrow at $(x,y)$ is the vector $(x,y)$ itself, whose slope is $y/x$. The tangent to a level curve $x^2 + y^2 = \text{constant}$ has slope $-x/y$. So the page's $x/y$ matches neither: check that line against your lecturer's version before relying on it.

## Work and energy

### Work done by a constant force

For a constant force and a straight displacement:

$$W = F\,d$$

$F$ is the force (newtons, N), $d$ the displacement (metres, m), $W$ the work (joules, J).

This only works for constant forces and straight displacements. If the force varies or the path bends (for example a block pushed over a hill), we need the small-step form

$$dW = \vec{F}\cdot d\vec{r}$$

and add up the steps along the path (see: Work done along a general path).

### Work done along a general path

#definition

$$W = \int_\Gamma \vec{F}\cdot d\vec{r}$$

$\Gamma$ is the path, $\vec{F}$ the force, $d\vec{r}$ a small displacement along it.

Does this reproduce the normal 1D case? Yes. Take $x$ along an incline with $\vec{F} = F\hat{x}$ and $d\vec{r} = dx\,\hat{x}$:

$$W = \int F\,dx\,(\hat{x}\cdot\hat{x}) = \int_{x_0}^{x_1}F\,dx$$

and for constant $F$ this is $F\,x\big|_{x_0}^{x_1} = F\,d$.

The line integral has useful properties depending on $\vec{F}$ and the path:

1. If $\vec{F}$ is conservative, the work is path independent.
2. If $\vec{F}$ is conservative, $\oint\vec{F}\cdot d\vec{r} = 0$.

### Kinetic energy from Newton's second law

#theorem

Start from $\vec{F} = m\,d\vec{v}/dt$ and ask for the work done by any given force:

$$W = \int\vec{F}\cdot d\vec{r} = \int m\frac{d\vec{v}}{dt}\cdot d\vec{r} = \int m\frac{d\vec{v}}{dt}\cdot\vec{v}\,dt = m\int\vec{v}\cdot d\vec{v} = \frac{m}{2}v^2\Big|_{1}^{2}$$

which gives the work-energy theorem:

$$W = \Delta T = \tfrac12 m v_2^2 - \tfrac12 m v_1^2$$

$m$ is the mass (kg), $v_1$ and $v_2$ the initial and final speeds (m/s), $T = \tfrac12 mv^2$ the kinetic energy (J).

Kinetic energy is the first integral of Newton's second law. The fact that $\Delta T = W$ is completely independent of the nature of $\vec{F}$: it holds for any force, conservative or not.

### Magnetic force does no work

The page's interesting example: $\vec{F} = q(\vec{v}\times\vec{B})$, a charge $q$ in a magnetic field $\vec{B}$.

$$W = \int\vec{F}\cdot d\vec{r} = \int\vec{F}\cdot\vec{v}\,dt = 0$$

because $\vec{v}\times\vec{B}$ is perpendicular to $\vec{v}$. So magnetic fields do no work.

In general, if $W = \int_\Gamma\vec{F}\cdot d\vec{r} = 0$ then $\vec{F}\perp d\vec{r}$ along $\Gamma$. (added) Since $W = \Delta T$, a force that does no work leaves the speed unchanged.

### Power

#formula

From $dW = \vec{F}\cdot d\vec{r} = \vec{F}\cdot\vec{v}\,dt$:

$$P = \frac{dW}{dt} = \vec{F}\cdot\vec{v}$$

$P$ is power (watts, W), $\vec{F}$ the force (N), $\vec{v}$ the velocity (m/s).

### Potential energy and conservation of mechanical energy

#definition #theorem

For a conservative force, define the potential energy by integrating the force from a reference point $\vec{r}_0$ along any path $\Gamma$ to $\vec{r}$:

$$V(\vec{r}) = -\int_{\vec{r}_0}^{\vec{r}}\vec{F}\cdot d\vec{r}$$

Then $V(\vec{r})$ is the potential energy and

$$\vec{F} = -\vec{\nabla}V$$

Potential energy is stored in the system, allowing it to do work.

Putting this into the work-energy theorem:

$$\Delta T = -\int_\Gamma\vec{\nabla}V\cdot d\vec{r} = -\Delta V$$

$$\Delta T + \Delta V = \Delta E = 0$$

$E = T + V$ is called the mechanical energy. For conservative systems $\Delta E = 0$, so $E$ is constant.

> [!warning] ⚠️ Conservation has a condition
> $\Delta E = 0$ only if $\vec{F} = -\vec{\nabla}V$. If a non-conservative force (friction, drag) also acts, mechanical energy is not conserved. A force that does no work, such as the normal force on a fixed smooth surface, does not break conservation.

The closing statement on the pages: if $W = \oint\vec{F}\cdot d\vec{r} = 0$, then $\vec{F}$ is conservative, which means $\vec{F} = -\vec{\nabla}V$ as in $T + V$. Equivalently $\vec{\nabla}\times\vec{F} = \vec{0}$, and this is the way to check whether $\vec{F}$ is conservative.

### One-dimensional link between v dv/dx and energy

The substitution used to solve NII (see: Separable force of position and speed) also gives energy conservation in 1D. Since

$$\ddot{x} = v\frac{dv}{dx} = \frac12\frac{d(v^2)}{dx}$$

NII ($\ddot{x} = F/m$) gives $\tfrac12\,\dfrac{d(v^2)}{dx} = \dfrac{F}{m}$, so

$$F = \frac{d}{dx}\left(\tfrac12 mv^2\right)$$

Then, integrating, and writing the force as the negative slope of a potential energy $U$ when it is conservative:

$$\Delta K = \int F\,dx = \int\left(-\frac{dU}{dx}\right)dx = -\Delta U$$

so $\Delta K + \Delta U = 0$ and $\Delta E_{total} = 0$. Here $K,U$ are the page's names for $T,V$.

### Potential energy of uniform gravity

For constant gravitational field, $\vec{F} = -mg\,\hat{y}$ with $g$ in m/s$^2$ and $y$ the height (m). Using the definition with reference height $0$:

$$V(y) = \int_0^y mg\,dy = mgy$$

Without limits, $V(y) = mgy + c$. Since only differences of $V$ enter, the constant $c$ can be anything.

Check the sign: $F = -\dfrac{dV}{dy} = -mg$.

Example (source): the speed of a projectile at height $h$, if its initial speed at $h = 0$ is $v_0$ and $g$ is constant. Uniform gravity is conservative, so $\Delta E = 0$:

$$\tfrac12 mv_0^2 + mg(0) + V_0 = \tfrac12 mv_h^2 + mgh + V_0$$

The constant $V_0$ cancels, leaving

$$v_h = \sqrt{v_0^2 - 2gh}$$

### Potential energy of real gravity

For gravity from a point mass $M$ (a planet of radius $R$, with $y$ the height above its surface), $T = \tfrac12 mv^2$ is unchanged and $V$ must be recalculated from the force:

$$F = -\frac{GMm}{r^2} = -\frac{GMm}{y'^2} = -\frac{GMm}{(R+y)^2}$$

where $y'$ is the distance from the centre. Then

$$V(y) = -\int F\,dy = -\frac{GMm}{R+y} + V_0$$

$G$ is the gravitational constant, $M$ the planet mass, $m$ the particle mass. Remember to check $F = -\dfrac{dV}{dy}$.

### Potential energy of a spring

#formula

(added) Source: course notes chapter 6 (spring example) and tutorial 12 and 13 questions. This section was not on the lecturer's handwritten pages.

Take a spring along the $x$ axis with its natural length at $x = 0$, so $x$ is the extension. The restoring force (Hooke's law) is

$$F = -kx$$

with $k$ the spring constant in N/m. Define $V$ from the force with $V(0) = 0$:

$$V(x) = -\int_0^x F\,dx' = -\int_0^x (-kx')\,dx' = \tfrac12 kx^2$$

Check: $F = -\dfrac{dV}{dx} = -kx$. ✓

Use it in conservation of energy, as with gravity. Released from rest at extension $x_1$ and passing through $x = 0$ with speed $v$:

$$\tfrac12 mv^2 + 0 = 0 + \tfrac12 kx_1^2 \;\Rightarrow\; v = x_1\sqrt{\frac{k}{m}}$$

If gravity acts as well, add both potentials, $V = \tfrac12 kx^2 + mgh$, since both forces are conservative.

> [!tip] Energy differentiation (exam pattern)
> Write $E = \tfrac12 m\dot{x}^2 + \tfrac12 kx^2$ and differentiate with respect to time. Since $E$ is constant,
> $$\frac{dE}{dt} = m\dot{x}\ddot{x} + kx\dot{x} = \dot{x}\,(m\ddot{x} + kx) = 0$$
> so $m\ddot{x} = -kx$, which is NII again. This is the "differentiate the energy to recover NII" question.

### Escape speed

#worked-example

Conservation of energy for a particle launched from the surface with speed $v_0$:

$$\tfrac12 mv_0^2 - \frac{GMm}{R} = \tfrac12 mv^2 - \frac{GMm}{R+y}$$

$$v = \sqrt{v_0^2 + \frac{2GM}{R+y} - \frac{2GM}{R}}$$

To leave the Earth take $y\to\infty$. Using $g = GM/R^2$:

$$v = \sqrt{v_0^2 - \frac{2GM}{R}} = \sqrt{v_0^2 - 2gR}$$

If we want $v\to 0$ at infinity (the least launch speed that still escapes):

$$v_0^2 - 2gR = 0 \;\Rightarrow\; v_0 = \sqrt{2gR}, \qquad \tfrac12 mv_0^2 = mgR$$

Order of magnitude on the page: $m\sim10^4$ kg, $g\sim10$ m/s$^2$, $R\sim10^6$ m.

(added) Arithmetic check: $mgR\sim10^4\times10\times10^6 = 10^{11}$ J (about $6\times10^{11}$ J with $R = 6.4\times10^6$ m). The page's quoted power of ten looks different, so recompute it before copying it.

### Mitchell dark star

John Mitchell, 1700s. Use $\Delta E = 0$ from the surface of a star of mass $M$ and radius $r$ (the page uses $r$ for the surface radius):

$$v = \sqrt{v_0^2 - \frac{2GM}{r}}$$

Where is $v = 0$? Setting the square root to zero:

$$r = \frac{2GM}{v_0^2}$$

Now let $v_0 = c$, the speed of light:

$$r = \frac{2GM}{c^2}$$

A photon leaving the surface of an object this compact cannot get away, so we cannot see the object: a dark star, and in modern terms a black hole. Indeed the event horizon of a black hole is

$$r_s = \frac{2GM}{c^2}$$

### Block and bullet up a smooth slope

Setup (source): a bullet of mass $m$ with velocity $v_0\hat{x}$ hits a block of mass $M$ at rest at the foot of a slope of angle $\theta$ and the pair rises to height $h$. No friction. The page notes this is a momentum balance problem, and that for "how far up the slope the block travels" the velocity alone does not help but energy does.

As written on the page: gravity is conservative so $\Delta E = 0$, with $V = 0$ at the ground:

$$\tfrac12 mv_0^2 + 0 = 0 + (m+M)gh \;\Rightarrow\; h = \frac{mv_0^2}{2g(m+M)}$$

> [!warning] ❌ Energy through an embedding impact
> The step above equates the bullet's initial kinetic energy to the final potential energy. That only works if no kinetic energy is lost in the impact. If the bullet embeds in the block, the impact is perfectly inelastic: momentum is conserved through it, energy is not. Use momentum for the impact, then energy for the climb.

<span style="color:#e03131">Wrong (for an embedding bullet):</span> $h = \dfrac{mv_0^2}{2g(m+M)}$, because it assumes the impact loses no energy.

<span style="color:#2f9e44">Right (added):</span> momentum through the impact gives the speed $V_1$ of block and bullet together, and energy then carries them up:

$$mv_0 = (m+M)V_1 \;\Rightarrow\; V_1 = \frac{mv_0}{m+M}$$

$$\tfrac12(m+M)V_1^2 = (m+M)gh \;\Rightarrow\; h = \frac{V_1^2}{2g} = \frac{m^2v_0^2}{2g(m+M)^2}$$

The page's value is larger than this by a factor $(m+M)/m$. (added) Energy lost in the impact: $\tfrac12 mv_0^2\,\dfrac{M}{m+M}$.

How far up the slope: the height is related to the distance $s$ along the slope by $h/s = \sin\theta$, so $h = s\sin\theta$. The page's version gives

$$s = \frac{mv_0^2}{2g\sin\theta\,(m+M)}$$

and the corrected version gives $s = \dfrac{m^2v_0^2}{2g\sin\theta\,(m+M)^2}$.

Interpret the result properly. At $\theta = 0$ the formula breaks mathematically (division by $\sin 0$), but physically it makes sense: on flat frictionless ground there is no slope to climb. At $\theta = \pi/2$ the formula is fine mathematically, but physically it would not make sense. Learn to interpret the models you create and their physical constraints, not only the mathematical ones.

### Slope with friction proportional to speed

Now introduce friction $\mu$ along the slope, modelled as a force $-\mu V$ proportional to the speed $V$ along the slope. The mechanical energy is no longer conserved, $\Delta E\neq 0$. Take block and bullet moving together as one body of mass $(m+M)$, with $s$ measured up the slope.

The work-energy theorem still holds:

$$W = \Delta T = T_f - T_i$$

with $T_f = 0$ at the highest point, so $\Delta T = -T_i$ (the page writes this as $-\tfrac12 Mv_0^2$).

The total force along the slope is

$$\vec{F} = F_{tot}\,\hat{s} = (F_{g\parallel} + F_f)\,\hat{s} = \big[-(m+M)g\sin\theta - \mu V\big]\hat{s}$$

so the work is

$$W = \int_\Gamma\vec{F}\cdot d\vec{r} = -\int_0^s\big[(m+M)g\sin\theta + \mu V\big]\,ds$$

where $V(s)$ is the velocity along the slope. This needs $V$, which must come from NII:

$$(m+M)\frac{d^2s}{dt^2} = -\big[(m+M)g\sin\theta + \mu V\big]$$

Using $\dfrac{d^2s}{dt^2} = V\dfrac{dV}{ds}$ (see: Separable force of position and speed):

$$V\frac{dV}{ds} = -g\sin\theta - \frac{\mu}{m+M}V$$

Write it as a separable equation:

$$\frac{V}{g\sin\theta + \dfrac{\mu V}{m+M}}\,dV = -ds$$

Substitute

$$u = g\sin\theta + \frac{\mu V}{m+M}, \qquad du = \frac{\mu}{m+M}\,dV, \qquad V = \frac{m+M}{\mu}\big(u - g\sin\theta\big)$$

Then, with $K = \left(\dfrac{m+M}{\mu}\right)^2$:

$$K\int\left(1 - \frac{g\sin\theta}{u}\right)du = K\big[u - g\sin\theta\,\ln u\big] = -s + c$$

$V$ cannot be found explicitly from this, but $s$ in terms of $V$ can. Work-energy does not help here, while NII gives everything.

To find $c$ use $V(0) = V_0$ at $s = 0$, where $u_0 = g\sin\theta + \dfrac{\mu V_0}{m+M}$:

$$c = K\big[u_0 - g\sin\theta\,\ln u_0\big]$$

At the highest point $V = 0$, so $u = g\sin\theta$. The distance reached, $s_{max}$, is the page's "interpret this" result.

(added) Combining the two (the last lines on the page carry a different sign from this derivation, which is internally consistent and passes the check below):

$$s_{max} = \frac{(m+M)V_0}{\mu} - K\,g\sin\theta\,\ln\!\left(1 + \frac{\mu V_0}{(m+M)\,g\sin\theta}\right)$$

(added) Check: as $\mu\to0$, expanding the logarithm to second order gives $s_{max}\to\dfrac{V_0^2}{2g\sin\theta}$, the frictionless result. Friction shortens the climb.

### Particle on a sphere

A particle (the page says bead) rests on the outside of a sphere of radius $R$, with $\theta$ measured from the vertical through the top. When does it leave the surface? Assume it starts at $\theta_0 = 0$ with speed $v_0$.

Start from $\vec{F}_{net} = m\vec{a}$. The radial (normal) equation, with the centripetal acceleration pointing inward, is

$$N - mg\cos\theta = -\frac{mv^2}{R}$$

where $N$ is the normal force (N). The normal force does no work, so $\Delta E = 0$:

$$\tfrac12 mv^2 + mgR\cos\theta = \tfrac12 mv_0^2 + mgR$$

$$mv^2 = mv_0^2 + 2mgR\,(1 - \cos\theta)$$

The particle leaves the surface when the normal force drops to zero: gravity alone can no longer supply the centripetal force the motion needs.

(added) Setting $N = 0$ in the radial equation and using the energy result:

$$\cos\theta = \frac{v_0^2 + 2gR}{3gR}$$

For $v_0 = 0$ this gives $\cos\theta = 2/3$, so $\theta\approx 48.2^\circ$. For the particle to be on the surface at the top at all, $v_0^2\le gR$.

### Work done by drag around a circle

Consider the drag force $\vec{F} = -k\vec{v}$ ($k$ in kg/s) on a particle moving on the circle $\vec{r}(t) = R\cos\omega t\,\hat{x} + R\sin\omega t\,\hat{y}$. Find the work done if $\omega = 2\pi$ and the time taken is $3$ s (reading taken from the page's result).

$$W = \oint\vec{F}\cdot d\vec{r} = \int\vec{F}\cdot\frac{d\vec{r}}{dt}\,dt = \int -k\,\vec{v}\cdot\vec{v}\,dt$$

with

$$\vec{v} = -R\omega\sin\omega t\,\hat{x} + R\omega\cos\omega t\,\hat{y}, \qquad \vec{v}\cdot\vec{v} = R^2\omega^2$$

so

$$W = -kR^2\omega^2\,t$$

and for $t = 3$ s this is $-3kR^2\omega^2$ (the page's result).

(added) With $\omega = 2\pi$ that is $-12\pi^2kR^2$. The path is a closed loop, yet the work is not zero, so drag is not conservative. Compare the magnetic force, which does no work at all.

## Oscillations and orbits

### Quadratic potentials and harmonic motion

Quadratic potentials produce harmonic motion. On a potential-against-position graph shaped like a bowl, a particle with total energy $E$ is trapped between the two points where the bowl rises to the level $E$, and oscillates between them.

(added) For $V = \tfrac12\kappa y^2$ the force is $F = -\kappa y$, a restoring force proportional to the displacement.

### Tunnel through the Earth

#exam-flagged #worked-example

Question: a hole is drilled through the centre of the Earth. What is the frequency of the mass's oscillations?

Let $y$ be the distance from the centre. Start from $F = ma$:

$$m\frac{d^2y}{dt^2} = -\frac{GM(y)\,m}{y^2}$$

The Earth here is not a point mass, so the mass attracting the particle is not constant: $M = M(y)$. (added) Only the mass inside radius $y$ pulls the particle (the shell theorem), which is what the page uses.

To find $M(y)$ we need the density. Assume the density $\rho$ is constant:

$$M(y) = \rho V(y) = \rho\,\tfrac43\pi y^3 = \frac{M_E}{\tfrac43\pi R^3}\cdot\tfrac43\pi y^3 = \frac{M_E\,y^3}{R^3}$$

$M_E$ is the mass of the Earth and $R$ its radius. Substituting:

$$\frac{d^2y}{dt^2} = -\frac{GM_E\,y}{R^3}$$

Recall $GM_E/R^2 = g$, so

$$\frac{d^2y}{dt^2} = -\frac{g}{R}\,y \;\Rightarrow\; \frac{d^2y}{dt^2} + \frac{g}{R}\,y = 0$$

This is the same equation as for a spring, a pendulum and so on. The standard form is $\ddot{y} + \omega^2 y = 0$, where here $\omega^2 = g/R$ (the page writes $\omega$ without the square). The solution is

$$y = A\cos\!\left(\sqrt{\tfrac{g}{R}}\,t\right) + B\sin\!\left(\sqrt{\tfrac{g}{R}}\,t\right)$$

The frequency (angular frequency, rad/s) is

$$\omega = \sqrt{\frac{g}{R}}$$

(added) Period $2\pi\sqrt{R/g}\approx 84$ minutes (with $R = 6.371\times10^6$ m and $g = 9.81$ m/s$^2$). Dropping from rest at the surface, $y(0) = R$ and $\dot{y}(0) = 0$ give $A = R$ and $B = 0$.

### Moon orbiting Earth and the mass of the Earth

Find the mass of the Earth from the Moon's motion, assuming a circular orbit. The Earth-Moon distance is $3.8\times10^5$ km. Use polar coordinates, since circular motion is natural there. NII, $\vec{F} = m\vec{a}$, with the polar acceleration:

$$-\frac{GMm}{r^2}\,\hat{r} = m\Big[(\ddot{r} - r\dot{\theta}^2)\hat{r} + (r\ddot{\theta} + 2\dot{r}\dot{\theta})\hat{\theta}\Big]$$

For a circle $r = d$ is constant, so $\dot{r} = \ddot{r} = 0$. The radial equation becomes

$$-\frac{GMm}{r^2} = -m\,r\,\dot{\theta}^2$$

Solving for the Earth's mass, with $\dot{\theta} = \omega = 2\pi/T$:

$$M = \frac{d^3\dot{\theta}^2}{G} = \frac{4\pi^2 d^3}{GT^2}$$

$M$ is the mass of the Earth (kg), $d$ the orbital radius (m), $T$ the period (s), $G = 6.67\times10^{-11}$ N m$^2$/kg$^2$. The page uses $d = 3.8\times10^5$ km and $T = 30$ days $= 30\times24\times3600$ s, and gets $M\approx10^{24}$ kg. The page's printed $d$ exponent looks like a square, but dimensionally it must be a cube.

> *I computed it: with $d = 3.8\times10^8$ m and $T = 2.592\times10^6$ s, $M\approx4.8\times10^{24}$ kg. The page's $10^{24}$ kg is the order of magnitude.*

## Rough incline and pulleys

(added) Source: course notes chapter 4 (section 4.4 on pulleys) and chapter 6, tutorials 9 and 12, and the 2025 papers A, B and C. These examples were not on the lecturer's handwritten pages, but they recur in the papers.

### Distance up a rough incline by work-energy

#worked-example #exam-flagged

A block of mass $m$ is projected up a rough incline of angle $\theta$ with speed $v_0$ and coefficient of kinetic friction $\mu$. How far up does it go before it stops?

Forces along the slope (up the slope is positive). Perpendicular to the slope there is no acceleration, so

$$N = mg\cos\theta$$

and the friction magnitude is $\mu N = \mu mg\cos\theta$, acting down the slope while the block moves up. Both gravity's component and friction act down the slope, so the net force along the slope is

$$F = -mg(\sin\theta + \mu\cos\theta)$$

This is constant, so the work over a distance $d$ is $W = Fd$. The work-energy theorem $W = \Delta T$ with the final speed zero gives

$$-mg(\sin\theta + \mu\cos\theta)\,d = 0 - \tfrac12 mv_0^2$$

$$d = \frac{v_0^2}{2g(\sin\theta + \mu\cos\theta)}$$

Do not use $\Delta E = 0$ here. Friction is not conservative, so mechanical energy is lost, and $W = \Delta T$ is the right tool. Equivalently, the lost mechanical energy is $\mu mg\cos\theta\,d$.

Checks: with $\mu = 0$ this gives $d = v_0^2/(2g\sin\theta)$, the smooth result. With $\theta = 0$ it gives $v_0^2/(2\mu g)$, the braking distance on flat ground.

If instead the block is launched down the slope, friction acts up the slope and the net force down the slope is $mg(\sin\theta - \mu\cos\theta)$. The block only stops if $\mu\cos\theta > \sin\theta$, that is $\mu > \tan\theta$, and then the stopping distance for a downward launch at $v_0$ is

$$d = \frac{v_0^2}{2g(\mu\cos\theta - \sin\theta)}$$

(added) Numbers: for $v_0 = 5$ m/s, $\theta = 30^\circ$, $\mu = \tfrac12$ (the 2025 paper A question) 

$$d = \frac{25}{2g(\tfrac12 + \tfrac{\sqrt3}{4})} \approx 1.37\text{ m}$$

> [!warning] ❌ Memo error, paper C question 1
> The printed memo answer of 28.83 m for the paper C incline question does not follow from its own formula. Recomputing gives $d = 40\sqrt2/g \approx 5.77$ m. Always recompute the final number from the formula.

### Pulleys and the Atwood machine

#worked-example

Method (chapter 4, section 4.4): isolate each mass, draw the forces on it, write NII for each, and then use the constraint from the rope.

Setup: mass $m_1$ rests on a smooth slope of angle $\theta$, joined by a light rope over a smooth pulley to mass $m_2$ hanging freely. Let $T$ be the rope tension. A light rope over a smooth pulley has the same tension on both sides, $T_1 = T_2 = T$, because a massless rope or pulley cannot carry a net force.

Constraint: if $x_1$ is the length of rope on the slope side and $x_2$ the length on the hanging side, then $x_1 + x_2 = l$ is constant. Differentiating twice, $\ddot{x}_1 = -\ddot{x}_2$: when one mass moves by some amount the other moves by the same amount the opposite way along the rope.

Let $a = \ddot{x}_2$ be the downward acceleration of $m_2$, so $m_1$ accelerates up the slope with the same magnitude $a$.

NII for $m_2$ (down positive): $m_2 a = m_2 g - T$

NII for $m_1$ (up the slope positive): $m_1 a = T - m_1 g\sin\theta$

Add the two equations to eliminate $T$:

$$a = \frac{(m_2 - m_1\sin\theta)\,g}{m_1 + m_2}$$

and substitute back:

$$T = m_1(a + g\sin\theta) = \frac{m_1m_2(1 + \sin\theta)\,g}{m_1 + m_2}$$

Checks (do these on every pulley question):

- Dimensions: $a$ is an acceleration and $T$ is a force. ✓
- $\theta = \pi/2$ (both hanging, the vertical Atwood machine): $a = \dfrac{(m_2 - m_1)g}{m_1+m_2}$ and $T = \dfrac{2m_1m_2g}{m_1+m_2}$. ✓
- $m_1 = m_2 = m$ and $\theta = \pi/2$: $a = 0$ and $T = mg$. ✓
- If $m_2 = m_1\sin\theta$ the system is in balance and $a = 0$.

(added) One related example from chapter 4, same method:

- Elevator: a mass $m$ on the floor of a lift accelerating upward at $a$ feels a normal reaction $R$ with $R - mg = ma$, so $R = m(g + a)$. The scale reads more than $mg$ when the lift accelerates up.

### Beam in equilibrium with a pulley

#worked-example #exam-flagged

Setup (2025 paper C question 4 and tutorial 9 question 1): a beam with pivot $O$. A mass $m_1$ hangs at distance $\ell$ to the left of $O$. At distance $\lambda\ell$ to the right of $O$ hangs a pulley carrying a rope with masses $m_1$ and $m_2$ on its two sides. Find the $\lambda$ for which the beam can be in equilibrium. The note in the question says the beam can be in equilibrium even though $m_2$ accelerates.

Moments about $O$ (the pivot is the natural point because its own reaction has no moment). Equilibrium means the total moment is zero:

$$\ell F_1 - \lambda\ell F_2 = 0 \;\Rightarrow\; \lambda = \frac{F_1}{F_2}$$

where $F_1$ and $F_2$ are the downward loads on the beam at the two ends.

Left end: the hanging mass is at rest, so its rope tension balances its weight and $F_1 = m_1 g$.

Right end: the load is the force the rope puts on the pulley. The rope passes over the pulley, so the load is twice the rope tension $T_3$:

$$F_2 = 2T_3$$

Find $T_3$ from the Atwood machine of $m_1$ and $m_2$ (the vertical case above):

$$T_3 = \frac{2m_1m_2g}{m_1 + m_2} \;\Rightarrow\; F_2 = \frac{4m_1m_2g}{m_1 + m_2}$$

Then

$$\lambda = \frac{F_1}{F_2} = \frac{m_1 g\,(m_1 + m_2)}{4m_1m_2g} = \frac{m_1 + m_2}{4m_2}$$

Check: if $m_1 = m_2$ the pulley load is $2mg$ (the rope is static, $T_3 = mg$), and $\lambda = \dfrac{2m}{4m} = \tfrac12$, which matches $F_1 = mg$ against $F_2 = 2mg$. ✓

> [!tip] Why the beam balances while $m_2$ accelerates
> The beam only feels the tension in the rope over the pulley, and that tension is constant while the masses move with constant acceleration, so the moment stays constant.

## Systems of particles

### N-body motion

For $N$ particles there are $3N$ equations in general. A galaxy simulation is the standard example. The Milky Way has about $2\times10^{11}$ stars.

The page writes the equation of motion for particle $i$ as

$$\frac{d^2\vec{x}_i}{dt^2} = \sum_{j\neq i}\frac{G\,m_i m_j}{\|\vec{x}_i - \vec{x}_j\|^2}\,\hat{x}_{ij}$$

(added) As an acceleration equation the factor $m_i$ should not appear on the right: the force form is $m_i\ddot{\vec{x}}_i = \sum_{j\neq i}\dfrac{Gm_im_j}{\|\vec{x}_i-\vec{x}_j\|^2}\hat{x}_{ij}$, which gives $\ddot{\vec{x}}_i = \sum_{j\neq i}\dfrac{Gm_j}{\|\vec{x}_i-\vec{x}_j\|^2}\hat{x}_{ij}$. Here $\hat{x}_{ij}$ is the unit vector along the line joining particles $i$ and $j$ (pointing from $i$ toward $j$ for attraction).

### Lagrangian and Hamiltonian mechanics

Two reformulations are named:

- Lagrangian mechanics, with $L = T - V$ and the action $S = \int L\,dt$.
- Hamiltonian mechanics, with $H = T + V$, and $H\equiv E$.

Both are formed from scalars, so they are invariant: the coordinate system does not matter. This allows generalised coordinates, for example $(x,\theta)$ for a mass on a spring (position $x$) carrying a hanging pendulum (angle $\theta$).

(added) The pages name these only. No equations of motion are derived from them here.

## Dynamics revision pages

These pages revise solving NII for the four kinds of force. They are included here because the substitution $\ddot{x} = v\,dv/dx$ underlies the energy results above.

### The four force cases

The core of solving is $\vec{F} = m\vec{a}$, or equivalently $d\vec{p}/dt = \vec{F}$. We are attempting to find $\vec{r}(t)$, though sometimes we land at finding $\vec{v}(\vec{x})$ instead.

There are four cases:

- $\vec{F} = \vec{F}_0$ (constant)
- $\vec{F} = \vec{F}(t)$
- $\vec{F} = \vec{F}(\vec{v})$
- $\vec{F} = \vec{F}(\vec{x})$

The easiest types need only direct integration. Since $\vec{F} = m\vec{a}$ is the same as $\ddot{\vec{r}}(t) = \vec{F}/m$:

$$\dot{\vec{r}}(t) = \int\frac{\vec{F}}{m}\,dt, \qquad \vec{r}(t) = \int\left(\int\frac{\vec{F}}{m}\,dt\right)dt + \text{initial or boundary conditions}$$

### Separable force of position and speed

For velocity-dependent forces ($\vec{F} = \vec{F}(\vec{v})$) and force depending on position and speed, we cannot simply integrate with respect to time: $\int f(v_x,x)\,dt$ cannot be computed without knowing $x(t)$ and $v(t)$ explicitly. Since $f$ does not depend on $t$, make $x$ the independent variable, which means expressing $v$ in terms of $x$.

$$a_x = \frac{dv_x}{dt} = \frac{dv_x}{dx}\frac{dx}{dt} = v_x\frac{dv_x}{dx}$$

NII becomes

$$mv_x\frac{dv_x}{dx} = f(v_x,x)$$

For a force that factorises as $f(v_x,x) = f_1(v_x)\,g_1(x)$, this separates:

$$m\int\frac{v_x}{f_1(v_x)}\,dv_x = \int g_1(x)\,dx$$

For now you will always be able to write $v_x = v_x(x)$. The page marks the 2012 semester test 2, question 1 as extra work on this equation, $m\,d^2x/dt^2 = F$ with $F$ depending on speed and position.

### Friction proportional to speed

The page takes $F = -kv$, written per unit mass as $\ddot{x} = -k\dot{x}$. Using $\ddot{x} = v\,dv/dx$:

$$v\frac{dv}{dx} = -kv \;\Rightarrow\; \frac{dv}{dx} = -k \;\Rightarrow\; v = -kx + c$$

With $v = v_0$ at $x = x_0$: $v_0 = -kx_0 + c$, so $c = v_0 + kx_0$. Then $dx/dt = -kx + c$, which separates:

$$\int\frac{1}{-kx + c}\,dx = \int 1\,dt$$

Substitute $u = -kx + c$, $du = -k\,dx$. The page's final line is $x = Ae^{-kt}$, which is the special case $c = 0$.

(added) General solution of $dx/dt = -kx + c$ with $x(0) = x_0$:

$$x(t) = x_0 + \frac{v_0}{k}\left(1 - e^{-kt}\right)$$

### Force proportional to speed cubed

$F = -kv^3$ gives $m\ddot{x} = -k\dot{x}^3$, that is $m\,\dfrac{d^2x}{dt^2} = -k\left(\dfrac{dx}{dt}\right)^3$. With $\dot{x} = v$ and $\ddot{x} = v\,dv/dx$:

$$v\frac{dv}{dx} = -\frac{k}{m}v^3 \;\Rightarrow\; \frac{dv}{dx} = -\frac{k}{m}v^2$$

Separate variables:

$$\int\frac{dv}{v^2} = -\int\frac{k}{m}\,dx \;\Rightarrow\; -\frac{1}{v} = -\frac{kx}{m} + c \;\Rightarrow\; v = \frac{1}{\frac{kx}{m} - c}$$

Now $v = dx/dt$, so

$$\int\left(\frac{kx}{m} - c\right)dx = \int 1\,dt \;\Rightarrow\; \frac{k}{2m}x^2 - cx + d = t$$

This is a quadratic in $x$ for each $t$, so

$$x = \frac{c \pm\sqrt{c^2 - 2\frac{k}{m}(d - t)}}{k/m}$$

The page sketches $t$ against $x$ as a parabola. (added) The initial conditions choose the root and fix the constants: $c = \dfrac{kx_0}{m} - \dfrac{1}{v_0}$ from $v(x_0) = v_0$, and $d$ from $t = 0$ at $x = x_0$.

## Do not forget

- $\vec{\nabla}\times(\vec{\nabla}f) = \vec{0}$ always. A force is conservative when its curl is zero (no holes in the region), and then $\oint\vec{F}\cdot d\vec{r} = 0$ and work is path independent.
- <span style="color:#f08c00">Open:</span> curl is nabla cross a vector field. The gradient needs a scalar.
- <span style="color:#f08c00">Open:</span> finding the potential is partial integration with an unknown function of the other variable, matched with the other partial derivative. It is not separation of variables.
- $W = \Delta T$ holds for any force. $\Delta E = 0$ holds only if $\vec{F} = -\vec{\nabla}V$.
- Sign convention: chapter 5 writes $\vec{F} = \vec{\nabla}f$, the energy chapter writes $\vec{F} = -\vec{\nabla}V$, and $V = -f$.
- ❌ Through an embedding impact use momentum, then use energy for the climb.
- Leaving a surface happens when the normal force reaches zero.
- Drag is not conservative (nonzero work on a closed loop). A magnetic force does no work.
- A rough incline needs $W = \Delta T$, not $\Delta E = 0$: $d = v_0^2/\big(2g(\sin\theta + \mu\cos\theta)\big)$ going up.
- Pulley: one equation per mass, same tension on a light rope, and the constraint $\ddot{x}_1 = -\ddot{x}_2$.
- Spring: $V = \tfrac12 kx^2$, and $F = -dV/dx$ as the check.
- $\ddot{x} = v\,dv/dx$ turns a position-dependent or speed-dependent NII into something separable.

## See also

- [[APM01B1_Notes_S1_PolarIntrinsicCoordinates]]
- [[APM01B1_Notes_S2_Dynamics]]
