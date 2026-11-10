---
module: MAT01B1
topic: ST2 Summary (Related Rates to Polar Coordinates)
session: ST2
tags:
  - definition
  - formula
  - theorem
  - worked-example
  - common-mistake
  - added
---

# MAT01B1 Summary ST2

Built for fast review, not first learning. Links go to the session notes for this range and to [[MAT01B1_Proofs_ST1]] for full depth. Every slide reference is the PDF page number inside Dr K's deck. Anything beyond the slides is marked `(added)`.

## Material covered

Session notes in the ST2 range, each with the Dr K deck it was built from:

- [[MAT01B1_Notes_S4_RelatedRates]] (§3.9 Related rates, 19 slides)
- [[MAT01B1_Notes_S5_OptimizationProblems]] (§4.7 Optimization Problems, 26 slides)
- [[MAT01B1_Notes_S6_MVTForIntegrals]] (Mean Value Theorem for Integrals proof deck, 8 slides)
- [[MAT01B1_Notes_S7_AreaBetweenCurves]] (§6.1 Areas between curves, 20 slides)
- [[MAT01B1_Notes_S8_Volumes]] (§6.2 Volumes, 34 slides)
- [[MAT01B1_Notes_S9_CylindricalShells]] (§6.3 Volumes, cylindrical shells, 22 slides)
- [[MAT01B1_Notes_S10_AverageValueOfAFunction]] (§6.5 Average value of a function, 11 slides)
- [[MAT01B1_Notes_S11_ArcLength]] (§8.1 Arc Length, 20 slides)
- [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]] (§8.2 Area of a surface of revolution, 21 slides, and the one-page Surface Area handout)
- [[MAT01B1_Notes_S13_SeparableDifferentialEquations]] (§9.3 Variable separable differential equations, 24 slides)
- [[MAT01B1_Notes_S14_LinearDifferentialEquations]] (§9.5 Linear differential equations, 13 slides)
- [[MAT01B1_Notes_S15_ParametricEquations]] (§10.1 Curves defined by parametric equations, 12 slides)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations]] (§10.2 Calculus with parametric equations, 26 slides)
- [[MAT01B1_Notes_S17_PolarCoordinates]] (§10.3 Polar coordinates, 19 slides)

Proofs these sessions lean on: [[MAT01B1_Proofs_ST1]] (Fermat's Theorem, Rolle's Theorem, the Mean Value Theorem, Theorem 5 and Corollary 7).

Scope notes:
- The §10.3 deck stops at polar coordinates and polar curves. It has no area or arc length in polar form, so this summary has none.
- The linear algebra notes and the Binomial Theorem note sit outside the range Related Rates to §10.3 and are not covered here. The three ST1 background notes (extremum theory, the derivative and integral reference, and integration examples) appear under See also.

## Condensed concept pass

### Related rates (§3.9)

Full notes: [[MAT01B1_Notes_S4_RelatedRates]]. The seven steps: [[MAT01B1_Notes_S4_RelatedRates#Problem Solving Strategy (source, slide 13)|Problem Solving Strategy]].

- Idea: two quantities that change with time are tied by one equation. Differentiate both sides with respect to $t$ using the Chain Rule, then put in the values at the instant asked about and solve for the unknown rate (source, §3.9 slides 2 and 13).
- Order of the source's strategy: diagram, symbols for every quantity that depends on time, given and required rates written as derivatives, one relating equation (use geometry such as similar triangles to leave one variable), differentiate, substitute last (source, §3.9 slide 13).
- Sign rule: a quantity that is decreasing has a negative derivative (source, §3.9 slides 8 and 16).

$$\frac{dV}{dt}=\frac{dV}{dr}\cdot\frac{dr}{dt}$$

#formula (source, §3.9 slide 5)

### Optimization (§4.7)

Full notes: [[MAT01B1_Notes_S5_OptimizationProblems]]. See [[MAT01B1_Notes_S5_OptimizationProblems#First Derivative Test for Absolute Extreme Values (source, slide 16)|First Derivative Test for Absolute Extreme Values]] and [[MAT01B1_Notes_S5_OptimizationProblems#The Closed Interval Method (source, §4.1)|Closed Interval Method]]. The extremum theory underneath is [[MAT01B1_Proofs_ST1#Fermat's Theorem|Fermat's Theorem]].

- The hard part is the model. Name the quantity $Q$ to optimise, write it in one variable using the constraint, write the domain of that function, then find the absolute maximum or minimum on that domain (source, §4.7 slides 3 to 5).
- Closed interval domain: compare $f$ at the critical numbers and at both endpoints (source, §4.7 slide 9).
- Domain with no endpoints to test, such as $(0,\infty)$: use the First Derivative Test for Absolute Extreme Values below.
- To minimise a distance, minimise its square. Same minimiser, easier derivative (source, §4.7 slide 18).
- If $A''<0$ everywhere, the critical number gives an absolute maximum (source, §4.7 slide 9).

First Derivative Test for Absolute Extreme Values #theorem (source, §4.7 slide 16):

- Hypotheses: $c$ is a critical number of a continuous function $f$ defined on an interval.
- If $f'(x)>0$ for all $x<c$ and $f'(x)<0$ for all $x>c$, then $f(c)$ is the absolute maximum value of $f$.
- If $f'(x)<0$ for all $x<c$ and $f'(x)>0$ for all $x>c$, then $f(c)$ is the absolute minimum value of $f$.

### Average value and the Mean Value Theorem for Integrals (§6.5 and MVT deck)

Full notes: [[MAT01B1_Notes_S10_AverageValueOfAFunction]] for the definition and [[MAT01B1_Notes_S6_MVTForIntegrals]] for the theorem. The derivative counterpart is [[MAT01B1_Proofs_ST1#Mean Value Theorem|Mean Value Theorem]].

Average value #definition (source, §6.5 slide 5):

$$f_{\text{ave}}=\frac{1}{b-a}\int_a^b f(x)\,dx$$

It comes from averaging $n$ sample values, rewriting $n=(b-a)/\Delta x$, and letting $n\to\infty$ (source, §6.5 slides 3 to 5).

Mean Value Theorem for Integrals #theorem (source, MVT deck slide 1):

- Hypothesis: $f$ is continuous on $[a,b]$.
- Conclusion: there is $c\in[a,b]$ with

$$f(c)=f_{\text{ave}}=\frac{1}{b-a}\int_a^b f(x)\,dx,\qquad\text{equivalently}\qquad \int_a^b f(x)\,dx=f(c)(b-a).$$

- Proof: two cases, constant $f$ and non-constant $f$. The non-constant case chains the Extreme Value Theorem into the Intermediate Value Theorem. Full proof: [[MAT01B1_Notes_S6_MVTForIntegrals#Proof]] (source, MVT deck slides 4 to 8).
- The §6.5 deck (slide 8) credits the derivative Mean Value Theorem and the Fundamental Theorem of Calculus. The MVT deck proves it with EVT and IVT. Both are in the slides; the deck proof is the one written out step by step.
- Geometry: the rectangle on $[a,b]$ with height $f(c)$ has the same area as the region under $f$ (source, §6.5 slide 9).

### Area between curves (§6.1)

Full notes: [[MAT01B1_Notes_S7_AreaBetweenCurves]], including [[MAT01B1_Notes_S7_AreaBetweenCurves#When the curves cross]].

Each strip has width $\Delta x$ and height $f(x_i^*)-g(x_i^*)$; the limit of the sum is an integral (source, §6.1 slides 3 to 5).

$$A=\int_a^b\big[f(x)-g(x)\big]\,dx,\qquad f,g\text{ continuous},\ f(x)\ge g(x)\text{ on }[a,b]$$

$$A=\int_a^b\big|f(x)-g(x)\big|\,dx\qquad\text{(split at every crossing)}$$

$$A=\int_c^d\big[f(y)-g(y)\big]\,dy,\qquad x=f(y),\ x=g(y),\ f(y)\ge g(y)\text{ on }[c,d]$$

#formula (source, §6.1 slides 5, 15 and 18)

- Find the limits by solving the two curve equations simultaneously. If that is impossible, read the intersection from a graph and integrate numerically (source, §6.1 slides 11 to 13).

### Volumes by cross-sections, disks and washers (§6.2)

Full notes: [[MAT01B1_Notes_S8_Volumes]], starting from [[MAT01B1_Notes_S8_Volumes#Definition of Volume (source, slide 8)|Definition of Volume]].

Volume #definition (source, §6.2 slide 8): if $S$ lies between $x=a$ and $x=b$ and the cross-sectional area $A(x)$ perpendicular to the $x$-axis is continuous, then

$$V=\lim_{n\to\infty}\sum_{i=1}^n A(x_i^*)\,\Delta x=\int_a^b A(x)\,dx$$

The same holds with $y$ and limits $c$ to $d$. $A(x)$ is the area of the moving slice through $x$.

- Disk: $A=\pi(\text{radius})^2$.
- Washer: $A=\pi(\text{outer radius})^2-\pi(\text{inner radius})^2$ (source, §6.2 slide 22).
- Rotating about a line other than an axis: measure each radius from that line. About $y=2$ the radii were $2-x^2$ and $2-x$; about $x=-1$ they were $1+\sqrt y$ and $1+y$ (source, §6.2 slides 19 and 25).
- Solids with known cross-sections: build $A(x)$ from the geometry of the slice, using similar triangles where needed (source, §6.2 slides 27 to 34).

### Cylindrical shells (§6.3)

Full notes: [[MAT01B1_Notes_S9_CylindricalShells]]. See [[MAT01B1_Notes_S9_CylindricalShells#Volume of a single shell (source, slides 3 to 5)|the single shell]], [[MAT01B1_Notes_S9_CylindricalShells#Building the volume formula (source, slides 6 to 10)|the volume formula]] and [[MAT01B1_Notes_S9_CylindricalShells#Disks/washers vs cylindrical shells (source, slides 21 to 22)|choosing between disks/washers and shells]].

Shell volume from $V_2-V_1$ (source, §6.3 slide 4), remembered as circumference times height times thickness:

$$V=2\pi r\,h\,\Delta r$$

Rotating the region under $y=f(x)\ge0$ from $a$ to $b$ about the $y$-axis (source, §6.3 slide 9):

$$V=\int_a^b 2\pi x\,f(x)\,dx,\qquad 0\le a<b$$

#formula

- About another vertical line the radius is the distance to that line. About $x=2$ it is $2-x$ (source, §6.3 slide 19).
- Choosing the method: draw a sample rectangle. Its thickness ($\Delta x$ or $\Delta y$) fixes the variable. Revolved, it becomes a disk or washer, or a shell. Ask whether the region is easier as $y=f(x)$ or $x=g(y)$, whether limits are easier in one variable, whether one variable forces two integrals, and whether the resulting integral can be evaluated (source, §6.3 slides 21 and 22).

### Arc length (§8.1)

Full notes: [[MAT01B1_Notes_S11_ArcLength]]. See [[MAT01B1_Notes_S11_ArcLength#The Arc Length Formula (source, slides 7 to 9)|the Arc Length Formula]] and [[MAT01B1_Notes_S11_ArcLength#The arc length function (source, slides 16 to 17)|the arc length function]]. The parametric version is in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Arc length of a parametric curve]].

Arc length #definition (source, §8.1 slide 6): the limit of the lengths of inscribed polygons,

$$L=\lim_{n\to\infty}\sum_{i=1}^n\big|P_{i-1}P_i\big|.$$

Arc Length Formula #theorem (source, §8.1 slide 9):

- Hypothesis: $f'$ is continuous on $[a,b]$.

$$L=\int_a^b\sqrt{1+[f'(x)]^2}\,dx=\int_a^b\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx$$

- For $x=g(y)$, $c\le y\le d$, with $g'$ continuous (source, §8.1 slide 13):

$$L=\int_c^d\sqrt{1+[g'(y)]^2}\,dy=\int_c^d\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy$$

- Proof shape (source, §8.1 slides 7 and 8; full derivation in [[MAT01B1_Notes_S11_ArcLength#The Arc Length Formula (source, slides 7 to 9)|The Arc Length Formula]]): $|P_{i-1}P_i|=\sqrt{(\Delta x)^2+(\Delta y_i)^2}$, [[MAT01B1_Proofs_ST1#Mean Value Theorem|the Mean Value Theorem]] gives $\Delta y_i=f'(x_i^*)\Delta x$, and the sum becomes a Riemann sum of a continuous function.

Arc length function and differential (source, §8.1 slides 16 to 18):

$$s(x)=\int_a^x\sqrt{1+[f'(t)]^2}\,dt,\qquad \frac{ds}{dx}=\sqrt{1+\left(\frac{dy}{dx}\right)^2}\ \ge 1,\qquad (ds)^2=(dx)^2+(dy)^2$$

$\dfrac{ds}{dx}=1$ exactly where the slope is $0$. The symmetric form $(ds)^2=(dx)^2+(dy)^2$ is the memory device for both length formulas.

### Surface area of revolution (§8.2)

Full notes: [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]]. See [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution#Building the surface area formula (source, slides 7 to 10)|building the formula]] and [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution#The four cases (source: handout)|the four cases]]. The parametric version is in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Surface area]].

- Simple surfaces (source, §8.2 slides 2 and 3): lateral area of a cylinder $2\pi rh$; lateral area of a cone $\pi r\ell$ ($\ell$ the slant height).
- A band (frustum) with slant height $\ell$ and average radius $r=\tfrac12(r_1+r_2)$ has area $2\pi r\ell$ (source, §8.2 slide 6).

About the $x$-axis, $y=f(x)\ge0$, $f'$ continuous (source, §8.2 slide 10):

$$S=\int_a^b 2\pi f(x)\sqrt{1+[f'(x)]^2}\,dx=\int_a^b 2\pi y\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx$$

Symbolic forms, with $ds$ in either its $dx$ form or its $dy$ form (source, §8.2 slide 12):

$$S=\int 2\pi y\,ds\ \ (\text{about the }x\text{-axis}),\qquad S=\int 2\pi x\,ds\ \ (\text{about the }y\text{-axis})$$

#formula

The four cases from the handout (source, §8.2 Surface Area handout):

| Axis | Curve | Surface area |
|---|---|---|
| $x$-axis | $y=f(x)$, $a\le x\le b$ | $\displaystyle\int_a^b 2\pi f(x)\sqrt{1+[f'(x)]^2}\,dx$ |
| $x$-axis | $x=g(y)$, $c\le y\le d$ | $\displaystyle\int_c^d 2\pi y\sqrt{1+[g'(y)]^2}\,dy$ |
| $y$-axis | $y=f(x)$, $a\le x\le b$ | $\displaystyle\int_a^b 2\pi x\sqrt{1+\left(\frac{dy}{dx}\right)^2}\,dx$ |
| $y$-axis | $x=g(y)$, $c\le y\le d$ | $\displaystyle\int_c^d 2\pi g(y)\sqrt{1+\left(\frac{dx}{dy}\right)^2}\,dy$ |

- Memory device: $2\pi y$ or $2\pi x$ is the circumference traced by the point $(x,y)$ as it rotates (source, §8.2 slide 13).

### Differential equations and separable equations (§9.3)

Full notes: [[MAT01B1_Notes_S13_SeparableDifferentialEquations]]. See [[MAT01B1_Notes_S13_SeparableDifferentialEquations#What a differential equation is]], [[MAT01B1_Notes_S13_SeparableDifferentialEquations#Separable equations]] and [[MAT01B1_Notes_S13_SeparableDifferentialEquations#Orthogonal trajectories]]. The reason for the $+C$ is [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7|Theorem 5 and Corollary 7]].

Terms #definition (source, §9.3 slides 2 and 6):

- A differential equation contains an unknown function and one or more of its derivatives. Its order is the order of the highest derivative in it.
- A function is a solution if the equation holds when the function and its derivatives are substituted, for all $x$ in some interval. Solving means finding all solutions.
- To check a claimed family of solutions: differentiate, substitute, and show left side equals right side (source, §9.3 slide 7). An initial condition fixes the constant (source, §9.3 slide 9).

Separable equation #definition (source, §9.3 slides 11 and 12): first order, with $\dfrac{dy}{dx}=g(x)f(y)$. If $f(y)\ne0$ write $h(y)=1/f(y)$, so

$$h(y)\,dy=g(x)\,dx\quad\Longrightarrow\quad\int h(y)\,dy=\int g(x)\,dx.$$

- This defines $y$ implicitly. Solve for $y$ only when that is possible, for example $y^2+\sin y=2x^3+C$ cannot be solved for $y$ (source, §9.3 slide 16).
- The Chain Rule justifies the method (source, §9.3 slide 13).

Orthogonal trajectories (source, §9.3 slides 20 to 23): curves meeting every member of a family at right angles.

1. Differentiate the family equation.
2. Eliminate the parameter $k$ using the family equation, leaving one differential equation for $dy/dx$.
3. Replace the slope by its negative reciprocal.
4. Solve the new equation, which is separable.

### Linear differential equations (§9.5)

Full notes: [[MAT01B1_Notes_S14_LinearDifferentialEquations]]. See [[MAT01B1_Notes_S14_LinearDifferentialEquations#Standard form]], [[MAT01B1_Notes_S14_LinearDifferentialEquations#Building the integrating factor (source, slides 3 to 7)|building the integrating factor]] and [[MAT01B1_Notes_S14_LinearDifferentialEquations#Method summary]].

Standard form, $P$ and $Q$ continuous on the interval (source, §9.5 slide 2):

$$\frac{dy}{dx}+P(x)\,y=Q(x)$$

Integrating factor and solution (source, §9.5 slides 6 to 8):

$$I(x)=e^{\int P(x)\,dx},\qquad y(x)=\frac{1}{I(x)}\left[\int I(x)\,Q(x)\,dx+C\right]$$

#formula

- Why it works: require $I\,(y'+Py)=(Iy)'$. Expanding gives $I'=IP$, which is separable, so $\ln|I|=\int P\,dx$, and the constant is taken as $A=1$ (source, §9.5 slides 5 to 7).
- Get standard form first, by dividing through if needed (source, §9.5 slide 10).
- If $\int I\,Q\,dx$ has no elementary form, leave it as an integral, or write it with a definite integral from any lower limit using the Fundamental Theorem of Calculus (source, §9.5 slides 12 and 13).

### Parametric curves (§10.1)

Full notes: [[MAT01B1_Notes_S15_ParametricEquations]], including [[MAT01B1_Notes_S15_ParametricEquations#Worked example: the cycloid (source, slides 10 to 12)|the cycloid derivation]].

Parametric equations #definition (source, §10.1 slide 2): $x=f(t)$, $y=g(t)$ with parameter $t$. For $a\le t\le b$ the curve has initial point $(f(a),g(a))$ and terminal point $(f(b),g(b))$ (source, §10.1 slide 6).

- Eliminate the parameter to identify the curve. The parametrisation still carries direction and number of passes: $x=\cos t,\ y=\sin t$ goes once counterclockwise from $(1,0)$; $x=\sin 2t,\ y=\cos 2t$ goes twice clockwise from $(0,1)$ over the same $t$-interval (source, §10.1 slides 7 to 9).
- Cycloid, radius $r$, rolling on the $x$-axis, $\theta$ the angle of rotation; one arch is $0\le\theta\le2\pi$ (source, §10.1 slides 10 to 12):

$$x=r(\theta-\sin\theta),\qquad y=r(1-\cos\theta)$$

#formula

### Calculus with parametric equations (§10.2)

Full notes: [[MAT01B1_Notes_S16_CalculusWithParametricEquations]]. See [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Tangents]], [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Area under a parametric curve]], [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Arc length of a parametric curve]] and [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Surface area]].

Tangent slope (source, §10.2 slide 2), and second derivative (source, §10.2 slide 4):

$$\frac{dy}{dx}=\frac{dy/dt}{dx/dt}\quad(dx/dt\ne0),\qquad \frac{d^2y}{dx^2}=\frac{\dfrac{d}{dt}\!\left(\dfrac{dy}{dx}\right)}{dx/dt}$$

#formula

- Horizontal tangent: $dy/dt=0$ with $dx/dt\ne0$. Vertical tangent: $dx/dt=0$ with $dy/dt\ne0$ (source, §10.2 slide 3).
- If both derivatives are $0$ at a point, examine the limit of $dy/dx$, for example with l'Hospital's Rule at the cycloid points $\theta=2n\pi$, where the tangent is vertical (source, §10.2 slides 10 and 11).

Area under a parametrised curve traced once, $F\ge0$ (source, §10.2 slide 12):

$$A=\int_a^b y\,dx=\int_\alpha^\beta g(t)\,f'(t)\,dt$$

Arc length theorem #theorem (source, §10.2 slide 19):

- Hypotheses: $x=f(t)$, $y=g(t)$, $\alpha\le t\le\beta$, with $f'$ and $g'$ continuous on $[\alpha,\beta]$, and $C$ traversed exactly once as $t$ goes from $\alpha$ to $\beta$.

$$L=\int_\alpha^\beta\sqrt{\left(\frac{dx}{dt}\right)^2+\left(\frac{dy}{dt}\right)^2}\,dt$$

- Proof: full derivation in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Arc length of a parametric curve]], which applies [[MAT01B1_Proofs_ST1#Mean Value Theorem|the Mean Value Theorem]] once to $f$ and once to $g$ (source, §10.2 slides 14 to 18).

Surface area about the $x$-axis, with $f',g'$ continuous, $g(t)\ge0$, curve traversed once (source, §10.2 slide 25):

$$S=\int_\alpha^\beta 2\pi y\sqrt{\left(\frac{dx}{dt}\right)^2+\left(\frac{dy}{dt}\right)^2}\,dt$$

### Polar coordinates (§10.3)

Full notes: [[MAT01B1_Notes_S17_PolarCoordinates]]. See [[MAT01B1_Notes_S17_PolarCoordinates#Multiple representations]], [[MAT01B1_Notes_S17_PolarCoordinates#Converting between polar and Cartesian]] and [[MAT01B1_Notes_S17_PolarCoordinates#Polar curves]].

Polar coordinates #definition (source, §10.3 slides 3 and 4):

- $P=(r,\theta)$: $r$ is the distance from the pole $O$, and $\theta$ is the angle from the polar axis, positive counterclockwise. $(0,\theta)$ is the pole for every $\theta$.
- For $r<0$, the point $(r,\theta)$ is $|r|$ from $O$ on the opposite side of $O$ from the direction $\theta$.
- Representations are not unique. The point $(r,\theta)$ is also $(r,\theta+2n\pi)$ and $(-r,\theta+(2n+1)\pi)$ for any integer $n$ (source, §10.3 slide 6).

Conversions (source, §10.3 slides 7 to 9). The first pair holds for all $r$ and $\theta$:

$$x=r\cos\theta,\quad y=r\sin\theta\qquad\qquad r^2=x^2+y^2,\quad \tan\theta=\frac{y}{x}\ \ (x\ne0)$$

#formula

- Going from $(x,y)$ to $(r,\theta)$: $\tan\theta$ alone does not fix $\theta$, so choose $\theta$ in the correct quadrant (source, §10.3 slide 12).
- Polar curve: all points with at least one representation satisfying the equation (source, §10.3 slide 13).
- $r=a$ is the circle with centre $O$ and radius $|a|$. $\theta=c$ is a line through $O$. $r=2\cos\theta$ is the circle $(x-1)^2+y^2=1$. $r=\cos2\theta$ is a four-leaved rose (source, §10.3 slides 13 to 19).

## Worked example notebook

One representative example per distinct principle. Each is taken from the slides, and the label says where.

### Related rates

Full working: [[MAT01B1_Notes_S4_RelatedRates#Worked example: sliding ladder (source, slides 6 to 8)|ladder]], [[MAT01B1_Notes_S4_RelatedRates#Worked example: filling cone (source, slides 9 to 12)|cone]], [[MAT01B1_Notes_S4_RelatedRates#Worked example: rotating searchlight (source, slides 18 to 19)|searchlight]].

Pythagorean relation and sign #worked-example (source, §3.9 slides 6 to 8). A 5 m ladder, bottom sliding away at $dx/dt=1$ m/s. Find $dy/dt$ when $x=3$.

$$x^2+y^2=25\ \Rightarrow\ 2x\frac{dx}{dt}+2y\frac{dy}{dt}=0\ \Rightarrow\ \frac{dy}{dt}=-\frac{x}{y}\frac{dx}{dt}$$

With $x=3$, $y=4$, so $dy/dt=-\tfrac34$ m/s. The negative sign says the top is sliding down.

Eliminating a variable with similar triangles #worked-example (source, §3.9 slides 9 to 12). Cone tank, radius 2 m, height 4 m, $dV/dt=2$ m$^3$/min. Find $dh/dt$ at $h=3$.

$$\frac rh=\frac24\Rightarrow r=\frac h2,\qquad V=\frac13\pi\left(\frac h2\right)^2h=\frac{\pi}{12}h^3,\qquad \frac{dV}{dt}=\frac{\pi}{4}h^2\frac{dh}{dt}$$

So $\dfrac{dh}{dt}=\dfrac{4}{9\pi}\cdot2=\dfrac{8}{9\pi}\approx0.28$ m/min.

Trigonometric relation, angular rate #worked-example (source, §3.9 slides 18 and 19). Searchlight 6 m from the path, man walking at $dx/dt=1.5$ m/s. Find $d\theta/dt$ at $x=8$.

$$x=6\tan\theta\ \Rightarrow\ \frac{dx}{dt}=6\sec^2\theta\frac{d\theta}{dt}\ \Rightarrow\ \frac{d\theta}{dt}=\frac{1}{4}\cos^2\theta$$

At $x=8$ the beam has length 10, so $\cos\theta=\tfrac35$ and $d\theta/dt=\tfrac{9}{100}=0.09$ rad/s.

### Optimization

Full working: [[MAT01B1_Notes_S5_OptimizationProblems#Worked example: rectangular field along a river (source, slides 6 to 9)|fencing]], [[MAT01B1_Notes_S5_OptimizationProblems#Worked example: minimum-surface-area can (source, slides 10 to 14)|can]], [[MAT01B1_Notes_S5_OptimizationProblems#Worked example: closest point on a parabola (source, slides 17 to 19)|closest point]].

Closed interval method #worked-example (source, §4.7 slides 6 to 9). 1200 m of fencing, three sides of a rectangle, river on the fourth. $A(x)=1200x-2x^2$ on $[0,600]$. $A'(x)=1200-4x=0$ gives $x=300$. $A(0)=0$, $A(300)=180\,000$, $A(600)=0$. Depth 300 m, width 600 m, area $180\,000\ \text{m}^2$.

First Derivative Test on an open domain #worked-example (source, §4.7 slides 10 to 14; the problem statement slide is not in the deck, the 1 L volume constraint is on slide 11). Can of volume $1000\ \text{cm}^3$, minimise surface area:

$$A(r)=2\pi r^2+\frac{2000}{r}\ (r>0),\qquad A'(r)=\frac{4(\pi r^3-500)}{r^2}$$

$A'<0$ for $r<r_0$ and $A'>0$ for $r>r_0$ where $r_0=\sqrt[3]{500/\pi}$, so $A(r_0)$ is the absolute minimum, and $h=2r_0$.

Minimising a squared distance #worked-example (source, §4.7 slides 17 to 19). Point on $y^2=2x$ closest to $(1,4)$. With $x=\tfrac12y^2$, minimise $f(y)=\left(\tfrac12y^2-1\right)^2+(y-4)^2$. Then $f'(y)=y^3-8$, so $y=2$, the point is $(2,2)$ and the distance is $\sqrt5$.

### Average value and the MVT for Integrals

Full working: [[MAT01B1_Notes_S10_AverageValueOfAFunction#Worked example: average value of $1+x^2$ (source, slide 6)|average value]] and [[MAT01B1_Notes_S10_AverageValueOfAFunction#Worked example: finding $c$ explicitly (source, slide 10)|finding $c$]].

#worked-example (source, §6.5 slides 6 and 10). $f(x)=1+x^2$ on $[-1,2]$:

$$f_{\text{ave}}=\frac13\left[x+\frac{x^3}{3}\right]_{-1}^{2}=\frac13\cdot6=2$$

$f(c)=2$ gives $1+c^2=2$, so $c=\pm1$. Both lie in $[-1,2]$.

### Area between curves

Full working: [[MAT01B1_Notes_S7_AreaBetweenCurves#Worked example: region between $\sin x$ and $\cos x$ (source, slides 16 to 17)|sin and cos]], [[MAT01B1_Notes_S7_AreaBetweenCurves#Worked example: area via $y$-strips (source, slides 19 to 20)|$y$-strips]].

Splitting at a crossing #worked-example (source, §6.1 slides 16 and 17). Between $y=\sin x$ and $y=\cos x$ for $0\le x\le\pi/2$, the curves cross at $\pi/4$:

$$A=\int_0^{\pi/4}(\cos x-\sin x)\,dx+\int_{\pi/4}^{\pi/2}(\sin x-\cos x)\,dx=2\sqrt2-2$$

Symmetry about $x=\pi/4$ gives the shortcut $A=2\int_0^{\pi/4}(\cos x-\sin x)\,dx$.

Integrating in $y$ #worked-example (source, §6.1 slides 19 and 20). Region between $y=x-1$ and $y^2=2x+6$, meeting at $(-1,-2)$ and $(5,4)$. Left boundary $x=\tfrac12y^2-3$, right boundary $x=y+1$:

$$A=\int_{-2}^{4}\left[(y+1)-\left(\tfrac12y^2-3\right)\right]dy=18$$

### Volumes

Full working: [[MAT01B1_Notes_S8_Volumes#Worked example: washer method, axis shifted off the boundary (source, slides 19 to 20)|washer about y=2]], [[MAT01B1_Notes_S8_Volumes#Worked example: disk method, rotating about the $y$-axis (source, slides 15 to 16)|disk about the y-axis]], [[MAT01B1_Notes_S8_Volumes#Worked example: non-circular cross-sections, equilateral triangles (source, slides 27 to 29)|equilateral triangles]].

Washer about a shifted line #worked-example (source, §6.2 slides 19 and 20). Region between $y=x$ and $y=x^2$ rotated about $y=2$. Outer radius $2-x^2$, inner radius $2-x$:

$$V=\pi\int_0^1\big[(2-x^2)^2-(2-x)^2\big]dx=\pi\int_0^1(x^4-5x^2+4x)\,dx=\frac{8\pi}{15}$$

Disk about the $y$-axis #worked-example (source, §6.2 slides 15 and 16). Region bounded by $y=x^3$, $y=8$, $x=0$ rotated about the $y$-axis. Slice perpendicular to the $y$-axis, radius $x=y^{1/3}$:

$$V=\pi\int_0^8y^{2/3}\,dy=\frac{96\pi}{5}$$

Known cross-sections #worked-example (source, §6.2 slides 27 to 29). Base is the unit circle, slices perpendicular to the base are equilateral triangles. Base of the triangle $2\sqrt{1-x^2}$, height $\sqrt3\sqrt{1-x^2}$:

$$V=\int_{-1}^{1}\sqrt3\,(1-x^2)\,dx=\frac{4\sqrt3}{3}$$

### Cylindrical shells

Full working: [[MAT01B1_Notes_S9_CylindricalShells#Worked example: the motivating region, resolved with shells (source, slides 11 to 14)|motivating region]], [[MAT01B1_Notes_S9_CylindricalShells#Worked example: shells about a vertical line other than the axis (source, slides 19 to 20)|shells about x=2]].

Shells when solving for $x$ is hard #worked-example (source, §6.3 slides 11 and 12). Region between $y=2x^2-x^3$ and $y=0$ about the $y$-axis. A washer would need $x$ in terms of $y$ from a cubic. With shells:

$$V=\int_0^2 2\pi x\,(2x^2-x^3)\,dx=2\pi\left[\frac{x^4}{2}-\frac{x^5}{5}\right]_0^2=\frac{16\pi}{5}$$

Shells about a line other than the $y$-axis #worked-example (source, §6.3 slides 19 and 20). Region between $y=x-x^2$ and $y=0$ about $x=2$. Radius $2-x$, height $x-x^2$:

$$V=\int_0^1 2\pi(2-x)(x-x^2)\,dx=2\pi\int_0^1(x^3-3x^2+2x)\,dx=\frac{\pi}{2}$$

### Arc length

Full working: [[MAT01B1_Notes_S11_ArcLength#Worked example: semicubical parabola (source, slides 10 to 12)|semicubical parabola]], [[MAT01B1_Notes_S11_ArcLength#Worked example: arc length function (source, slides 19 to 20)|arc length function]].

Substitution #worked-example (source, §8.1 slides 10 to 12). Semicubical parabola $y^2=x^3$ from $(1,1)$ to $(4,8)$. Top half $y=x^{3/2}$, $y'=\tfrac32x^{1/2}$, and with $u=1+\tfrac94x$:

$$L=\int_1^4\sqrt{1+\tfrac94x}\,dx=\frac{4}{9}\cdot\frac23\Big[u^{3/2}\Big]_{13/4}^{10}=\frac{1}{27}\left(80\sqrt{10}-13\sqrt{13}\right)$$

Arc length function, perfect square under the root #worked-example (source, §8.1 slides 19 and 20). $y=x^2-\tfrac18\ln x$ from $(1,1)$. Here $1+[f'(x)]^2=\left(2x+\tfrac{1}{8x}\right)^2$, so

$$s(x)=\int_1^x\left(2t+\frac{1}{8t}\right)dt=x^2+\frac18\ln x-1,\qquad s(3)=8+\frac{\ln3}{8}\approx8.1373$$

### Surface area

Full working: [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution#Worked example: a portion of a sphere (source, slides 14 to 16)|sphere portion]], [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution#Worked example: a parabola about the y-axis, two ways (source, slides 17 to 19)|parabola about the y-axis]].

Simplification under the root #worked-example (source, §8.2 slides 14 to 16). $y=\sqrt{4-x^2}$, $-1\le x\le1$, about the $x$-axis. Since $1+(y')^2=\dfrac{4}{4-x^2}$,

$$S=2\pi\int_{-1}^{1}\sqrt{4-x^2}\cdot\frac{2}{\sqrt{4-x^2}}\,dx=4\pi\int_{-1}^{1}dx=8\pi$$

About the $y$-axis with $2\pi x\,ds$ #worked-example (source, §8.2 slides 17 and 18). $y=x^2$ from $(1,1)$ to $(2,4)$ about the $y$-axis, with $u=1+4x^2$:

$$S=\int_1^2 2\pi x\sqrt{1+4x^2}\,dx=\frac{\pi}{4}\int_5^{17}\sqrt u\,du=\frac{\pi}{6}\left(17\sqrt{17}-5\sqrt5\right)$$

The slides redo it as $x=\sqrt y$ with $2\pi x\,ds$ in $dy$ form and get the same value (source, §8.2 slide 19).

### Separable equations

Full working: [[MAT01B1_Notes_S13_SeparableDifferentialEquations#Worked example: $y'=x^2/y^2$, with an initial condition (source, slides 14 to 15)|initial-value problem]], [[MAT01B1_Notes_S13_SeparableDifferentialEquations#Worked example: $y'=x^2y$ (source, slides 17 to 18)|dividing by y]], [[MAT01B1_Notes_S13_SeparableDifferentialEquations#Worked example: orthogonal trajectories of a family of parabolas (source, slides 21 to 23)|orthogonal trajectories]].

Initial-value problem #worked-example (source, §9.3 slides 14 and 15). $\dfrac{dy}{dx}=\dfrac{x^2}{y^2}$, $y(0)=2$. Then $y^2\,dy=x^2\,dx$, so $\tfrac13y^3=\tfrac13x^3+C$, so $y=\sqrt[3]{x^3+K}$ with $K=3C$. The condition gives $K=8$:

$$y=\sqrt[3]{x^3+8}$$

Dividing by $y$ #worked-example (source, §9.3 slides 17 and 18). $y'=x^2y$. For $y\ne0$: $\displaystyle\int\frac{dy}{y}=\int x^2\,dx$, so $\ln|y|=\tfrac{x^3}{3}+C$ and $y=Ae^{x^3/3}$. See the correction in Common mistakes about $A=0$.

Orthogonal trajectories #worked-example (source, §9.3 slides 21 to 23). Family $x=ky^2$. Differentiating and eliminating $k=x/y^2$ gives $\dfrac{dy}{dx}=\dfrac{y}{2x}$. Trajectories satisfy $\dfrac{dy}{dx}=-\dfrac{2x}{y}$, so $\displaystyle\int y\,dy=-\int2x\,dx$ and

$$x^2+\frac{y^2}{2}=C\qquad(C>0),$$

a family of ellipses.

### Linear equations

Full working: [[MAT01B1_Notes_S14_LinearDifferentialEquations#Worked example: an initial value problem (source, slides 10 to 11)|standard form first]], [[MAT01B1_Notes_S14_LinearDifferentialEquations#Worked example: a non-elementary integral (source, slides 12 to 13)|non-elementary integral]].

Not yet in standard form #worked-example (source, §9.5 slides 10 and 11). $x^2y'+xy=1$, $x>0$, $y(1)=2$. Divide by $x^2$: $y'+\tfrac1xy=\tfrac1{x^2}$. Then $I(x)=e^{\ln x}=x$, so $(xy)'=\tfrac1x$, $xy=\ln x+C$, and $y(1)=2$ gives $C=2$:

$$y=\frac{\ln x+2}{x}$$

Non-elementary integral #worked-example (source, §9.5 slides 12 and 13). $y'+2xy=1$ has $I=e^{x^2}$, so $y=e^{-x^2}\displaystyle\int e^{x^2}\,dx+Ce^{-x^2}$. It stays as an integral, or is written $y=e^{-x^2}\displaystyle\int_0^xe^{t^2}\,dt+Ce^{-x^2}$.

### Parametric curves

Full working: [[MAT01B1_Notes_S15_ParametricEquations#Worked example: identifying a curve by eliminating the parameter (source, slides 3 to 6)|eliminating the parameter]], [[MAT01B1_Notes_S15_ParametricEquations#Worked example: the unit circle, traced once (source, slides 7 to 8)|circle once]], [[MAT01B1_Notes_S15_ParametricEquations#Worked example: the unit circle, traced twice (source, slide 9)|circle twice]].

Eliminating the parameter #worked-example (source, §10.1 slides 3 to 5). $x=t^2-2t$, $y=t+1$. From $t=y-1$:

$$x=(y-1)^2-2(y-1)=y^2-4y+3$$

a parabola.

Same curve, different tracing #worked-example (source, §10.1 slides 7 to 9 and §10.2 slides 20 and 21). $x=\cos t,\ y=\sin t$ and $x=\sin2t,\ y=\cos2t$, both for $0\le t\le2\pi$, give the unit circle. Arc lengths from the theorem are $2\pi$ (once round) and $4\pi$ (twice round).

### Calculus with parametric equations

Full working: [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: a self-crossing curve (source, slides 5 to 8)|self-crossing curve]], [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: area under one arch of the cycloid (source, slide 13)|cycloid area]], [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: arc length of one arch of the cycloid (source, slides 22 to 24)|cycloid arc length]], [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: surface area of a sphere (source, slides 25 to 26)|sphere surface area]].

Tangents, extremes and concavity #worked-example (source, §10.2 slides 5 to 8). $x=t^2$, $y=t^3-3t$.

- Self-crossing: $y=0$ at $t=0,\pm\sqrt3$, so $(3,0)$ comes from $t=\pm\sqrt3$. With $\dfrac{dy}{dx}=\dfrac{3t^2-3}{2t}=\dfrac32\left(t-\dfrac1t\right)$ the slopes there are $\pm\sqrt3$, giving tangents $y=\pm\sqrt3\,(x-3)$.
- Horizontal tangents at $t=\pm1$, points $(1,-2)$ and $(1,2)$. Vertical tangent at $t=0$, point $(0,0)$.
- Concavity: $\dfrac{d^2y}{dx^2}=\dfrac{3(t^2+1)}{4t^3}$, concave up for $t>0$, concave down for $t<0$.

Area under one cycloid arch #worked-example (source, §10.2 slide 13):

$$A=\int_0^{2\pi}r(1-\cos\theta)\cdot r(1-\cos\theta)\,d\theta=r^2\int_0^{2\pi}\left[\tfrac32-2\cos\theta+\tfrac12\cos2\theta\right]d\theta=3\pi r^2$$

Arc length of one cycloid arch #worked-example (source, §10.2 slides 22 to 24). Using $1-\cos\theta=2\sin^2(\theta/2)$ and $\sin(\theta/2)\ge0$ on $[0,2\pi]$:

$$L=r\int_0^{2\pi}\sqrt{2(1-\cos\theta)}\,d\theta=2r\int_0^{2\pi}\sin\frac\theta2\,d\theta=8r$$

Surface area of a sphere #worked-example (source, §10.2 slide 26). Semicircle $x=r\cos t$, $y=r\sin t$, $0\le t\le\pi$, about the $x$-axis:

$$S=\int_0^\pi2\pi r\sin t\cdot r\,dt=2\pi r^2\Big[-\cos t\Big]_0^\pi=4\pi r^2$$

### Polar coordinates

Full working: [[MAT01B1_Notes_S17_PolarCoordinates#Worked example: polar to Cartesian (source, slide 10)|polar to Cartesian]], [[MAT01B1_Notes_S17_PolarCoordinates#Worked example: Cartesian to polar (source, slide 11)|Cartesian to polar]], [[MAT01B1_Notes_S17_PolarCoordinates#Worked example: $r=2\cos\theta$ (source, slides 15 to 17)|r = 2cos theta]].

Polar to Cartesian #worked-example (source, §10.3 slide 10). $(2,\pi/3)$: $x=2\cos\tfrac\pi3=1$, $y=2\sin\tfrac\pi3=\sqrt3$, so $(1,\sqrt3)$.

Cartesian to polar, quadrant check #worked-example (source, §10.3 slide 11). $(1,-1)$: $r=\sqrt2$, $\tan\theta=-1$, and the point is in the fourth quadrant, so $(\sqrt2,-\pi/4)$ or $(\sqrt2,7\pi/4)$.

Polar equation to Cartesian #worked-example (source, §10.3 slide 17). $r=2\cos\theta$: multiply through by $r$ using $\cos\theta=x/r$, so $r^2=2x$, hence $x^2+y^2-2x=0$ and

$$(x-1)^2+y^2=1,$$

the circle with centre $(1,0)$ and radius $1$.

## Common mistakes

No handoff memos or struggle logs were supplied for these sessions, so nothing here is drawn from those. What follows are slips found in the slides themselves. Each is stated as it appears, with the correct version marked `(added)`, so the wrong version is not learned. #common-mistake

- §3.9 slide 10 ([[MAT01B1_Notes_S4_RelatedRates#Worked example: filling cone (source, slides 9 to 12)|Related Rates note]]) writes the given rate as $dy/dt=2$ m$^3$/min. It is $dV/dt$ `(added)`.
- §6.1 slide 13 ([[MAT01B1_Notes_S7_AreaBetweenCurves#Worked example: curves with no exact intersection point (source, slides 11 to 13)|Area Between Curves note]]) writes the upper limit $2.29$ for the $u$-integral. Slide 12 has $u\approx2.39$ and the next line uses $\sqrt{2.39}$, so the limit is $2.39$ `(added)`.
- §6.2 slide 10, volume of a sphere ([[MAT01B1_Notes_S8_Volumes#Worked example: volume of a sphere (source, slides 9 to 10)|Volumes note]]), writes $2\pi\int_0^r\pi(r^2-x^2)\,dx$ with an extra $\pi$, and gives the bracket's upper limit as $1$. It should be $2\int_0^r\pi(r^2-x^2)\,dx=2\pi\left[r^2x-\tfrac{x^3}{3}\right]_0^r$ `(added)`.
- §6.2 slide 26 ([[MAT01B1_Notes_S8_Volumes#Worked example: washer method, rotating about a vertical line, sliced in $y$ (source, slides 24 to 26)|Volumes note]]) ends the second line with $dx$ although the variable is $y$. It is $dy$ `(added)`.
- §9.3 slide 15 ([[MAT01B1_Notes_S13_SeparableDifferentialEquations#Worked example: $y'=x^2/y^2$, with an initial condition (source, slides 14 to 15)|Separable Equations note]]) says "we must have $\sqrt[3]{K}$ and so $K=8$". The condition is $\sqrt[3]{K}=2$ `(added)`.
- §9.3 slide 18 ([[MAT01B1_Notes_S13_SeparableDifferentialEquations#Worked example: $y'=x^2y$ (source, slides 17 to 18)|Separable Equations note]]) says $y=0$ cannot be a solution of $y'=x^2y$. It is one, since $0=x^2\cdot0$. So $y=Ae^{x^3/3}$ holds for every real $A$, including $A=0$ `(added)`.
- §10.2 slide 26 ([[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: surface area of a sphere (source, slides 25 to 26)|Calculus with Parametric Equations note]]) has a stray leading $2\pi$ on the second line of the sphere calculation, in front of $\int_0^\pi2\pi r\sin t\ldots$. The integral already contains the $2\pi$ `(added)`.
- §10.3 slide 4 ([[MAT01B1_Notes_S17_PolarCoordinates|Polar Coordinates note]]) says $(r,\theta)$ is the same point as $(r,\theta+\pi)$. It is $(-r,\theta)$ that equals $(r,\theta+\pi)$, matching slide 6 `(added)`.
- §10.3 slide 19 ([[MAT01B1_Notes_S17_PolarCoordinates#Worked example: $r=\cos2\theta$, the four-leaved rose (source, slides 18 to 19)|Polar Coordinates note]]) says $r$ goes from $0$ to $2\pi$ as $\theta$ goes from $\pi/4$ to $\pi/2$ on $r=\cos2\theta$. It goes from $0$ to $-1$ `(added)`.

> [!warning] Two of these slips are copied into the vault notes
> - [[MAT01B1_Notes_S13_SeparableDifferentialEquations]] (the $y'=x^2y$ example) repeats the slide's claim that $y=0$ is not a solution and calls $A$ nonzero. Correct: $y=0$ is a solution, and $A$ can be any real number.
> - [[MAT01B1_Notes_S17_PolarCoordinates]] (under Negative $r$) says $(r,\theta)$ and $(r,\theta+\pi)$ are the same point. Correct: $(-r,\theta)$ and $(r,\theta+\pi)$ are.
>
> The other seven slips were already corrected when those notes were written.

## Tips

No handoff memos or session discussion were available for these sessions, so every tip below is one the slides state or show.

- Related rates: differentiate first, substitute the instant's values second (source, §3.9 slide 13). A shrinking quantity has a negative rate (source, §3.9 slides 8 and 16).
- Optimization: the modelling is the real work, so write the domain before differentiating (source, §4.7 slides 3 to 5). Closed interval means test the endpoints too; open domain means use the First Derivative Test for Absolute Extreme Values.
- Volumes and shells: sketch a sample rectangle first. Its thickness gives the variable and whether it revolves into a disk, washer or shell (source, §6.3 slides 21 and 22). Radii come from the axis of rotation, not always from $0$.
- Area: if the curves cross inside $[a,b]$, use $|f-g|$ and split. Look for symmetry to halve the work (source, §6.1 slide 17).
- Arc length: in the source's arc length function example the expression under the root collapsed to a perfect square, which is what made the integral easy (source, §8.1 slide 19). Try completing the square early.
- Surface area: match $ds$ to the variable of integration, and the circumference factor to the axis: $2\pi y$ for the $x$-axis, $2\pi x$ for the $y$-axis (source, §8.2 slides 12 and 13).
- Separable: only divide by $y$ after noting $y\ne0$, and then check $y=0$ separately (source, §9.3 slide 17). Merge constants into one, for example $K=3C$ (source, §9.3 slide 14).
- Linear: rewrite in standard form before reading off $P(x)$ (source, §9.5 slide 10). Setting the integration constant in $I$ to $A=1$ is enough.
- Parametric: the tangent slope needs $dx/dt\ne0$. When both derivatives vanish, take a limit (source, §10.2 slides 10 and 11). One cycloid arch is $0\le\theta\le2\pi$.
- Polar: $\tan\theta=y/x$ does not fix $\theta$, so check the quadrant (source, §10.3 slide 12). A point has many polar representations, so two different-looking answers can both be right.

## See also
- [[MAT01B1_Proofs_ST1]] (Fermat's Theorem, Rolle's Theorem, Mean Value Theorem, Theorem 5 and Corollary 7)
- [[MAT01B1_Notes_S11_ArcLength]] and [[MAT01B1_Notes_S12_SurfaceAreaOfRevolution]] (rotating curves: arc length and surface area)
- [[MAT01B1_Notes_S1_CalculusApplications]] (extremum theory, curve sketching, improper integrals)
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]] (derivative and integral formulas used throughout)
- [[MAT01B1_Notes_S3_IntegrationExamples]] (worked integration techniques)
