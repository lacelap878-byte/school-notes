# APM01A1 Handoff Notes: Vectors, Parametric Curves, and Polar Motion

A working reference built from a full tutoring session. Read this before your next lecture or study block so the material lands the second time around instead of feeling brand new.

---

## 1. The Big Picture (why we're learning all of this)

You're building a toolkit to describe motion in any coordinate system, then confirming the physics doesn't change depending on who's observing.

1. Parametric equations: describe "where is the particle at time t" using r(t) = x(t) x̂ + y(t) ŷ
2. Vector differentiation: prove the calculus rules (product rule, etc.) still work when applied to vectors, not just scalars
3. Galilean invariance: confirm F = ma looks the same in every inertial frame (frames moving at constant velocity relative to each other)
4. Polar coordinates (r̂, θ̂): a more natural system for circular/rotational motion, but the unit vectors themselves rotate, which is the entire reason polar is harder than Cartesian
5. Applications: circular motion, projectile motion
6. Average vs instantaneous velocity: average only needs two points, instantaneous needs the full path equation

---

## 2. Notation Decoder

- A dot over a variable (θ̇, ṙ) always means d/dt, the derivative with respect to time. Nothing more.
- θ̈, r̈ mean the second time derivative.
- x̂, ŷ (Cartesian unit vectors) never change direction, so their derivative is always zero.
- r̂, θ̂ (polar unit vectors) DO change direction as the particle moves, because they're defined relative to the particle's current angle θ, not fixed in space.

---

## 3. Deriving r̂ and θ̂ (do this once, reuse forever)

Start from Cartesian: r = x x̂ + y ŷ

Convert using x = r cos θ, y = r sin θ:
r = r cos θ x̂ + r sin θ ŷ

The direction part (magnitude stripped away) defines r̂:

**r̂ = cos θ x̂ + sin θ ŷ**

θ̂ is defined as perpendicular to r̂, pointing in the direction of increasing θ (counterclockwise). Rotate r̂ by 90 degrees:

**θ̂ = −sin θ x̂ + cos θ ŷ**

Check: r̂ · θ̂ = cos θ(−sin θ) + sin θ(cos θ) = 0, confirming perpendicularity.

Important: these formulas are fixed and general. You never "solve" for r̂ or θ̂ from scratch each problem, you just substitute whatever θ(t) you're given into the formulas above.

---

## 4. Where dr̂/dt = θ̇ θ̂ Actually Comes From

This is not a rule to memorize blindly, it falls straight out of the chain rule.

r̂ is a function of θ, and θ is a function of t, so r̂ is a composition: r̂(θ(t))

Chain rule: dr̂/dt = (dr̂/dθ) · (dθ/dt)

- dr̂/dθ = −sin θ x̂ + cos θ ŷ = θ̂ (differentiate r̂'s formula directly with respect to θ, and it equals θ̂ by design)
- dθ/dt = θ̇ (just the definition of the dot)

Multiply: dr̂/dt = θ̂ · θ̇ = θ̇ θ̂

Same chain rule as d/dt[sin(t²)] = cos(t²) · 2t, just producing a vector output instead of a scalar.

---

## 5. Two Different Roles θ Plays (the source of a lot of confusion)

**Role 1, θ as an argument (substitution, no multiplication):**
θ̂ = −sin θ x̂ + cos θ ŷ. If θ(t) = t², substitute directly:
θ̂(t) = −sin(t²) x̂ + cos(t²) ŷ

**Role 2, θ̇ as a multiplying scalar (this is where multiplication happens):**
dr̂/dt = θ̇ θ̂. Here θ̇ is a number (or scalar function of t) multiplying the vector θ̂.

These are two separate operations that happen to both involve θ. Don't conflate substitution with multiplication.

---

## 6. Velocity in Polar Coordinates

Position: r(t) = r(t) r̂(t), a scalar times a vector. Apply the ordinary product rule:

**v(t) = ṙ r̂ + r θ̇ θ̂**

Physical meaning of each term:
- ṙ r̂: radial velocity, how fast the particle moves straight outward along r̂
- r θ̇ θ̂: tangential velocity, how fast the particle sweeps around due to changing angle, scaled by r because sweeping the same angular rate covers more distance farther from the origin

This is the polar equivalent of v = vx x̂ + vy ŷ in Cartesian: r̂ and θ̂ are the only two independent directions available in polar, so velocity must decompose into these two terms no matter what path is being traced.

### Worked example
Given r(t) = 3t, θ(t) = t²:
- ṙ = 3
- θ̇ = 2t
- v(t) = 3 r̂ + (3t)(2t) θ̂ = **3 r̂ + 6t² θ̂**

---

## 7. When to Substitute θ(t) Into r̂ and θ̂ (Level 1 vs Level 2)

**Level 1, leave answer in polar form (r̂, θ̂ symbols):**
Use the general formula v = ṙ r̂ + r θ̇ θ̂, plug in ṙ, r, θ̇ as numbers/expressions, leave r̂ and θ̂ as symbols. This is usually the expected final answer unless told otherwise. No substitution of θ(t) needed.

**Level 2, expand into Cartesian (x̂, ŷ):**
Only needed if the question specifically wants x̂, ŷ components, e.g. to plot on ordinary axes or combine with a vector already in Cartesian form. Substitute θ(t) into:
r̂(t) = cos(θ(t)) x̂ + sin(θ(t)) ŷ
θ̂(t) = −sin(θ(t)) x̂ + cos(θ(t)) ŷ
then expand v(t) fully.

r̂ and θ̂ are left as symbols in most answers because they represent directions, not numbers, similar to writing "5 m/s eastward" instead of forcing it into components.

---

## 8. Galilean Invariance

Setup: if frame 2's position is x2(t) = x1(t) + x0 + v0 t (frame 2 offset by a constant plus a constant-velocity drift relative to frame 1)

Differentiate twice: the x0 term vanishes (derivative of a constant is 0), and the v0 t term also vanishes on the second derivative (its second derivative is 0). Result: a2 = a1, acceleration is identical in both frames.

Conclusion: F = ma holds identically in any frame moving at constant velocity relative to another (an inertial frame). If asked to prove this: write out x2 = x1 + x0 + v0 t, differentiate twice, show the constant and linear terms disappear.

If frames were accelerating relative to each other (non-inertial), extra terms would survive, this is the origin of fictitious forces (later topic).

---

## 9. Spatial vs Temporal Differentiation

- Temporal differentiation: d/dt, how something changes over time (velocity, acceleration, all the dot notation)
- Spatial differentiation: derivative with respect to a space variable, like dr/dθ, describes the shape of a path, not how fast you move along it

Why it matters: a curve r(θ) can be looked at geometrically (how does r change as θ changes, shape only, no time) or kinematically (how does position change as time passes, requires θ = θ(t) and the chain rule: dr/dt = (dr/dθ)(dθ/dt)). Spatial differentiation gives the shape, temporal differentiation (via chain rule through θ(t)) gives the actual motion.

---

## 10. Why Polar Beats Cartesian for Rotational Motion

Circular motion in Cartesian: x(t) = R cos(θ(t)), y(t) = R sin(θ(t)), two functions, both oscillating.

Circular motion in polar: r(t) = R (constant), only θ(t) changes. One variable instead of two, and it directly represents the physically meaningful quantity (angle swept). This is why anything involving rotation, orbits, or circular motion collapses to much simpler algebra in polar.

---

## 11. Graphing Parametric and Polar Curves, the Real Method

Point plotting is a confirmation step, not the method itself. Full sequence:

1. Find axis crossings: set x(t) = 0, solve for t, find y at that t (and vice versa)
2. Check symmetry: compare x(−t), y(−t) to x(t), y(t) to see if the curve is symmetric about an axis or the origin
3. Find critical points: compute dx/dt and dy/dt separately. Where dx/dt = 0, vertical tangent. Where dy/dt = 0, horizontal tangent. These mark where the curve turns
4. Check boundary behavior: what happens as t approaches the edges of its domain, including infinity
5. Eliminate the parameter if possible, to recognize the curve as a known family (parabola, hyperbola, semicubical parabola, etc.)
6. Only now plot a few points, using the special t values already found in steps 1 and 3, to confirm direction of travel

### Connecting the dots correctly
- Always connect points in order of increasing parameter (t, or θ). There is no other valid order, since the particle only moves forward in t
- Use a sign chart on the relevant derivative (dr/dt, dθ/dt, dx/dt, dy/dt) to know if the curve is monotonic (safe to connect with a simple sweep) or oscillating (needs more points near turning points, or recognition of the curve family, e.g. a rose curve)
- Straight lines between plotted points, smoothed slightly by eye, is the standard and correct approach for a hand sketch. More points near turning points improves accuracy

### Polar points on ordinary x, y axes
No separate graph paper needed. Given (r, θ): from the origin, draw a line at angle θ measured counterclockwise from the positive x-axis (same convention as the unit circle), then mark a point a distance r along that line. Angles of 0, π/2, π, 3π/2 land exactly on an axis, making them the easiest points to plot exactly.

### Critical distinction: what the sign of a derivative means, by context
- Cartesian, dy/dx: tells you if the graph is rising or falling as x increases (standard slope interpretation)
- Parametric, dx/dt and dy/dt separately: tell you which direction the particle is physically traveling (left/right, up/down) as time passes, not slope
- Polar, dr/dt and dθ/dt: tell you if the particle is spiraling inward/outward, and rotating clockwise/counterclockwise
- To get the actual tangent slope of a parametric curve: dy/dx = (dy/dt) / (dx/dt)

---

## 12. Families of Polar Curves (recognize the shape from the formula's structure)

Ask: does r depend on θ linearly, exponentially, trig-wise, or not at all?

- Archimedean spiral: r = a + bθ. Linear in θ, evenly spaced coils
- Logarithmic spiral: r = a e^(bθ). Exponential in θ, coils spread apart more each loop, never reaches the origin
- Rose curve: r = a cos(kθ) or a sin(kθ). k odd gives k petals, k even gives 2k petals
- Limaçon: r = a + b cos θ. Shape depends on the ratio a/b: a/b < 1 gives an inner loop, a/b = 1 gives a cardioid (heart shape), 1 < a/b < 2 gives a dimple, a/b ≥ 2 gives a convex shape with no dent
- Lemniscate: r² = a² cos(2θ). Figure eight shape
- Circle: r = a (constant)

General rule: linear in θ gives an evenly spaced spiral, exponential in θ gives an unevenly spaced spiral, a trig function of θ gives a closed repeating shape (petals, loops, hearts), constant gives a circle.

---

## 13. Common Misconception, Clarified

r² = x² + y² is NOT a special spiral equation. It's the Pythagorean definition of distance from the origin, true for every single point on any curve, spiral or otherwise. It does not connect the spiral family (r = a + bθ, a relationship between radius and angle) to the hyperbola family (xy = constant, a relationship between two Cartesian lengths). These are unrelated curve families. θ is an angle, not a coordinate like x, so "r times θ" resembling "x times y" is a false pattern match.

---

## 14. Suggested Study Approach Going Forward

- In lecture: prioritize copying what's on the board accurately over understanding it live. Understanding happens afterward, at home, trying to do both simultaneously is why material feels rushed
- Record lectures if permitted, to recover missed sections
- Leave gaps in notes for missed material rather than guessing and writing something wrong
- Before attempting a graphing question, run the six step method above rather than jumping to point plotting
- When stuck on notation, isolate whether the confusion is substitution (plugging a function in as an argument) or multiplication (a scalar coefficient in front of a vector), these are frequently conflated but are different operations
