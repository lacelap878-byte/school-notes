---
module: APM01B1
topic: Proofs for ST1
tags: [theorem, formula]
---

# APM01B1 — Proofs for ST1

Every theorem or formula covered whose derivation was actually shown in the source material, collected for memorisation. Each is labelled by where it came from.

## Time derivatives of $\hat r$ and $\hat\theta$

#theorem

(source: lecture photo, polar unit vector derivation, "For $\theta=\theta(t)$" boxed result)

$$\hat r = \cos\theta\,\hat x+\sin\theta\,\hat y, \qquad \hat\theta=-\sin\theta\,\hat x+\cos\theta\,\hat y$$

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.3]
  \draw[->] (-0.3,0) -- (3,0) node[right] {$x$};
  \draw[->] (0,-0.3) -- (0,3) node[above] {$y$};
  \draw[->, thick, blue] (0,0) -- (1.88,0.68) node[right] {$\hat r(\theta)$};
  \draw[->, thick, blue!60] (0,0) -- (1.41,1.41) node[above] {$\hat r(\theta+d\theta)$};
  \draw (0.5,0) arc (0:20:0.5);
  \node at (0.62,0.13) {$\theta$};
  \draw[->, thick, red, dashed] (1.88,0.68) -- (1.41,1.41) node[midway, right] {$d\hat r$};
\end{tikzpicture}
\end{document}
```

Differentiate with the chain rule, $\theta=\theta(t)$:

$$\frac{d\hat r}{dt} = -\dot\theta\sin\theta\,\hat x+\dot\theta\cos\theta\,\hat y = \dot\theta(-\sin\theta\,\hat x+\cos\theta\,\hat y) = \dot\theta\,\hat\theta$$

$$\frac{d\hat\theta}{dt} = -\dot\theta\cos\theta\,\hat x-\dot\theta\sin\theta\,\hat y = -\dot\theta(\cos\theta\,\hat x+\sin\theta\,\hat y) = -\dot\theta\,\hat r$$

$$\therefore \frac{d\hat r}{dt}=\dot\theta\,\hat\theta, \qquad \frac{d\hat\theta}{dt}=-\dot\theta\,\hat r \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Time derivatives of hat r and hat theta]] for surrounding context)

## Velocity and acceleration in polar coordinates

#theorem

(source: lecture photo, Coriolis derivation)

Starting from $\vec r = r(t)\,\hat r$, apply the product rule and substitute the boxed result above.

$$\vec v = \frac{d\vec r}{dt} = \dot r\,\hat r + r\frac{d\hat r}{dt} = \dot r\,\hat r + r\dot\theta\,\hat\theta$$

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.2]
  \draw[->] (-0.3,0) -- (3.5,0) node[right] {$x$};
  \draw[->] (0,-0.3) -- (0,3) node[above] {$y$};
  \draw[->, thick] (0,0) -- (2,1.5) node[above] {$\hat r$};
  \draw[->, thick] (0,0) -- (-1.5,2) node[above] {$\hat\theta$};
  \draw[->, thick, purple] (0,0) -- (1.2,2.4) node[right] {$\vec v$};
  \draw[dashed] (1.2,2.4) -- (1.68,1.26);
  \draw[dashed] (1.2,2.4) -- (-0.9,1.2);
  \node at (1.9,0.9) {$v_r\hat r$};
  \node at (-1.3,1.6) {$v_\theta\hat\theta$};
\end{tikzpicture}
\end{document}
```

Differentiate again, applying the product rule to each term and substituting both boxed derivatives:

$$\vec a = \frac{d\vec v}{dt} = \ddot r\,\hat r + \dot r\dot\theta\,\hat\theta + \dot r\dot\theta\,\hat\theta + r\ddot\theta\,\hat\theta - r\dot\theta^2\,\hat r$$

$$\therefore \vec a = (\ddot r-r\dot\theta^2)\hat r + (r\ddot\theta+2\dot r\dot\theta)\hat\theta \qquad\blacksquare$$

Four terms: $\ddot r$ radial, $r\ddot\theta$ angular, $-r\dot\theta^2$ centripetal, $2\dot r\dot\theta$ Coriolis.

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Velocity and acceleration in polar coordinates]])

## Time derivatives of $\hat T$ and $\hat n$

#theorem

(source: lecture photo, tangential-normal derivation with curvature $\rho$)

$$\hat T = \cos\psi\,\hat x+\sin\psi\,\hat y, \qquad \hat n=-\sin\psi\,\hat x+\cos\psi\,\hat y$$

With respect to arc length: $\dfrac{d\hat T}{d\psi}=\hat n$, $\dfrac{d\hat n}{d\psi}=-\hat T$ (by the same cosine/sine differentiation pattern as $\hat r,\hat\theta$ above).

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.1]
  \draw[thick] (0,0) to[out=15,in=200] (3.6,1.4);
  \draw[->, thick, blue] (0,0) -- (0.75,0.14);
  \draw[->, thick, blue] (3.6,1.4) -- (4.3,1.75);
  \node[left] at (-0.15,-0.05) {$\psi$};
  \node[right] at (4.4,1.85) {$\psi+\Delta\psi$};
  \node at (1.9,0.5) {$\Delta s$};
  \draw[dashed] (0,0) -- (0.9,-1.6);
  \draw[dashed] (3.6,1.4) -- (0.9,-1.6);
  \node at (1.55,-1.0) {$\rho$};
  \filldraw (0.9,-1.6) circle (1pt);
\end{tikzpicture}
\end{document}
```

Define curvature by $\dfrac{d\psi}{ds}=\dfrac{1}{\rho}$. By the chain rule:

$$\frac{d\hat T}{dt} = \frac{d\hat T}{d\psi}\cdot\frac{d\psi}{ds}\cdot\frac{ds}{dt} = \hat n\cdot\frac{1}{\rho}\cdot v$$

$$\frac{d\hat n}{dt} = \frac{d\hat n}{d\psi}\cdot\frac{d\psi}{ds}\cdot\frac{ds}{dt} = -\hat T\cdot\frac{1}{\rho}\cdot v$$

$$\therefore \frac{d\hat T}{dt}=\frac{v}{\rho}\hat n, \qquad \frac{d\hat n}{dt}=-\frac{v}{\rho}\hat T \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Time derivatives of hat T and hat n]])

## Acceleration in tangential-normal coordinates

#theorem

(source: lecture photo, tangential-normal derivation, "since $\vec v=v\hat T$" step)

Since $\vec v = v\hat T$, apply the product rule and substitute the result above:

$$\vec a = \frac{d\vec v}{dt} = \dot v\,\hat T + v\frac{d\hat T}{dt} = \dot v\,\hat T + v\cdot\frac{v}{\rho}\hat n$$

$$\therefore \vec a = \dot v\,\hat T + \frac{v^2}{\rho}\hat n \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Acceleration in tangential-normal coordinates]])

## Product rule for the dot product

#theorem

(source: lecture photo, "Proof $\vec a\cdot\vec b=a_xb_x+a_yb_y+a_zb_z$")

$$\vec a\cdot\vec b = a_xb_x+a_yb_y+a_zb_z$$

Differentiate term by term with the ordinary scalar product rule:

$$\frac{d(\vec a\cdot\vec b)}{dt} = \frac{da_x}{dt}b_x+a_x\frac{db_x}{dt}+\frac{da_y}{dt}b_y+a_y\frac{db_y}{dt}+\frac{da_z}{dt}b_z+a_z\frac{db_z}{dt}$$

Group the terms carrying $\dot{\vec a}$ and those carrying $\dot{\vec b}$:

$$= \left(\frac{da_x}{dt}b_x+\frac{da_y}{dt}b_y+\frac{da_z}{dt}b_z\right) + \left(a_x\frac{db_x}{dt}+a_y\frac{db_y}{dt}+a_z\frac{db_z}{dt}\right)$$

$$\therefore \frac{d(\vec a\cdot\vec b)}{dt} = \frac{d\vec a}{dt}\cdot\vec b + \vec a\cdot\frac{d\vec b}{dt} \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Vector differentiation rules]])

## Path equation from Newton's second law, constant force

#formula

(source: lecture photo, "$\vec F=-mg\hat z$" worked example, $\vec r(0)=\vec 0$, $\vec v(0)=\hat x+2\hat y+3\hat z$)

Start from $m\ddot{\vec r}=\vec F$. Integrate once:

$$m\int\ddot{\vec r}\,dt = \int\vec F_{const}\,dt \;\Rightarrow\; \dot{\vec r} = \frac{\vec Ft}{m}+\vec c$$

At $t=0$: $\vec c=\vec v(0)$, so $\vec v(t) = \dfrac{\vec Ft}{m}+\vec v(0)$.

Integrate a second time from $t=0$:

$$\vec r(t)-\vec r(0) = \frac{\vec Ft^2}{2m}+\vec v(0)\,t$$

Substituting $\vec F=-mg\hat z$, $\vec r(0)=\vec 0$, $\vec v(0)=\hat x+2\hat y+3\hat z$:

$$\vec r(t) = \frac{-mg\hat z\,t^2}{2m}+(\hat x+2\hat y+3\hat z)t$$

$$\therefore \vec r(t) = t\,\hat x+2t\,\hat y+\left(3t-\tfrac12 gt^2\right)\hat z \qquad\blacksquare$$

(see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Worked example constant force vec F equals negative mg hat z]])

## Angle identity from $\hat r,\hat\theta$ projections (Q4-style)

#formula

Proof not shown in source, statement only. The source material intentionally left this derivation as an exercise for the student, drawing on the projection technique from Velocity and acceleration in polar coordinates (see above); it was never itself worked on the page. A derivation exists in `APM01B1_Notes_S1_PolarIntrinsicCoordinates.md` under "(added) Deriving the Q4-style angle identity", built from taught material rather than transcribed from a lecture source, and is not exam-verified against the lecturer's own version.

$$\theta = \arccos\!\left(\frac{a\dot r+b\,r\dot\theta}{v^2}\right), \qquad \theta = \arcsin\!\left(\frac{b\dot r-a\,r\dot\theta}{v^2}\right)$$
