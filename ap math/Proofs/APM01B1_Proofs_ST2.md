---
module: APM01B1
topic: Proofs for ST2
tags: [theorem, formula]
---

# APM01B1 — Proofs for ST2

Every theorem or formula covered whose derivation was actually shown in some source, collected for memorisation. Each is labelled by where it came from; unlike ST1, sources here are mixed (personal notebook, the official Chapter 4 course notes, and two tutorial-driven additions), so each entry says which.

## General solution for a time-dependent force

#formula

(source: personal notebook, incline worked example, $\vec F=F_0e^{-t}\hat x$, pages 34 then 1)

For an object on an incline at angle $\theta$, with the perpendicular component of gravity cancelled by the normal force, only the along-slope equation survives:

$$m\ddot x = F_0e^{-t}-mg\sin\theta \;\Rightarrow\; \ddot x = \frac{F_0}{m}e^{-t}-g\sin\theta$$

Integrate once:

$$\dot x = -\frac{F_0}{m}e^{-t}-(g\sin\theta)t+v_0$$

Integrate again:

$$x(t) = \frac{F_0}{m}e^{-t}-\tfrac12(g\sin\theta)t^2+v_0t+r_0$$

$$\therefore\ \text{for general } \vec F(t):\quad \vec x(t) = \frac1m\int\!\left(\int\vec F(t)\,dt\right)dt+\vec v_0t+\vec r_0 \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Time-dependent force: an incline worked example]])

## Terminal velocity from the force balance

#formula

(source: personal notebook, friction/terminal-velocity setup)

A body falling with linear drag: $m\ddot z=-mg-k\dot z$. At terminal velocity $\ddot z=0$:

$$0 = -mg-k\dot z_{term} \;\Rightarrow\; \therefore\ \dot z_{term}=-\frac{mg}{k} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Setup and terminal velocity]])

## Separable-variables solution of $\dot z=-kz+C$

#theorem

(source: personal notebook, pages 2 and 25, the "ignore gravity for now" warm-up finished later in the notebook)

$$\frac{dz}{dt}=-kz+C \;\Rightarrow\; \frac{dz}{-kz+C}=dt$$

Substitute $Z=-kz+C$, $dZ=-k\,dz$:

$$-\frac1k\int\frac{dZ}{Z}=\int dt \;\Rightarrow\; -\frac1k\ln Z = t+C_2 \;\Rightarrow\; Z=Ke^{-kt}$$

$$-kz+C = Ke^{-kt}$$

$$\therefore\ z(t) = \frac{C}{k}-\frac{K}{k}e^{-kt} \qquad\blacksquare$$

Any equation of the form $\dot z=-kz+(\text{const})$ produces an $e^{-kt}$ solution, this is the general pattern, not specific to this example.

(see: [[APM01B1_Notes_S2_Dynamics#Solving for $z(t)$: separation of variables]])

## $v\,dv/dz$ reduction for a speed-dependent force

#theorem

(source: personal notebook, pages 3-4, the "express acceleration in terms of displacement" derivation)

By the chain rule, writing $v=\dot z$:

$$a = \frac{d^2z}{dt^2} = \frac{dv}{dt} = \frac{dv}{dz}\cdot\frac{dz}{dt} = v\frac{dv}{dz}$$

Applied to $\ddot z=-g-\frac km\dot z$:

$$v\frac{dv}{dz} = -g-\frac km v \;\Rightarrow\; \int\frac{v\,dv}{g+\frac km v} = -\int dz$$

Substitute $u=g+\frac km v$, $du=\frac km dv$, $v=\frac mk(u-g)$:

$$\int\frac{v\,dv}{g+\frac km v} = \frac mk\int\left(1-\frac gu\right)du = \frac mk\big(u-g\ln u\big)$$

$$\therefore\ \frac mk\left[g+\frac km v - g\ln\!\left(g+\frac km v\right)\right]_{v_0}^{v} = -(z-z_0) \qquad\blacksquare$$

An implicit relation between $v$ and $z$, not every $F(v)$ case reduces to an explicit closed form.

(see: [[APM01B1_Notes_S2_Dynamics#Solving for $v(z)$: the $v\,dv/dz$ trick]])

## SHM ansatz, $\omega=\sqrt{k/m}$

#theorem

(source: personal notebook, page 26, spring force, "let's guess" derivation)

$\ddot\xi=-\frac km\xi$ (spring force, origin shifted to natural length). Guess $\xi(t)=A\cos\omega t+B\sin\omega t$:

$$\ddot\xi = -A\omega^2\cos\omega t-B\omega^2\sin\omega t = -\omega^2\xi$$

Substituting into the original equation:

$$-\omega^2(A\cos\omega t+B\sin\omega t) = -\frac km(A\cos\omega t+B\sin\omega t) \;\Rightarrow\; \frac km-\omega^2=0$$

$$\therefore\ \omega=\sqrt{\frac km} \qquad\blacksquare$$

```tikz
\begin{document}
\begin{tikzpicture}[scale=1]
  \draw[->] (0,0) -- (6,0) node[right] {$t$};
  \draw[->] (0,-1.5) -- (0,1.5) node[above] {$\xi$};
  \draw[thick, blue, domain=0:6, samples=80] plot (\x, {cos(\x*120)});
\end{tikzpicture}
\end{document}
```

The ansatz only works for this specific $\omega$; $A,B$ are then fixed by initial/boundary conditions.

(see: [[APM01B1_Notes_S2_Dynamics#The ansatz method]])

## Conservation of angular momentum for a central force, $r^2\dot\theta=h$

#theorem

(source: personal notebook, pages 6-7, gravity central-force derivation)

Central force in polar coordinates gives two component equations; the $\hat\theta$ one is zero (no tangential force):

$$r\ddot\theta+2\dot r\dot\theta = 0$$

Recognise this as a product rule run backwards:

$$\frac{d}{dt}(r^2\dot\theta) = r^2\ddot\theta+2r\dot r\dot\theta = r(r\ddot\theta+2\dot r\dot\theta) = r\cdot 0 = 0$$

$$\therefore\ r^2\dot\theta = h = \text{const} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Worked example: central (inverse-square) force]])

## Energy conservation for the inverse-square (gravitational) central force

#formula

(source: personal notebook, pages 7-9)

Starting from the radial equation with $h$ substituted, $\ddot r-\frac{h^2}{r^3}=-\frac{GM}{r^2}$, multiply by $\dot r$ and use $\dot r\ddot r = v\,dv/dr$ (with $v\equiv\dot r$):

$$\frac{d}{dr}\!\left(\frac{v^2}{2}\right) = \frac{h^2}{r^3}-\frac{GM}{r^2} \;\Rightarrow\; \frac12v^2 = -\frac{h^2}{2r^2}+\frac{GM}{r}+C$$

Multiply by $m$ and regroup the radial and tangential kinetic terms against the potential energy:

$$\therefore\ \left(\frac12mv^2+\frac{h^2m}{2r^2}\right)-\frac{GMm}{r} = E \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Worked example: central (inverse-square) force]])

## Torque and angular momentum for a charge in a magnetic field

#formula

(source: personal notebook, pages 9, 12-14, Lorentz force worked in polar coordinates)

$\vec F=q(\vec v\times\vec B)$ with $\vec B=B\hat z$, $\vec v=\dot r\hat r+r\dot\theta\hat\theta$:

$$\vec F = Bq\big[\dot r(\hat r\times\hat z)+r\dot\theta(\hat\theta\times\hat z)\big] = Bqr\dot\theta\,\hat r-Bq\dot r\,\hat\theta$$

Moment about the origin:

$$\vec M = \vec r\times\vec F = r\hat r\times(Bqr\dot\theta\,\hat r-Bq\dot r\,\hat\theta) = -Bqr\dot r\,(\hat r\times\hat\theta) = -Bqr\dot r\,\hat z$$

With $\vec H=mr^2\dot\theta\,\hat z$ and $d\vec H/dt=\vec M$:

$$\frac{d}{dt}(mr^2\dot\theta) = -Bqr\dot r = -\frac{Bq}{2}\frac{d}{dt}(r^2)$$

$$\therefore\ mr^2\dot\theta+\frac{Bqr^2}{2} = C \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Further examples in polar coordinates: circular motion in a magnetic field]])

## Angular momentum theorem, $d\vec H/dt=\vec M$

#theorem

(source: personal notebook, page 30)

$\vec H=\vec r\times\vec p$. Differentiate:

$$\frac{d\vec H}{dt} = \dot{\vec r}\times\vec p+\vec r\times\dot{\vec p} = (\vec r\times m\dot{\vec r})+\vec r\times\vec F$$

The first term vanishes ($\dot{\vec r}\times\dot{\vec r}=\vec 0$, since $\vec p=m\dot{\vec r}$):

$$\therefore\ \frac{d\vec H}{dt} = \vec r\times\vec F = \vec M \qquad\blacksquare$$

$\vec H,\vec M$ must be measured about the same fixed point, any fixed point.

(see: [[APM01B1_Notes_S2_Dynamics#Angular momentum and the rotational form of N2]])

## Variable-mass (rocket) equation of motion

#formula

(source: personal notebook, page 9, $m(t)=m_0e^{-\lambda t}$, gravity only)

Momentum form, $\frac{d}{dt}(mv)=-mg$. Differentiate the product directly:

$$m\dot v+\dot m v = -mg \;\Rightarrow\; \dot v = -\frac{\dot m}{m}v-g$$

With $\dot m/m=-\lambda$:

$$\dot v = \lambda v-g$$

Solve with integrating factor $e^{-\lambda t}$: $\frac{d}{dt}(ve^{-\lambda t}) = -ge^{-\lambda t}$, so $ve^{-\lambda t}=\frac{g}{\lambda}e^{-\lambda t}+C$:

$$\therefore\ v(t) = \frac{g}{\lambda}+\left(v_0-\frac{g}{\lambda}\right)e^{\lambda t} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Worked example: rocket with exponentially decaying mass]])

## Impulse, $\Delta\vec p=\int\vec F\,dt$

#formula

(source: personal notebook, page 30, integrating the momentum form directly)

$$\frac{d\vec p}{dt} = \vec F(t) \;\Rightarrow\; \int_{\vec p_0}^{\vec p_1}d\vec p = \int_{t_0}^{t}\vec F(t')\,dt'$$

$$\therefore\ \Delta\vec p = \int_{t_0}^{t}\vec F(t')\,dt' \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Impulse]])

## (added) Elastic collision formulas

#formula

(source: not in the personal notebook or `Notes_-_Chapter_4.pdf`; derived here to answer Tutorial 9 Q2, from momentum conservation for a two-particle system plus the elastic-collision assumption)

Particle 1 (speed $u$) strikes stationary particle 2, momentum and kinetic energy both conserved:

$$m_1u = m_1v_1+m_2v_2 \qquad\qquad m_1u^2 = m_1v_1^2+m_2v_2^2$$

Rearranged: $m_1(u-v_1)=m_2v_2$ and $m_1(u-v_1)(u+v_1)=m_2v_2^2$. Dividing the second by the first (valid whenever $v_2\neq 0$):

$$u+v_1 = v_2$$

Substituting back into the momentum equation:

$$\therefore\ v_1 = \frac{m_1-m_2}{m_1+m_2}u, \qquad v_2 = \frac{2m_1}{m_1+m_2}u \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#(added) Conservation of momentum for a system of two particles, and collisions]])

## (added) Coupled two-mass spring system, reduced mass

#formula

(source: not in the personal notebook or `Notes_-_Chapter_4.pdf`; derived here to answer Tutorial 8 Q2, using the centre-of-mass/relative-displacement substitution the tutorial itself hints at)

$$m_1\ddot x_1 = k(x_2-x_1-L_0), \qquad m_2\ddot x_2 = -k(x_2-x_1-L_0)$$

Define $x_d=x_2-x_1$. Subtract the first equation (divided by $m_1$) from the second (divided by $m_2$):

$$\ddot x_d = -k\left(\frac1{m_1}+\frac1{m_2}\right)(x_d-L_0)$$

Define the reduced mass $\mu=\dfrac{m_1m_2}{m_1+m_2}$, so $\dfrac1\mu=\dfrac1{m_1}+\dfrac1{m_2}$:

$$\ddot x_d = -\frac{k}{\mu}(x_d-L_0)$$

$$\therefore\ \omega = \sqrt{\frac{k}{\mu}} = \sqrt{\frac{k(m_1+m_2)}{m_1m_2}}, \qquad T=2\pi\sqrt{\frac{m_1m_2}{k(m_1+m_2)}} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#(added) Worked example: two masses coupled by a spring]])

## (added) Simple pendulum, $\ddot\theta=-\frac gl\sin\theta$

#theorem

(source: `Notes_-_Chapter_4.pdf`, §4.7.1, not in the personal notebook)

Tension contributes no moment about the pivot $O$ (always directed toward $O$), so $\vec M_O=\vec r\times m\vec g=mgl\sin\theta\,(-\hat z)$. With $\vec H_O=ml^2\dot\theta\,\hat z$ and $\vec M_O=d\vec H_O/dt$:

$$ml^2\ddot\theta = -mgl\sin\theta$$

$$\therefore\ \ddot\theta = -\frac gl\sin\theta \qquad\blacksquare$$

For small $\theta$, $\sin\theta\approx\theta$, giving the SHM equation with $\omega=\sqrt{g/l}$, $T=2\pi\sqrt{l/g}$.

(see: [[APM01B1_Notes_S2_Dynamics#(added) Worked example: the simple pendulum]])

## (added) Angular impulse, $\vec J_O=\Delta\vec H_O$

#formula

(source: `Notes_-_Chapter_4.pdf`, §4.8, not in the personal notebook)

Integrate $\vec M_O=d\vec H_O/dt$ between $t_1,t_2$:

$$\int_{t_1}^{t_2}\vec M_O\,dt = \vec H_O(t_2)-\vec H_O(t_1)$$

$$\therefore\ \vec J_O \equiv \int_{t_1}^{t_2}\vec M_O\,dt = \Delta\vec H_O \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#(added) Definition]])
