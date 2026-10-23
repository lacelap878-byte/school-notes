---
module: APM01B1
topic: Summary for the Final
tags: [exam-flagged]
---

# APM01B1 Summary for the Final

## Contents

- [[#Definitions]] terms used in this file
  - [[#Motion and frames]] polar, intrinsic, NII
  - [[#Momentum and rotation]] impulse, angular momentum, collisions
  - [[#Multivariable calculus]] gradient, curl, line integral, potential
  - [[#Work and energy terms]] work, T, V, E, escape speed
  - [[#Pulleys and beams (added)]] Atwood machine, beam moments
- [[#Material covered]] what the file draws on
  - [[#Up to semester test 1]] ST1 files
  - [[#Up to semester test 2]] ST2 files
  - [[#After the last test]] S3 and past papers
- [[#Condensed concept pass]] one entry per result
  - [[#Earlier tests]] links to the ST summaries
  - [[#Dynamics additions for the final]] cubic drag, rocket, beams
  - [[#Multivariable functions and fields]] gradient to conservative fields
  - [[#Work and energy]] work, T, V, E, escape speed
  - [[#Oscillations and orbits]] tunnel, Moon's orbit
- [[#Worked example notebook]] one example per principle
- [[#Common mistakes]] merged by pattern
  - [[#Open items]] still to fix
  - [[#Method traps]] recurring slips
  - [[#Past-paper memo slips]] errors found in memos
- [[#Decision aids]] method tables and checklists
  - [[#Which method for a force question (added)]] force type to method
  - [[#Which energy tool (added)]] work-energy or conservation
  - [[#Is the force conservative (added)]] curl then potential
  - [[#Which frame for a motion question (added)]] Cartesian, polar or intrinsic
- [[#Exam procedure]] what the papers support
- [[#Tips]] question-dissection takeaways

## Definitions

Terms this file uses, in the order they are needed. Formal statements stay in the linked notes.

### Motion and frames

- **Polar unit vectors** $\hat r,\hat\theta$: unit vectors along the line from the origin to the particle and at right angles to it. They turn as the particle moves but are tied to the origin.
- **Tangential-normal (intrinsic) frame** $\hat T,\hat n$: $\hat T$ points along the velocity, $\hat n$ is at right angles to it toward the centre of curvature. Tied to the path, not the origin. Not the same frame as $\hat r,\hat\theta$.
- **Radius of curvature** $\rho$: the radius of the circle that best fits the path at a point, $\rho=v^2/a_n$. Do not confuse it with $r$, the distance from the origin.
- **Newton's second law (NII)**: $\vec F=m\vec a$ for constant mass, and $\vec F=d\vec p/dt$ in general.
- **Path equation**: $\vec r(t)$ found by integrating NII twice, with the constants fixed by the starting conditions.
- **Galilean invariance**: NII keeps its form between frames moving at constant relative velocity only.

### Momentum and rotation

- **Momentum** $\vec p=m\vec v$. **Impulse** is the change in momentum, $\int\vec F\,dt$. Momentum is a state of motion, impulse is what changes it.
- **Angular momentum** $\vec H=\vec r\times\vec p$ and **moment** (torque) $\vec M=\vec r\times\vec F$, both about a chosen point. $d\vec H/dt=\vec M$.
- **Central force**: a force along $\hat r$ only, so it has no moment about the origin and $r^2\dot\theta$ stays constant.
- **Elastic versus inelastic collision**: momentum is conserved in both, kinetic energy only in the elastic one.
- **Turning point versus terminal velocity**: a turning point is where the speed momentarily reaches zero at a finite position (a position force). Terminal velocity is the steady speed where forces balance (drag). Drag never stops a particle at a finite position.

### Multivariable calculus

- **Partial derivative**: differentiate with respect to one variable and hold the others constant. A variable that does not appear gives zero.
- **Gradient** $\vec\nabla f$: acts on a scalar and gives a vector pointing the way $f$ rises fastest. **Divergence** $\vec\nabla\cdot\vec F$ and **curl** $\vec\nabla\times\vec F$ act on a vector field. There is no such thing as the gradient of a vector.
- **Level surface**: the set where $f$ equals a constant. The gradient is perpendicular to it.
- **Line integral** $\int_\Gamma\vec F\cdot d\vec r$: the sum of $\vec F\cdot d\vec r$ along the path $\Gamma$. The capital gamma is only the name of the path, and the subscript means the whole path.
- **Conservative field**: the work between two points does not depend on the path. Equivalent to zero circulation, zero curl (on a region with no holes) and $\vec F=\vec\nabla\phi$.
- **Scalar potential** $\phi$: the function whose gradient is $\vec F$. In the energy chapter $V=-\phi$, so $\vec F=-\vec\nabla V$.

Anatomy of a line integral:

```
  W  =  integral over path Gamma of  F . dr
        |                            |   |
        the path                     |   a small step along the path
                                     the force at that point
```

### Work and energy terms

- **Work** $W=\int\vec F\cdot d\vec r$, in joules (J).
- **Kinetic energy** $T=\tfrac12mv^2$. **Potential energy** $V$ is defined from a conservative force, $\vec F=-\vec\nabla V$. **Mechanical energy** $E=T+V$. The pages also write $K$ and $U$.
- **Work-energy theorem versus conservation of energy**: $W=\Delta T$ is true for every force. $\Delta E=0$ needs every force that does work to be conservative.
- **Power**: the rate of doing work, $\vec F\cdot\vec v$.
- **Escape speed** $\sqrt{2gR}$: the least launch speed that still reaches infinity. **Dark star radius** $2GM/c^2$ is the radius at which that speed equals the speed of light.
- **Normal force** $N$: the contact force perpendicular to a surface. The particle leaves the surface when $N$ reaches zero.

### Pulleys and beams (added)

- (added) **Atwood machine**: two masses joined by a light rope over a smooth pulley. The tension is the same on both sides and the accelerations are equal and opposite along the rope.
- (added) **Equilibrium of a beam**: the moments about the pivot sum to zero.

## Material covered

### Up to semester test 1

- [[APM01B1_Summary_ST1]], with the notes [[APM01B1_Notes_S1_PolarIntrinsicCoordinates]] and the proofs [[APM01B1_Proofs_ST1]]. Polar and intrinsic coordinates, vector differentiation, the path equation, Galilean invariance.

### Up to semester test 2

- [[APM01B1_Summary_ST2]], with the notes [[APM01B1_Notes_S2_Dynamics]] and the proofs [[APM01B1_Proofs_ST2]]. Dynamics of a particle: the four force types, momentum, impulse, rotation, collisions, central force. Practice questions are in [[APM01B1_Extra_Examples_Dynamics]].

### After the last test

- [[APM01B1_Notes_S3_MultivariableWorkEnergy]]: multivariable functions, line integrals, conservative fields, work and energy, oscillations and orbits, and the pulley, beam, spring and rough incline sections. New derivations are in [[APM01B1_Proofs_Final]], which links to the two earlier proof files.
- Past papers used: the 2025 Final memos (Papers A, B and C) and the 2023 Supplementary memo, which are this module's real exam papers.
- What the lecturer flagged for the final (from the S3 note): chapters 3 and 4 (the tools and the work) and chapters 5 and 6 together; coordinate systems; path equations; solving Newton's second law in its four cases; work-energy; impulse and momentum conservation; formulating Newton's second law in different coordinate systems; and the tunnel through the Earth. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#What the final covers]])

## Condensed concept pass

### Earlier tests

The kinematics and dynamics entries are not repeated here. Open the condensed pass in each summary:

- Kinematics (polar and intrinsic frames, vector differentiation, path equation, Galilean invariance): [[APM01B1_Summary_ST1#Condensed concept pass]]
- Dynamics (classify the force, speed and position forces, SHM, central force, momentum, collisions, impulse, rotation): [[APM01B1_Summary_ST2#Condensed concept pass]]

### Dynamics additions for the final

- **Cubic drag**: $\dot x^2=\dfrac{m\dot x_0^2}{m+2k\dot x_0^2t}$. (see: [[APM01B1_Proofs_Final#Cubic drag in time form]])
- **Momentum and mass change**: $\vec F=d\vec p/dt$, not $m\vec a$, whenever mass varies. A rocket in tangential-normal coordinates gives $\dot v=-\frac{\dot m}{m}v_e-g\cos\vartheta$ and $\dot\vartheta=\frac gv\sin\vartheta$. (see: [[APM01B1_Proofs_Final#Rocket with thrust in tangential-normal coordinates]])
- **Beams and pulleys**: moments about the pivot must cancel, and the rope tension comes from the Atwood-type equations. (see: [[APM01B1_Proofs_Final#Beam in equilibrium with a pulley]])

### Multivariable functions and fields

- **Partial derivative and gradient**: differentiate in one variable, treat the rest as constants. $\vec\nabla f$ is a vector. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Gradient of a scalar function]])
- **Operators**: gradient acts on a scalar, divergence and curl act on a vector field. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Nabla, divergence and curl]])
- **Directional derivative**: $\dfrac{df}{ds}=\vec\nabla f\cdot\dfrac{d\vec r}{ds}$. (see: [[APM01B1_Proofs_Final#Chain rule along a path]])
- **Level surfaces**: $\vec\nabla F$ is perpendicular to $F=c$. (see: [[APM01B1_Proofs_Final#Gradient is perpendicular to a level surface]])
- **Line integral in four steps**: parametrise, write $d\vec r=\frac{d\vec r}{ds}ds$, substitute, integrate. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Computing a line integral in four steps]])
- **Conservative field**: $\vec F=\vec\nabla\phi$, path independent, zero circulation, zero curl. Test with the curl, or find the potential by partial integration. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Testing for a conservative field with the curl]])
- **Finding the potential**: integrate one partial derivative, keep an unknown function of the other variables, match the others. If no consistent choice exists the field is not conservative. (see: [[APM01B1_Proofs_Final#Finding the potential, and detecting a non-conservative field]])

### Work and energy

- **Work-energy theorem**: $W=\int\vec F\cdot d\vec r=\Delta T$ for every force. (see: [[APM01B1_Proofs_Final#Work-energy theorem]])
- **Potential energy**: $V=mgy$ near the surface, $V=\frac12kx^2$ for a spring, $V=-GMm/r$ far away, always with $\vec F=-\vec\nabla V$. (see: [[APM01B1_Proofs_Final#Potential energy of a spring]])
- **Conservation**: $E=T+V$ is constant only when every force doing work is conservative. (see: [[APM01B1_Proofs_Final#Conservation of mechanical energy]])
- **Energy differentiates back to Newton's second law**: $ma=-dV/dx$. Set in every 2025 final. (see: [[APM01B1_Proofs_Final#Differentiating the energy gives Newton's second law]])
- **Escape speed**: $\sqrt{2gR}$, and the dark-star radius $2GM/c^2$. (see: [[APM01B1_Proofs_Final#Escape speed]])
- **Rough incline**: $d=\dfrac{v_0^2}{2g(\sin\theta+\mu\cos\theta)}$ up the slope. (see: [[APM01B1_Proofs_Final#Distance up a rough incline from the work-energy principle]])
- **Leaving a surface**: the normal force reaches zero. (see: [[APM01B1_Proofs_Final#Particle leaves a smooth sphere]])
- **Drag and magnetic force**: drag does nonzero work over a closed loop, a magnetic force does none. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Magnetic force does no work]])

### Oscillations and orbits

- **Tunnel through a planet**: $\ddot r=-\dfrac{g}{R}r$, so $\omega^2=g_{surf}/R_{planet}$ and the fall to the centre takes a quarter period. (see: [[APM01B1_Proofs_Final#Tunnel through a planet]])
- **Mass from an orbit**: $M=4\pi^2d^3/(GT^2)$. (see: [[APM01B1_Proofs_Final#Mass of the Earth from the Moon's orbit]])

## Worked example notebook

Each entry is one representative example per principle. Answers were checked by recomputing. Examples from the test summaries are linked there, not repeated: [[APM01B1_Summary_ST1#Worked example notebook]] and [[APM01B1_Summary_ST2#Worked example notebook]].

- **Average versus instantaneous speed** (source: 2025 Final Paper B memo, Q5). Cameras read 118 and 115 km/h at points 100 km apart (a semicircle, so the arc is $50\pi=157.08$ km) with 45 minutes between them. Average speed $157.08/0.75=209.44$ km/h, over the 120 km/h limit, so the driver must have sped up between the cameras.
- **Intrinsic quantities at a point** (source: 2025 Final Paper C memo, Q3). For $\vec r=t^2\hat x+(3t^2-4t)\hat y$ at $t=1$: $\vec v=(2,2)$, $\vec a=(2,6)$, $\hat\tau=\frac{\hat x+\hat y}{\sqrt2}$, $\hat n=\hat z\times\hat\tau=\frac{-\hat x+\hat y}{\sqrt2}$, $a_\tau=4\sqrt2$, $a_n=2\sqrt2$, $\rho=v^2/a_n=2\sqrt2$ m. (see: [[APM01B1_Proofs_ST1#Acceleration in tangential-normal coordinates]])
- **Two cars, do they collide** (source: 2025 Final Paper C memo, Q2). Split into two 1D problems. Car 1 reaches 40 m at $t=2+\frac{40-36}{6}=\frac83$ s. Car 2 reaches 22 m at $t=4+\frac{22-20}{10}=4.2$ s. The times differ, so no collision.
- **Projectile from a roof** (source: composite, from the 2025 Final Paper A question statement, 40 m roof, 20 m/s at $\pi/6$). Integrate Newton's second law, with $y(t)=40+10t-\tfrac12gt^2$ and $x(t)=10\sqrt3\,t$. Time of flight from $y=0$ is $\approx4.052$ s, range $\approx70.17$ m, impact velocity $(17.32,\,-29.75)$ m/s. Covers: the standard "integrate, find $t$, then range and speed" sequence repeated across A and B.
- **Skydiver with cubic drag** (source: 2025 Final Paper B memo, Q4). Vertical motion is free fall: after $10$ s, $\dot y=-98.1$ m/s and $y=3509.5$ m. Horizontal motion has $\ddot x=-\frac km\dot x^3$, giving $\dot x^2=\frac{m\dot x_0^2}{m+2k\dot x_0^2t}$. Kinetic energy at $10$ s is $\approx4.89\times10^5$ J. (see: [[APM01B1_Proofs_Final#Cubic drag in time form]])
- **Work along an arc** (source: 2025 Final Paper B memo, Q2). $\vec F=3xy\hat x+2\hat y$ along the ellipse arc $(0,b)\to(a,0)$ with $\vec r=(a\cos s,b\sin s)$: $W=a^2b-2b$. Curl is $-3x\hat z\neq0$, so not conservative, yet the full-ellipse work is zero. (see: [[APM01B1_Proofs_Final#Zero work around a closed loop is not enough]])
- **Line integral on a parabola** (source: Chapter 5 V5.7.1). $\vec p=(x,y^2)$ along $y=x^2$ from $(1,1)$ to $(2,4)$: $\int_1^2(s+2s^5)\,ds=22.5$. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Computing a line integral in four steps]])
- **Conservative or not** (source: Chapter 6 V6.4.1). $(y,x+z,y)$ has potential $xy+yz$. $(yz,xz,y)$ has none. (see: [[APM01B1_Proofs_Final#Finding the potential, and detecting a non-conservative field]])
- **Block up a rough incline** (source: 2025 Final Paper C memo, Q1, corrected). $v_0=10$ m/s, $\theta=\pi/4$, $\mu=\frac14$: $d=40\sqrt2/g\approx5.766$ m. (see: [[APM01B1_Proofs_Final#Distance up a rough incline from the work-energy principle]])
- **Energy differentiated** (source: 2025 Final Papers A, B and C memos, Q6). Spring: $E=\tfrac12mv^2+\tfrac12kx^2$ gives $ma=-kx$. (see: [[APM01B1_Proofs_Final#Differentiating the energy gives Newton's second law]])
- **Tunnel through Mars** (source: 2025 Final Paper A memo, Q3). $g_M=g/3$, $R_M=R/2$ give $\omega^2=\frac{2g}{3R}$ and a fall time $\frac\pi2\sqrt{\frac{3R}{2g}}\approx1550$ s. (see: [[APM01B1_Proofs_Final#Tunnel through a planet]])
- **Rocket in intrinsic coordinates** (source: 2025 Final Paper A memo, Q4). $v(\vartheta)=C\csc\vartheta\tan^{\alpha}(\vartheta/2)$ with $\alpha=kv_e/g$. (see: [[APM01B1_Proofs_Final#Rocket with thrust in tangential-normal coordinates]])
- **Beam and pulley** (source: 2025 Final Paper C memo, Q4). $\lambda=\dfrac{m_1+m_2}{4m_2}$. (see: [[APM01B1_Proofs_Final#Beam in equilibrium with a pulley]])
- **Escape and leaving a sphere** (source: lecture photos, Chapter 6 V6.5.2). $v_{esc}=\sqrt{2gR}$. From rest on a smooth sphere the particle leaves at $\cos\theta=\frac23$, about $48.19^\circ$. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Particle on a sphere]])

## Common mistakes

Earlier lists are in [[APM01B1_Summary_ST1#Common mistakes]] and [[APM01B1_Summary_ST2#Common mistakes]]. This list merges them by pattern and adds what the final material showed.

### Open items

- <span style="color:#f08c00">Open:</span> "grad cross F" does not exist. The gradient acts on a scalar. The conservative-force test is the curl, nabla crossed with the vector field. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Nabla, divergence and curl]])
- <span style="color:#f08c00">Open:</span> finding the potential is partial integration and matching, not separation of variables. Keep the unknown function of the other variable ($g(y)$) and pin it down with the other partial derivative. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Finding the scalar potential by partial integration]])
- <span style="color:#f08c00">Open:</span> sign convention. Chapter 5 writes $\vec F=\vec\nabla f$, the energy chapter writes $\vec F=-\vec\nabla V$, so $V=-f$. The minus sign is the one that gets forgotten.

### Method traps

- Zero work around one closed loop does not make a force conservative. It must be zero for every closed loop, or the curl must vanish. (see: [[APM01B1_Proofs_Final#Zero work around a closed loop is not enough]])
- Bullet embedded in a block: momentum through the impact, energy only for the climb afterwards. Using the bullet's full kinetic energy overstates the height by the factor $(m+M)/m$. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Block and bullet up a smooth slope]])
- Mechanical energy is conserved only when every force that does work is conservative. A force that does no work (normal force on a fixed smooth surface, magnetic force) does not break it. Friction and drag do.
- $\hat T,\hat n$ are not $\hat r,\hat\theta$, despite the same construction.
- Momentum form $\vec F=d\vec p/dt$ whenever mass changes. $\vec F=m\vec a$ silently assumes constant mass.
- Turning point is not terminal state: $F=-cx^n$ gives a finite stopping point, drag never stops at finite $x$.
- Unit-prefix slip: check that ns, $\mu$s and ms carry the right power of ten.

### Past-paper memo slips

- Past-paper memo slips found by recomputing: Paper C Q1 prints $28.83$ m but its own working gives $5.766$ m. Paper C Q2 prints $4.5$ s for $4+\frac{22-20}{10}$, which is $4.2$ s (the conclusion stands). Paper B Q4(b) prints $4.98\times10^5$ J, recomputing gives $\approx4.89\times10^5$ J. Paper B Q2(b) drops a sign in the curl ($-3x$, not $3x$). Paper C Q6 writes the far-gravity potential as $+GMm/r$ instead of $-GMm/r$. The handwritten 2023 supplementary answer for the braking car is hard to read and the formula gives about $22.98$ m. Trust your own working.

## Decision aids

The force-classification tree is the diagram at the end of the ST2 summary: [[APM01B1_Summary_ST2#Common mistakes]]. The aids below are new.

### Which method for a force question (added)

| The force depends on | Method |
|---|---|
| constant or time | integrate NII twice, constants from the starting conditions |
| speed or position | substitute $a=v\,dv/dx$ and separate |
| position, proportional to $-x$ | SHM ansatz, $\omega=\sqrt{k/m}$ |
| speed only, wanting $v(t)$ | separate variables in time |
| changing mass | $\vec F=d\vec p/dt$ |

### Which energy tool (added)

1. Does the question name the work-energy principle or give no time? Use $W=\Delta T$. It holds for every force.
2. Are all forces that do work conservative (gravity, spring, normal force on a fixed smooth surface)? Then $\Delta E=0$ is a shortcut.
3. Is there friction or drag? $\Delta E\neq0$. Use $W=\Delta T$ with the work of friction included.
4. Is there an impact in the middle (a bullet embedding)? Momentum through the impact, energy only before and after it.

### Is the force conservative (added)

1. Compute the curl $\vec\nabla\times\vec F$. Nonzero means not conservative.
2. If the curl is zero, confirm by finding $\phi$: integrate one component, keep an unknown function of the other variables, match the others.
3. If no consistent function exists, the field is not conservative whatever one closed loop gives.

### Which frame for a motion question (added)

- Position given in Cartesian form and the question asks for tangential or normal quantities: $\hat T=\vec v/v$, $\hat n=\hat z\times\hat T$, then project with dot products.
- Motion about a centre, a central force, or a circle: polar coordinates.

## Exam procedure

Only what the supplied papers and test pages support. No account of how your earlier tests went was given, so nothing about your own sittings is claimed here.

- The 2025 finals were 2 hours, 60 marks, six questions. Paper A had 10, 10, 10, 15, 10 and 5 marks; Paper B had 10, 15, 11, 14, 5 and 5; Paper C had 10, 7, 10, 15, 12 and 6. Check your own paper's format.
- Question 1 of every 2025 paper was intrinsic quantities at a point, so it is a safe place to start and to collect marks.
- Question 6 of every 2025 paper was the energy-differentiation question, worth 5 or 6 marks, so it is short.
- The 2026 semester test 1 cover page says no books or notes are allowed and its formula sheet carries only the polar vector formulas and the vector differentiation and integration rules. Assume the energy and line-integral results must be known.
- Memo answers contain slips (see Past-paper memo slips). Recompute the final arithmetic of your own answer before moving on.

## Tips

- Questions that recur across the three 2025 finals: intrinsic quantities at a point (every paper, Q1), integrate Newton's second law for a projectile, a tunnel through a planet, a block on a rough incline by work-energy, and "differentiate the energy to recover Newton's second law" (Q6 in every paper). Practise those first.
- Read the question for which method it names. "Use the work-energy principle" means no time variable, and the mass usually cancels.
- Always take components first (perpendicular balance gives $N=mg\cos\theta$), then the work.
- For intrinsic coordinates at a point: $\hat\tau=\vec v/v$, $\hat n=\hat z\times\hat\tau$, then project with dot products, and $\rho=v^2/a_n$.
- For a different planet in a tunnel question, swap in $\omega^2=g_{surf}/R_{planet}$ instead of rederiving the whole density argument. Show the derivation anyway if the marks ask for it.
- To test a force: curl first. If it is zero, then find the potential by partial integration to confirm.
- The dot, cross and gradient operators all come from the same $\vec\nabla$: dot a vector field for divergence, cross it for curl, apply to a scalar for gradient.
