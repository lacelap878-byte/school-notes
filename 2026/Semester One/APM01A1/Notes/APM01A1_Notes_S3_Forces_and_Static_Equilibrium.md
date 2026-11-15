---
module: APM01A1
topic: Forces and Static Equilibrium
session: S3
tags: [definition, formula, worked-example, common-mistake, added]
---

# APM01A1 Notes S3: Forces and Static Equilibrium

Source: your handwritten Semester One notes, pages 14 to 26 (cited by PDF page). Short revision notes, not from a teaching session.

Checked: every equation and number below was checked in Python (SymPy) on 15 Nov 2026. Numbers use $g = 9.8$ m/s$^2$ unless the notes fix another value.

## Definitions (source: pages 14 to 15)

> - **Static equilibrium:** a window of time in which dynamic processes can be ignored.
> - **Space:** physical "empty" space, the place in which objects move.
> - **Time:** the measurement taken on a clock.
> - **Mass:** a measure of how much matter makes up an object.
> - **Force:** the mutual influence of one object on another.
> - **Particle:** a body that may be treated as a point (a point in the Euclidean sense: its position can be given by coordinates).
> - **Rigid body:** an extended body whose deformations may be ignored.

Limits of Newtonian mechanics:
- Quantum limit: on a small, sub-atomic scale Newton's laws break down.
- Relativistic limits: at speeds close to the speed of light (special relativity), and near very large masses such as the sun (general relativity), Newton's laws break down.
- So the forces holding a table together can be found with statics, but not those holding a neutron star in equilibrium (too heavy).

## Forces (source: page 16)

- A force is a push or a pull (direction is part of it, so $+$ and $-$ matter); physical contact is not necessary. It is an action that makes an object react as though pushed or pulled, so forces are described by vectors and all vector algebra applies.

| Force | Kind |
|---|---|
| Gravitation, electrostatic, magnetic | field |
| Normal, friction, buoyancy | contact, reaction |
| Tension | contact, continuous |
| Applied force | dynamic |
| Centrifugal | fictitious, frame dependent |
| Pressure gradients | direct contact |
| Quantum: strong and weak, exclusion principle | quantum |

## Newton's laws and connectors (source: page 20)

> - **NI (inertia):** still things stay still, and motion stays constant, provided no force acts.
> - **NII:** $\vec{F} = m\vec{a}$, better read as $\vec{a} = \dfrac{\vec{F}}{m}$ (the force is the cause, the acceleration the effect).
> - **NIII:** $\vec{F}_{ij} = -\vec{F}_{ji}$

$$\vec{F} = \frac{d\vec{p}}{dt} = \frac{d}{dt}(m\vec{v})$$

$\vec{p} = m\vec{v}$ is the momentum; this form allows the mass to change (mass loss or gain).

- Newton's laws only work in an inertial system (the notes: a still box of finite size over a finite time).
- Connectors transmit forces. Rods: rigid, inextensible and incompressible. Springs: extensible and compressible. Cords: cannot be extended, but can go slack.

## The equilibrium method (source: pages 17 to 18, 25)

The main point of statics:

$$\vec{F}_{net} = \vec{0} \quad \Longleftrightarrow \quad F^x_{net} = 0, \ F^y_{net} = 0, \ F^z_{net} = 0$$

Resolving forces therefore reduces to solving simultaneous equations (for rigid bodies, $\vec{M}_{net} = \vec{0}$ as well: see S4).

1. Identify every force acting on the body (draw it).
2. Write each force in components: magnitude times a unit vector. For a cable, the unit vector comes from the coordinates of its two ends: $\vec{T} = T\,\dfrac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|}$.
3. Set $\vec{F}_{net} = \vec{0}$, one equation per component, and solve.

- Friction: $F_\mu = \mu N$, where $N$ is the size $\|\vec{N}\|$ of the normal force, but friction acts along the surface, not along $\vec{N}$. Be careful with its direction.
- If there are several bodies (or points such as a knot), each has its own equilibrium equations.

Example (source: page 26, pencil note): a cable meets the object at $A = (0, 3, 4)$ and the wall at $B = (1, 5, 6)$.
   $\overrightarrow{AB} = (1, 2, 2)$ with length 3, so $\vec{T} = \dfrac{T}{3}(\hat{x} + 2\hat{y} + 2\hat{z})$.

## Block on a slope (source: pages 17 to 19)

Take $x$ up the slope and $y$ perpendicular to it. For a block of mass $m$ on a slope at angle $\theta$ with friction coefficient $\mu$:

$$\vec{F}_g = -mg\sin\theta\,\hat{x} - mg\cos\theta\,\hat{y} \qquad \vec{F}_N = N\hat{y} \qquad \vec{F}_\mu = \mu N\hat{x}$$

$$-mg\sin\theta + \mu N = 0 \qquad -mg\cos\theta + N = 0$$

- A coupled linear system. With the unknowns as a vector it becomes a matrix equation:

$$\begin{pmatrix} -g\sin\theta & \mu \\ -g\cos\theta & 1 \end{pmatrix}\begin{pmatrix} m \\ N \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

- (added) Solving: $N = mg\cos\theta$ and $\tan\theta = \mu$. That is the steepest slope at which the block stays put; the matrix has a nonzero solution only when its determinant $g(\mu\cos\theta - \sin\theta)$ is 0, which is the same condition.

Example (source: page 19)
$\mu = 0.001$, $m = 10$ kg, $\theta = 30^\circ = \frac{\pi}{6}$. A horizontal force $\vec{F}_A$ pushes the block into the slope. Find $\|\vec{F}_A\|$ so that the block stays stationary.

WORKING
$\vec{F}_A = F_A\cos\theta\,\hat{x} - F_A\sin\theta\,\hat{y}$.
(1) $-mg\sin\theta + \mu N + F_A\cos\theta = 0$; (2) $-mg\cos\theta + N - F_A\sin\theta = 0$.
From (2), $N = mg\cos\theta + F_A\sin\theta$; into (1):

$$F_A = \frac{mg(\sin\theta - \mu\cos\theta)}{\mu\sin\theta + \cos\theta} = 56.45 \text{ N} \quad \text{(added: the number, with } g = 9.8 \text{ m/s}^2\text{)}$$

## Cords on a ceiling (source: pages 21 to 22)

Example (source: page 21)
Two cords at $30^\circ$ and $45^\circ$ to the ceiling meet at a knot, and a vertical cord from the knot holds a 100 kg mass. Find the tensions $T_1$ (left cord) and $T_2$ (right cord).

WORKING
The mass is in equilibrium, so the vertical cord pulls down on the knot with $T_3 = mg = 980$ N.
$\vec{T}_1 = -T_1\cos30^\circ\,\hat{x} + T_1\sin30^\circ\,\hat{y}$, $\vec{T}_2 = T_2\cos45^\circ\,\hat{x} + T_2\sin45^\circ\,\hat{y}$.
$x$: $-T_1\cos30^\circ + T_2\cos45^\circ = 0$. $y$: $T_1\sin30^\circ + T_2\sin45^\circ - mg = 0$.

$$\begin{pmatrix} -\cos30^\circ & \cos45^\circ \\ \sin30^\circ & \sin45^\circ \end{pmatrix}\begin{pmatrix} T_1 \\ T_2 \end{pmatrix} = \begin{pmatrix} 0 \\ mg \end{pmatrix}$$

Solve by substitution (or with the inverse matrix): $T_1 = 717.4$ N, $T_2 = 878.6$ N (added: the numbers; the notes stop at the method).

## Spring and pulley (source: pages 22 to 23)

Example (source: page 22)
Block A on a horizontal table is attached to a spring (fixed to the wall, natural length $x_0$, constant $k$) and, by a cord over a pulley, to a hanging mass B of 20 kg. Find the extension of the spring.

WORKING
There are two points of equilibrium.
B: $-m_Bg + T_B = 0$, so $T_B = m_Bg$.
A: $-m_Ag\,\hat{y} + N_A\,\hat{y} + T_A\,\hat{x} + F_{SA}\,\hat{x} = \vec{0}$, so $N_A = m_Ag$ and $F_{SA} = -T_A$.
Same cord, same tension: $T_A = T_B = m_Bg$. With $F_{SA} = -k(x - x_0)$: $k(x - x_0) = m_Bg$, so

$$x - x_0 = \frac{m_Bg}{k} = \frac{196}{k} \text{ m}$$

- (added) The notes write $F_{SA} = T_A$ and end with $x = x_0 - \frac{m_Bg}{k}$, a sign slip: the $x$-equation gives $F_{SA} = -T_A$, and the spring is stretched, so $x = x_0 + \frac{m_Bg}{k}$.

## Three cables in 3D (source: pages 23 to 25)

Example (source: page 23)
A 500 kg mass hangs from three cables. $\vec{T}_1$ lies in the $x$-$z$ plane at angle $\theta$ above the horizontal; $\vec{T}_2$ and $\vec{T}_3$ run along $(10, \mp2.5, 10)$ m and are symmetric about the vertical. Find the tensions.

WORKING
Unit vectors: divide each direction by its length, since only the direction is wanted.
$\vec{T}_1 = T_1(-\cos\theta\,\hat{x} + \sin\theta\,\hat{z})$ (from $-10\hat{x} + 10\tan\theta\,\hat{z}$ divided by $10\sec\theta$).
$\vec{T}_2 = \dfrac{T_2}{\sqrt{206.25}}(10\hat{x} - 2.5\hat{y} + 10\hat{z})$, $\vec{T}_3 = \dfrac{T_3}{\sqrt{206.25}}(10\hat{x} + 2.5\hat{y} + 10\hat{z})$, with $\sqrt{206.25} = 14.36$.
$\vec{W} + \vec{T}_1 + \vec{T}_2 + \vec{T}_3 = \vec{0}$ with $\vec{W} = -mg\,\hat{z}$:
(1) $x$: $-T_1\cos\theta + \dfrac{10T_2}{\sqrt{206.25}} + \dfrac{10T_3}{\sqrt{206.25}} = 0$
(2) $y$: $\dfrac{2.5T_3}{\sqrt{206.25}} - \dfrac{2.5T_2}{\sqrt{206.25}} = 0$, so $T_3 = T_2$
(3) $z$: $-mg + T_1\sin\theta + \dfrac{10T_2}{\sqrt{206.25}} + \dfrac{10T_3}{\sqrt{206.25}} = 0$
(added) Subtract (1) from (3): $T_1(\sin\theta + \cos\theta) = mg$, so

$$T_1 = \frac{mg}{\sin\theta + \cos\theta} = \frac{4900}{\sin\theta + \cos\theta} \text{ N} \qquad T_2 = T_3 = \frac{\sqrt{33}}{8}\,T_1\cos\theta$$

The notes give no value for $\theta$, so the answer stays in terms of $\theta$.

## Do not forget

- Equilibrium: $\vec{F}_{net} = \vec{0}$ gives one equation per component.
- A tension is magnitude times a unit vector; the unit vector comes from the coordinates of the cable's ends.
- Friction $\mu N$ uses the size of $\vec{N}$ but acts along the surface.
- Same cord over a frictionless pulley means the same tension at both ends.

## See also

- [[APM01A1_Notes_S1_Vectors]]
- [[APM01A1_Notes_S2_Vector_Products]]

---
*CDG v13 | written S3 | 2026-11-15*
