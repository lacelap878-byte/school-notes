---
module: APM01A1
topic: Moments, Couples and Rigid Bodies
session: S4
tags: [definition, formula, theorem, worked-example, exam-flagged, common-mistake, added]
---

# APM01A1 Notes S4: Moments, Couples and Rigid Bodies

Source: your handwritten Semester One notes, pages 25 to 38 (cited by PDF page); Problem 3 is checked against its official memo, 2024 Final Exam B Question 5 (`Tests\Exam B Memo.pdf`); one example from the June 2025 final, Question 1.5. Short revision notes, not from a teaching session.

Checked: every moment, tension and reaction below was checked in Python (SymPy) on 15 Nov 2026; Problem 3 matches the memo.

## Rigid bodies and moment of force (source: pages 25 to 27)

> **Torque (moment of force):** the ability of a force to rotate an object.

- Rotation needs an extended body (not a point); in first year it is rigid (solid, cannot be deformed): for any two points $i$, $j$ of the body, $\|\vec{P}_{ij}\|$ stays constant. A rigid body can feel forces at many points.
- A free body reacts in two ways: translation and rotation. With a pivot (a pendulum), the body keeps a fixed distance from the pivot, which serves as the origin.
- Motion about the $z$-axis means a fixed axis: the rotation is along $+\hat{z}$ (out of the page) or $-\hat{z}$ (into the page), by the right-hand rule. Forces and positions in the $x$-$y$ plane are taken into $z$ by the cross product.

$$\vec{M} = \vec{r} \times \vec{F} \qquad \vec{M}_{net} = \sum_i \vec{r}_i \times \vec{F}_i = \vec{0} \text{ for equilibrium}$$

$\vec{M}$ is the moment of force (torque) in N m and $\vec{r}_i$ the position of the point where $\vec{F}_i$ acts, measured from the pivot. In 2D the moment equations reduce to one equation, in the $z$ direction.

Example (source: pages 27 to 28)
A horizontal beam, pivoted on a wall, carries a 5000 kg mass at its end, 10 m from the wall. A cable from the end of the beam to the wall makes angle $\theta$ with the beam. Find the tension. (The notes use $g = 10$ m/s$^2$.)

WORKING
$\vec{r} = 10\hat{x}$ m, $\vec{T} = T(-\cos\theta\,\hat{x} + \sin\theta\,\hat{y})$, $\vec{W} = -mg\,\hat{y}$.
$\vec{M}_{net} = 10\hat{x} \times \vec{T} + 10\hat{x} \times \vec{W} = 10T\sin\theta\,\hat{z} - 5 \times 10^5\,\hat{z}$.
$M_z = 0$ gives $T = \dfrac{5 \times 10^4}{\sin\theta}$ N. The tension grows rapidly as $\theta \to 0$ (at $30^\circ$ it is already 100 kN).

## Lines of action and couples (source: pages 28 to 29)

- A force may be slid along its line of action without changing its effect on a rigid body. Two coplanar, non-parallel forces can be slid until they meet, and replaced there by their sum.
- Parallel forces have lines of action that never meet. If $\vec{F_2} = -\vec{F_1}$ acts at a different point, then $\vec{F}_{net} = \vec{0}$ but $\vec{M}_{net} \ne \vec{0}$: pure rotation.

> **Couple:** a pair of forces $\vec{F_1}$ and $\vec{F_2} = -\vec{F_1}$ acting at different points. Couples act only in rotation.

- If $\vec{F_1} + \vec{F_2} + \vec{F_3} + \vec{F_4} = \vec{0}$ with $\vec{F_1} = -\vec{F_3}$ and $\vec{F_2} = -\vec{F_4}$, then $(\vec{F_1}, \vec{F_3})$ and $(\vec{F_2}, \vec{F_4})$ are two couples.

$$\vec{M}_{couple} = \vec{r} \times \vec{F} + (-\vec{r}) \times (-\vec{F}) = 2\,\vec{r} \times \vec{F} \qquad \|\vec{M}_{couple}\| = dF$$

$d$ is the perpendicular distance between the two lines of action ($d = 2r\sin\theta$ when the forces act at $\pm\vec{r}$).

Example (source: June 2025 final, Question 1.5): $\vec{F_1} = -\hat{x} + 2\hat{y}$ acts at $(-1, 2)$ and $\vec{F_2} = 3\hat{x} - \hat{y}$ at $(6, -2)$. Where do their lines of action meet?
   $(-1, 2) + s(-1, 2) = (6, -2) + t(3, -1)$ gives $s = -1$, $t = -2$: they meet at $(0, 0)$.

## The moment does not depend on the reference point (source: page 30)

Shift every position by $\vec{a}$: $\vec{r}_i\,' = \vec{r}_i - \vec{a}$. Then

$$\vec{M}\,'_{net} = \sum_i (\vec{r}_i - \vec{a}) \times \vec{F}_i = \vec{M}_{net} - \vec{a} \times \sum_i \vec{F}_i$$

For a body in equilibrium $\sum \vec{F}_i = \vec{0}$, so $\vec{M}\,'_{net} = \vec{M}_{net}$: take moments about whichever point is easiest. The best choice is usually where an unknown reaction acts, since its moment there is zero.

## Reduction theorem (source: page 32)

- The aim is to separate the motion into translation ($\sum \vec{F}_i$) and rotation (couples).
- Move a force $\vec{F_2}$ to the reference point by adding $\vec{F_2}$ and $-\vec{F_2}$ there (they cancel). The original $\vec{F_2}$ and the added $-\vec{F_2}$ form a couple; the remaining $\vec{F_2}$ acts at the reference point.
- Doing this for every force leaves the total force at the reference point plus the sum of all the couples, so $\sum \vec{r}_i \times \vec{F}_i$ becomes the sum of the couple moments.

## Forces acting at one point (source: pages 31 to 32)

- If several forces act at the same point $\vec{r}$, their total moment is $\vec{r} \times \sum \vec{F}_i$, so for equilibrium it is enough that $\sum \vec{F}_i = \vec{0}$ at that point.

Example (source: pages 31 to 32): a vertical rod $OP$, 5 m, stands on the floor at $O$ and weighs 10 kN; cables $PA$ and $PB$ and an applied force $\vec{F}_{PC}$ of 8 kN act at its top $P = (0, 0, 5)$, with $A = (1, 1, 5)$ and $B = (1, -1, 5)$.
   The weight is balanced by the floor: $\vec{W} = -\vec{N}$. At $P$: $\vec{F}_{PC} + \vec{T}_{PA} + \vec{T}_{PB} = \vec{0}$, with $\vec{T}_{PA} = \dfrac{T_{PA}}{\sqrt{2}}(\hat{x} + \hat{y})$ and $\vec{T}_{PB} = \dfrac{T_{PB}}{\sqrt{2}}(\hat{x} - \hat{y})$. The notes do not give the direction of $\vec{F}_{PC}$, so the example stops at this set-up.

## NB Problem 2: a pole held by two cables (source: pages 33 to 35)

A vertical pole stands at $P = (0, 5, 0)$, 10 m tall. A force $\vec{F} = -F\hat{y}$ acts at its top; cables run from $Q = (0, 5, Q_z)$ on the pole to $A = (A_x, A_y, 0)$ and $B = (B_x, B_y, 0)$ on the ground.

$$\vec{T}_{QA} = T_{QA}\,\frac{A_x\hat{x} + (A_y - 5)\hat{y} - Q_z\hat{z}}{\|\overrightarrow{QA}\|} \qquad \vec{T}_{QB} = T_{QB}\,\frac{B_x\hat{x} + (B_y - 5)\hat{y} - Q_z\hat{z}}{\|\overrightarrow{QB}\|}$$

Moments about the base $P$ (positions $10\hat{z}$ for $\vec{F}$ and $Q_z\hat{z}$ for the cables; the reaction $\vec{R}$ at $P$ has no moment there):

$$x: \ 10F - \frac{Q_z(A_y - 5)\,T_{QA}}{\|\overrightarrow{QA}\|} - \frac{Q_z(B_y - 5)\,T_{QB}}{\|\overrightarrow{QB}\|} = 0 \qquad y: \ \frac{A_x\,T_{QA}}{\|\overrightarrow{QA}\|} + \frac{B_x\,T_{QB}}{\|\overrightarrow{QB}\|} = 0$$

The $y$-equation gives $T_{QA} = -T_{QB}\,\dfrac{B_x\|\overrightarrow{QA}\|}{A_x\|\overrightarrow{QB}\|}$; the $x$-equation then gives both tensions. Finally, force balance gives the reaction: $-F\hat{y} + \vec{T}_{QA} + \vec{T}_{QB} + \vec{R} = \vec{0}$.

> [!warning] Include the reaction, or take moments where it acts (added)
> The notes take moments about the origin $O$ but leave out the reaction $\vec{R}$ at the base, whose moment $5\hat{y} \times \vec{R}$ is not zero. That puts extra terms in the $x$-equation. Taking moments about the base removes $\vec{R}$ and gives the equations above (checked: identical to moments about $O$ with $\vec{R}$ included). The notes also write $+Q_z\hat{z}$ in $\vec{T}_{QB}$; both cables point down, so it is $-Q_z\hat{z}$.

## NB Problem 3: a beam on a ball-and-socket joint (source: pages 36 to 37, memo: 2024 Exam B Q5)

> A massless beam $AD$ is supported by a ball-and-socket joint at $A$ and two cables, $ECD$ and $BD$. Cable $ECD$ moves over a frictionless pulley at point $C$. The weight of the object suspended at $D$ is 30 N. Let $a = 1$ m.

Coordinates: $A$ at the origin, $E = (0, a, 0)$, $D = (0, 2a, 0)$, $B = (a, 0, 2a)$, $C = (-a, 0, a)$.

WORKING (as in the memo)
(a) Tension vectors, each magnitude times the unit vector from the beam to the anchor:

$$\vec{T}_{DB} = \frac{T_{DB}}{3}(\hat{x} - 2\hat{y} + 2\hat{z}) \qquad \vec{T}_{DC} = \frac{T_{DC}}{\sqrt{6}}(-\hat{x} - 2\hat{y} + \hat{z}) \qquad \vec{T}_{EC} = \frac{T_{EC}}{\sqrt{3}}(-\hat{x} - \hat{y} + \hat{z})$$

(b) Moments about $A$: $\vec{M}_A = 2\hat{y} \times \vec{T}_{DB} + 2\hat{y} \times \vec{T}_{DC} + \hat{y} \times \vec{T}_{EC} + 2\hat{y} \times (-30\hat{z}) = \vec{0}$. Since $\hat{y} \times \vec{V} = V_z\hat{x} - V_x\hat{z}$, only the $x$ and $z$ parts give equations:

$$x: \ \tfrac{4}{3}T_{DB} + \tfrac{\sqrt{6}}{3}T_{DC} + \tfrac{\sqrt{3}}{3}T_{EC} - 60 = 0 \qquad z: \ -\tfrac{2}{3}T_{DB} + \tfrac{\sqrt{6}}{3}T_{DC} + \tfrac{\sqrt{3}}{3}T_{EC} = 0$$

(c) Subtracting: $2T_{DB} = 60$, so $T_{DB} = 30$ N, and $T_{EC} = 20\sqrt{3} - \sqrt{2}\,T_{DC}$. One tension is undetermined.
(d) Force balance $\vec{A} + \vec{T}_{DC} + \vec{T}_{DB} + \vec{T}_{EC} + \vec{W} = \vec{0}$ gives the reaction at $A$:

$$A_x = 10 - \frac{T_{DC}}{\sqrt{6}} \qquad A_y = 40 \qquad A_z = -10 + \frac{T_{DC}}{\sqrt{6}} \quad \text{(N)}$$

(e) $(T_{DC})_{max} = 20\sqrt{\tfrac{3}{2}} = 10\sqrt{6} \approx 24.49$ N: above this, $T_{EC}$ becomes negative, which is not possible.

> [!warning] Where the notes went wrong (added)
> All forces act at points on the $y$-axis, so $\vec{M}_A$ has no $y$-part: there are only two moment equations. The notes also set the $y$-part of $\vec{T}_{DB} + \frac{1}{2}\vec{T}_{EC} + \vec{T}_{DC} + \vec{W}$ to zero; that third equation is not a real condition and gives $T_{DC} = -30\sqrt{6}$ N, a negative tension. Any $y$-force is taken by the reaction at $A$.

- (added) Since $ECD$ runs over a frictionless pulley, one could also set $T_{EC} = T_{DC}$, which gives 14.35 N each. The memo does not do this, so follow the memo in an exam.

## Exam layout, June 2026 (source: page 38)

8 June, 16h30 to 18h30, E-Les 200; 65 marks, 5 questions: (1) MCQ, 10 marks; (2) vector proof, 10 to 15; (3) maths application, 10 to 15; (4) force balance in 2D, 10 to 15; (5) force and moment of force balance in 3D, 15. The June 2025 final had the same shape (see the Past Papers folder).

## Do not forget

- Equilibrium of a rigid body needs $\vec{F}_{net} = \vec{0}$ and $\vec{M}_{net} = \vec{0}$.
- Take moments about the point where the unknown reaction acts; its moment there is zero.
- A couple has $\vec{F}_{net} = \vec{0}$ but a moment $dF$: pure rotation.
- If every force acts on one line, the moment about a point on that line has no component along it: count the real equations before solving.

## See also

- [[APM01A1_Notes_S2_Vector_Products]]
- [[APM01A1_Notes_S3_Forces_and_Static_Equilibrium]]

---
*CDG v13 | written S4 | 2026-11-15*
