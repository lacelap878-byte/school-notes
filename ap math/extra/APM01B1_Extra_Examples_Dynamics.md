---
module: APM01B1
topic: Extra Examples for Dynamics (exotic and multi-concept problems)
tags: [worked-example, added, common-mistake, formula, exam-flagged]
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

---

# (added) Addendum: 2012 ST2 and 2024 ST2

## Sources used (2012 and 2024 papers)

- 2012 ST2, 27 September 2012, 27 marks, 70 minutes, with official solutions. Label: `(source: 2012 ST2 solutions)`.
- 2024 ST2, 28 September 2024, 40 marks, 80 minutes, with the lecturer's handwritten solutions. Label: `(source: 2024 ST2 memo)`. The file called `2024apm01b1_sao2_memo.pdf` is this same paper and the same handwriting, so there is one paper here, not two.
- Not used: 2024 ST1 (17 August) and the 2024 Sick Test 1 (26 August), with the files `2024apm01b1_sao1_questions.pdf` and `Sample_Test_1_with_memo.pdf`. All four are pure kinematics (polar coordinates, path sketches, integrating acceleration), which is outside a dynamics-only test and already covered by the ST1 files.

## What this adds

Compared against the earlier dynamics files.

| Question | Technique | Status |
|---|---|---|
| 2012 (a) | chain rule $v\,dv/dx$ for a force $F(x)$, turning point | New |
| 2012 (b), (c) | linear drag plus gravity, closed form for $v_y(t)$ and $y(t)$ | Partly covered (separable $\dot z=-kz+C$ and $v\,dv/dz$ exist in the notes); new as a complete projectile |
| 2024 Q1 | same, general $k$, launch height 2 | New, and the printed target in (c) has a typo |
| 2024 Q2 | $F(t)$ for two bodies, arrival-time condition, perfectly inelastic 2D collision | New as one combined problem; the memo's part (e) has two problems |
| 2024 Q3 | SHM ansatz | Covered, only the initial-condition step is added |
| 2024 Q4 | tunnel through the earth | Covered (full transit is in the earlier file), numeric check added |

## What the 2012 paper tells you about your test

Your lecturer said the upcoming test will be very similar to the 2012 one, out of 25 marks in 70 minutes (confirmed by you). That is about 2.8 minutes per mark. (added)

The 2012 paper is one scenario with three "show that" parts, each feeding the next:

- (a) the force depends on position, so use the chain rule $v\,dv/dx$ and find where $v_x=0$
- (b) the force depends on velocity (plus gravity), so separate variables in time
- (c) integrate the result and fix the constant from the initial condition

N.B The three parts use three different methods on one particle. Classify the force first (see: the roadmap at the top of [[APM01B1_Notes_S2_Dynamics]]), then the method follows.

Likely variations, my forecast and not information from the lecturer: a different exponent or coefficient in the $x$ force, a different drag coefficient, a launch height above zero, or the roles of the axes swapped. Practice A and Practice B below cover the first three. (added)

## Linear-drag projectile, general result

#formula #added

Take $\vec F=-mg\hat{y}-k\dot{\vec r}$, launch from $(0,y_0)$ at speed $v_0$ and angle $\theta$ above $\hat{x}$.

Horizontal: $m\ddot x=-k\dot x$, so $\dot x=v_0\cos\theta\,e^{-kt/m}$ and

$$x(t)=\frac{m v_0\cos\theta}{k}\left(1-e^{-kt/m}\right)$$

Vertical: $\ddot y+\frac km\dot y=-g$. Let $u=\dot y+\frac{mg}{k}$, then $\dot u=-\frac kmu$, so $u=\left(v_0\sin\theta+\frac{mg}{k}\right)e^{-kt/m}$ and

$$\dot y(t)=\left(v_0\sin\theta+\frac{mg}{k}\right)e^{-kt/m}-\frac{mg}{k}$$

$$y(t)=y_0+\frac mk\left(v_0\sin\theta+\frac{mg}{k}\right)\left(1-e^{-kt/m}\right)-\frac{mg}{k}t$$

Symbols: $m$ in kg, $k$ the drag coefficient in kg/s, $g$ in m/s$^2$, $v_0$ in m/s, $t$ in s.

Terminal (long-time) vertical speed: $\dot y\to-\frac{mg}{k}$.

Apex, from $\dot y=0$:

$$t^*=\frac mk\ln\left(1+\frac{k v_0\sin\theta}{mg}\right),\qquad y_{apex}=y_0+\frac mk v_0\sin\theta-\frac{m^2g}{k^2}\ln\left(1+\frac{k v_0\sin\theta}{mg}\right)$$

> *I checked these against a numerical integration of the equations of motion, and they agree to better than ten digits.*

Both papers are special cases:

- 2012: $k=1$, $y_0=0$ gives $\dot y=(v_0\sin\theta+mg)e^{-t/m}-mg$ and $B=mv_0\sin\theta+m^2g$
- 2024 Q1: $\theta=60^\circ$, $y_0=2$ gives the target in Worked Example 2 (with the typo corrected)

## Worked Example 1: 2012 ST2, projectile with $F_f=(-x^2,-v_y)$

#worked-example #exam-flagged

(source: 2012 ST2 solutions, 27 marks for the whole paper)

A particle of mass $m$ is projected from the origin at angle $\theta$ to the horizontal with speed $v_0$. Besides gravity it feels $\vec F_f=(-x^2,-v_y)$.

- (a) Show $v_x=0$ when $x=\left(\dfrac{3mv_0^2\cos^2\theta}{2}\right)^{1/3}$.
- (b) Show $v_y(t)=(v_0\sin\theta+mg)e^{-t/m}-mg$.
- (c) Show $y(t)=B\left(1-e^{-t/m}\right)-mgt$, where $B=mv_0\sin\theta+m^2g$.

Useful result given on the paper: $F=m\dfrac{dv}{dt}=m\dfrac{dv}{dx}\dfrac{dx}{dt}$.

WORKING (a)

$$m\frac{dv_x}{dt}=-x^2$$

Chain rule, $\dfrac{dv_x}{dt}=\dfrac{dv_x}{dx}\dfrac{dx}{dt}=v_x\dfrac{dv_x}{dx}$:

$$m v_x\frac{dv_x}{dx}=-x^2\;\Rightarrow\; m\int v_x\,dv_x=-\int x^2\,dx\;\Rightarrow\;\frac{mv_x^2}{2}=-\frac{x^3}{3}+A_1$$

At $t=0$: $x=0$, $v_x=v_0\cos\theta$, so $A_1=\dfrac{m v_0^2\cos^2\theta}{2}$.

$$v_x=\sqrt{v_0^2\cos^2\theta-\frac{2x^3}{3m}}$$

$v_x=0$ gives $x^3=\dfrac{3mv_0^2\cos^2\theta}{2}$, which is the stated result.

WORKING (b)

$$m\frac{dv_y}{dt}=-mg-v_y\;\Rightarrow\;\frac{m\,dv_y}{mg+v_y}=-dt\;\Rightarrow\;m\ln(mg+v_y)=-t+A_2$$

So $v_y=e^{A_2/m}e^{-t/m}-mg$. At $t=0$, $v_y=v_0\sin\theta$ gives $e^{A_2/m}=v_0\sin\theta+mg$, which is the stated result.

WORKING (c)

$$y=\int v_y\,dt=-m(v_0\sin\theta+mg)e^{-t/m}-mgt+A_3$$

At $t=0$, $y=0$ gives $A_3=m(v_0\sin\theta+mg)=mv_0\sin\theta+m^2g=B$, so

$$y(t)=B\left(1-e^{-t/m}\right)-mgt$$

> [!warning] Turning point, not a stop
> The force $-x^2$ is negative for every $x$, so the particle does not rest at the $x$ found in (a). The $+$ square root holds only on the way out. After that point $v_x<0$ and the particle comes back. The question asks where $v_x=0$, nothing more.

N.B Part (a) needs the chain rule because the force depends on $x$. Part (b) needs plain separation in $t$ because the force depends on $v_y$. Choosing the wrong one is the usual way to get stuck.

Apex of the 2012 trajectory (from the general result with $k=1$): (added)

$$t^*=m\ln\left(1+\frac{v_0\sin\theta}{mg}\right),\qquad y_{apex}=mv_0\sin\theta-m^2g\ln\left(1+\frac{v_0\sin\theta}{mg}\right)$$

Generalising (a) to $F_x=-c\,x^n$: (added)

$$v_x^2=v_0^2\cos^2\theta-\frac{2c\,x^{n+1}}{(n+1)m},\qquad x^*=\left(\frac{(n+1)\,m\,v_0^2\cos^2\theta}{2c}\right)^{\frac{1}{n+1}}$$

Checks: $n=2$, $c=1$ reproduces (a). $n=0$ (constant force) gives $x^*=\dfrac{v_0^2\cos^2\theta}{2(c/m)}$, which is the familiar $v^2/2a$ stopping distance. A numerical run with $n=2$, $c=0.7$ agrees with the formula.

## Worked Example 2: 2024 ST2 Q1, projectile with air resistance $-k\dot{\vec r}$

#worked-example

(source: 2024 ST2 memo, Q1, 10 marks)

A projectile of mass $m$ is launched from $\vec r(0)=0\hat{x}+2\hat{y}$ with speed $v$ at $60^\circ$ above $+\hat{x}$. Gravity acts, and air resistance is $\vec F_{air}=-k\dot{\vec r}(t)$.

- (a) Set up the equations of motion with initial conditions. (2)
- (b) Show $x(t)=\dfrac{mv}{2k}\left(1-e^{-kt/m}\right)$. (5)
- (c) Given $\dot y(t)=\dfrac{\sqrt3}{2}v\,e^{-kt/m}-\dfrac{gm}{k}\left(1-e^{-kt/m}\right)$, find $y(t)$. (3)

WORKING (a)

$m\ddot{\vec r}=\vec F_{net}$ with $\vec F_{net}=-k\dot x\,\hat{x}-(k\dot y+mg)\,\hat{y}$, so

$$\ddot x=-\frac km\dot x,\quad x(0)=0,\quad \dot x(0)=\frac v2$$

$$\ddot y=-\frac km\dot y-g,\quad y(0)=2,\quad \dot y(0)=\frac{\sqrt3\,v}{2}$$

WORKING (b)

$\dfrac{1}{\dot x}\dfrac{d\dot x}{dt}=-\dfrac km\Rightarrow\ln\dot x=-\dfrac km t+c_1\Rightarrow\dot x=Ce^{-kt/m}$, and $\dot x(0)=\dfrac v2$ gives $C=\dfrac v2$.

$$x=\int\frac v2e^{-kt/m}\,dt=-\frac{mv}{2k}e^{-kt/m}+C_2$$

$x(0)=0$ gives $C_2=\dfrac{mv}{2k}$, which is the stated result.

WORKING (c)

$$y=\int\dot y\,dt=-\frac{\sqrt3\,mv}{2k}e^{-kt/m}-\frac{gm}{k}\left(t+\frac mk e^{-kt/m}\right)+C_3$$

$y(0)=2$ gives $C_3=\dfrac{\sqrt3\,mv}{2k}+\dfrac{m^2g}{k^2}+2$. Substituting:

$$y(t)=\frac{\sqrt3\,mv}{2k}\left(1-e^{-kt/m}\right)+\frac{m^2g}{k^2}\left(1-e^{-kt/m}\right)-\frac{mg}{k}t+2$$

> [!warning] The printed target in (c) has a typo
> The paper prints the last two coefficients as $\dfrac{m^2g}{2k^2}$ and $\dfrac{mg}{2k}$. The correct coefficients are $\dfrac{m^2g}{k^2}$ and $\dfrac{mg}{k}$, with no factor 2. Three checks agree: the memo's own constant $C_3$ carries $\dfrac{m^2g}{k^2}$, integrating the given $\dot y$ produces these coefficients, and a numerical test ($k=0.8$, $m=1.1$, $v=7$, $t=1.3$) gives $y=0.9032$ from direct integration and from the correct formula, but $4.0002$ from the printed one. Dimensional analysis cannot catch this, since both versions have units of metres.
>
> If a "show that" target ever disagrees with a clean derivation, plug in numbers before you fudge anything. If the derivation holds, write what you derived and state the discrepancy in one line. You may also want to ask your lecturer whether the printed version was a typo.

## Worked Example 3: 2024 ST2 Q2, two cars, arrival time and collision

#worked-example #exam-flagged

(source: 2024 ST2 memo, Q2, 15 marks; corrections to part (e) are mine and marked)

Two cars of equal mass $m$ race in straight lines to a common point $P$. Car A has driving force $\vec F_1=ma\hat{y}$ ($a$ constant). Car B has $\vec F_2=m\frac{\sqrt2}{2}\left(t\hat{x}+t\hat{y}\right)$. Both start at rest, A at $\vec r_1(0)=1\hat{x}$ and B at $\vec r_2(0)=\vec 0$.

- (a) Coordinates of $P$. (2)
- (b) Equations of motion with initial conditions. (2)
- (c) Solutions. (3)
- (d) Condition on $a$ for car A to beat car B. (2)
- (e) If they collide at $P$ and move on as one mass, find the magnitude and direction of the wreckage velocity. (6)

```tikz
\begin{document}
\begin{tikzpicture}[scale=2.2]
  \draw[->] (0,0) -- (1.5,0) node[right] {$x$};
  \draw[->] (0,0) -- (0,1.4) node[above] {$y$};
  \draw[dashed] (0,0) -- (1,1);
  \draw[dashed] (1,0) -- (1,1);
  \fill (1,1) circle (0.03) node[above right] {$P(1,1)$};
  \fill (0,0) circle (0.03) node[below left] {B};
  \fill (1,0) circle (0.03) node[below] {A};
\end{tikzpicture}
\end{document}
```

WORKING (a)

A starts at $(1,0)$ and is pushed along $\hat{y}$, so it moves along the line $x=1$. B starts at the origin and is pushed along $\hat{x}+\hat{y}$, so it moves along $y=x$. They meet at $P=(1,1)$.

WORKING (b)

$$\text{A: }\ddot x_A=0,\ x_A(0)=1,\ \dot x_A(0)=0;\qquad \ddot y_A=a,\ y_A(0)=0,\ \dot y_A(0)=0$$

$$\text{B: }\ddot x_B=\tfrac{\sqrt2}{2}t,\ x_B(0)=0,\ \dot x_B(0)=0;\qquad \ddot y_B=\tfrac{\sqrt2}{2}t,\ y_B(0)=0,\ \dot y_B(0)=0$$

WORKING (c)

$$x_A=1,\quad y_A=\tfrac12at^2,\qquad x_B=y_B=\tfrac{\sqrt2}{12}t^3$$

and the velocities, which part (e) needs: $\dot y_A=at$, and $\dot x_B=\dot y_B=\tfrac{\sqrt2}{4}t^2$.

WORKING (d)

B reaches $P$ when $\tfrac{\sqrt2}{12}t_B^3=1$, so $t_B=(6\sqrt2)^{1/3}\approx2.040\ \text{s}$. A reaches $P$ when $\tfrac12at_A^2=1$, so $t_A=\sqrt{2/a}$.

A beats B when $t_A<t_B$:

$$a>\frac{2}{t_B^2}=\frac{2}{72^{1/3}}\approx0.481\ \text{m/s}^2$$

Equality means they arrive together, which is exactly the collision case in (e).

WORKING (e)

Momentum is conserved through the collision. The collision forces are internal and act over an instant, while the drive forces are finite and contribute a negligible impulse during that instant. Both cars are at $P$ at $t_B=2.040\ \text{s}$ with $a=0.481\ \text{m/s}^2$.

$$\vec v_A=at_B\,\hat{y}\approx0.981\,\hat{y}\ \text{m/s},\qquad \vec v_B=\tfrac{\sqrt2}{4}t_B^2\,(\hat{x}+\hat{y})\approx1.471\,(\hat{x}+\hat{y})\ \text{m/s}$$

$$m\vec v_A+m\vec v_B=(2m)\,\vec v_w\;\Rightarrow\;\vec v_w=\tfrac12(\vec v_A+\vec v_B)\approx(0.735\,\hat{x}+1.226\,\hat{y})\ \text{m/s}$$

$$|\vec v_w|\approx1.429\ \text{m/s},\qquad \varphi=\arctan\frac{1.226}{0.735}\approx1.030\ \text{rad}\ (59.036^\circ)\ \text{above }+\hat{x}$$

> [!warning] Two problems in the memo's part (e)
> The memo writes $\vec p_{tot}=m\left(at\,\hat{y}+\tfrac{\sqrt2}{4}t\,\hat{x}+\tfrac{\sqrt2}{4}t\,\hat{y}\right)$, evaluates $0.72$ for the B components, and reports $1.85m$ at $1.17$ rad ($67.05^\circ$).
>
> 1. The B velocity should be $\tfrac{\sqrt2}{4}t^2$, not $\tfrac{\sqrt2}{4}t$. Differentiating the memo's own part (c), $x_B=\tfrac{\sqrt2}{12}t^3$, gives $\tfrac{\sqrt2}{4}t^2$, which is $1.471$ at $t_B$, not $0.72$.
> 2. The question asks for the wreckage velocity, but $1.85m$ is the total momentum (per unit $m$, $1.85$). The velocity is that divided by the combined mass $2m$.
>
> Both come from reading the memo against its own (b) and (c). The memo's (a) to (d) are correct. Check part (e) with your lecturer or a tutor before relying on either number in a test.

Shortcuts for a power law $x\propto t^n$: velocity is $nx/t$. So A: $v=2(1)/t_B=0.981$, B: $v=3(1)/t_B=1.471$ per component. Exact closed form: $\vec v_w=\dfrac{1}{t_B}\left(\tfrac32\hat{x}+\tfrac52\hat{y}\right)$, so $|\vec v_w|=\dfrac{\sqrt{34}}{2\,t_B}$ and $\varphi=\arctan\tfrac53$. (added)

If the masses differ, $\vec v_w=\dfrac{m_A\vec v_A+m_B\vec v_B}{m_A+m_B}$. For $m_A=3m_B$ with the same velocities, $\vec v_w\approx(0.368\,\hat{x}+1.103\,\hat{y})\ \text{m/s}$, $|\vec v_w|\approx1.163\ \text{m/s}$, $71.57^\circ$ above $+\hat{x}$. (added)

N.B Find the impact time from the car whose equation is hardest to invert (here B's cubic), then feed that same time into the other car.

## Worked Example 4: 2024 ST2 Q3 and Q4

#worked-example #added

(source: 2024 ST2 memo, Q3 and Q4)

Q3(a) to (c) are the spring ansatz already in the notes (see: The ansatz method in [[APM01B1_Notes_S2_Dynamics]]). The new part is (d), applying initial conditions.

Statement (d): with $w=x-x_0$, $w=A\cos\lambda t+B\sin\lambda t$ and $\lambda=\sqrt{k/m}$, find $A$ and $B$ given $x(0)=x_0$ and $x'(0)=-1$.

WORKING (d)

$x(0)=x_0$ gives $w(0)=0$, so $A=0$. Since $x_0$ is constant, $\dot w=\dot x$, so $\dot w(0)=-1$ gives $B\lambda=-1$:

$$B=-\sqrt{\frac mk},\qquad x(t)=x_0-\sqrt{\frac mk}\,\sin\!\left(\sqrt{\frac km}\,t\right)$$

In general, $w(0)=w_0$ and $\dot w(0)=u_0$ give $A=w_0$ and $B=u_0/\lambda$. (added)

Q4, the tunnel (see: (added) Worked example: a tunnel through the earth in [[APM01B1_Notes_S2_Dynamics]], and the full-transit version under the 2011 tunnel example earlier in this file). The memo gets $\omega=\sqrt{g/R}=1.24\times10^{-3}\ \text{rad/s}$ and says north to south is half a cycle, so

$$t=\frac{2\pi}{2\omega}=\pi\sqrt{\frac Rg}$$

> [!note] The number 42.4 does not come out of the arithmetic
> The memo's own $2531\ \text{s}$ is $42.18$ minutes, not $42.4$. With $R=6.371\times10^6\ \text{m}$ and $g=9.81\ \text{m/s}^2$ the exact value is $\pi\sqrt{R/g}=2531.7\ \text{s}\approx42.20$ minutes. Other standard constants give $42.2$ to $42.3$. Reaching $42.4$ would need $R\approx6.43\times10^6\ \text{m}$, about 1 percent above Earth's mean radius.
>
> If a test asks you to show a "roughly" figure, give your own working and number, write $\approx42.2$ minutes, and say it matches the quoted value to within 0.5 percent.

N.B North to south is half a period, $\pi\sqrt{R/g}$. Time to the centre is a quarter, $\frac\pi2\sqrt{R/g}$. The two are easy to swap.

## Practice A: the 2012 structure with different numbers

#worked-example #added

(constructed, added)

Same set-up as 2012 (mass $m$, from the origin, speed $v_0$ at angle $\theta$, gravity plus a frictional force) but with $\vec F_f=(-x^3,-2v_y)$.

- (a) Show $v_x=0$ when $x=\left(2mv_0^2\cos^2\theta\right)^{1/4}$.
- (b) Show $v_y(t)=\left(v_0\sin\theta+\tfrac{mg}{2}\right)e^{-2t/m}-\tfrac{mg}{2}$.
- (c) Show $y(t)=\tfrac m2\left(v_0\sin\theta+\tfrac{mg}{2}\right)\left(1-e^{-2t/m}\right)-\tfrac{mg}{2}t$.
- (d) Find the time and height of the apex.

WORKING

(a) $m v_x\dfrac{dv_x}{dx}=-x^3\Rightarrow\dfrac{mv_x^2}{2}=-\dfrac{x^4}{4}+\dfrac{mv_0^2\cos^2\theta}{2}$. Setting $v_x=0$: $x^4=2mv_0^2\cos^2\theta$.

(b) $m\dot v_y=-mg-2v_y\Rightarrow\dfrac{m\,dv_y}{mg+2v_y}=-dt\Rightarrow\dfrac m2\ln(mg+2v_y)=-t+A$. With $v_y(0)=v_0\sin\theta$: $mg+2v_y=(mg+2v_0\sin\theta)e^{-2t/m}$, which gives the stated $v_y$.

(c) Integrate: $y=-\dfrac m2\left(v_0\sin\theta+\dfrac{mg}2\right)e^{-2t/m}-\dfrac{mg}{2}t+A_3$. $y(0)=0$ fixes $A_3=\dfrac m2\left(v_0\sin\theta+\dfrac{mg}{2}\right)$.

(d) From the general result with $k=2$:

$$t^*=\frac m2\ln\left(1+\frac{2v_0\sin\theta}{mg}\right),\qquad y_{apex}=\frac m2v_0\sin\theta-\frac{m^2g}{4}\ln\left(1+\frac{2v_0\sin\theta}{mg}\right)$$

Numeric check ($m=1.2\ \text{kg}$, $v_0=6\ \text{m/s}$, $\theta=0.9\ \text{rad}$, $g=9.81\ \text{m/s}^2$), matched by direct numerical integration: $x^*=2.404\ \text{m}$, $t^*=0.352\ \text{s}$, $y_{apex}=0.747\ \text{m}$. At $t=0.9\ \text{s}$: $v_y=-3.524\ \text{m/s}$ and $y=-0.363\ \text{m}$ (below the launch height).

## Practice B: when the chain rule and the ansatz must agree

#worked-example #added

(constructed, added)

Same set-up, but $\vec F_f=(-x,-v_y)$. This makes the $x$ equation $m\ddot x=-x$, a spring.

- (a) Use $v\,dv/dx$ to show $v_x=0$ at $x=v_0\cos\theta\sqrt m$.
- (b) Confirm with the SHM ansatz and find the time at which it happens.

WORKING

(a) $m v_x\dfrac{dv_x}{dx}=-x\Rightarrow\dfrac{mv_x^2}{2}+\dfrac{x^2}{2}=\dfrac{mv_0^2\cos^2\theta}{2}$. Setting $v_x=0$: $x^2=mv_0^2\cos^2\theta$, so $x=v_0\cos\theta\sqrt m$.

(b) $\ddot x=-\dfrac1mx$, so $\omega=\dfrac{1}{\sqrt m}$. With $x(0)=0$ and $\dot x(0)=v_0\cos\theta$: $x=v_0\cos\theta\sqrt m\,\sin\dfrac{t}{\sqrt m}$. The amplitude matches (a), and $v_x=0$ first occurs at a quarter period, $t=\dfrac\pi2\sqrt m$.

> *The chain-rule route produced the energy equation $\tfrac12mv^2+\tfrac12x^2=\text{const}$ for free, which is the same conserved quantity the spring has. When you have both methods available, doing the cheaper one and checking against the other is a quick error test.*

Numeric check with $m=1.2\ \text{kg}$, $v_0=6\ \text{m/s}$, $\theta=0.9\ \text{rad}$: $x^*=4.086\ \text{m}$ and $t^*=1.721\ \text{s}$, matched by direct numerical integration.

## Do not forget

- Force depends on $x$: chain rule $m v\,dv/dx$. Force depends on $v$ or $t$: separate in time.
- After $v_x=0$ the particle turns back, so the $+$ root is only valid up to that point.
- Linear drag with gravity: terminal vertical speed is $-mg/k$, and the $y$ solution carries $y_0$ in its constant.
- A "show that" target can contain a typo (2024 Q1 does). Check with numbers before bending your working.
- Cars: both start at rest, impact time comes from the cubic, wreckage velocity is total momentum divided by the combined mass.
- Tunnel: half a period for north to south, and $\approx42.2$ minutes from the arithmetic, not the printed $42.4$.
- Marks to minutes: 25 marks in 70 minutes is 2.8 minutes per mark, so a 3-mark part should not take more than about 8 minutes.

## See also

- [[APM01B1_Notes_S2_Dynamics]]
- [[APM01B1_Proofs_ST2]]
- [[APM01B1_Summary_ST2]]
