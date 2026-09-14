---
module: MAT01B1
topic: Related Rates
session: S4
tags: [formula, worked-example]
---

# Related Rates

Source: Dr K, §3.9 Related Rates (slides 1 to 19).

## What a related rates problem asks for

Two quantities change over time and are tied together by some geometric or physical equation. Knowing the rate of change of one (usually the one that's easy to measure directly) lets you find the rate of change of the other, by differentiating the connecting equation with respect to time using the Chain Rule. Every example below runs the same underlying move: find the equation, then let the Chain Rule turn it into a rate equation.

## Problem Solving Strategy (source, slide 13)

1. Read the problem carefully.
2. Draw a diagram if possible.
3. Introduce notation: assign symbols to every quantity that is a function of time.
4. Express the given information and the required rate in terms of derivatives.
5. Write an equation relating the quantities. If necessary, use the geometry of the situation to eliminate a variable by substitution.
6. Use the Chain Rule to differentiate both sides of the equation with respect to $t$.
7. Substitute the given values into the resulting equation and solve for the unknown rate.

N.B Step 5, eliminating an extra variable using the problem's geometry, is usually where a related rates problem is actually won or lost; the differentiation in step 6 is close to automatic once the equation is right.

## Worked example: expanding balloon (source, slides 3 to 5)

Air is pumped into a spherical balloon at $dV/dt = 100\text{ cm}^3/\text{s}$. Find $dr/dt$ when the diameter is $50\text{ cm}$ (so $r=25\text{ cm}$).

$$
V = \frac{4}{3}\pi r^3 \quad\Rightarrow\quad \frac{dV}{dt} = 4\pi r^2\frac{dr}{dt}.
$$

(added, completing the arithmetic) $\dfrac{dr}{dt} = \dfrac{dV/dt}{4\pi r^2} = \dfrac{100}{4\pi(25)^2} = \dfrac{1}{25\pi} \approx 0.0127\text{ cm/s}$.

## Worked example: sliding ladder (source, slides 6 to 8)

A 5 m ladder rests against a wall. The foot slides away at $dx/dt = 1\text{ m/s}$. Find $dy/dt$ when $x=3\text{ m}$, where $x$ is the foot's distance from the wall and $y$ the top's height on the wall.

$$
x^2+y^2=25 \quad\Rightarrow\quad 2x\frac{dx}{dt}+2y\frac{dy}{dt}=0 \quad\Rightarrow\quad \frac{dy}{dt}=-\frac{x}{y}\frac{dx}{dt}.
$$

$x=3\Rightarrow y=4$ (Pythagoras on the same equation). $\dfrac{dy}{dt}=-\dfrac{3}{4}(1)=-\dfrac{3}{4}\text{ m/s}$. The negative sign means $y$ is decreasing, the top of the ladder is sliding down, as expected.

## Worked example: filling cone (source, slides 9 to 12)

A tank is an inverted cone, base radius 2 m, height 4 m. Water is pumped in at $dV/dt=2\text{ m}^3/\text{min}$. Find $dh/dt$ when the water is $h=3\text{ m}$ deep.

$V=\frac{1}{3}\pi r^2h$ depends on two variables. Similar triangles give $\dfrac{r}{h}=\dfrac{2}{4}\Rightarrow r=\dfrac{h}{2}$, so

$$
V=\frac{1}{3}\pi\left(\frac{h}{2}\right)^2h=\frac{\pi}{12}h^3 \quad\Rightarrow\quad \frac{dV}{dt}=\frac{\pi}{4}h^2\frac{dh}{dt}.
$$

Substituting $h=3$, $dV/dt=2$: $\dfrac{dh}{dt}=\dfrac{4(2)}{\pi(3)^2}=\dfrac{8}{9\pi}\approx 0.28\text{ m/min}$.

N.B Eliminating the second variable ($r$) via similar triangles before differentiating is the extra step this example adds on top of the ladder example, where Pythagoras already ties the two variables directly with no elimination needed.

-> The same "eliminate a variable via geometry" move (step 5) shows up again, with a different geometric tool, in the two cars example below.

## Worked example: two cars approaching an intersection (source, slides 14 to 17)

Car A travels west at 90 km/h, distance $x$ from intersection $C$. Car B travels north at 100 km/h, distance $y$ from $C$. $z$ is the distance between the cars. $dx/dt=-90$, $dy/dt=-100$ (both negative since $x,y$ are decreasing). Find $dz/dt$ when $x=0.06\text{ km}$, $y=0.08\text{ km}$.

$$
z^2=x^2+y^2 \quad\Rightarrow\quad \frac{dz}{dt}=\frac{1}{z}\left(x\frac{dx}{dt}+y\frac{dy}{dt}\right).
$$

At the given instant, Pythagoras gives $z=0.1\text{ km}$, so

$$
\frac{dz}{dt}=\frac{1}{0.1}\big[0.06(-90)+0.08(-100)\big]=-134\text{ km/h}.
$$

## Worked example: rotating searchlight (source, slides 18 to 19)

A man walks at $1.5\text{ m/s}$ along a path. A searchlight 6 m from the path tracks him; $\theta$ is the angle between the beam and the perpendicular to the path. Find $d\theta/dt$ when $x=8\text{ m}$ ($x$ = man's distance along the path from the closest point).

$$
\tan\theta=\frac{x}{6} \quad\Rightarrow\quad \frac{dx}{dt}=6\sec^2\theta\,\frac{d\theta}{dt} \quad\Rightarrow\quad \frac{d\theta}{dt}=\frac{1}{6}\cos^2\theta\,\frac{dx}{dt}=\frac{1}{4}\cos^2\theta.
$$

When $x=8$, the beam length is 10 (6, 8, 10 triangle), so $\cos\theta=\dfrac{6}{10}=\dfrac{3}{5}$, giving

$$
\frac{d\theta}{dt}=\frac{1}{4}\left(\frac{3}{5}\right)^2=\frac{9}{100}=0.09\text{ rad/s}.
$$

This example needed a trig relation instead of a direct Pythagorean or similar-triangle one, the same overall method still applies once the connecting equation is written down.

## See also
- [[MAT01B1_Notes_S1_CalculusApplications]] (Chain Rule context, curve sketching)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (Chain Rule formula)
- [[MAT01B1_Notes_S5_OptimizationProblems]]
