---
module: APM01B1
topic: Extra Examples for Dynamics (exotic and multi-concept problems)
tags: [worked-example, added, common-mistake, formula]
---

# APM01B1 — Extra Examples (Dynamics)

This file is not a source of new theory, everything here reuses techniques already derived in [[APM01B1_Notes_S2_Dynamics]] and [[APM01B1_Proofs_ST2]]. It exists for problems that are "exotic" in the sense of pulling on more than one concept at once, or that expose a genuine gap or gotcha the plain derivations don't make obvious. Every problem is tagged by source and cross-linked to the technique(s) it uses.

Two real past papers fed this file:
- **2025 ST2, official solutions** (Dr K. D. Anderson, Dr S. R. Herbst, 27 September 2025) — used directly, these are lecturer-verified.
- **2011 ST2** (22 September 2011) — no solutions were provided with this one, so the solutions below are worked here from scratch and are **not** exam-verified against an official answer.

The notebook itself (see [[APM01B1_Summary_ST2#Material covered]]) records this year's ST2 as "2 Big Ass Questions", consistent with these past papers being multi-part, multi-concept questions rather than single-technique drills, exactly the style this file collects.

## 2025 ST2 Q1 — Airdrop: constant force, solved for impact time, velocity, and range

#worked-example

(source: 2025 ST2 official solutions, Q1, 15 marks)

A $100\,\text{kg}$ crate is released at $t=0$ from an aircraft moving horizontally at $\vec v_0=100\hat x\,\text{m/s}$, at height $200\,\text{m}$, air resistance neglected.

```tikz
\usepackage{tikz}
\usepackage{amsmath}
\begin{document}
\begin{tikzpicture}[scale=1]
  \draw[->] (0,0) -- (5.5,0) node[right] {$\hat x$};
  \draw[->] (0,0) -- (0,3.5) node[above] {$\hat y$};
  \draw[dashed] (0,3) -- (4,3);
  \node[draw, fill=gray!20] at (1,3) {$m$};
  \draw[->, thick] (1.4,3) -- (2.4,3) node[right] {$\vec v_0$};
  \draw[->, thick] (1,2.6) -- (1,1.8) node[right] {$\vec g$};
  \node at (-0.4,1.5) {$200\,\text{m}$};
  \draw[<->] (-0.15,0) -- (-0.15,3);
\end{tikzpicture}
\end{document}
```

This is a plain constant-force problem, $\vec F=m\vec g$, so it reuses the general result (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Worked example: constant force, $\vec F = -mg\hat z$]]):

$$\vec v(t) = \vec v_0+t\vec g, \qquad \vec r(t) = \vec r_0+t\vec v_0+\tfrac12t^2\vec g$$

Componentwise, with $y_0=200$: $x(t)=v_{x,0}t$, $y(t)=y_0-\tfrac12gt^2$. The crate lands when $y(t^*)=0$:

$$t^* = \sqrt{\frac{2y_0}{g}} = \sqrt{\frac{400}{9.81}} \approx 6.386\,\text{s}$$

Velocity at impact, $\vec v(t^*)=v_{x,0}\hat x-gt^*\hat y$:

$$\vec v^* \approx (100\hat x - 62.642\hat y)\ \text{m/s}$$

Horizontal range, $x(t^*)=v_{x,0}t^*$:

$$x^* \approx 638.551\ \text{m}$$

> [!note] N.B
> Nothing here needed the crate's mass ($100\,\text{kg}$ never enters the answer), a reminder that under gravity alone every object follows the same trajectory regardless of mass, the mass was given only to set the scene.

## 2025 ST2 Q2 — Escape velocity as the $h=0$ special case of a central force

#worked-example

(source: 2025 ST2 official solutions, Q2, 10 marks)

A projectile is launched **vertically** (straight up, purely radial) from Earth's surface at speed $v_0=\sqrt{\alpha gR}$. Because the motion is purely radial, $\dot\theta=0$ throughout, so the angular momentum $h=r^2\dot\theta=0$ identically, this is the special case of the general central-force result (see: [[APM01B1_Proofs_ST2#Conservation of angular momentum for a central force, $r^2\dot\theta=h$]]) with $h=0$, so the radial equation is just

$$\ddot r = -\frac{GM}{r^2} = -\frac{gR^2}{r^2}$$

(using $GM=gR^2$, matching the [[APM01B1_Notes_S2_Dynamics#(added) Worked example: a tunnel through the earth|tunnel-through-the-earth]] convention). Apply the same $v\,dv/dr$ device as always:

$$v\frac{dv}{dr} = -\frac{gR^2}{r^2} \;\Rightarrow\; \int v\,dv = -gR^2\int\frac{dr}{r^2} \;\Rightarrow\; \frac12v^2 = \frac{gR^2}{r}+A$$

At $t=0$: $v=v_0=\sqrt{\alpha gR}$, $r=R$, so $\tfrac12\alpha gR = gR + A \Rightarrow A=\left(\tfrac{\alpha-2}{2}\right)gR$. Hence

$$\frac12v^2 = \frac{gR^2}{r}+\left(\frac{\alpha-2}{2}\right)gR$$

Maximum height $r_m$ is where $v=0$:

$$0 = \frac{gR^2}{r_m}+\left(\frac{\alpha-2}{2}\right)gR \;\Rightarrow\; \boxed{r_m = \left(\frac{2}{\alpha-2}\right)R, \qquad h_{max}=r_m-R=\left(\frac{\alpha}{\alpha-2}\right)R}$$

**Special case $\alpha=2$**: $h_{max}\to\infty$, the projectile never returns, this is **escape velocity**, $v_{esc}=\sqrt{2gR}$.

> [!note] N.B
> This is the same equation and the same $v\,dv/dr$ technique as the orbital central-force example, with one difference: setting $h=0$ up front rather than carrying it through. Watch for exactly this kind of "special case of a general result" framing, recognising it saves re-deriving from scratch.

## 2025 ST2 Q3 — The rocket equation, with real thrust (Tsiolkovsky)

#worked-example

(source: 2025 ST2 official solutions, Q3, 10 marks)

> [!note] Extends existing content
> [[APM01B1_Proofs_ST2#Variable-mass (rocket) equation of motion]] covers a rocket losing mass under gravity **alone**, no thrust. This question adds an actual thrust force, $\vec F_{thrust}=\dot m(v-v_e)\hat y$ ($v_e$ constant, the exhaust speed), giving the real rocket equation.

**(a) Setting up the equation of motion.** Momentum form of N2, vertical motion only:

$$\frac{dp}{dt} = -m(t)g+F_{thrust} \;\Rightarrow\; m\frac{dv}{dt}+\frac{dm}{dt}v = -mg+\frac{dm}{dt}(v-v_e)$$

The $\frac{dm}{dt}v$ terms cancel from both sides:

$$\boxed{m(t)\frac{dv}{dt} = -m(t)g-\frac{dm}{dt}v_e}$$

**(b) Solving for $v(t)$.** Rearranging and separating:

$$\frac{dv}{dt} = -g-\frac{v_e}{m}\frac{dm}{dt} \;\Rightarrow\; v(t) = -gt - v_e\int_{m_0}^{m(t)}\frac{dm}{m} = -gt-v_e\big[\ln m(t)-\ln m_0\big]$$

$$\boxed{v(t) = -gt+v_e\ln\!\left(\frac{m_0}{m(t)}\right)}$$

**(c) With $m(t)=m_0e^{-\lambda t}$**, find $t_{v_e}$, the time to reach speed $v_e$:

$$v(t) = -gt+v_e\ln\!\left(\frac{m_0}{m_0e^{-\lambda t}}\right) = -gt+v_e\lambda t$$

Setting $v(t_{v_e})=v_e$:

$$v_e = -gt_{v_e}+v_e\lambda t_{v_e} \;\Rightarrow\; \boxed{t_{v_e} = \frac{v_e}{\lambda v_e-g}}$$

**(d) At $v=v_e$**, the thrust force $\dot m(v-v_e)=\dot m\cdot 0=0$, so the boosters should be **shut down**, they are producing zero net thrust at exactly that speed.

> [!warning] Common mistake
> Don't confuse this with the toy rocket example already in the notes: there, $\vec F=-mg$ alone (no thrust), and the "surprising" result was that $v$ could still grow because $p=mv$ with shrinking $m$. Here there's a genuine propulsive force, and it exactly cancels the $\dot m v$ term from expanding $d(mv)/dt$, that cancellation is the whole trick of part (a) and is easy to miss if you differentiate the momentum without also substituting $F_{thrust}$'s own $v$ term.

## 2025 ST2 Q4 — Rotating sphere with cubic air resistance

#worked-example

(source: 2025 ST2 official solutions, Q4, 10 marks)

A sphere of fixed radius $R$ (so $r(t)=R$, $\dot r=0$) experiences friction $\vec F=-kR^3\dot\theta^3\hat\theta$.

**(a) Transversal (θ) component of N2** (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Velocity and acceleration in polar coordinates]] for the boxed acceleration):

$$m(r\ddot\theta+2\dot r\dot\theta) = F_\theta \;\overset{\dot r=0}{\Longrightarrow}\; mR\ddot\theta = -kR^3\dot\theta^3 \;\Rightarrow\; \boxed{\ddot\theta = -\frac{kR^2}{m}\dot\theta^3}$$

**(b) Reducing to $\omega(\theta)$.** Let $\omega=\dot\theta$. This is exactly the $v\,dv/dr$ trick (see: [[APM01B1_Proofs_ST2#$v\,dv/dz$ reduction for a speed-dependent force]]), with $\theta$ playing the role of position and $\omega$ the role of velocity:

$$\frac{d\omega}{dt} = \frac{d\theta}{dt}\frac{d\omega}{d\theta} = \omega\frac{d\omega}{d\theta} \;\Rightarrow\; \omega\frac{d\omega}{d\theta} = -\frac{kR^2}{m}\omega^3 \;\Rightarrow\; \boxed{\frac{d\omega}{d\theta} = -\frac{kR^2}{m}\omega^2}$$

**(c) Solving for $\omega(\theta)$.** Separable:

$$\frac{d\omega}{\omega^2} = -\frac{kR^2}{m}\,d\theta \;\Rightarrow\; \int_{\omega_0}^{\omega}\frac{d\omega'}{\omega'^2} = -\frac{kR^2}{m}\int_0^\theta d\theta'$$

$$-\frac1\omega+\frac1{\omega_0} = -\frac{kR^2}{m}\theta \;\Rightarrow\; \frac1\omega = \frac{m+kR^2\omega_0\theta}{m\omega_0} \;\Rightarrow\; \boxed{\omega(\theta) = \frac{m\omega_0}{m+kR^2\omega_0\theta}}$$

**(d) What kind of function is $\theta(t)$, without solving for it?** Rewrite $\omega(\theta)$ back as a separable equation in $t$: $(m+kR^2\omega_0\theta)\,d\theta = m\omega_0\,dt$. The left side is quadratic in $\theta$, the right side linear in $t$, so integrating gives $\theta$'s defining equation as quadratic-in-$\theta$ equals linear-in-$t$, i.e. $\theta(t)\propto t^{1/2}$.

> [!warning] Common mistake (official erratum)
> The official solutions note that the information sheet handed out with this paper had a **typo** in the transversal acceleration formula (missing an $r$ in front of $\ddot\theta$). Students who used the misprinted formula get $\ddot\theta=-\frac{kR^3}{m}\dot\theta^3$ instead (an extra factor of $R$), which changes the constant throughout but not the qualitative shape of the answer ($\theta(t)\propto t^{1/2}$ either way). The lesson: **always sanity-check a given formula sheet against the boxed result you've derived and memorised** (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Velocity and acceleration in polar coordinates]]) rather than trusting it blindly, a wrong information sheet is a real, recorded failure mode on this exact paper.

## 2011 ST2 Q1 — Quick drill: velocity from a given $\vec F(t)$

#worked-example

(source: 2011 ST2, Q1, 6 marks; not exam-verified, solved here)

$\vec F(t)=(e^t,\,t^2,\,\sin t)$, mass $1\,\text{kg}$, $\vec v(0)=(1,2,5)$, find $\vec v(2)$.

Direct integration (see: [[APM01B1_Proofs_ST2#General solution for a time-dependent force]]):

$$\vec v(t) = \vec v(0)+\int_0^t\vec F(t')\,dt' = (1+e^t-1,\ 2+\tfrac13t^3,\ 5+1-\cos t) = (e^t,\ 2+\tfrac13t^3,\ 6-\cos t)$$

$$\vec v(2) = (e^2,\ 2+\tfrac83,\ 6-\cos 2) \approx (7.389,\ 4.667,\ 6.416)$$

## 2011 ST2 Q2 — Tunnel through the Earth: full transit, not just to the centre

#worked-example

(source: 2011 ST2, Q2, 6 marks; not exam-verified, solved here)

> [!warning] Common mistake
> This question asks for the time to fall **right through** the tunnel, from surface to the *opposite* surface, not just to the centre. [[APM01B1_Notes_S2_Dynamics#(added) Worked example: a tunnel through the earth]] only computed the time to the centre, a quarter period. Reusing that number here would be wrong by a factor of 2.

The motion is SHM with $\omega=\sqrt{g/R}$ (same derivation, unchanged). Falling from one surface ($r=+R$) through the centre to the opposite surface ($r=-R$) is **half** a full oscillation, not a quarter:

$$t_{through} = \frac{T}{2} = \frac{\pi}{\omega} = \pi\sqrt{\frac{R}{g}}$$

compared with $t_{centre}=\frac{T}{4}=\frac\pi2\sqrt{R/g}$ for reaching only the centre, exactly twice as long.

## 2011 ST2 Q3 — Bullet with linear drag, no gravity: the simpler complementary case

#worked-example

(source: 2011 ST2, Q3, 13 marks; not exam-verified, solved here)

A bullet penetrates a medium at speed $v_0$, resistance $\propto$ speed (constant $k$), gravity negligible.

> [!note] N.B
> [[APM01B1_Notes_S2_Dynamics#Solving for $v(z)$: the $v\,dv/dz$ trick|Speed-dependent force]] in the main notes needed the harder $v\,dv/dz$ route because gravity was also present. Here gravity is negligible, so $m\dot v=-kv$ is **directly separable in $t$**, no chain-rule trick needed, a genuinely simpler case worth telling apart.

**(a) How far does it penetrate?** $m\dfrac{dv}{dt}=-kv \Rightarrow \dfrac{dv}{v}=-\dfrac km\,dt \Rightarrow v(t)=v_0e^{-kt/m}$. Integrate to get position:

$$x(t) = \int_0^tv_0e^{-kt'/m}\,dt' = \frac{mv_0}{k}\left(1-e^{-kt/m}\right)$$

As $t\to\infty$, $x(t)\to\dfrac{mv_0}{k}$, a **finite** total penetration depth.

**(b) Show $x(t)=\dfrac{mv_0}{k}\left(e^{-kt/m}-1\right)$** — as given in the question, this is the same result with the opposite sign convention (penetration measured as a negative displacement, or $k$ absorbing a sign); the derivation above already establishes the magnitude.

**(c) Derive $a=-\dfrac km v$ from (1).** Differentiate $x(t)$ twice: $\dot x=v_0e^{-kt/m}=v(t)$ (consistent), $\ddot x=-\dfrac km v_0e^{-kt/m}=-\dfrac km v$, recovering the original equation of motion, a consistency check rather than new information.

> [!note] N.B on quadratic vs linear drag
> Contrast this with resistance $\propto v^2$ (Tutorial 7 Q2, "a bullet penetrates a medium... resistance proportional to the square of its speed"): $m\,v\,dv/dx=-kv^2 \Rightarrow dv/dx=-\frac km v \Rightarrow v(x)=v_0e^{-kx/m}$. Here $v\to0$ only as $x\to\infty$, so the model predicts **unbounded** penetration depth, unlike the linear-drag case above, which converges to the finite depth $mv_0/k$. If a question asks for "the distance to reach some fraction of $v_0$" under quadratic drag, use $x=\dfrac mk\ln(v_0/v_f)$ directly rather than looking for a finite "stopping point": there isn't one in this idealised model.

## (added) A constructed multi-concept question: quadratic drag, then an impulse

#worked-example

> [!note] Constructed for practice, not from any source
> Built specifically to combine the quadratic-drag result above with impulse, since no source problem does both. Treat this as practice, not as a predicted exam question.

A particle of mass $m$ moves in a straight line, initial speed $v_0$, experiencing quadratic drag $F=-kv^2$ for a time $T$, after which the drag switches off and an impulsive force $\vec J$ (in the direction of motion) acts instantaneously.

**Phase 1 (drag only).** From above, $\dfrac{1}{v}=\dfrac1{v_0}+\dfrac km t$, so

$$v(T) = \frac{v_0}{1+\dfrac{kv_0}{m}T}$$

**Phase 2 (impulse).** By definition (see: [[APM01B1_Proofs_ST2#Impulse, $\Delta\vec p=\int\vec F\,dt$]]), $\Delta p=J$, so immediately after the impulse:

$$v(T^+) = v(T)+\frac{J}{m} = \frac{v_0}{1+\dfrac{kv_0}{m}T}+\frac{J}{m}$$

**Phase 3 (drag resumes).** The particle again obeys $m\,dv/dt=-kv^2$, but now starting from $v(T^+)$ as its new "$v_0$"; reapplying the phase-1 result with a shifted time origin and initial speed $v(T^+)$ gives $v(t)$ for $t>T$, and, per the N.B above, the further distance travelled after the impulse is again formally unbounded (the quadratic-drag model never brings the particle to rest at a finite distance).

> [!note] N.B
> The point of this question is less the algebra (each phase reuses a technique already derived) and more recognising that an impulse **resets the initial condition** for whatever ODE governs the next phase, it does not change which ODE applies. That "reset the initial condition, keep the same equation" pattern is worth having ready for any piecewise-force problem.
