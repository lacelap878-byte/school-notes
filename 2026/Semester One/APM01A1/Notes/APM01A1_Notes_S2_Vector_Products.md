---
module: APM01A1
topic: Vector Products
session: S2
tags: [definition, formula, worked-example, common-mistake, added]
---

# APM01A1 Notes S2: Vector Products

Source: your handwritten Semester One notes, pages 9 to 14 (cited by PDF page), plus Question 1.2 and Question 3 of the June 2025 final (in the APM01A1 Past Papers folder, no memo) as an exam-style example. Short revision notes, not from a teaching session.

Checked: every product, projection and area below was checked in Python (SymPy) on 15 Nov 2026.

## Three ways to multiply vectors (source: page 9)

$\vec{a}$ times $\vec{b}$ can give:
- a scalar: the dot (scalar) product $\vec{a} \cdot \vec{b}$
- a vector: the cross (vector) product $\vec{a} \times \vec{b}$
- a tensor: the tensor product $\vec{a} \otimes \vec{b}$ (named only, not used further)

## The dot product (source: pages 9 to 11)

$$\vec{a} \cdot \vec{b} = \|\vec{a}\|\,\|\vec{b}\|\cos\theta \qquad \vec{a} \cdot \vec{b} = a_x b_x + a_y b_y + a_z b_z$$

$\theta$ is the angle between $\vec{a}$ and $\vec{b}$ (geometric form); the second is the component form.

- The component form follows from expanding $(a_x\hat{x} + a_y\hat{y}) \cdot (b_x\hat{x} + b_y\hat{y})$ with $\hat{x} \cdot \hat{x} = \hat{y} \cdot \hat{y} = 1$ and $\hat{x} \cdot \hat{y} = 0$.

> If $\vec{a} \cdot \vec{b} = 0$ then $\vec{a}$ is orthogonal (perpendicular) to $\vec{b}$.

## Projections (source: pages 9 to 10)

- The projection of $\vec{a}$ on $\vec{b}$ tells how much of $\vec{a}$ points along $\vec{b}$:

$$\vec{a} \cdot \hat{b} = \|\vec{a}\|\cos\theta \qquad \hat{a} \cdot \vec{b} = \|\vec{b}\|\cos\theta$$

- Components are projections on the basis vectors: $P_x = \vec{P} \cdot \hat{x}$, since $(P_x, P_y) \cdot (1, 0) = P_x$.
- (added) The projection vector of $\vec{b}$ in the direction of $\vec{c}$ is $(\vec{b} \cdot \hat{c})\,\hat{c} = \dfrac{\vec{b} \cdot \vec{c}}{\vec{c} \cdot \vec{c}}\,\vec{c}$ (the 2025 final asks for it).

Examples (source: pages 10 to 11), with $\vec{a} = (1, 2, 3)$ and $\vec{b} = (x, 5, 7)$:
- Orthogonal: $\vec{a} \cdot \vec{b} = x + 10 + 21 = 0$, so $x = -31$.
- $\vec{b}$ a unit vector: $x^2 + 25 + 49 = 1$ gives $x^2 = -73$: no real $x$.
- $\|\overrightarrow{ab}\| = 1$: $(x - 1)^2 + 3^2 + 4^2 = 1$ gives $x^2 - 2x + 25 = 0$, discriminant $4 - 100 < 0$: no real $x$ (the last step is added; the notes stop at the quadratic).

## Handedness of axes (source: page 11)

- Right-handed system: curl the fingers of the right hand from $x$ to $y$; the thumb points along $z$. Seen from the top of $z$, going from $x$ to $y$ is anticlockwise.
- If going from $x$ to $y$ is clockwise seen from the top, the system is left-handed. Always draw right-handed axes.

## Torque: why the cross product (source: pages 12 to 13)

- Opening a 1000 kg safe door: the size of the force is not enough; where and in which direction it acts matters. A push along the door towards the hinge, or at the hinge, does nothing; a push perpendicular to the door at the far edge works best.
- Only the component of $\vec{F}$ perpendicular to $\vec{r}$ turns the door: $F_\perp = F\sin\theta$.

$$\|\vec{M}\| = \|\vec{r}\|\,\|\vec{F}\|\sin\theta \qquad \vec{M} = \vec{r} \times \vec{F}$$

$\vec{M}$ is the torque (moment of force) in N m, $\vec{r}$ is the position of the point where $\vec{F}$ acts, measured from the pivot, and $\theta$ is the angle between $\vec{r}$ and $\vec{F}$.

- The door moves in the $x$-$y$ plane, about the $z$-axis, so its torque points along $\pm\hat{z}$.

## The cross product (source: page 13)

$$\hat{x} \times \hat{y} = \hat{z} \qquad \hat{y} \times \hat{z} = \hat{x} \qquad \hat{z} \times \hat{x} = \hat{y}$$

$$\hat{y} \times \hat{x} = -\hat{z} \qquad \hat{z} \times \hat{y} = -\hat{x} \qquad \hat{x} \times \hat{z} = -\hat{y} \qquad \hat{x} \times \hat{x} = \hat{y} \times \hat{y} = \hat{z} \times \hat{z} = \vec{0}$$

$$\vec{a} \times \vec{b} = (a_y b_z - a_z b_y)\,\hat{x} + (a_z b_x - a_x b_z)\,\hat{y} + (a_x b_y - a_y b_x)\,\hat{z}$$

- Cyclic order $x \to y \to z \to x$ gives $+$; the reverse order gives $-$. So $\vec{a} \times \vec{b} = -\vec{b} \times \vec{a}$, and parallel vectors (including $\vec{a} \times \vec{a}$) give $\vec{0}$.
- (added) $\vec{a} \times \vec{b}$ is perpendicular to both $\vec{a}$ and $\vec{b}$, in the right-hand-rule direction, with length $\|\vec{a}\|\,\|\vec{b}\|\sin\theta$.
- The cross product is not associative: $(\vec{a} \times \vec{b}) \times \vec{c} \ne \vec{a} \times (\vec{b} \times \vec{c})$ in general.
- Memory aid for the components (the notes' corner sketch): write $x\ y\ z\ x\ y$ and cross-multiply diagonally.

Example (composite, with the vectors from the dot product examples): $\vec{a} = (1, 2, 3)$, $\vec{b} = (-31, 5, 7)$.
   $\vec{a} \times \vec{b} = (2 \cdot 7 - 3 \cdot 5,\ 3(-31) - 1 \cdot 7,\ 1 \cdot 5 - 2(-31)) = (-1, -100, 67)$. Check: $\vec{a} \cdot (\vec{a} \times \vec{b}) = -1 - 200 + 201 = 0$.

## Which products make sense (source: page 13)

- Allowed: $\vec{a} \cdot (\vec{b} \times \vec{c})$, $(\vec{a} \times \vec{b}) \cdot \vec{c}$, $(\vec{a} \times \vec{b}) \cdot (\vec{b} \times \vec{c})$.
- Not allowed: $\vec{a} \times (\vec{b} \cdot \vec{c})$ and $(\vec{a} \cdot \vec{b}) \cdot (\vec{a} \times \vec{b})$: a dot or cross product needs a vector on each side, and $\vec{b} \cdot \vec{c}$ is a scalar.

If $\vec{a} \times \vec{b} = \vec{c}$:
- $(\vec{a} \times \vec{b}) \times \vec{c} = \vec{c} \times \vec{c} = \vec{0}$
- $(\vec{a} \times \vec{b}) \cdot \vec{c} = \vec{c} \cdot \vec{c} = \|\vec{c}\|^2$, and so $\vec{a} \cdot (\vec{b} \times \vec{c}) = \|\vec{c}\|^2$ too (cyclic triple product, added)
- $(\vec{a} \times \vec{c}) \cdot \vec{c} = 0$, because $\vec{a} \times \vec{c}$ is perpendicular to $\vec{c}$

(One more item in the notes, $\vec{a} \times \vec{c} \times \vec{b}$, has no brackets, so its meaning is unclear; it is left out.)

## Triple product and area (source: page 14)

$$V = (\vec{a} \times \vec{b}) \cdot \vec{c} = (\vec{b} \times \vec{c}) \cdot \vec{a} = (\vec{c} \times \vec{a}) \cdot \vec{b}$$

$V$ is the volume of the parallelepiped (a 3D parallelogram, all opposite sides parallel) with edges $\vec{a}$, $\vec{b}$, $\vec{c}$. (added) Take the absolute value if the result is negative.

$$\text{Area of } \triangle ABC = \tfrac{1}{2}\|\vec{a}\|\,\|\vec{c}\|\sin\theta = \tfrac{1}{2}\|\vec{a} \times \vec{c}\| = \tfrac{1}{2}\|\vec{b} \times \vec{c}\| = \tfrac{1}{2}\|\vec{a} \times \vec{b}\|$$

- From area $= \frac{1}{2}\|\vec{a}\|h$ with height $h = \|\vec{c}\|\sin\theta$. The area vector $\vec{A} = \frac{1}{2}\vec{a} \times \vec{b}$ has this length and points perpendicular to the triangle.

Example (source: June 2025 final, Question 3)
$A = (1, 0, 2)$, $B = (0, 2, 2)$, $C = (2, 3, 0)$, with $\vec{a} = \overrightarrow{AB}$, $\vec{b} = \overrightarrow{AC}$, $\vec{c} = \overrightarrow{BC}$. Find $\vec{a} \times \vec{b}$, the area of the triangle, the projection vector of $\vec{b}$ in the direction of $\vec{c}$, and $\hat{e} \times (\vec{a} \times \vec{b})$ for $\hat{e} = \frac{\sqrt{5}}{15}(4\hat{x} + 2\hat{y} + 5\hat{z})$.

WORKING
$\vec{a} = (-1, 2, 0)$, $\vec{b} = (1, 3, -2)$, $\vec{c} = (2, 1, -2)$.
$\vec{a} \times \vec{b} = (2(-2) - 0,\ 0 - (-1)(-2),\ (-1)(3) - 2(1)) = (-4, -2, -5)$.
Area $= \frac{1}{2}\sqrt{16 + 4 + 25} = \frac{3\sqrt{5}}{2} = 3.354$ square units.
$\vec{b} \cdot \vec{c} = 2 + 3 + 4 = 9$ and $\vec{c} \cdot \vec{c} = 9$, so the projection vector is $(2, 1, -2)$.
$\hat{e}$ is parallel to $\vec{a} \times \vec{b}$ (a multiple of $(4, 2, 5)$), so $\hat{e} \times (\vec{a} \times \vec{b}) = \vec{0}$.

- Also from that paper (Question 1.2): $\vec{a} = \hat{y}$, $\vec{b} = \hat{z}$, $\vec{c} = \hat{y} + \hat{z}$ give $\vec{a} \cdot (\vec{b} \times \vec{c}) = \hat{y} \cdot (-\hat{x}) = 0$.

## Do not forget

- $\vec{a} \cdot \vec{b} = 0$ means perpendicular; $\vec{a} \times \vec{b} = \vec{0}$ means parallel.
- $\vec{a} \times \vec{b} = -\vec{b} \times \vec{a}$; the cross product is neither commutative nor associative.
- Torque $\vec{M} = \vec{r} \times \vec{F}$ in N m, with $\vec{r}$ measured from the pivot; only $F\sin\theta$ turns.
- Triangle area $= \frac{1}{2}\|\vec{a} \times \vec{b}\|$; parallelepiped volume $= (\vec{a} \times \vec{b}) \cdot \vec{c}$.

## See also

- [[APM01A1_Notes_S1_Vectors]]

---
*CDG v13 | written S2 | 2026-11-15*
