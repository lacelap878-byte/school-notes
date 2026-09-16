---
module: APM01B1
topic: Summary for ST2
tags: [exam-flagged]
---

# APM01B1 — Summary for ST2

## Material covered

Personal notebook photos, 34 pages, badly non-chronological (the incline example starts on page 34 and finishes on page 1; the separable-ODE warm-up starts on page 2 and finishes on page 25; the angular-momentum theorem used from page 9 onward isn't itself derived until page 30). Dynamics and Multivariable Functions content is interleaved page-to-page in the source; only the dynamics threads are covered here. Cross-checked against `Notes_-_Chapter_4.pdf` (the official course notes for Chapter 4) and Tutorials 6-9. Full detail in [[APM01B1_Notes_S2_Dynamics]].

The notebook itself (page 24) records: **Semester Test 2, 3 October, content: all of Chapter 4** — i.e. exactly this session's scope.

## Condensed concept pass

- **Roadmap**: classify the force first, const/$F(t)$ integrate directly, $F(v)$ use $v\,dv/dr$, $F(r)$ ansatz/guess. Not every case is solvable in closed form. (see: [[APM01B1_Notes_S2_Dynamics]], top)
- **Time-dependent force**: on a constrained surface (e.g. an incline), isolate the component the constraint force does *not* cancel before integrating twice. (see: [[APM01B1_Notes_S2_Dynamics#Time-dependent force: an incline worked example]])
- **Terminal velocity**: set $\ddot z=0$ directly in the force balance, never solve the full ODE for it. (see: [[APM01B1_Notes_S2_Dynamics#Setup and terminal velocity]])
- **Speed-dependent force**: two techniques, separation of variables for $v(t)$ when the equation allows it, and the $v\,dv/dz$ chain-rule trick for $v(z)$ when it doesn't. (see: [[APM01B1_Proofs_ST2#$v\,dv/dz$ reduction for a speed-dependent force]])
- **Position-dependent force (springs)**: guess-and-verify (ansatz) $A\cos\omega t+B\sin\omega t$, only solves the equation for the specific $\omega=\sqrt{k/m}$. (see: [[APM01B1_Proofs_ST2#SHM ansatz, $\omega=\sqrt{k/m}$]])
- **$F(r)\propto -r$ is always SHM**: a spring and gravity inside a uniform sphere (tunnel-through-earth) are the same equation with a different constant. (see: [[APM01B1_Notes_S2_Dynamics#(added) Worked example: a tunnel through the earth]])
- **Central (inverse-square) force**: zero torque in $\hat\theta$ gives $r^2\dot\theta=h=$ const; substituting $h$ into the radial equation and using $v\,dv/dr$ again gives the energy equation. (see: [[APM01B1_Proofs_ST2#Conservation of angular momentum for a central force, $r^2\dot\theta=h$]], [[APM01B1_Proofs_ST2#Energy conservation for the inverse-square (gravitational) central force]])
- **Momentum**: general form $\vec F=d\vec p/dt$, required (not $\vec F=m\vec a$) whenever mass is not constant. Total momentum of a two-particle system is conserved whenever they interact only with each other. (see: [[APM01B1_Notes_S2_Dynamics#Momentum]])
- **Collisions**: momentum conservation holds for every collision; kinetic-energy conservation is the *extra* assumption that makes it elastic, never automatic. (see: [[APM01B1_Proofs_ST2#(added) Elastic collision formulas]])
- **Impulse**: $\Delta\vec p=\int\vec F\,dt$, for short-lasting, transient, non-repetitive forces. (see: [[APM01B1_Proofs_ST2#Impulse, $\Delta\vec p=\int\vec F\,dt$]])
- **Rotational motion**: $\vec H=\vec r\times\vec p$, $d\vec H/dt=\vec r\times\vec F=\vec M$ is a reformulation of N2, not new physics. Choosing the reference point to kill an unknown force's moment (e.g. pendulum tension) is the main reason to use it. (see: [[APM01B1_Proofs_ST2#Angular momentum theorem, $d\vec H/dt=\vec M$]])
- **Angular impulse**: $\vec J_O=\Delta\vec H_O$, directly analogous to linear impulse. (see: [[APM01B1_Notes_S2_Dynamics#Angular impulse]])

## Worked example notebook

- **Incline, time-dependent force**: $F_0e^{-t}$, only the along-slope component survives once the normal force is accounted for. (see: [[APM01B1_Proofs_ST2#General solution for a time-dependent force]])
- **Falling with linear drag**: separable-variables solve $\dot z=-kz+C\Rightarrow z(t)=\frac Ck-\frac Kk e^{-kt}$, and the displacement-based $v\,dv/dz$ solve of the full equation with gravity. (see: [[APM01B1_Notes_S2_Dynamics#Speed-dependent force: friction and terminal velocity]])
- **Spring, SHM ansatz**: $\ddot\xi=-\frac km\xi\Rightarrow\omega=\sqrt{k/m}$; equivalent complex-exponential form given as an alternative route. (see: [[APM01B1_Notes_S2_Dynamics#The ansatz method]])
- **Two masses coupled by a spring**: centre of mass moves freely ($\ddot x_c=0$), relative coordinate obeys SHM with reduced mass $\mu=m_1m_2/(m_1+m_2)$. (see: [[APM01B1_Proofs_ST2#(added) Coupled two-mass spring system, reduced mass]])
- **Tunnel through the earth**: $F(r)=-\frac{GMm}{R^3}r$ (shell theorem), SHM with $\omega=\sqrt{g/R}$; time to centre $\frac\pi2\sqrt{R/g}$, speed at centre $\sqrt{gR}$. (see: [[APM01B1_Notes_S2_Dynamics#(added) Worked example: a tunnel through the earth]])
- **Spring pendulum**: gravity plus spring, resolved into $\hat r,\hat\theta$, needs $\hat y$ rewritten in the moving basis first. (see: [[APM01B1_Notes_S2_Dynamics#Worked example: spring pendulum (gravity plus a spring, in polar coordinates)]])
- **Central (gravitational) force**: $r^2\dot\theta=h$, then energy equation $\left(\frac12mv^2+\frac{h^2m}{2r^2}\right)-\frac{GMm}{r}=E$. (see: [[APM01B1_Proofs_ST2#Energy conservation for the inverse-square (gravitational) central force]])
- **Charged particle in a magnetic field (cyclotron motion)**: $\vec F=q(\vec v\times\vec B)$ in polar coordinates, cross-checked via the angular-momentum route and the direct $\vec F=m\vec a$ route. (see: [[APM01B1_Notes_S2_Dynamics#Further examples in polar coordinates: circular motion in a magnetic field]])
- **Rocket, exponentially decaying mass**: $m(t)=m_0e^{-\lambda t}$ under gravity alone, $v(t)=\frac g\lambda+(v_0-\frac g\lambda)e^{\lambda t}$, solved two ways (differentiate the product; integrate directly) as a consistency check. (see: [[APM01B1_Proofs_ST2#Variable-mass (rocket) equation of motion]])
- **Elastic and inelastic collisions**: $v_1=\frac{m_1-m_2}{m_1+m_2}u$, $v_2=\frac{2m_1}{m_1+m_2}u$ (elastic); $v_f=\frac{m_1}{m_1+m_2}u$ with $\Delta KE<0$ (inelastic). (see: [[APM01B1_Proofs_ST2#(added) Elastic collision formulas]])
- **Rebound impulse**: $\Delta\vec p=-4\vec p_0$ over $4\,\text{ns}$ gives $F\sim10^9\,\text{N}$, why impulsive forces are treated as short transient events rather than integrated over an unknown time profile. (see: [[APM01B1_Notes_S2_Dynamics#Worked example: rebound (particle accelerator)]])
- **Simple pendulum**: $\ddot\theta=-\frac gl\sin\theta$, small-angle SHM, $T=2\pi\sqrt{l/g}$. (see: [[APM01B1_Proofs_ST2#(added) Simple pendulum, $\ddot\theta=-\frac gl\sin\theta$]])

## Common mistakes

- **Unit-prefix slip**: an impulse example computed "$3\,\text{ns}$" as $3\times10^{-6}$ (microseconds) instead of $3\times10^{-9}$, a three-order-of-magnitude error. The method (impulse = force × time, for constant force) was correct; only the prefix conversion was wrong. Always check the power of ten actually matches the prefix written (n, $\mu$, m). (see: [[APM01B1_Notes_S2_Dynamics#Worked example: force applied briefly]])
- **Momentum vs energy conservation in collisions**: momentum conservation is unconditional (it only needs $\vec F_{12}=-\vec F_{21}$), kinetic-energy conservation is not, it is the specific extra assumption that defines an *elastic* collision. Do not assume KE is conserved by default.
- **Classification ambiguity, not an error**: the central-force and Lorentz-force examples use the same polar-coordinates $\vec F=m\vec a$ machinery the official Chapter 4 "Further Applications of N2" section uses, but that section's actual worked examples are pulleys/rotating platforms/beams, not central or magnetic forces. Don't expect a central-force question to be labelled "§4.4" on a paper, it may appear anywhere position-dependent or polar-coordinate technique is being tested.
- **Momentum form vs $\vec F=m\vec a$**: whenever mass changes with time (e.g. the rocket example), $\vec F=d\vec p/dt$ must be used from the start, $\vec F=m\vec a$ silently assumes constant mass and gives the wrong equation if applied directly.

```tikz
\begin{document}
\begin{tikzpicture}[scale=1]
  \node at (0,2.3) {\textbf{Classify the force, pick the method}};
  \node[draw, rounded corners, align=center] (f) at (0,1.2) {$\vec F$ depends on...};
  \node[draw, align=center] (a) at (-4.5,0) {const or $t$\\direct integration};
  \node[draw, align=center] (b) at (-1.5,0) {$v$\\$v\,dv/dr$ trick};
  \node[draw, align=center] (c) at (1.5,0) {$r$\\ansatz/guess};
  \node[draw, align=center] (d) at (4.5,0) {mass itself\\$\vec F=d\vec p/dt$};
  \draw[->] (f) -- (a);
  \draw[->] (f) -- (b);
  \draw[->] (f) -- (c);
  \draw[->] (f) -- (d);
\end{tikzpicture}
\end{document}
```

## Tips

- Before reaching for $\vec F=m\vec a$ in polar coordinates, check whether the force is genuinely central (points along $\hat r$ only), if so the $\hat\theta$ equation is zero-torque and gives $r^2\dot\theta=h$ for free, a large shortcut.
- Whenever a force depends on velocity or position, the standard first move is the chain-rule substitution $a=v\,dv/dr$, converting a time-derivative equation into one separable in $v$ and $r$ (or $v$ and $z$).
- If a guessed ansatz (e.g. $A\cos\omega t+B\sin\omega t$) doesn't obviously verify, don't force it, check whether the equation is really linear and homogeneous in the way SHM requires.
- Two particles interacting only with each other always decouple into a freely-moving centre of mass and a relative coordinate obeying the one-body equation with reduced mass $\mu=m_1m_2/(m_1+m_2)$, this pattern reappears anywhere two bodies interact only via an internal force, not only for springs.
