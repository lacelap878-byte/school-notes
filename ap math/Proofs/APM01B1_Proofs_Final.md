---
module: APM01B1
topic: Proofs for the Final
tags: [theorem, formula]
---

# APM01B1 Proofs for the Final

Every theorem or formula from sessions S1 to S3 whose derivation was actually shown in some source, collected for memorisation. Each entry says where it came from. Results already in the ST1 and ST2 proof files are carried over unchanged, so this file is the only one needed for the final. Entries taken from a past-paper memo are labelled with the paper and question.

Statement-only entries say so plainly: a proof that no source shows is never constructed here.

## Kinematics results

### Time derivatives of the polar unit vectors

#theorem

(source: lecture photo, polar unit vector derivation)

$$\hat r = \cos\theta\,\hat x+\sin\theta\,\hat y, \qquad \hat\theta=-\sin\theta\,\hat x+\cos\theta\,\hat y$$

Differentiate with the chain rule, $\theta=\theta(t)$:

$$\frac{d\hat r}{dt} = -\dot\theta\sin\theta\,\hat x+\dot\theta\cos\theta\,\hat y = \dot\theta(-\sin\theta\,\hat x+\cos\theta\,\hat y) = \dot\theta\,\hat\theta$$

$$\frac{d\hat\theta}{dt} = -\dot\theta\cos\theta\,\hat x-\dot\theta\sin\theta\,\hat y = -\dot\theta(\cos\theta\,\hat x+\sin\theta\,\hat y) = -\dot\theta\,\hat r$$

$$\therefore \frac{d\hat r}{dt}=\dot\theta\,\hat\theta, \qquad \frac{d\hat\theta}{dt}=-\dot\theta\,\hat r \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Time derivatives of $\hat r$ and $\hat\theta$]])

### Velocity and acceleration in polar coordinates

#theorem

(source: lecture photo, Coriolis derivation)

Start from $\vec r = r(t)\,\hat r$, apply the product rule and the result above:

$$\vec v = \frac{d\vec r}{dt} = \dot r\,\hat r + r\frac{d\hat r}{dt} = \dot r\,\hat r + r\dot\theta\,\hat\theta$$

Differentiate again, product rule on each term, substituting both derivatives:

$$\vec a = \ddot r\,\hat r + \dot r\dot\theta\,\hat\theta + \dot r\dot\theta\,\hat\theta + r\ddot\theta\,\hat\theta - r\dot\theta^2\,\hat r$$

$$\therefore \vec a = (\ddot r-r\dot\theta^2)\hat r + (r\ddot\theta+2\dot r\dot\theta)\hat\theta \qquad\blacksquare$$

Four terms: $\ddot r$ radial, $r\ddot\theta$ angular, $-r\dot\theta^2$ centripetal, $2\dot r\dot\theta$ Coriolis.

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Velocity and acceleration in polar coordinates]])

### Time derivatives of the tangent and normal unit vectors

#theorem

(source: lecture photo, tangential-normal derivation with curvature)

$$\hat T = \cos\psi\,\hat x+\sin\psi\,\hat y, \qquad \hat n=-\sin\psi\,\hat x+\cos\psi\,\hat y$$

By the same cosine and sine differentiation pattern as the polar case, $\dfrac{d\hat T}{d\psi}=\hat n$ and $\dfrac{d\hat n}{d\psi}=-\hat T$. Define curvature by $\dfrac{d\psi}{ds}=\dfrac1\rho$. By the chain rule:

$$\frac{d\hat T}{dt} = \frac{d\hat T}{d\psi}\cdot\frac{d\psi}{ds}\cdot\frac{ds}{dt} = \hat n\cdot\frac1\rho\cdot v$$

$$\frac{d\hat n}{dt} = \frac{d\hat n}{d\psi}\cdot\frac{d\psi}{ds}\cdot\frac{ds}{dt} = -\hat T\cdot\frac1\rho\cdot v$$

$$\therefore \frac{d\hat T}{dt}=\frac v\rho\hat n, \qquad \frac{d\hat n}{dt}=-\frac v\rho\hat T \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Time derivatives of $\hat T$ and $\hat n$]])

### Acceleration in tangential-normal coordinates

#theorem

(source: lecture photo, "since $\vec v=v\hat T$" step)

$$\vec a = \frac{d\vec v}{dt} = \dot v\,\hat T + v\frac{d\hat T}{dt} = \dot v\,\hat T + v\cdot\frac v\rho\hat n$$

$$\therefore \vec a = \dot v\,\hat T + \frac{v^2}{\rho}\hat n \qquad\blacksquare$$

Reading off the radius of curvature at a point (source: 2025 Final Papers A, B and C memos, Q1 part e): since $a_n=\vec a\cdot\hat n=v^2/\rho$,

$$\rho = \frac{v^2}{\vec a\cdot\hat n}$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Acceleration in tangential-normal coordinates]])

### Product rule for the dot product

#theorem

(source: lecture photo)

$$\vec a\cdot\vec b = a_xb_x+a_yb_y+a_zb_z$$

Differentiate term by term with the scalar product rule:

$$\frac{d(\vec a\cdot\vec b)}{dt} = \left(\frac{da_x}{dt}b_x+\frac{da_y}{dt}b_y+\frac{da_z}{dt}b_z\right) + \left(a_x\frac{db_x}{dt}+a_y\frac{db_y}{dt}+a_z\frac{db_z}{dt}\right)$$

$$\therefore \frac{d(\vec a\cdot\vec b)}{dt} = \frac{d\vec a}{dt}\cdot\vec b + \vec a\cdot\frac{d\vec b}{dt} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Vector differentiation rules]])

### Path equation from Newton's second law with constant force

#formula

(source: lecture photo, $\vec F=-mg\hat z$, $\vec r(0)=\vec 0$, $\vec v(0)=\hat x+2\hat y+3\hat z$)

Integrate $m\ddot{\vec r}=\vec F$ once:

$$\dot{\vec r} = \frac{\vec Ft}{m}+\vec c, \qquad \vec c=\vec v(0)$$

Integrate a second time from $t=0$:

$$\vec r(t)-\vec r(0) = \frac{\vec Ft^2}{2m}+\vec v(0)\,t$$

Substituting the given data:

$$\therefore \vec r(t) = t\,\hat x+2t\,\hat y+\left(3t-\tfrac12 gt^2\right)\hat z \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Worked example: constant force, $\vec F = -mg\hat z$]])

### Angle identity from polar projections

#formula

Proof not shown in source, statement only. The derivation was left as an exercise and was never worked on the page. A version built from taught material sits in S1 under the (added) angle identity heading. It is not checked against the lecturer's own version.

$$\theta = \arccos\!\left(\frac{a\dot r+b\,r\dot\theta}{v^2}\right), \qquad \theta = \arcsin\!\left(\frac{b\dot r-a\,r\dot\theta}{v^2}\right)$$

Here $\vec v=a\hat x+b\hat y$ and $v^2=a^2+b^2$.

## Dynamics results

### General solution for a time-dependent force

#formula

(source: personal notebook, incline example $\vec F=F_0e^{-t}\hat x$)

With the perpendicular component of gravity cancelled by the normal force, only the along-slope equation survives:

$$m\ddot x = F_0e^{-t}-mg\sin\theta \;\Rightarrow\; \ddot x = \frac{F_0}{m}e^{-t}-g\sin\theta$$

$$\dot x = -\frac{F_0}{m}e^{-t}-(g\sin\theta)t+v_0, \qquad x(t) = \frac{F_0}{m}e^{-t}-\tfrac12(g\sin\theta)t^2+v_0t+r_0$$

$$\therefore\ \vec x(t) = \frac1m\int\!\left(\int\vec F(t)\,dt\right)dt+\vec v_0t+\vec r_0 \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Time-dependent force: an incline worked example]])

### Terminal velocity from the force balance

#formula

(source: personal notebook)

Falling with linear drag, $m\ddot z=-mg-k\dot z$. At terminal velocity $\ddot z=0$:

$$0 = -mg-k\dot z_{term} \;\Rightarrow\; \therefore\ \dot z_{term}=-\frac{mg}{k} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Setup and terminal velocity]])

### Exponential solution of the linear drag equation

#theorem

(source: personal notebook)

$$\frac{dz}{dt}=-kz+C \;\Rightarrow\; \frac{dz}{-kz+C}=dt$$

Substitute $Z=-kz+C$, $dZ=-k\,dz$:

$$-\frac1k\int\frac{dZ}{Z}=\int dt \;\Rightarrow\; Z=Ke^{-kt}$$

$$\therefore\ z(t) = \frac Ck-\frac Kk e^{-kt} \qquad\blacksquare$$

Any equation of the form $\dot z=-kz+(\text{const})$ produces an $e^{-kt}$ solution.

(see: [[APM01B1_Notes_S2_Dynamics#Solving for $z(t)$: separation of variables]])

### The v dv by dz reduction for a speed-dependent force

#theorem

(source: personal notebook)

By the chain rule, with $v=\dot z$:

$$a = \frac{dv}{dt} = \frac{dv}{dz}\cdot\frac{dz}{dt} = v\frac{dv}{dz}$$

Applied to $\ddot z=-g-\frac km\dot z$:

$$v\frac{dv}{dz} = -g-\frac km v \;\Rightarrow\; \int\frac{v\,dv}{g+\frac km v} = -\int dz$$

Substitute $u=g+\frac km v$, $du=\frac km dv$, $v=\frac mk(u-g)$:

$$\int\frac{v\,dv}{g+\frac km v} = \frac mk\int\left(1-\frac gu\right)du = \frac mk\big(u-g\ln u\big)$$

$$\therefore\ \frac mk\left[g+\frac km v - g\ln\!\left(g+\frac km v\right)\right]_{v_0}^{v} = -(z-z_0) \qquad\blacksquare$$

An implicit relation between $v$ and $z$. Not every $F(v)$ case reduces to an explicit closed form.

(see: [[APM01B1_Notes_S2_Dynamics#Solving for $v(z)$: the $v\,dv/dz$ trick]])

### Separable force of position and speed

#theorem

(source: personal notebook and ST2 2012 working)

Claim: if $F_x=f_1(v_x)\,g_1(x)$ then $m\displaystyle\int\frac{v_x}{f_1(v_x)}\,dv_x=\int g_1(x)\,dx$.

Newton's second law gives $m\ddot x=f_1(v_x)g_1(x)$. By the chain rule

$$\ddot x=\frac{dv_x}{dt}=\frac{dv_x}{dx}\frac{dx}{dt}=v_x\frac{dv_x}{dx}$$

so $m\,v_x\dfrac{dv_x}{dx}=f_1(v_x)g_1(x)$. Divide by $f_1(v_x)$ and integrate in $x$: the left side depends only on $v_x$ and the right side only on $x$. $\blacksquare$

Turning point for $F_x=-cx^n$ ($f_1=1$):

$$\tfrac12 m v_x^2=\tfrac12 m v_{0x}^2-\frac{c\,x^{n+1}}{n+1}, \qquad x^*=\left(\frac{(n+1)\,m\,v_{0x}^2}{2c}\right)^{1/(n+1)}$$

Symbols: $c$ in N m$^{-n}$, $m$ in kg, $v_{0x}$ in m/s.

(see: [[APM01B1_Notes_S2_Dynamics#(added) Force depending on both $v$ and $x$: the separable chain rule]])

### Cubic drag in time form

#formula

(source: 2025 Final Paper B memo, Q4 part b; the position form is in the S3 note)

$F=-kv^3$ along $\hat x$ gives $\ddot x=-\dfrac km\dot x^3$. Divide by $\dot x^3$ and integrate in time:

$$\frac1{\dot x^3}\frac{d\dot x}{dt}=-\frac km \;\Rightarrow\; \int_{\dot x_0}^{\dot x}\frac{d\dot x}{\dot x^3}=-\frac km\int_0^t dt$$

$$-\frac1{2\dot x^2}+\frac1{2\dot x_0^2}=-\frac{kt}{m}$$

$$\therefore\ \dot x^2=\frac{m\dot x_0^2}{m+2k\dot x_0^2\,t} \qquad\blacksquare$$

Units: $k$ in kg s m$^{-2}$, so that $k\dot x_0^2t$ has the units of $m$ (kg). In the paper $k=0.03$, $m=100$ kg, $\dot x_0=100$ m/s and $t=10$ s, so $2k\dot x_0^2t=6000$ kg and $\dot x^2\approx163.9$ m$^2$/s$^2$.

N.B the memo's kinetic energy at $t=10$ s is printed as $4.98\times10^5$ J. Adding $\dot y^2=(gt)^2\approx9621.6$ gives $T=\tfrac12m(\dot x^2+\dot y^2)\approx4.89\times10^5$ J, so the printed value looks like a swapped digit.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Force proportional to speed cubed]])

### The simple harmonic motion ansatz

#theorem

(source: personal notebook)

$\ddot\xi=-\frac km\xi$ with the origin shifted to the natural length. Guess $\xi(t)=A\cos\omega t+B\sin\omega t$:

$$\ddot\xi = -\omega^2\xi$$

Substitute into the original equation:

$$-\omega^2(A\cos\omega t+B\sin\omega t) = -\frac km(A\cos\omega t+B\sin\omega t) \;\Rightarrow\; \frac km-\omega^2=0$$

$$\therefore\ \omega=\sqrt{\frac km} \qquad\blacksquare$$

$A$ and $B$ come from the initial conditions.

(see: [[APM01B1_Notes_S2_Dynamics#The ansatz method]])

### Conservation of angular momentum for a central force

#theorem

(source: personal notebook)

A central force has no $\hat\theta$ component, so the $\hat\theta$ equation is $r\ddot\theta+2\dot r\dot\theta=0$. Recognise a product rule run backwards:

$$\frac{d}{dt}(r^2\dot\theta) = r^2\ddot\theta+2r\dot r\dot\theta = r(r\ddot\theta+2\dot r\dot\theta) = 0$$

$$\therefore\ r^2\dot\theta = h = \text{const} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Worked example: central (inverse-square) force]])

### Energy equation for the inverse-square central force

#formula

(source: personal notebook)

From the radial equation with $h$ substituted, $\ddot r-\frac{h^2}{r^3}=-\frac{GM}{r^2}$. Multiply by $\dot r$ and use $\dot r\ddot r=v\,dv/dr$ with $v\equiv\dot r$:

$$\frac{d}{dr}\!\left(\frac{v^2}{2}\right) = \frac{h^2}{r^3}-\frac{GM}{r^2} \;\Rightarrow\; \frac12v^2 = -\frac{h^2}{2r^2}+\frac{GM}{r}+C$$

Multiply by $m$ and regroup:

$$\therefore\ \left(\frac12mv^2+\frac{h^2m}{2r^2}\right)-\frac{GMm}{r} = E \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Worked example: central (inverse-square) force]])

### Angular momentum theorem

#theorem

(source: personal notebook)

With $\vec H=\vec r\times\vec p$:

$$\frac{d\vec H}{dt} = \dot{\vec r}\times\vec p+\vec r\times\dot{\vec p} = (\vec r\times m\dot{\vec r})+\vec r\times\vec F$$

The first term vanishes since $\dot{\vec r}\times\dot{\vec r}=\vec 0$:

$$\therefore\ \frac{d\vec H}{dt} = \vec r\times\vec F = \vec M \qquad\blacksquare$$

$\vec H$ and $\vec M$ must be measured about the same fixed point.

(see: [[APM01B1_Notes_S2_Dynamics#Angular momentum and the rotational form of N2]])

### Torque and angular momentum for a charge in a magnetic field

#formula

(source: personal notebook)

$\vec F=q(\vec v\times\vec B)$ with $\vec B=B\hat z$ and $\vec v=\dot r\hat r+r\dot\theta\hat\theta$:

$$\vec F = Bqr\dot\theta\,\hat r-Bq\dot r\,\hat\theta$$

Moment about the origin:

$$\vec M = \vec r\times\vec F = -Bqr\dot r\,(\hat r\times\hat\theta) = -Bqr\dot r\,\hat z$$

With $\vec H=mr^2\dot\theta\,\hat z$ and $d\vec H/dt=\vec M$:

$$\frac{d}{dt}(mr^2\dot\theta) = -Bqr\dot r = -\frac{Bq}{2}\frac{d}{dt}(r^2)$$

$$\therefore\ mr^2\dot\theta+\frac{Bqr^2}{2} = C \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Further examples in polar coordinates: circular motion in a magnetic field]])

### Variable-mass equation of motion

#formula

(source: personal notebook, $m(t)=m_0e^{-\lambda t}$, gravity only)

Momentum form $\frac{d}{dt}(mv)=-mg$. Differentiate the product:

$$m\dot v+\dot m v = -mg \;\Rightarrow\; \dot v = -\frac{\dot m}{m}v-g = \lambda v-g$$

Integrating factor $e^{-\lambda t}$ gives $\frac{d}{dt}(ve^{-\lambda t})=-ge^{-\lambda t}$, so $ve^{-\lambda t}=\frac g\lambda e^{-\lambda t}+C$:

$$\therefore\ v(t) = \frac g\lambda+\left(v_0-\frac g\lambda\right)e^{\lambda t} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Worked example: rocket with exponentially decaying mass]])

### Rocket with thrust in tangential-normal coordinates

#theorem

(source: 2025 Final Paper A memo, Q4)

Setup given in the question: thrust $\vec F_{thrust}=\dot m(v-v_e)\hat\tau$ with constant exhaust speed $v_e$, gravity $-mg$ resolved along the path as $-mg\cos\vartheta\,\hat\tau+mg\sin\vartheta\,\hat n$, and $m(t)=m_0e^{-kt}$.

Start from $d\vec p/dt=\vec F$ with $\vec p=m\vec v=mv\hat\tau$:

$$\frac{d\vec p}{dt}=\dot m v\hat\tau+m\left(\dot v\hat\tau+\frac{v^2}{\rho}\hat n\right)$$

Equate to the forces. The $\dot m v\hat\tau$ cancels against the matching part of the thrust:

$$m\left(\dot v\hat\tau+\frac{v^2}{\rho}\hat n\right)=-\dot m v_e\hat\tau-mg\cos\vartheta\,\hat\tau+mg\sin\vartheta\,\hat n$$

Match components, with $\dfrac{v^2}{\rho}=v^2\dfrac{d\vartheta}{ds}=v\dfrac{d\vartheta}{dt}$:

$$\dot v=-\frac{\dot m}{m}v_e-g\cos\vartheta, \qquad \dot\vartheta=\frac gv\sin\vartheta$$

With $\dot m/m=-k$, divide the first by the second, $\dfrac{dv}{d\vartheta}=\dfrac{\dot v}{\dot\vartheta}$:

$$\frac{dv}{d\vartheta}=\frac{kv_e-g\cos\vartheta}{g\sin\vartheta}\,v=\frac{kv\,v_e}{g}\csc\vartheta-v\cot\vartheta$$

Separate with $\alpha=kv_e/g$ and integrate, using $\int\csc\vartheta\,d\vartheta=\ln|\csc\vartheta-\cot\vartheta|$ and $\int\cot\vartheta\,d\vartheta=\ln|\sin\vartheta|=-\ln|\csc\vartheta|$:

$$\int\frac{dv}{v}=\int(\alpha\csc\vartheta-\cot\vartheta)\,d\vartheta \;\Rightarrow\; \ln v=\alpha\ln|\csc\vartheta-\cot\vartheta|+\ln|\csc\vartheta|+A$$

Since $\csc\vartheta-\cot\vartheta=\dfrac{1-\cos\vartheta}{\sin\vartheta}=\tan\dfrac\vartheta2$:

$$\therefore\ v(\vartheta)=C\csc\vartheta\,\tan^{\alpha}\!\left(\frac\vartheta2\right),\qquad \alpha=\frac{kv_e}{g} \qquad\blacksquare$$

The vertical-launch version with real thrust is worked in [[APM01B1_Extra_Examples_Dynamics]].

### Impulse

#formula

(source: personal notebook)

$$\frac{d\vec p}{dt} = \vec F(t) \;\Rightarrow\; \int_{\vec p_0}^{\vec p_1}d\vec p = \int_{t_0}^{t}\vec F(t')\,dt'$$

$$\therefore\ \Delta\vec p = \int_{t_0}^{t}\vec F(t')\,dt' \qquad\blacksquare$$

For a constant force $\Delta\vec p=\vec F\,\Delta t$.

(see: [[APM01B1_Notes_S2_Dynamics#Impulse]])

### Elastic collision formulas

#formula

(source: added in S2 to answer Tutorial 9, from momentum conservation plus the elastic assumption)

Particle 1 (speed $u$) strikes stationary particle 2. Momentum and kinetic energy are both conserved:

$$m_1u = m_1v_1+m_2v_2 \qquad\qquad m_1u^2 = m_1v_1^2+m_2v_2^2$$

Rearranged: $m_1(u-v_1)=m_2v_2$ and $m_1(u-v_1)(u+v_1)=m_2v_2^2$. Dividing the second by the first (valid whenever $v_2\neq0$):

$$u+v_1 = v_2$$

Substitute back into the momentum equation:

$$\therefore\ v_1 = \frac{m_1-m_2}{m_1+m_2}u, \qquad v_2 = \frac{2m_1}{m_1+m_2}u \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#(added) Conservation of momentum for a system of two particles, and collisions]])

### Perfectly inelastic collision

#formula

(source: added in S2, same tutorial)

The particles stick together with common final velocity $v_f$. Momentum is conserved, kinetic energy is not:

$$m_1u=(m_1+m_2)v_f \;\Rightarrow\; v_f=\frac{m_1}{m_1+m_2}u$$

$$\Delta KE=\tfrac12m_1u^2-\tfrac12(m_1+m_2)v_f^2<0$$

The same momentum balance with unequal speeds gives $\vec v_f=(m_1\vec v_1+m_2\vec v_2)/(m_1+m_2)$. For equal masses, $\vec v_f=(\vec p_1+\vec p_2)/(2m)$.

(see: [[APM01B1_Notes_S2_Dynamics#(added) Conservation of momentum for a system of two particles, and collisions]])

### Coupled two-mass spring system

#formula

(source: added in S2 to answer Tutorial 8)

$$m_1\ddot x_1 = k(x_2-x_1-L_0), \qquad m_2\ddot x_2 = -k(x_2-x_1-L_0)$$

Adding the two gives $\ddot x_c=0$ for the centre of mass. Define $x_d=x_2-x_1$ and subtract the first equation (divided by $m_1$) from the second (divided by $m_2$):

$$\ddot x_d = -k\left(\frac1{m_1}+\frac1{m_2}\right)(x_d-L_0)$$

With the reduced mass $\mu=\dfrac{m_1m_2}{m_1+m_2}$:

$$\therefore\ \omega = \sqrt{\frac{k}{\mu}} = \sqrt{\frac{k(m_1+m_2)}{m_1m_2}}, \qquad T=2\pi\sqrt{\frac{m_1m_2}{k(m_1+m_2)}} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#(added) Worked example: two masses coupled by a spring]])

### Simple pendulum

#theorem

(source: Chapter 4 course notes, via S2)

Tension is always directed toward the pivot $O$, so it has no moment about $O$ and $\vec M_O=\vec r\times m\vec g=mgl\sin\theta\,(-\hat z)$. With $\vec H_O=ml^2\dot\theta\,\hat z$ and $\vec M_O=d\vec H_O/dt$:

$$ml^2\ddot\theta = -mgl\sin\theta$$

$$\therefore\ \ddot\theta = -\frac gl\sin\theta \qquad\blacksquare$$

For small $\theta$, $\sin\theta\approx\theta$, giving $\omega=\sqrt{g/l}$ and $T=2\pi\sqrt{l/g}$.

(see: [[APM01B1_Notes_S2_Dynamics#(added) Worked example: the simple pendulum]])

### Angular impulse

#formula

(source: Chapter 4 course notes, via S2)

$$\int_{t_1}^{t_2}\vec M_O\,dt = \vec H_O(t_2)-\vec H_O(t_1)$$

$$\therefore\ \vec J_O \equiv \int_{t_1}^{t_2}\vec M_O\,dt = \Delta\vec H_O \qquad\blacksquare$$

(see: [[APM01B1_Notes_S2_Dynamics#Angular impulse]])

### Beam in equilibrium with a pulley

#formula

(source: 2025 Final Paper C memo, Q4; the S2 note names pulleys and beams but never works one)

A beam pivots at $O$. A mass $m_1$ hangs at distance $\ell$ to the left. At distance $\lambda\ell$ to the right hangs a pulley carrying a rope with $m_1$ on one side and $m_2$ on the other. Find $\lambda$ for equilibrium.

Moments about $O$ must cancel, with $F_1$ the downward load at the left end and $F_2$ the downward load at the pulley:

$$\ell F_1-\lambda\ell F_2=0 \;\Rightarrow\; \lambda=\frac{F_1}{F_2}$$

Left end, $m_1$ in equilibrium: $F_1=m_1g$.

Pulley load: the rope pulls down on the pulley with $2T_3$, where $T_3$ is the rope tension, so $F_2=2T_3$.

Rope masses, Newton's second law on each, with the rope length fixed so $\ddot r_2=-\ddot r_3$:

$$m_1\ddot r_2=T_3-m_1g, \qquad -m_2\ddot r_2=T_3-m_2g$$

Subtract the two:

$$(m_1+m_2)\ddot r_2=(m_2-m_1)g \;\Rightarrow\; \ddot r_2=\frac{m_2-m_1}{m_1+m_2}g$$

Substitute back into $m_2\ddot r_3=T_3-m_2g$ with $\ddot r_3=-\ddot r_2$:

$$T_3=m_2(g-\ddot r_2)=\frac{2m_1m_2}{m_1+m_2}g, \qquad F_2=2T_3=\frac{4m_1m_2}{m_1+m_2}g$$

$$\therefore\ \lambda=\frac{m_1g}{F_2}=\frac{m_1+m_2}{4m_2} \qquad\blacksquare$$

N.B the beam can be in equilibrium while $m_2$ accelerates: only the tension in the pulley rope matters, not whether the masses are at rest.

## Multivariable results

### Chain rule along a path

#theorem

(source: lecture photos, personal notebook)

Take a path $\vec r(s)=x(s)\hat x+y(s)\hat y$. Along it $f$ is a function of $s$ alone. Start from the total change

$$df=\frac{\partial f}{\partial x}dx+\frac{\partial f}{\partial y}dy$$

and divide by $ds$:

$$\therefore\ \frac{df}{ds}=\frac{\partial f}{\partial x}\frac{dx}{ds}+\frac{\partial f}{\partial y}\frac{dy}{ds}=\vec\nabla f\cdot\frac{d\vec r}{ds} \qquad\blacksquare$$

For a straight path in the direction of a unit vector $\hat s$, with $\vec r=\vec r_0+s\hat s$, this is $\vec\nabla f\cdot\hat s$.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Chain rule along a path and the directional derivative]])

### Gradient is perpendicular to a level surface

#theorem

(source: lecture photos)

Take a surface $F(x,y,z)=c$ and a path $\vec r(s)$ lying on it. $F$ never changes along the path, so $dF/ds=0$. By the chain rule above:

$$\vec\nabla F\cdot\frac{d\vec r}{ds}=0$$

$d\vec r/ds$ is tangent to the surface and the path was arbitrary:

$$\therefore\ \vec\nabla F\ \text{is perpendicular to the surface} \qquad\blacksquare$$

Example from the pages: $F=x^2+y^2+z^2$ gives $\vec\nabla F=2x\hat x+2y\hat y+2z\hat z$, pointing radially across each sphere.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Level surfaces and the gradient]])

### Line integral of a gradient is path independent

#theorem

(source: lecture photos, and Chapter 5 course notes 5.7.2)

For $\psi=\psi(x,y,z)$ the total change is

$$d\psi=\frac{\partial\psi}{\partial x}dx+\frac{\partial\psi}{\partial y}dy+\frac{\partial\psi}{\partial z}dz=\vec\nabla\psi\cdot d\vec r$$

so from $A$ to $B$:

$$\int_A^B\vec\nabla\psi\cdot d\vec r=\int_A^B d\psi=\psi(\vec r_B)-\psi(\vec r_A)$$

For a closed path $A=B$:

$$\therefore\ \oint_\Gamma\vec\nabla\psi\cdot d\vec r=0 \qquad\blacksquare$$

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Integral of a gradient along a path]])

### Curl of a gradient is zero

#theorem

Proof not shown in source, statement only. The pages state it and use it as the conservative-force test.

$$\vec\nabla\times\left(\vec\nabla f\right)=\vec 0$$

In 2D, with $F_z=0$, the test reduces to $\dfrac{\partial F_y}{\partial x}-\dfrac{\partial F_x}{\partial y}=0$.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Testing for a conservative field with the curl]])

### Zero circulation implies a gradient field

#theorem

Proof not shown in source, statement only. Chapter 5 says "we can also prove the opposite" and moves on: if $\oint\vec a\cdot d\vec r=0$ for every closed curve, a scalar $\phi$ exists with $\vec a=\vec\nabla\phi$. Chapter 6 states that the three conditions (a scalar $\phi$ with $\vec F=\vec\nabla\phi$, path independence, zero circulation) are equivalent without showing the steps.

### Finding the potential, and detecting a non-conservative field

#formula

(source: Chapter 6 course notes, V6.4.1)

Suppose $\vec F=\vec\nabla\phi$. Compare components and integrate each partial derivative, keeping an unknown function of the other variables.

Field (a): $\vec F=(y,\ x+z,\ y)$

$$\frac{\partial\phi}{\partial x}=y,\quad\frac{\partial\phi}{\partial y}=x+z,\quad\frac{\partial\phi}{\partial z}=y$$

$$\phi=xy+f_1(y,z),\quad\phi=xy+yz+f_2(x,z),\quad\phi=yz+f_3(x,y)$$

All three describe the same function for $f_1=yz$, $f_2=0$, $f_3=xy$:

$$\therefore\ \phi=xy+yz \quad\text{and } \vec F \text{ is conservative} \qquad\blacksquare$$

Field (b): $\vec F=(yz,\ xz,\ y)$

$$\phi=xyz+g_1(y,z),\quad\phi=xyz+g_2(x,z),\quad\phi=yz+g_3(x,y)$$

No choice of $g_1,g_2,g_3$ makes these agree, because the third carries $yz$ while the first two carry $xyz$:

$$\therefore\ \vec F \text{ is not conservative} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Finding the scalar potential by partial integration]])

### Zero work around a closed loop is not enough

#theorem

(source: 2025 Final Paper B memo, Q2)

The field $\vec F=3xy\,\hat x+2\hat y$ is not conservative:

$$\vec\nabla\times\vec F=\left(\frac{\partial}{\partial x}(2)-\frac{\partial}{\partial y}(3xy)\right)\hat z=-3x\,\hat z\neq\vec 0$$

(the memo prints $+3x\,\hat z$, which drops a sign: the $\hat z$ component is $\partial F_y/\partial x-\partial F_x/\partial y=0-3x$. It is non-zero either way, so the conclusion stands).

Yet the work around the whole ellipse $\vec r=a\cos s\,\hat x+b\sin s\,\hat y$ is zero. With $d\vec r=(-a\sin s\,\hat x+b\cos s\,\hat y)\,ds$ and $\vec F=(3ab\sin s\cos s,\ 2)$:

$$W=\int\left(-3a^2b\sin^2s\cos s+2b\cos s\right)ds=\left[-a^2b\sin^3s+2b\sin s\right]$$

Over a full loop $\sin$ returns to its starting value, so $W=0$.

$$\therefore\ \text{a non-conservative force can still give zero work over one particular loop} \qquad\blacksquare$$

N.B conservative means zero work for every closed loop. One loop giving zero proves nothing. For this field the work from $(0,b)$ to $(a,0)$ along the quarter arc is $a^2b-2b$, which differs from the work along other routes.

## Work and energy results

### Work-energy theorem

#theorem

(source: Chapter 6 course notes, and lecture photos)

Start from $\vec F=m\,d\vec v/dt$ and $d\vec r=\vec v\,dt$:

$$W=\int\vec F\cdot d\vec r=\int m\frac{d\vec v}{dt}\cdot\vec v\,dt=\frac m2\int\frac{d}{dt}(\vec v\cdot\vec v)\,dt$$

because $\dfrac{d}{dt}(\vec v\cdot\vec v)=2\vec v\cdot\dfrac{d\vec v}{dt}$. The integrand no longer depends on the path:

$$\therefore\ W=\frac m2v_f^2-\frac m2v_0^2=\Delta T,\qquad T=\tfrac12mv^2 \qquad\blacksquare$$

This holds for every force, conservative or not, because it is the first integral of Newton's second law. For motion along $\hat x$, $\vec F\cdot d\vec r=F_x\,dx$ and the 1D form follows.

Units: $W$ and $T$ in J, $F$ in N, $m$ in kg, $v$ in m/s.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Kinetic energy from Newton's second law]])

### One-dimensional work-energy from v dv by dx

#formula

(source: lecture photos)

$$\ddot x=v\frac{dv}{dx}=\frac12\frac{d(v^2)}{dx}\;\Rightarrow\;F=m\ddot x=\frac{d}{dx}\left(\tfrac12mv^2\right)$$

With $F=-dU/dx$:

$$\Delta K=\int F\,dx=-\int\frac{dU}{dx}\,dx=-\Delta U$$

$$\therefore\ \Delta K+\Delta U=0 \qquad\blacksquare$$

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#One-dimensional link between v dv/dx and energy]])

### Work of a constant force, and a force perpendicular to the path

#formula

(source: Chapter 6 course notes, V6.2.1 and V6.2.2)

On the $x$-axis, $d\vec r=dx\,\hat x$, so $\vec F\cdot d\vec r=F_x\,dx$:

$$W=\int_{x_0}^{x_0+s}F_x\,dx=F_xs$$

For constant $\vec F$ between any two points, $W=\vec F\cdot\int d\vec r=\vec F\cdot\Delta\vec r$, which is independent of the path. A force perpendicular to the path has $\vec F\cdot d\vec r=0$ and does no work.

### Power

#formula

(source: lecture photos)

$$dW=\vec F\cdot d\vec r=\vec F\cdot\vec v\,dt \;\Rightarrow\; P=\frac{dW}{dt}=\vec F\cdot\vec v$$

Units: $P$ in W.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Power]])

### Magnetic force does no work

#formula

(source: lecture photos)

$$W=\int\vec F\cdot d\vec r=\int q(\vec v\times\vec B)\cdot\vec v\,dt=0$$

because $\vec v\times\vec B$ is perpendicular to $\vec v$. By $W=\Delta T$ the speed is unchanged.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Magnetic force does no work]])

### Potential energy of uniform gravity

#formula

(source: Chapter 6 course notes V6.4.2 and lecture photos)

From a reference height $y_0=0$, with $\vec F=-mg\hat y$:

$$V=-\int_0^y(-mg\hat y)\cdot dy\,\hat y=mgy$$

Check: $F=-\dfrac{dV}{dy}=-mg$.

Speed at height $h$ from launch speed $v_0$ (Chapter 6, V6.5.1), by $\Delta E=0$:

$$\tfrac12mv^2+mgh=\tfrac12mv_0^2 \;\Rightarrow\; v=\sqrt{v_0^2-2gh}$$

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Potential energy of uniform gravity]])

### Potential energy of a spring

#formula

(source: Chapter 6 course notes, V6.4.3; see [[APM01B1_Notes_S3_MultivariableWorkEnergy#Potential energy of a spring]])

The spring force is $\vec F=-kx\,\hat x$, always along the spring, so only a straight path in $x$ matters. From the natural length:

$$V=-\int_0^x(-kx')\,dx'=\frac{kx^2}{2}$$

Check that $F$ is conservative: $-\dfrac{dV}{dx}=-kx=F$. $\blacksquare$

$x$ is the extension or compression from the natural length.

### Conservation of mechanical energy

#theorem

(source: Chapter 6 course notes, 6.5)

For a conservative force and a reference point $P_0$:

$$T(\vec r_2)-T(\vec r_1)=\int_{\vec r_1}^{\vec r_2}\vec F\cdot d\vec r=\int_{\vec r_1}^{\vec r_0}\vec F\cdot d\vec r+\int_{\vec r_0}^{\vec r_2}\vec F\cdot d\vec r$$

The route through $\vec r_0$ is allowed because the work is path independent. With $V(\vec r)=-\int_{\vec r_0}^{\vec r}\vec F\cdot d\vec r$:

$$T(\vec r_2)-T(\vec r_1)=V(\vec r_1)-V(\vec r_2)$$

$$\therefore\ T(\vec r_2)+V(\vec r_2)=T(\vec r_1)+V(\vec r_1),\qquad E=T+V=\text{const} \qquad\blacksquare$$

Equivalent statement: $\vec F=-\vec\nabla V$ turns the work-energy theorem into $\Delta T=-\Delta V$.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Potential energy and conservation of mechanical energy]])

### Differentiating the energy gives Newton's second law

#theorem

(source: 2025 Final Papers A, B and C memos, Q6)

Write $E=T+V$ and differentiate, assuming $E$ is constant:

$$0=\frac{dE}{dt}=\frac{d}{dt}\left(\tfrac12m\vec v\cdot\vec v+V\right)=m\vec v\cdot\vec a+\frac{dV}{dx}\frac{dx}{dt}=v\left(ma+\frac{dV}{dx}\right)$$

The particle is moving, so $v\neq0$:

$$\therefore\ ma=-\frac{dV}{dx}=F \qquad\blacksquare$$

Three cases the papers set:

Spring on a smooth horizontal plane, $V=\tfrac12kx^2$:

$$E=\tfrac12mv^2+\tfrac12kx^2 \;\Rightarrow\; ma+kx=0 \;\Rightarrow\; ma=-kx$$

Near the surface of the Earth, $V=mgx$:

$$E=\tfrac12mv^2+mgx \;\Rightarrow\; ma+mg=0 \;\Rightarrow\; ma=-mg$$

Far from the surface, $V=-\dfrac{GMm}{r}$, with $v=\dot r$ and $a=\ddot r$:

$$E=\tfrac12mv^2-\frac{GMm}{r} \;\Rightarrow\; \dot r\left(m\ddot r+\frac{GMm}{r^2}\right)=0 \;\Rightarrow\; m\ddot r=-\frac{GMm}{r^2}$$

N.B Paper C's memo writes the far-gravity potential as $+GMm/r$ and then lands on $ma+mg=0$. The potential energy of an attractive inverse-square force is $-GMm/r$, so write that.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Potential energy of real gravity]])

### Potential energy of real gravity

#formula

(source: lecture photos)

$$F=-\frac{GMm}{(R+y)^2} \;\Rightarrow\; V(y)=-\int F\,dy=-\frac{GMm}{R+y}+V_0$$

Check: $-\dfrac{dV}{dy}=-\dfrac{GMm}{(R+y)^2}=F$. $G$ is the gravitational constant, $M$ the planet mass, $m$ the particle mass, $R$ the planet radius, $y$ the height above the surface.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Potential energy of real gravity]])

### Escape speed

#formula

(source: lecture photos)

Energy conservation from the surface with launch speed $v_0$:

$$\tfrac12mv_0^2-\frac{GMm}{R}=\tfrac12mv^2-\frac{GMm}{R+y}$$

Let $y\to\infty$ and require $v\to0$, with $g=GM/R^2$:

$$v_0^2-\frac{2GM}{R}=0 \;\Rightarrow\; \therefore\ v_{esc}=\sqrt{\frac{2GM}{R}}=\sqrt{2gR} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Escape speed]])

### Mitchell dark star radius

#formula

(source: lecture photos)

Set $v_0=c$ and $v=0$ in the escape condition:

$$v=\sqrt{v_0^2-\frac{2GM}{r}}=0 \;\Rightarrow\; r=\frac{2GM}{v_0^2}$$

$$\therefore\ r_s=\frac{2GM}{c^2} \qquad\blacksquare$$

A photon leaving a body this compact cannot escape.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Mitchell dark star]])

### Distance up a rough incline from the work-energy principle

#formula

(source: 2025 Final Paper A memo Q5 and Paper C memo Q1; Chapter 6 P6.3.2)

A block of mass $m$ is projected up an incline of angle $\theta$ with speed $v_0$, friction coefficient $\mu$. Take $\hat x$ up the slope and $\hat y$ perpendicular to it.

Perpendicular balance: $N=mg\cos\theta$. Friction opposes the motion: $\vec f=-\mu N\,\hat x$. Gravity along the slope: $-mg\sin\theta\,\hat x$. With $d\vec r=dx\,\hat x$:

$$W=\int_0^{d}\left(-mg\sin\theta-\mu mg\cos\theta\right)dx=-mg(\sin\theta+\mu\cos\theta)\,d$$

The block stops, so $W=\Delta T=0-\tfrac12mv_0^2$:

$$\therefore\ d=\frac{v_0^2}{2g(\sin\theta+\mu\cos\theta)} \qquad\blacksquare$$

The mass cancels. Down a slope, with the friction now acting up the slope and gravity helping, the block stops only if $\mu>\tan\theta$, and

$$d=\frac{v_0^2}{2g(\mu\cos\theta-\sin\theta)}$$

(this form is added, from the same working with the sign of gravity reversed; the 2023 supplementary memo uses it for $\mu=0.6$, $\theta=20^\circ$, $v_0=10$ m/s).

Numbers: Paper C ($v_0=10$, $\theta=\pi/4$, $\mu=\tfrac14$) gives $d=40\sqrt2/g\approx5.766$ m. Paper A ($v_0=5$, $\theta=30^\circ$, $\mu=\tfrac12$) gives $d\approx1.366$ m.

N.B the Paper C memo prints $200\sqrt2/g\approx28.83$ m. Its own line $-\frac{5mg}{4\sqrt2}x_B=-\tfrac12m\cdot100$ gives $x_B=40\sqrt2/g$, so the final division by $5$ was dropped. The 2023 supplementary memo's handwritten answer is hard to read; the formula above gives about $22.98$ m for that question.

### Particle leaves a smooth sphere

#formula

(source: Chapter 6 course notes V6.5.2, and lecture photos)

A particle starts at the top of a sphere of radius $R$ with speed $v_0$, $\theta$ measured from the vertical.

Radial equation (centripetal acceleration points inward):

$$N-mg\cos\theta=-\frac{mv^2}{R}$$

The normal force does no work, so $\Delta E=0$:

$$\tfrac12mv^2+mgR\cos\theta=\tfrac12mv_0^2+mgR \;\Rightarrow\; mv^2=mv_0^2+2mgR(1-\cos\theta)$$

Eliminate $v^2$:

$$N=3mg\cos\theta-2mg-\frac{mv_0^2}{R}$$

The particle leaves when $N=0$:

$$\therefore\ \cos\theta=\frac{2gR+v_0^2}{3gR} \qquad\blacksquare$$

From rest, $N=mg(3\cos\theta-2)$ and $\theta=\arccos\tfrac23\approx48.19^\circ$.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Particle on a sphere]])

### Rough slope with friction proportional to speed

#formula

(source: lecture photos, with the closing step added)

Block and bullet moving together, mass $m+M$, speed $V$ along the slope, friction $-\mu V$. Work-energy does not help here because the friction work needs $V(s)$, so use Newton's second law:

$$(m+M)\frac{d^2s}{dt^2}=-\big[(m+M)g\sin\theta+\mu V\big]$$

With $\dfrac{d^2s}{dt^2}=V\dfrac{dV}{ds}$:

$$V\frac{dV}{ds}=-g\sin\theta-\frac{\mu}{m+M}V$$

Substitute $u=g\sin\theta+\dfrac{\mu V}{m+M}$, so $V=\dfrac{m+M}{\mu}(u-g\sin\theta)$ and $dV=\dfrac{m+M}{\mu}du$, with $K=\left(\dfrac{m+M}{\mu}\right)^2$:

$$K\int\left(1-\frac{g\sin\theta}{u}\right)du=K\big[u-g\sin\theta\ln u\big]=-s+c$$

$V$ is not explicit, but $s$ in terms of $V$ is. At the top $V=0$, so $u=g\sin\theta$ (added):

$$\therefore\ s_{max}=\frac{(m+M)V_0}{\mu}-Kg\sin\theta\,\ln\!\left(1+\frac{\mu V_0}{(m+M)g\sin\theta}\right) \qquad\blacksquare$$

Check: as $\mu\to0$ this tends to $V_0^2/(2g\sin\theta)$.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Slope with friction proportional to speed]])

### Work done by drag around a circle

#formula

(source: lecture photos)

$\vec F=-k\vec v$ on $\vec r=R\cos\omega t\,\hat x+R\sin\omega t\,\hat y$:

$$W=\oint\vec F\cdot d\vec r=\int\vec F\cdot\frac{d\vec r}{dt}\,dt=\int-k\,\vec v\cdot\vec v\,dt$$

$$\vec v\cdot\vec v=R^2\omega^2 \;\Rightarrow\; \therefore\ W=-kR^2\omega^2\,t \qquad\blacksquare$$

Nonzero over a closed loop, so drag is not conservative. Units: $k$ in kg/s.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Work done by drag around a circle]])

## Oscillation and orbit results

### Tunnel through a planet

#theorem

(source: lecture photos, 2025 Final Paper C memo Q5, and Paper A memo Q3)

Inside a uniform-density planet only the mass within radius $r$ pulls the particle (spherical symmetry). Let the planet have mass $M$ and radius $R$:

$$M(r)=\rho\tfrac43\pi r^3=\frac{M}{\tfrac43\pi R^3}\cdot\tfrac43\pi r^3=M\left(\frac rR\right)^3$$

Newton's second law along $\hat r$:

$$m\ddot r=-\frac{GM(r)\,m}{r^2} \;\Rightarrow\; \ddot r=-\frac{GM}{R^3}\,r$$

With the surface gravity $g=GM/R^2$:

$$\therefore\ \ddot r=-\frac gR\,r,\qquad \omega=\sqrt{\frac gR} \qquad\blacksquare$$

This is the spring equation with a different constant, so the SHM ansatz applies. For a different planet, use that planet's surface gravity and radius: $\omega^2=g_{surf}/R_{planet}$.

Mars (Paper A): $g_{Mars}=g/3$ and $R_{Mars}=R/2$ give $\omega^2=\dfrac{2g}{3R}$, which matches the memo's $\ddot r=-\dfrac{2g}{3R}r$.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Tunnel through the Earth]])

### Time to fall to the centre is a quarter period

#formula

(source: 2025 Final Paper A memo, Q3 part d)

Falling from the surface to the centre is a quarter of one full cycle, because a full cycle goes surface to the far side and back:

$$t_{fall}=\frac T4=\frac{\pi}{2\omega}$$

For the Earth, $t=\dfrac\pi2\sqrt{\dfrac Rg}$. For Mars, with $\omega=\sqrt{2g/(3R)}$:

$$t_{fall}=\frac\pi2\sqrt{\frac{3R}{2g}}\approx1550.4\ \text{s}\approx25.84\ \text{min}\qquad(R=6371\ \text{km},\ g=9.81\ \text{m/s}^2)$$

### Surface speed needed from the centre

#formula

(source: 2025 Final Paper C memo, Q5 parts b and c)

From $\ddot r=-\dfrac gRr$, use $\ddot r=\dot r\dfrac{d\dot r}{dr}$ and separate:

$$\dot r\,d\dot r=-\frac gR\,r\,dr \;\Rightarrow\; \int_{v_0}^{0}\dot r\,d\dot r=-\frac gR\int_0^Rr\,dr$$

$$-\tfrac12v_0^2=-\frac gR\cdot\tfrac12R^2 \;\Rightarrow\; \therefore\ v_0=\sqrt{gR} \qquad\blacksquare$$

If $v_0<\sqrt{gR}$ the particle falls back down the hole.

### Mass of the Earth from the Moon's orbit

#formula

(source: lecture photos)

Circular orbit, so $r=d$ is constant and $\dot r=\ddot r=0$. The radial component of Newton's second law in polar form:

$$-\frac{GMm}{d^2}=m(\ddot r-r\dot\theta^2)=-m\,d\,\dot\theta^2$$

With $\dot\theta=2\pi/T$:

$$\therefore\ M=\frac{d^3\dot\theta^2}{G}=\frac{4\pi^2d^3}{GT^2} \qquad\blacksquare$$

With $d=3.8\times10^8$ m and $T=2.592\times10^6$ s this gives $M\approx4.8\times10^{24}$ kg.

(see: [[APM01B1_Notes_S3_MultivariableWorkEnergy#Moon orbiting Earth and the mass of the Earth]])
