---
module: APM01A1
topic: Vectors
session: S1
tags: [definition, formula, theorem, worked-example, added]
---

# APM01A1 Notes S1: Vectors

Source: your handwritten Semester One notes (Applied_Maths_First_Semester_Notes.pdf, 38 pages), pages 1 to 9, cited by PDF page. Page 4 is the "continue on the page with the star" page and page 6 is the strip that finishes the proof on page 5; read in that order the notes run straight through. Short revision notes, not from a teaching session.

Checked: the worked results were checked in Python (SymPy) on 15 Nov 2026.

## Vectors and scalars (source: page 1)

> A vector is a quantity having both magnitude and direction. Scalars are quantities having magnitude but no direction and can be any real number.

- Graphically: an arrow $\overrightarrow{OP}$. The tail $O$ is the origin (initial point); the head $P$ is the terminal point (terminus). The length of the arrow is the magnitude.
- Notation: $\vec{A}$, magnitude $|\vec{A}|$ or $A$ (bold in printed books); $\overrightarrow{OP}$ with magnitude $|\overrightarrow{OP}|$.
- Scalar operations follow the ordinary rules of algebra.

## Vector algebra (source: pages 1 to 2)

1. $\vec{A}$ and $\vec{B}$ are equal if they have the same magnitude and direction, regardless of where their initial points are.
2. $-\vec{A}$ has the same magnitude as $\vec{A}$ and the opposite direction.
3. Sum (resultant): place the initial point of $\vec{B}$ on the terminal point of $\vec{A}$; $\vec{C} = \vec{A} + \vec{B}$ joins the initial point of $\vec{A}$ to the terminal point of $\vec{B}$ (head to tail).
4. Difference: $\vec{A} - \vec{B}$ is the vector $\vec{C}$ that, added to $\vec{B}$, gives $\vec{A}$, so $\vec{C} = \vec{A} + (-\vec{B})$. If $\vec{A} = \vec{B}$, then $\vec{A} - \vec{B} = \vec{0}$, the null vector; vectors that are not null are proper vectors.
5. $m\vec{A}$ is a vector: the scalar $m$ stretches it ($m > 1$), shrinks it ($0 < m < 1$), or reverses it ($m < 0$).

> **Laws of vector algebra:** if $\vec{A}$, $\vec{B}$, $\vec{C}$ are vectors and $m$, $n$ are scalars, then

$$\vec{A} + \vec{B} = \vec{B} + \vec{A} \qquad \vec{A} + (\vec{B} + \vec{C}) = (\vec{A} + \vec{B}) + \vec{C}$$

$$m\vec{A} = \vec{A}m \qquad m(n\vec{A}) = (mn)\vec{A} \qquad (m + n)\vec{A} = m\vec{A} + n\vec{A} \qquad m(\vec{A} + \vec{B}) = m\vec{A} + m\vec{B}$$

These are, in order: commutative and associative laws for addition, commutative and associative laws for multiplication by a scalar, and the two distributive laws. The product laws here are for scalar times vector only.

## Position vectors and invariants (source: page 2)

- The simplest vector is the position vector of a point $P$. It only makes sense once an origin and a set of axes are chosen, and that choice belongs to the observer, so two observers give $P$ different coordinates.
- An invariant is a quantity that does not depend on the observer: displacement, mass, distance, momentum, energy, area, volume, time difference. Invariants are the quantities everyone can agree on.
- The position vector is not invariant.

## Displacement vectors and distance (source: pages 3 to 4)

$$\overrightarrow{P_1P_2} = \vec{P_2} - \vec{P_1} = \langle P_{x_2} - P_{x_1},\ P_{y_2} - P_{y_1} \rangle$$

The displacement from $P_1$ to $P_2$; use $\langle \ \rangle$ for vectors and $( \ )$ for points.

- $\vec{P_2} = \vec{P_1} + \overrightarrow{P_1P_2}$: going to $P_2$ is the same as going to $P_1$, then from $P_1$ to $P_2$.
- A displacement does not need the axes or origin: every observer gets the same $\overrightarrow{P_1P_2}$, so it is invariant. The position vector becomes a displacement from the origin: $\overrightarrow{OP_1} = (P_{x_1}, P_{y_1}) - (0, 0) = \langle P_{x_1}, P_{y_1} \rangle$, where $\vec{0} = \langle 0, 0 \rangle$ is the zero vector.
- $\overrightarrow{P_1P_2} = -\overrightarrow{P_2P_1}$, so $\overrightarrow{P_1P_2} + \overrightarrow{P_2P_1} = \vec{0}$.

Euclidean distance (a scalar, the same for every observer):

$$\|\overrightarrow{P_1P_2}\| = \sqrt{(P_{x_2} - P_{x_1})^2 + (P_{y_2} - P_{y_1})^2} = \|\overrightarrow{P_2P_1}\|$$

$$\|\overrightarrow{Q_1Q_2}\| = \sqrt{(Q_{x_2} - Q_{x_1})^2 + (Q_{y_2} - Q_{y_1})^2 + (Q_{z_2} - Q_{z_1})^2} \quad \text{in 3D}$$

- The distances are equal, but $\overrightarrow{P_1P_2} \ne \overrightarrow{P_2P_1}$.

## Adding vectors geometrically (source: pages 4 to 5)

- Connecting vectors head to tail is addition: $\vec{a} + \vec{b} = \vec{c}$. Several vectors: $\vec{a} + \vec{b} + \vec{c} + \vec{d} = \vec{e}$.
- If the sum is $\vec{0}$, the vectors form a closed figure.
- Application: a body in equilibrium under $\vec{F_1}$, $\vec{F_2}$ and its weight $\vec{W}$ has $\vec{F}_{net} = \vec{F_1} + \vec{F_2} + \vec{W} = \vec{0}$, so the three force arrows drawn head to tail close into a triangle.

## Vector proof: the midpoints of a quadrilateral form a parallelogram (source: pages 5 to 6)

> Let $a$, $b$, $c$, $d$ be the midpoints of the sides $AB$, $BC$, $CD$, $DA$ of a quadrilateral $ABCD$. Prove that $abcd$ is a parallelogram.

Ingredients:
1. Triangle rule: $\vec{a} + \vec{b} = \vec{c}$.
2. $-\vec{a}$ is the reverse of $\vec{a}$.
3. $\alpha\vec{b}$ stretches ($\alpha > 1$) or shrinks ($0 < \alpha < 1$) $\vec{b}$.
4. If $\vec{a}$ and $\vec{b}$ are parallel, then $\vec{a} = \alpha\vec{b}$ for some scalar $\alpha$.

Proof (steps tidied, added):

$$\overrightarrow{da} = \tfrac{1}{2}\overrightarrow{DA} + \tfrac{1}{2}\overrightarrow{AB} = \tfrac{1}{2}\overrightarrow{DB} \qquad \overrightarrow{bc} = \tfrac{1}{2}\overrightarrow{BC} + \tfrac{1}{2}\overrightarrow{CD} = \tfrac{1}{2}\overrightarrow{BD}$$

So $\overrightarrow{da} = -\overrightarrow{bc}$: the sides $da$ and $bc$ have equal length and exactly opposite direction, so they are parallel and equal (ingredient 4 with $\alpha = -1$). The same argument gives $\overrightarrow{ab} = \tfrac{1}{2}\overrightarrow{AC} = \overrightarrow{dc}$. A quadrilateral with both pairs of opposite sides parallel and equal is a parallelogram. (The notes also use $\overrightarrow{AB} + \overrightarrow{BC} + \overrightarrow{CD} + \overrightarrow{DA} = \vec{0}$, the closed figure.)

## Components and direction cosines (source: pages 7 to 8)

- The measurable parts of $\vec{P}$ are its magnitude and its direction (angle, inclination).
- Radians represent angles with real numbers and no unit. 1 radian is the angle subtended by an arc equal in length to the radius; $180^\circ = \pi$ rad.

$$P_x = \|\vec{P}\|\cos\alpha \qquad P_y = \|\vec{P}\|\cos\beta \qquad P_z = \|\vec{P}\|\cos\gamma$$

$\alpha$, $\beta$, $\gamma$ are the angles between $\vec{P}$ and the $x$, $y$ and $z$ axes. In 2D, $P_y = \|\vec{P}\|\sin\alpha = \|\vec{P}\|\cos\beta$.

$$\|\vec{P}\|^2 = P_x^2 + P_y^2 + P_z^2 \qquad \cos^2\alpha + \cos^2\beta + \cos^2\gamma = 1$$

$$\cos\alpha = \frac{P_x}{\|\vec{P}\|} \qquad \cos\beta = \frac{P_y}{\|\vec{P}\|} \qquad \cos\gamma = \frac{P_z}{\|\vec{P}\|}$$

- These are the direction cosines. The angles are not complementary in 3D, but this identity links them (substitute the components into $\|\vec{P}\|^2$).
- (added) Two slips in the notes: page 7 says $\alpha$ is measured from the vertical and $\beta$ from the horizontal, but the diagram and page 8 ($P_x = \|\vec{P}\|\cos\alpha$) use $\alpha$ from the $x$-axis, as here; and page 8 writes $\cos\alpha = P_y/\|\vec{P}\|$, which should be $P_x$.

## Basis vectors (source: pages 8 to 9)

$$\vec{P} = P_x\hat{x} + P_y\hat{y} + P_z\hat{z} \qquad \hat{x} = (1, 0, 0), \ \hat{y} = (0, 1, 0), \ \hat{z} = (0, 0, 1)$$

- $\hat{x}$, $\hat{y}$ give the independent directions: they do not depend on each other or on $\vec{P}$, and $\|\hat{x}\| = \|\hat{y}\| = 1$. Other notations: $\hat{x} = \hat{i} = \vec{e}_x$.
- $P_x\hat{x} + P_y\hat{y} = (P_x, 0) + (0, P_y) = (P_x, P_y)$.
- The components are the projections of $\vec{P}$ on the basis vectors: $P_x = \vec{P} \cdot \hat{x}$ (see the next note).

## Do not forget

- Position vectors depend on the observer; displacements and distances do not.
- $\overrightarrow{P_1P_2} = \vec{P_2} - \vec{P_1}$ (end minus start), and $\overrightarrow{P_1P_2} = -\overrightarrow{P_2P_1}$.
- Vectors summing to $\vec{0}$ close into a figure: the picture of equilibrium.
- $\cos^2\alpha + \cos^2\beta + \cos^2\gamma = 1$.

---
*CDG v13 | written S1 | 2026-11-15*
