---
module: APM01B1
topic: Method card for the Final
tags: [exam-flagged]
---

# APM01B1 Method Card for the Final

Read this next to [[APM01B1_Summary_Final]]. The summary has the definitions, this has the steps.

## 1. Line integrals $W=\int \vec F\cdot d\vec r$
1. Parametrise with one variable. Circle: $x=R\cos\theta,\ y=R\sin\theta$. Ellipse: $x=a\cos\theta,\ y=b\sin\theta$.
2. Check that the endpoints match the path.
3. Differentiate to get $dx$ and $dy$.
4. Write $F_x\,dx$ and $F_y\,dy$ on **separate lines**, add them, then integrate.
5. If a coordinate is constant on a segment, its differential is $0$. A constant force gives $W=\vec F\cdot\Delta\vec r$. Reversing the path negates the answer.
6. Squared trig means the half-angle identity: $\sin^2,\cos^2\to\tfrac{1\mp\cos2\theta}{2}$, and $\int_0^{\pi/2}=\tfrac{\pi}{4}$ for each. Only $\sin\theta\cos\theta$ becomes $\tfrac12\sin2\theta$.

## 2. Conservative test and potential
- **Curl, main diagonal first:** $\partial_xF_y-\partial_yF_x$ (2D). In 3D there are three components, and all must be $0$.
- Conservative means zero work on **every** closed loop. Zero on one loop proves nothing.
- **Finding $\phi$ ($\vec F=\nabla\phi$):**
  1. Integrate $F_x$ in $x$ and add $g(y)$ (or $g(y,z)$ in 3D).
  2. Differentiate with respect to $y$ and match it to $F_y$.
  3. Solve for $g'$, integrate, and repeat for $z$ in 3D.
- Then $W=\phi(B)-\phi(A)$, $V=-\phi$, and $T+V=$ const.

## 3. Gradient and directional derivative
- $\nabla\psi$ is the vector of partial derivatives.
- $\dfrac{d\psi}{ds}=\nabla\psi\cdot\hat s$, with $\hat s=\dfrac{\text{direction}}{|\text{direction}|}$.
- The point goes into $\nabla\psi$. The direction gives $\hat s$.
- Example: $\psi=x^2y$ at $(1,2)$ in direction $(3,4)$ gives $(4,1)\cdot(\tfrac35,\tfrac45)=\tfrac{16}{5}$.

## 4. Equation of motion $m\ddot{\vec r}=\vec F$
- Split into components and integrate with constants. Fix the constants at $t=0$ and put the end time in last.
- **Force depends on time:** $\ddot x=\dfrac{dv}{dt}$.
- **Force depends on position:** $\ddot x=v\dfrac{dv}{dx}$, and with definite limits you need no constant.
- Pick **one** positive direction and keep gravity, drag, velocity and the limits consistent. In the ST2 question $+y$ is down, so gravity enters as $+mg$.

## 5. Impulse and energy
- Impulse: $\int\vec F\,dt=m\Delta\vec v$, per component.
- Work-energy: $W=\Delta T$, counting every force that does work. Friction on a floor uses $N=mg$. On a slope, use the distance along the slope.
- **Atwood machine:** $a=\dfrac{(m_2-m_1)g}{m_1+m_2}$, $T=\dfrac{2m_1m_2g}{m_1+m_2}$. For energy, treat both masses as one system: $(m_2-m_1)gh=\tfrac12(m_1+m_2)v^2$. The work is a difference because gravity helps one mass and fights the other. The kinetic energy is a sum because both masses move.

## 6. Intrinsic coordinates
- $\hat T=\dfrac{\vec v}{|\vec v|}$, $\hat n=\hat z\times\hat T$.
- $a_T=\vec a\cdot\hat T$ and $a_n=\vec a\cdot\hat n$. If $a_T>0$ the particle speeds up, and if $a_T<0$ it slows down.
- $\rho=\dfrac{v^2}{|a_n|}$ is the radius of the circle that best fits the path at that instant.
- Rule for any hat: take the vector and divide by its length.

## Common mistakes, in order of cost
1. Curl order reversed (5 times). Say it out loud: "main diagonal first."
2. Dropping $dy$, or using $dx$ where $dy$ is needed. Write $F_x\,dx$ and $F_y\,dy$ on separate lines.
3. Using a half-angle identity from memory without checking which one it is.
4. Mixing sign conventions for up and down.
5. Using only one mass in the Atwood energy equation.

## Exam rules
- Three questions in 120 minutes means about 3 minutes per mark.
- After every answer, do one sanity check: signs, units, and whether the size is reasonable.
- Write the formula before you substitute numbers. Marks go to the method.
