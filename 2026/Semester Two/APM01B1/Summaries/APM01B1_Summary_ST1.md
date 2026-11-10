---
module: APM01B1
topic: Summary for ST1
tags: [exam-flagged]
---

# APM01B1 — Summary for ST1

## Material covered

Personal notebook photos, 26 pages, Direct-source mode (no existing CDG session chain for this module). Spans polar unit vectors, tangential-normal coordinates, vector differentiation rules, Newton's second law and the path equation, and Galilean invariance. Full detail in [[APM01B1_Notes_S1_PolarIntrinsicCoordinates]].

## Condensed concept pass

- **Average vs instantaneous velocity**: $\vec v_{ave}$ needs endpoint positions only, $\vec v_{mean}$ needs instantaneous velocity at each endpoint, generally unequal. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Average vs instantaneous velocity]])
- **Vector differentiation**: componentwise, linear, dot product obeys the ordinary product rule. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Vector differentiation rules]])
- **Galilean invariance**: $\vec F=m\vec a$ keeps its form under a frame change only when the frames differ by constant velocity, not acceleration. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Galilean invariance]])
- **Polar unit vectors**: $\hat r,\hat\theta$ co-move with the particle but still reference the fixed Cartesian origin, unlike $\hat x,\hat y$ they are not constant in time. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Polar coordinates: why $\hat r, \hat\theta$ are needed]])
- **Polar $\vec v,\vec a$**: built entirely from $d\hat r/dt=\dot\theta\hat\theta$ and $d\hat\theta/dt=-\dot\theta\hat r$, see [[APM01B1_Proofs_ST1#Velocity and acceleration in polar coordinates]] for the full derivation.
- **Tangential-normal frame**: $\hat T=\vec v/\|\vec v\|$ is origin-independent, $\hat n\perp\hat T$ toward the path's concave side. Not the same construction as $\hat r,\hat\theta$ despite the parallel structure. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Tangential-normal (intrinsic) coordinates]])
- **Intrinsic $\vec a$**: $\vec a=\dot v\hat T+\frac{v^2}{\rho}\hat n$, tangential term changes speed, normal term changes direction. See [[APM01B1_Proofs_ST1#Acceleration in tangential-normal coordinates]] for the curvature-based derivation.
- **Path equation from $\vec F=m\vec a$**: integrate twice, first constant pinned by $\vec v(0)$, second by $\vec r(0)$. Two edge cases distinguished by which conditions are given: $(\vec r(0),\vec v(0))$ for constant force, $(\vec r(0),\vec r(1))$ for time-dependent force. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Two edge cases for solving $m\ddot{\vec r}=\vec F$]])
- **Angle identity ($\theta$ from $\hat r,\hat\theta$ projections)**: not lecturer-derived, intentionally left as a student exercise. See [[APM01B1_Proofs_ST1#Angle identity from $\hat r,\hat\theta$ projections (Q4-style)]] for the sourcing note.

## Worked example notebook

- **Average velocity, oscillation**: $r(t)=\sin(2\pi t)$, illustrates $v_{mean}\neq v_{ave}$. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Average vs instantaneous velocity]])
- **Projectile motion, 2D vs 1D graphs**: $x''=0,\ y''=-g$, shows why the parametric and $y(x)$ graphs coincide in shape. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Parametric motion, 2D vs 1D graphs]])
- **$\hat r,\hat\theta$ for a non-circular path**: $\vec r(t)=\sin t\,\hat x+\sin(2t)\,\hat y$, full computation of $\hat r,\hat\theta,v_\theta$. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Worked example: $\hat r(t), \hat\theta(t)$ for a non-circular path]])
- **Straight line into a circular arc**: constant-speed driver, $\vec a=0$ on straights, $\vec a=\frac{v^2}{\rho}\hat n$ on the arc. (see: [[APM01B1_Notes_S1_PolarIntrinsicCoordinates#Worked example: straight line into a circle]])
- **Constant force**, $\vec F=-mg\hat z$: full double integration to $\vec r(t)=t\hat x+2t\hat y+(3t-\tfrac12gt^2)\hat z$. (see: [[APM01B1_Proofs_ST1#Path equation from Newton's second law, constant force]])

## Common mistakes

- Final-step arithmetic slip after an otherwise correct vector decomposition: source computed $\vec a(\pi/4)=-\tfrac{\sqrt2}{2}\hat x-4\hat y$ correctly, then wrote its magnitude as $2\sqrt2$ where $\sqrt{\tfrac12+16}=\sqrt{16.5}\approx4.062$ is correct. The vector decomposition was sound, the error was purely in the final scalar simplification, worth double-checking the last arithmetic step even when the method is right.
- $(\hat T,\hat n)$ and $(\hat r,\hat\theta)$ are easy to conflate since both are constructed the same way (cosine/sine pair, cross-product orthogonality). They answer different questions, one is anchored to the origin, the other to the direction of motion.

```tikz
\begin{document}
\begin{tikzpicture}[scale=1.0]
  \draw[->] (-0.5,0) -- (2.5,0) node[right] {$x$};
  \draw[->] (0,-0.5) -- (0,2.5) node[above] {$y$};
  \draw[->, thick, blue] (0,0) -- (1.7,1.2) node[right] {$\hat r$};
  \draw[->, thick, red] (0,0) -- (-0.85,1.2) node[above] {$\hat\theta$};
  \node at (1,-1) {Polar: anchored to origin};
  \begin{scope}[xshift=5.5cm]
    \draw[thick] (-0.5,0.3) to[out=20,in=200] (3,1.8);
    \filldraw (1.2,0.85) circle (1.2pt);
    \draw[->, thick, blue] (1.2,0.85) -- (2.0,1.35) node[right] {$\hat T$};
    \draw[->, thick, red] (1.2,0.85) -- (0.7,1.65) node[above] {$\hat n$};
    \node at (1.2,-1) {Intrinsic: anchored to the path};
  \end{scope}
\end{tikzpicture}
\end{document}
```

## Tips

- When a question gives $\vec v$ in Cartesian form and asks for a polar or intrinsic quantity, project with a dot product rather than trying to read the component off by inspection, this is the technique behind $v_r=\vec v\cdot\hat r$, $v_\theta=\vec v\cdot\hat\theta$, $a_T=\vec a\cdot\hat T$ throughout.
- To tell which edge case a force problem is (constant vs time-dependent), check which two conditions are supplied: two positions ($\vec r(0)$ and $\vec r(1)$) signals a time-dependent force problem asking for $\vec v(0)$, a position and a velocity ($\vec r(0)$ and $\vec v(0)$) signals the standard constant-force integration.
