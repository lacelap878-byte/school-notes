---
module: APM01B1
topic: Summary for the Final
tags: [exam-flagged]
---

# APM01B1 Summary for the Final

## Material covered

All three sessions, in full detail in their own notes:

- [[APM01B1_Notes_S1_PolarIntrinsicCoordinates]] (kinematics: polar and intrinsic coordinates, vector differentiation, Newton's second law and the path equation)
- [[APM01B1_Notes_S2_Dynamics]] (dynamics of a particle: the four force types, momentum, impulse, rotation)
- [[APM01B1_Notes_S3_MultivariableWorkEnergy]] (multivariable functions, line integrals, conservative fields, work and energy, oscillations and orbits)

Every derivation worth memorising is collected in [[APM01B1_Proofs_Final]]. Past-paper examples come from [[APM01B1_Extra_Examples_Dynamics]] and from the 2025 Final memos (Papers A, B and C) and the 2023 Supplementary memo, which are the same module's real exam papers.

What the lecturer flagged for the final (from the S3 note): chapters 3 and 4 (the tools and the work) and chapters 5 and 6 together; coordinate systems (Cartesian, polar, tangential-normal); path equations; solving Newton's second law in its four cases; work-energy; impulse and momentum conservation; formulating Newton's second law in different coordinate systems; and the tunnel through the Earth. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#What the final covers]])

Format of the 2025 finals, for reference only (check yours): 2 hours, 60 marks, six questions. Paper A had 10, 10, 10, 15, 10 and 5 marks; Paper B had 10, 15, 11, 14, 5 and 5; Paper C had 10, 7, 10, 15, 12 and 6. The 2026 semester test 1 cover page says no books or notes are allowed and its formula sheet carries only the polar vector formulas and the vector differentiation and integration rules, so assume the energy and line-integral results must be known.

## Condensed concept pass

### Kinematics

- **Average versus instantaneous**: $\vec v_{ave}$ needs only endpoint positions, $\vec v_{mean}$ needs the instantaneous velocities, and they are generally unequal. A car with sub-limit speed readings at both ends can still have an average speed far over the limit. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Average vs instantaneous velocity]])
- **Polar frame**: $\hat r,\hat\theta$ move with the particle but are tied to the origin. Everything follows from $d\hat r/dt=\dot\theta\hat\theta$ and $d\hat\theta/dt=-\dot\theta\hat r$. (see: [[APM01B1_Proofs_Final#Velocity and acceleration in polar coordinates]])
- **Intrinsic frame**: $\hat T=\vec v/v$ is origin-independent, $\hat n=\hat z\times\hat T$, $\vec a=\dot v\hat T+\dfrac{v^2}{\rho}\hat n$, and $\rho=v^2/(\vec a\cdot\hat n)$. Not the same frame as $\hat r,\hat\theta$. (see: [[APM01B1_Proofs_Final#Acceleration in tangential-normal coordinates]])
- **Path equation**: integrate Newton's second law twice. Two edge cases are told apart by which conditions are given. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Two edge cases for solving $m\ddot{\vec r}=\vec F$]])
- **Galilean invariance**: $\vec F=m\vec a$ keeps its form only between frames of constant relative velocity. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Galilean invariance]])

### Dynamics

- **Classify the force first**: constant or $\vec F(t)$ means direct integration; $\vec F(v)$ or $\vec F(x)$ means $a=v\,dv/dx$ and separate; $\vec F(r)\propto-r$ means the SHM ansatz; changing mass means the momentum form. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#The four force cases]])
- **Position and speed together**: if $F_x=f_1(v_x)g_1(x)$, then $m\int\dfrac{v_x}{f_1}dv_x=\int g_1\,dx$. Pure position forces have a finite turning point, drag does not. (see: [[APM01B1_Proofs_Final#Separable force of position and speed]])
- **Terminal velocity**: set $\ddot z=0$ in the force balance, never solve the full equation. (see: [[APM01B1_Proofs_Final#Terminal velocity from the force balance]])
- **Linear drag**: $\dot z=-kz+C$ always gives an $e^{-kt}$ solution. (see: [[APM01B1_Proofs_Final#Exponential solution of the linear drag equation]])
- **Cubic drag**: $\dot x^2=\dfrac{m\dot x_0^2}{m+2k\dot x_0^2t}$. (see: [[APM01B1_Proofs_Final#Cubic drag in time form]])
- **Springs and SHM**: $\omega=\sqrt{k/m}$ from the ansatz $A\cos\omega t+B\sin\omega t$. (see: [[APM01B1_Proofs_Final#The simple harmonic motion ansatz]])
- **Central force**: zero $\hat\theta$ force gives $r^2\dot\theta=h$, and then the energy equation. (see: [[APM01B1_Proofs_Final#Conservation of angular momentum for a central force]])
- **Momentum and mass change**: $\vec F=d\vec p/dt$, not $m\vec a$, whenever mass varies. A rocket in tangential-normal coordinates gives $\dot v=-\frac{\dot m}{m}v_e-g\cos\vartheta$ and $\dot\vartheta=\frac gv\sin\vartheta$. (see: [[APM01B1_Proofs_Final#Rocket with thrust in tangential-normal coordinates]])
- **Collisions**: momentum is always conserved; kinetic energy is conserved only if elastic. (see: [[APM01B1_Proofs_Final#Elastic collision formulas]])
- **Impulse and rotation**: $\Delta\vec p=\int\vec F\,dt$, $d\vec H/dt=\vec M$, $\vec J_O=\Delta\vec H_O$. (see: [[APM01B1_Proofs_Final#Angular momentum theorem]])
- **Pendulum**: tension has no moment about the pivot, so $\ddot\theta=-\frac gl\sin\theta$. (see: [[APM01B1_Proofs_Final#Simple pendulum]])
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

Each entry is one representative example per principle. Answers were checked by recomputing.

- **Average versus instantaneous speed** (source: 2025 Final Paper B memo, Q5). Cameras read 118 and 115 km/h at points 100 km apart (a semicircle, so the arc is $50\pi=157.08$ km) with 45 minutes between them. Average speed $157.08/0.75=209.44$ km/h, over the 120 km/h limit, so the driver must have sped up between the cameras.
- **Intrinsic quantities at a point** (source: 2025 Final Paper C memo, Q3). For $\vec r=t^2\hat x+(3t^2-4t)\hat y$ at $t=1$: $\vec v=(2,2)$, $\vec a=(2,6)$, $\hat\tau=\frac{\hat x+\hat y}{\sqrt2}$, $\hat n=\hat z\times\hat\tau=\frac{-\hat x+\hat y}{\sqrt2}$, $a_\tau=4\sqrt2$, $a_n=2\sqrt2$, $\rho=v^2/a_n=2\sqrt2$ m. (see: [[APM01B1_Proofs_Final#Acceleration in tangential-normal coordinates]])
- **Two cars, do they collide** (source: 2025 Final Paper C memo, Q2). Split into two 1D problems. Car 1 reaches 40 m at $t=2+\frac{40-36}{6}=\frac83$ s. Car 2 reaches 22 m at $t=4+\frac{22-20}{10}=4.2$ s. The times differ, so no collision.
- **Projectile from a roof** (source: composite, from the 2025 Final Paper A question statement, 40 m roof, 20 m/s at $\pi/6$). Integrate Newton's second law, with $y(t)=40+10t-\tfrac12gt^2$ and $x(t)=10\sqrt3\,t$. Time of flight from $y=0$ is $\approx4.052$ s, range $\approx70.17$ m, impact velocity $(17.32,\,-29.75)$ m/s. Covers: the standard "integrate, find $t$, then range and speed" sequence repeated across A and B.
- **Past-paper template, mixed forces** (source: 2012 ST2). Position force by the chain rule, velocity force by separation. (see: [[APM01B1_Extra_Examples_Dynamics#Worked Example 1: 2012 ST2, projectile with $F_f=(-x^2,-v_y)$]])
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
- **Spring pendulum, central force and magnetic field in polar form** (source: S2 note). (see: [[APM01B1_Notes_S2_Dynamics#Worked example: spring pendulum (gravity plus a spring, in polar coordinates)]])
- **Elastic and inelastic collisions** (source: Tutorial 9, via S2). $v_1=\frac{m_1-m_2}{m_1+m_2}u$ and $v_2=\frac{2m_1}{m_1+m_2}u$. (see: [[APM01B1_Proofs_Final#Elastic collision formulas]])

## Common mistakes

- <span style="color:#f08c00">Open:</span> "grad cross F" does not exist. The gradient acts on a scalar. The conservative-force test is the curl, nabla crossed with the vector field. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Nabla, divergence and curl]])
- <span style="color:#f08c00">Open:</span> finding the potential is partial integration and matching, not separation of variables. Keep the unknown function of the other variable ($g(y)$) and pin it down with the other partial derivative. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Finding the scalar potential by partial integration]])
- <span style="color:#f08c00">Open:</span> sign convention. Chapter 5 writes $\vec F=\vec\nabla f$, the energy chapter writes $\vec F=-\vec\nabla V$, so $V=-f$. The minus sign is the one that gets forgotten.
- Zero work around one closed loop does not make a force conservative. It must be zero for every closed loop, or the curl must vanish. (see: [[APM01B1_Proofs_Final#Zero work around a closed loop is not enough]])
- Bullet embedded in a block: momentum through the impact, energy only for the climb afterwards. Using the bullet's full kinetic energy overstates the height by the factor $(m+M)/m$. (see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Block and bullet up a smooth slope]])
- Mechanical energy is conserved only when every force that does work is conservative. A force that does no work (normal force on a fixed smooth surface, magnetic force) does not break it. Friction and drag do.
- $\hat T,\hat n$ are not $\hat r,\hat\theta$, despite the same construction.
- Momentum form $\vec F=d\vec p/dt$ whenever mass changes. $\vec F=m\vec a$ silently assumes constant mass.
- Turning point is not terminal state: $F=-cx^n$ gives a finite stopping point, drag never stops at finite $x$.
- Unit-prefix slip: check that ns, $\mu$s and ms carry the right power of ten.
- Past-paper memo slips found by recomputing: Paper C Q1 prints $28.83$ m but its own working gives $5.766$ m. Paper C Q2 prints $4.5$ s for $4+\frac{22-20}{10}$, which is $4.2$ s (the conclusion stands). Paper B Q4(b) prints $4.98\times10^5$ J, recomputing gives $\approx4.89\times10^5$ J. Paper B Q2(b) drops a sign in the curl ($-3x$, not $3x$). Paper C Q6 writes the far-gravity potential as $+GMm/r$ instead of $-GMm/r$. The handwritten 2023 supplementary answer for the braking car is hard to read and the formula gives about $22.98$ m. Trust your own working.

## Tips

- Questions that recur across the three 2025 finals: intrinsic quantities at a point (every paper, Q1), integrate Newton's second law for a projectile, a tunnel through a planet, a block on a rough incline by work-energy, and "differentiate the energy to recover Newton's second law" (Q6 in every paper). Practise those first.
- Read the question for which method it names. "Use the work-energy principle" means no time variable, and the mass usually cancels.
- Always take components first (perpendicular balance gives $N=mg\cos\theta$), then the work.
- For intrinsic coordinates at a point: $\hat\tau=\vec v/v$, $\hat n=\hat z\times\hat\tau$, then project with dot products, and $\rho=v^2/a_n$.
- For a different planet in a tunnel question, swap in $\omega^2=g_{surf}/R_{planet}$ instead of rederiving the whole density argument. Show the derivation anyway if the marks ask for it.
- To test a force: curl first. If it is zero, then find the potential by partial integration to confirm.
- Pulleys, beams (moments about a pivot), the spring potential and the rough incline were added to your S3 note from the course notes, tutorials and 2025 papers: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Pulleys and the Atwood machine]], [[APM01B1_Notes_S3_MultivariableWorkEnergy#Beam in equilibrium with a pulley]], [[APM01B1_Notes_S3_MultivariableWorkEnergy#Potential energy of a spring]], [[APM01B1_Notes_S3_MultivariableWorkEnergy#Distance up a rough incline by work-energy]]. The derivations are in [[APM01B1_Proofs_Final#Beam in equilibrium with a pulley]].
- The dot, cross and gradient operators all come from the same $\vec\nabla$: dot a vector field for divergence, cross it for curl, apply to a scalar for gradient.
