---
module: MAT01B1
topic: ST2 proofs
tags: [theorem, formula]
---

# MAT01B1 ST2 Proofs

Scope: every theorem or formula between Related Rates (section 3.9) and Polar Coordinates (section 10.3) whose derivation is actually shown in Dr K's slides, plus two derivations taken from past paper memos. Each proof is labelled with where it came from.

Source labels used below:
- `(source, [deck], slide N)` is a slide in Dr K's PDF deck, numbered by PDF page.
- `(source: 2023 ST2 memo, Q7a)` is the MAT01B1 2023 Semester Test 2 memo.
- `(source: engineering ST2 memo photo, Q5)` is the photographed engineering department ST2 memo, Question 5.
- `(added)` marks anything I introduced beyond the source.

Where the source says a step is only "plausible", "it can be shown", or is left as an exercise, this file says so plainly.

---

## Mean Value Theorem for Integrals, proof 1 (EVT and IVT) #theorem

Statement (source, MVT Integrals, slide 1):

> If f is continuous on [a, b], then there exists a number c in [a, b] such that

$$f(c) = f_{ave} = \frac{1}{b-a}\int_a^b f(x)\,dx.$$

> Alternatively,

$$\int_a^b f(x)\,dx = f(c)(b-a)$$

Hypotheses:
- f is continuous on [a, b]

Proof (source, MVT Integrals, slides 4 to 8):

Case 1: f is constant on [a, b]. Let f(x) = z for all x in [a, b]. Then f(c) = z for all c in [a, b], so

$$f_{ave} = \frac{1}{b-a}\int_a^b f(x)\,dx = \frac{1}{b-a}\int_a^b z\,dx = \frac{1}{b-a}\,[z\cdot x]_a^b = z = f(c)$$

for any c in [a, b].

Case 2: f is not constant on [a, b].
- Since f is continuous on [a, b], by the Extreme Value Theorem there exist values m and M (both in [a, b]) such that f(m) is the absolute minimum and f(M) is the absolute maximum value of f on [a, b].
- Thus for any x in [a, b]:

$$f(m) \le f(x) \le f(M).$$

- Hence

$$\int_a^b f(m)\,dx \le \int_a^b f(x)\,dx \le \int_a^b f(M)\,dx.$$

- Therefore

$$[f(m)\,x]_a^b \le \int_a^b f(x)\,dx \le [f(M)\,x]_a^b$$

$$f(m)(b-a) \le \int_a^b f(x)\,dx \le f(M)(b-a)$$

$$f(m) \le \frac{1}{b-a}\int_a^b f(x)\,dx \le f(M).$$

- Since f is continuous on [a, b], it is continuous on the interval between m and M. Since the number

$$\frac{1}{b-a}\int_a^b f(x)\,dx$$

is between f(m) and f(M), by the Intermediate Value Theorem there exists c between m and M such that

$$f(c) = \frac{1}{b-a}\int_a^b f(x)\,dx.$$

- As c is between m and M, we have c in [a, b]. This completes the proof.

---

## Mean Value Theorem for Integrals, proof 2 (FTC and MVT) #theorem

Statement: same as in Mean Value Theorem for Integrals, proof 1 (EVT and IVT).

Hypotheses:
- f : [a, b] -> R is continuous

Proof (source: engineering ST2 memo photo, Q5):
- Define F : [a, b] -> R by

$$F(x) = \int_a^x f(t)\,dt \quad \text{for each } x \in [a, b].$$

- By the Fundamental Theorem of Calculus, F is continuous on [a, b], differentiable on (a, b), and F'(x) = f(x).
- So by the (ordinary) mean value theorem there exists a number c in [a, b] such that

$$F'(c) = \frac{F(b) - F(a)}{b - a}$$

$$\Rightarrow\; f(c) = \frac{\int_a^b f(t)\,dt - \int_a^a f(t)\,dt}{b-a}$$

$$\Rightarrow\; f(c) = \frac{1}{b-a}\int_a^b f(x)\,dx.$$

(added) The ordinary mean value theorem gives c in the open interval (a, b), which lies inside [a, b], and the integral from a to a is 0.

---

## Average value of a function (derivation from Riemann sums) #formula

Formula (source, 6.5 Average value, slide 5):

$$f_{ave} = \frac{1}{b-a}\int_a^b f(x)\,dx$$

Hypotheses:
- y = f(x) on the interval a <= x <= b
- the definite integral of f over [a, b] exists

Derivation (source, 6.5 Average value, slides 3 to 5):
- For finitely many numbers y_1, y_2, ..., y_n:

$$y_{ave} = \frac{y_1 + y_2 + \cdots + y_n}{n}.$$

- Divide [a, b] into n equal subintervals, each of width

$$\Delta x = \frac{b-a}{n}.$$

- Choose points x_1*, ..., x_n* in successive subintervals and average the numbers f(x_1*), ..., f(x_n*):

$$\frac{f(x_1^*) + \cdots + f(x_n^*)}{n}.$$

- Since Δx = (b - a)/n, we can write n = (b - a)/Δx, and the average becomes

$$\frac{f(x_1^*) + \cdots + f(x_n^*)}{\frac{b-a}{\Delta x}} = \frac{1}{b-a}\,[f(x_1^*) + \cdots + f(x_n^*)]\,\Delta x$$

$$= \frac{1}{b-a}\,[f(x_1^*)\Delta x + \cdots + f(x_n^*)\Delta x] = \frac{1}{b-a}\sum_{i=1}^{n} f(x_i^*)\,\Delta x.$$

- As n increases, the limiting value is

$$\lim_{n\to\infty}\frac{1}{b-a}\sum_{i=1}^{n} f(x_i^*)\,\Delta x = \frac{1}{b-a}\int_a^b f(x)\,dx$$

by the definition of a definite integral.
- Therefore the average value of f on [a, b] is defined as the formula above.

---

## Limit of the average value of f on [x, x + h] #theorem

Statement (source: 2023 ST2 memo, Q7a): if f is a continuous function on R, then

$$\lim_{h\to 0} f_{ave}\ \text{on}\ [x, x+h] = f(x).$$

Hypotheses:
- f is continuous on R

Proof (source: 2023 ST2 memo, Q7a):

$$\lim_{h\to 0} f_{ave} = \lim_{h\to 0}\frac{1}{(x+h)-x}\int_x^{x+h} f(t)\,dt = \lim_{h\to 0}\frac{1}{h}\Big[F(t)\Big]_x^{x+h}, \quad \text{where } F'(t) = f(t)$$

$$= \lim_{h\to 0}\frac{F(x+h) - F(x)}{h} = F'(x) = f(x).$$

(added) The memo writes the integrand as f(x) with variable x; t is used here so the dummy variable does not clash with the endpoint x. The last step is the definition of the derivative of F.

---

## Area between curves (formula) #formula

Formula (source, 6.1 Area between curves, slide 5):

> The area A of the region bounded by the curves y = f(x), y = g(x), and the lines x = a, x = b, where f and g are continuous and f(x) >= g(x) for all x in [a, b], is

$$A = \int_a^b [f(x) - g(x)]\,dx$$

Hypotheses:
- f and g are continuous
- f(x) >= g(x) for all x in [a, b]

Derivation (source, 6.1 Area between curves, slides 2 to 5):
- Let S be the region between y = f(x) and y = g(x) and between the vertical lines x = a and x = b.
- Divide S into n strips of equal width and approximate the ith strip by a rectangle with base Δx and height f(x_i*) - g(x_i*).
- The approximation appears to become better as n goes to infinity, so the area A of S is defined as the limiting value of the sum of the areas of the rectangles:

$$A = \lim_{n\to\infty}\sum_{i=1}^{n}\,[f(x_i^*) - g(x_i^*)]\,\Delta x.$$

- We recognise this limit as the definite integral of f - g, which gives the formula above.

---

## Volume by cross-sections (definition of volume) #formula

Formula (source, 6.2 Volumes, slide 8):

> Let S be a solid that lies between x = a and x = b. If the cross-sectional area of S in the plane P_x, through x and perpendicular to the x-axis, is A(x), where A is a continuous function, then the volume of S is

$$V = \lim_{n\to\infty}\sum_{i=1}^{n} A(x_i^*)\,\Delta x = \int_a^b A(x)\,dx.$$

Hypotheses:
- S lies between x = a and x = b
- A(x), the cross-sectional area in the plane P_x perpendicular to the x-axis, is continuous

Derivation (source, 6.2 Volumes, slides 6 to 8):
- Divide S into n slabs of equal width Δx using the planes P_x1, P_x2, ...
- Choose sample points x_i* and approximate the ith slab S_i by a cylinder with base area A(x_i*) and height Δx.
- The volume of this cylinder is A(x_i*)Δx, so

$$V(S_i) \approx A(x_i^*)\,\Delta x.$$

- Adding the slab volumes:

$$V \approx \sum_{i=1}^{n} A(x_i^*)\,\Delta x.$$

- This approximation appears to become better and better as n goes to infinity, so the volume is defined as the limit of these sums.

---

## Volume of a sphere #formula

Statement (source, 6.2 Volumes, slide 9): the volume of a sphere of radius r is

$$V = \frac{4}{3}\pi r^3.$$

Hypotheses:
- sphere of radius r, centre at the origin

Derivation (source, 6.2 Volumes, slides 9 to 10):
- With the centre at the origin, the plane P_x intersects the sphere in a circle whose radius (from the Pythagorean Theorem) is

$$y = \sqrt{r^2 - x^2}.$$

- So the cross-sectional area is

$$A(x) = \pi y^2 = \pi(r^2 - x^2).$$

- Using the definition of volume with a = -r and b = r:

$$V = \int_{-r}^{r} A(x)\,dx = \int_{-r}^{r} \pi(r^2 - x^2)\,dx$$

$$= 2\pi\int_0^r (r^2 - x^2)\,dx \quad \text{(the integrand is even)}$$

$$= 2\pi\left[r^2 x - \frac{x^3}{3}\right]_0^r = 2\pi\left(r^3 - \frac{r^3}{3}\right) = \frac{4}{3}\pi r^3.$$

> [!warning] Slide typo
> The slide's third line reads 2π times the integral of π(r² - x²), which counts π twice. The next line on the slide drops it, so the working above carries the corrected line. (added)

---

## Volume of a pyramid #formula

Statement (source, 6.2 Volumes, slide 30): the volume of a pyramid whose base is a square with side L and whose height is h is

$$V = \frac{L^2 h}{3}.$$

Hypotheses:
- square base of side L
- height h

Derivation (source, 6.2 Volumes, slides 30 to 31):
- Place the origin O at the vertex of the pyramid and the x-axis along its central axis.
- Any plane P_x through x perpendicular to the x-axis meets the pyramid in a square with side of length s.
- From similar triangles:

$$\frac{x}{h} = \frac{s/2}{L/2} = \frac{s}{L}, \quad \text{so } s = \frac{Lx}{h}.$$

- Therefore the cross-sectional area is

$$A(x) = s^2 = \frac{L^2}{h^2}\,x^2.$$

- The pyramid lies between x = 0 and x = h, so

$$V = \int_0^h A(x)\,dx = \int_0^h \frac{L^2}{h^2}\,x^2\,dx = \left[\frac{L^2 x^3}{3h^2}\right]_0^h = \frac{L^2 h}{3}.$$

---

## Volume of a cylindrical shell #formula

Formula (source, 6.3 Cylindrical shells, slide 4):

$$V = 2\pi r h\,\Delta r$$

where r is the average radius of the shell, h its height and Δr its thickness. Remembered as V = [circumference][height][thickness] (source, 6.3 Cylindrical shells, slide 5).

Hypotheses:
- shell with inner radius r_1, outer radius r_2 and height h
- Δr = r_2 - r_1 and r = (r_2 + r_1)/2

Derivation (source, 6.3 Cylindrical shells, slide 4): the volume is the outer cylinder V_2 minus the inner cylinder V_1:

$$V = V_2 - V_1 = \pi r_2^2 h - \pi r_1^2 h = \pi(r_2^2 - r_1^2)h$$

$$= \pi(r_2 + r_1)(r_2 - r_1)h = 2\pi\,\frac{r_2 + r_1}{2}\,h\,(r_2 - r_1).$$

With Δr = r_2 - r_1 and r = (r_2 + r_1)/2 this becomes V = 2πrhΔr.

---

## Shell method volume formula #formula

Formula (source, 6.3 Cylindrical shells, slide 9): the volume of the solid obtained by rotating about the y-axis the region under y = f(x) from a to b is

$$V = \int_a^b 2\pi x f(x)\,dx \quad \text{where } 0 \le a < b.$$

Hypotheses:
- f(x) >= 0
- the region is bounded by y = f(x), y = 0, x = a and x = b, with b > a >= 0
- rotation is about the y-axis

Derivation (source, 6.3 Cylindrical shells, slides 6 to 9):
- Divide [a, b] into n subintervals [x_{i-1}, x_i] of equal width Δx and let x̄_i be the midpoint of the ith subinterval.
- Rotating the rectangle with base [x_{i-1}, x_i] and height f(x̄_i) about the y-axis gives a cylindrical shell with average radius x̄_i, height f(x̄_i) and thickness Δx. By the cylindrical shell formula its volume is

$$V_i = (2\pi \bar{x}_i)\,[f(\bar{x}_i)]\,\Delta x.$$

- An approximation to the volume V of S is the sum of the shell volumes:

$$V \approx \sum_{i=1}^{n} V_i = \sum_{i=1}^{n} 2\pi \bar{x}_i f(\bar{x}_i)\,\Delta x.$$

- This approximation appears to become better as n goes to infinity. From the definition of an integral:

$$\lim_{n\to\infty}\sum_{i=1}^{n} 2\pi \bar{x}_i f(\bar{x}_i)\,\Delta x = \int_a^b 2\pi x f(x)\,dx.$$

- Thus the formula above "appears plausible". The source states it at this level and does not give a stricter proof.

---

## Arc length formula #theorem

Statement (source, 8.1 Arc length, slide 9):

> The Arc Length Formula. If f' is continuous on [a, b], then the length of the curve y = f(x), a <= x <= b, is

$$L = \int_a^b \sqrt{1 + [f'(x)]^2}\,dx.$$

> In Leibniz notation:

$$L = \int_a^b \sqrt{1 + \left(\frac{dy}{dx}\right)^2}\,dx.$$

Hypotheses:
- f' is continuous on [a, b]

Proof (source, 8.1 Arc length, slides 5 to 9):
- Divide [a, b] into n subintervals with endpoints x_0, x_1, ..., x_n and equal width Δx. If y_i = f(x_i), the point P_i(x_i, y_i) lies on the curve, and the polygon with vertices P_0, P_1, ..., P_n approximates it.
- The length of the curve is defined as the limit of the lengths of these inscribed polygons (if it exists):

$$L = \lim_{n\to\infty}\sum_{i=1}^{n}|P_{i-1}P_i|.$$

- Let Δy_i = y_i - y_{i-1}. Then

$$|P_{i-1}P_i| = \sqrt{(x_i - x_{i-1})^2 + (y_i - y_{i-1})^2} = \sqrt{(\Delta x)^2 + (\Delta y_i)^2}.$$

- Apply the Mean Value Theorem to f on [x_{i-1}, x_i]: there is a number x_i* between x_{i-1} and x_i such that

$$f(x_i) - f(x_{i-1}) = f'(x_i^*)(x_i - x_{i-1}), \quad \text{that is,} \quad \Delta y_i = f'(x_i^*)\,\Delta x.$$

- Thus, since Δx > 0:

$$|P_{i-1}P_i| = \sqrt{(\Delta x)^2 + [f'(x_i^*)\Delta x]^2} = \sqrt{1 + [f'(x_i^*)]^2}\;\Delta x.$$

- Therefore

$$L = \lim_{n\to\infty}\sum_{i=1}^{n}|P_{i-1}P_i| = \lim_{n\to\infty}\sum_{i=1}^{n}\sqrt{1 + [f'(x_i^*)]^2}\;\Delta x.$$

- We recognise this as equal to the integral of sqrt(1 + [f'(x)]^2) from a to b, by the definition of a definite integral. The integral exists because g(x) = sqrt(1 + [f'(x)]^2) is continuous. This proves the theorem.

---

## Lateral surface area of a cone #formula

Formula (source, 8.2 Surface of revolution, slide 3): the lateral surface area of a circular cone with base radius r and slant height ℓ is defined to be

$$A = \pi r \ell.$$

Hypotheses:
- circular cone with base radius r and slant height ℓ

Derivation (source, 8.2 Surface of revolution, slide 3):
- Cut the cone along a slant edge and flatten it to form a sector of a circle with radius ℓ and central angle

$$\theta = \frac{2\pi r}{\ell}.$$

- The area of a sector of a circle with radius ℓ and angle θ is (1/2)ℓ²θ, so here

$$A = \frac{1}{2}\ell^2\theta = \frac{1}{2}\ell^2\left(\frac{2\pi r}{\ell}\right) = \pi r \ell.$$

---

## Area of a frustum of a cone (band) #formula

Formula (source, 8.2 Surface of revolution, slide 6): the area of the band with slant height ℓ and upper and lower radii r_1 and r_2 is

$$A = 2\pi r \ell, \quad \text{where } r = \tfrac{1}{2}(r_1 + r_2) \text{ is the average radius of the band.}$$

Hypotheses:
- band (frustum) with slant height ℓ, upper radius r_1, lower radius r_2

Derivation (source, 8.2 Surface of revolution, slides 5 to 6): subtract the areas of two cones, with ℓ_1 the slant height of the small cone removed from the top:

$$A = \pi r_2(\ell_1 + \ell) - \pi r_1 \ell_1 = \pi[(r_2 - r_1)\ell_1 + r_2 \ell] \quad (1)$$

- From similar triangles:

$$\frac{\ell_1}{r_1} = \frac{\ell_1 + \ell}{r_2}$$

which gives r_2 ℓ_1 = r_1 ℓ_1 + r_1 ℓ, or

$$(r_2 - r_1)\ell_1 = r_1 \ell.$$

- Putting this in equation (1):

$$A = \pi(r_1 \ell + r_2 \ell) = 2\pi r \ell, \quad r = \tfrac{1}{2}(r_1 + r_2).$$

---

## Surface area of revolution about the x-axis #formula

Formula (source, 8.2 Surface of revolution, slide 10): if f is positive and has a continuous derivative, the surface area obtained by rotating the curve y = f(x), a <= x <= b, about the x-axis is

$$S = \int_a^b 2\pi f(x)\sqrt{1 + [f'(x)]^2}\,dx.$$

> Leibniz notation, slide 11:

$$S = \int_a^b 2\pi y\sqrt{1 + \left(\frac{dy}{dx}\right)^2}\,dx$$

> If the curve is x = g(y), c <= y <= d:

$$S = \int_c^d 2\pi y\sqrt{1 + \left(\frac{dx}{dy}\right)^2}\,dy$$

Hypotheses:
- f is positive
- f has a continuous derivative

Derivation (source, 8.2 Surface of revolution, slides 7 to 10):
- Divide [a, b] into n subintervals with endpoints x_0, x_1, ..., x_n and equal width Δx. If y_i = f(x_i), the point P_i(x_i, y_i) lies on the curve.
- The part of the surface between x_{i-1} and x_i is approximated by rotating the segment P_{i-1}P_i about the x-axis. The result is a band with slant height ℓ = |P_{i-1}P_i| and average radius r = (y_{i-1} + y_i)/2, so by the frustum formula its area is

$$2\pi\,\frac{y_{i-1} + y_i}{2}\,|P_{i-1}P_i|.$$

- As in the proof of the Arc Length Formula:

$$|P_{i-1}P_i| = \sqrt{1 + [f'(x_i^*)]^2}\;\Delta x$$

where x_i* is some number in [x_{i-1}, x_i].
- When Δx is small, y_i = f(x_i) is approximately f(x_i*) and y_{i-1} = f(x_{i-1}) is approximately f(x_i*), since f is continuous. Therefore

$$2\pi\,\frac{y_{i-1} + y_i}{2}\,|P_{i-1}P_i| \approx 2\pi f(x_i^*)\sqrt{1 + [f'(x_i^*)]^2}\;\Delta x.$$

- An approximation to the area of the complete surface is

$$\sum_{i=1}^{n} 2\pi f(x_i^*)\sqrt{1 + [f'(x_i^*)]^2}\;\Delta x. \quad (3)$$

- This appears to become better as n goes to infinity. Recognising (3) as a Riemann sum for g(x) = 2πf(x) sqrt(1 + [f'(x)]^2):

$$\lim_{n\to\infty}\sum_{i=1}^{n} 2\pi f(x_i^*)\sqrt{1 + [f'(x_i^*)]^2}\;\Delta x = \int_a^b 2\pi f(x)\sqrt{1 + [f'(x)]^2}\,dx.$$

- Therefore, when f is positive and has a continuous derivative, the surface area is defined as the integral above. The source defines the area this way rather than proving it from a prior definition.

---

## Surface area of a sphere (parametric derivation) #formula

Statement (source, 10.2 Parametric calculus, slide 26): the surface area of a sphere of radius r is

$$S = 4\pi r^2.$$

Hypotheses:
- sphere of radius r, obtained by rotating the semicircle x = r cos t, y = r sin t, 0 <= t <= π about the x-axis
- uses the parametric surface area formula (see Surface area of a parametric curve)

Derivation (source, 10.2 Parametric calculus, slide 26):

$$S = \int_0^\pi 2\pi r\sin t\,\sqrt{(-r\sin t)^2 + (r\cos t)^2}\,dt$$

$$= \int_0^\pi 2\pi r\sin t\,\sqrt{r^2(\sin^2 t + \cos^2 t)}\,dt$$

$$= 2\pi\int_0^\pi r\sin t\cdot r\,dt = 2\pi r^2\int_0^\pi \sin t\,dt = 2\pi r^2\,[-\cos t]_0^\pi = 4\pi r^2.$$

> [!warning] Slide typo
> The slide's second line has an extra 2π in front of the integral, in addition to the 2πr inside it. The third line returns to a single 2π, so the working above carries the corrected second line. (added)

---

## Surface area of a parametric curve #formula

Statement (source, 10.2 Parametric calculus, slide 25): suppose the curve C given by x = f(t), y = g(t), α <= t <= β is rotated about the x-axis. If C is traversed exactly once as t increases from α to β, then the area of the resulting surface is

$$S = \int_\alpha^\beta 2\pi y\sqrt{\left(\frac{dx}{dt}\right)^2 + \left(\frac{dy}{dt}\right)^2}\,dt.$$

Hypotheses:
- f' and g' are continuous
- g(t) >= 0
- C is traversed exactly once as t increases from α to β

The slide says only that this is obtained "in the same way as for arc length" by adapting the surface area formula. Proof not shown in source, statement only.

---

## Integrating factor for a linear differential equation #theorem

Statement (source, 9.5 Linear DEs, slide 8): to solve the linear differential equation

$$y' + P(x)\,y = Q(x)$$

multiply both sides by the integrating factor

$$I(x) = e^{\int P(x)\,dx}$$

and integrate both sides.

Hypotheses:
- P and Q are continuous functions on the given interval
- the equation is in standard form y' + P(x)y = Q(x)

Derivation (source, 9.5 Linear DEs, slides 5 to 8):
- Multiply the equation by a function I(x), chosen so that the left side is a product-rule derivative:

$$I(x)\,(y' + P(x)\,y) = (I(x)\,y)' \quad (3)$$

- Multiplied by I(x), the equation becomes

$$(I(x)\,y)' = I(x)\,Q(x).$$

- Integrating both sides:

$$I(x)\,y = \int I(x)Q(x)\,dx + C, \qquad y(x) = \frac{1}{I(x)}\left[\int I(x)Q(x)\,dx + C\right] \quad (4)$$

- To find I, expand (3) and cancel terms:

$$I(x)y' + I(x)P(x)y = (I(x)y)' = I'(x)y + I(x)y'$$

hence

$$I(x)P(x) = I'(x) = \frac{dI}{dx}. \quad (**)$$

- Equation (**) is separable:

$$\frac{dI}{I} = P(x)\,dx \;\Rightarrow\; \int\frac{dI}{I} = \int P(x)\,dx \;\Rightarrow\; \ln|I| = \int P(x)\,dx \;\Rightarrow\; I = A\,e^{\int P(x)\,dx}$$

where A = ±e^C for a constant C.
- Setting A = 1 gives

$$I(x) = e^{\int P(x)\,dx}. \quad (5)$$

---

## Separable differential equation procedure #theorem

Statement (source, 9.3 Separable DEs, slides 11 to 12): a separable equation is a first-order differential equation that can be written

$$\frac{dy}{dx} = g(x)f(y).$$

Equivalently, if f(y) is not 0,

$$\frac{dy}{dx} = \frac{g(x)}{h(y)} \quad (4)$$

where h(y) = 1/f(y). To solve, write it in differential form h(y) dy = g(x) dx and integrate both sides:

$$\int h(y)\,dy = \int g(x)\,dx. \quad (5)$$

Hypotheses:
- dy/dx factors as a function of x times a function of y
- f(y) is not 0 (for the form in (4))

Justification by the Chain Rule (source, 9.3 Separable DEs, slide 13): if h and g satisfy equation (5), then

$$\frac{d}{dx}\left(\int h(y)\,dy\right) = \frac{d}{dx}\left(\int g(x)\,dx\right)$$

$$\text{so}\quad \frac{d}{dy}\left(\int h(y)\,dy\right)\frac{dy}{dx} = g(x)$$

$$\text{and}\quad h(y)\,\frac{dy}{dx} = g(x).$$

Thus equation (4) is satisfied.

---

## Slope of a parametric curve and its second derivative #formula

Formulas (source, 10.2 Parametric calculus, slides 2 and 4):

$$\frac{dy}{dx} = \frac{dy/dt}{dx/dt} \quad (1) \qquad\qquad \frac{d^2y}{dx^2} = \frac{d}{dx}\left(\frac{dy}{dx}\right) = \frac{\frac{d}{dt}\left(\frac{dy}{dx}\right)}{\frac{dx}{dt}}$$

Hypotheses:
- f and g are differentiable, x = f(t), y = g(t), and y is also a differentiable function of x
- dx/dt is not 0

Derivation (source, 10.2 Parametric calculus, slides 2 and 4):
- The Chain Rule gives

$$\frac{dy}{dt} = \frac{dy}{dx}\cdot\frac{dx}{dt}.$$

- If dx/dt is not 0, solve for dy/dx to get (1).
- For the second derivative, in equation (1) replace y by dy/dx, which gives the second formula above.

---

## Area under a parametric curve #formula

Formula (source, 10.2 Parametric calculus, slide 12): if the curve y = F(x) is traced out once by x = f(t), y = g(t), α <= t <= β, then

$$A = \int_a^b y\,dx = \int_\alpha^\beta g(t)\,f'(t)\,dt \quad \text{or} \quad \int_\beta^\alpha g(t)\,f'(t)\,dt.$$

Hypotheses:
- F(x) >= 0
- the curve is traced out once by x = f(t), y = g(t), α <= t <= β

Derivation (source, 10.2 Parametric calculus, slide 12): the slide obtains the formula from A = the integral of F(x) from a to b by using the Substitution Rule for Definite Integrals.

(added) The substitution is x = f(t), dx = f'(t) dt, y = g(t). The first limits apply when f(α) = a and f(β) = b, and the bracketed alternative applies when the curve is traced from right to left. The slide does not spell out the substitution steps.

---

## Arc length of a parametric curve #theorem

Statement (source, 10.2 Parametric calculus, slide 19):

> If a curve C is described by the parametric equations x = f(t), y = g(t), α <= t <= β, where f' and g' are continuous on [α, β] and C is traversed exactly once as t increases from α to β, then the length of C is

$$L = \int_\alpha^\beta \sqrt{\left(\frac{dx}{dt}\right)^2 + \left(\frac{dy}{dt}\right)^2}\,dt.$$

Hypotheses:
- f' and g' are continuous on [α, β]
- C is traversed exactly once as t increases from α to β

Proof, case dx/dt > 0 (source, 10.2 Parametric calculus, slides 14 to 16):
- Suppose C can also be written y = F(x) and dx/dt = f'(t) > 0, so C is traversed once from left to right as t increases from α to β, with f(α) = a and f(β) = b.
- Put formula (1) into the arc length formula and use the Substitution Rule:

$$L = \int_a^b\sqrt{1 + \left(\frac{dy}{dx}\right)^2}\,dx = \int_\alpha^\beta\sqrt{1 + \left(\frac{dy/dt}{dx/dt}\right)^2}\;\frac{dx}{dt}\,dt.$$

- Since dx/dt > 0:

$$L = \int_\alpha^\beta\sqrt{\left(\frac{dx}{dt}\right)^2 + \left(\frac{dy}{dt}\right)^2}\,dt. \quad (3)$$

Proof, general case by polygonal approximation (source, 10.2 Parametric calculus, slides 16 to 19): even if C cannot be written y = F(x), formula (3) is still valid.
- Divide [α, β] into n subintervals of equal width Δt with endpoints t_0, t_1, ..., t_n. Then x_i = f(t_i) and y_i = g(t_i) are the coordinates of points P_i(x_i, y_i) on C, and the polygon P_0, P_1, ..., P_n approximates C.
- As in the arc length section, define

$$L = \lim_{n\to\infty}\sum_{i=1}^{n}|P_{i-1}P_i|.$$

- The Mean Value Theorem applied to f on [t_{i-1}, t_i] gives a number t_i* in (t_{i-1}, t_i) with f(t_i) - f(t_{i-1}) = f'(t_i*)(t_i - t_{i-1}). With Δx_i = x_i - x_{i-1} and Δy_i = y_i - y_{i-1} this reads

$$\Delta x_i = f'(t_i^*)\,\Delta t.$$

- Similarly, applied to g it gives a number t_i** in (t_{i-1}, t_i) with

$$\Delta y_i = g'(t_i^{**})\,\Delta t.$$

- Therefore

$$|P_iP_{i-1}| = \sqrt{(\Delta x_i)^2 + (\Delta y_i)^2} = \sqrt{[f'(t_i^*)\Delta t]^2 + [g'(t_i^{**})\Delta t]^2} = \sqrt{[f'(t_i^*)]^2 + [g'(t_i^{**})]^2}\;\Delta t$$

which gives

$$L = \lim_{n\to\infty}\sum_{i=1}^{n}\sqrt{[f'(t_i^*)]^2 + [g'(t_i^{**})]^2}\;\Delta t. \quad (4)$$

- The sum in (4) resembles a Riemann sum for sqrt([f'(t)]^2 + [g'(t)]^2) but is not exactly one, because in general t_i* is not equal to t_i**. The source then states that if f' and g' are continuous, "it can be shown" that the limit in (4) is the same as if t_i* and t_i** were equal, which gives the theorem. That final step is not shown in the source: proof of that step not shown in source, statement only.

---

## Referenced but not proved in the source

- The Extreme Value Theorem, Intermediate Value Theorem, Mean Value Theorem, Fundamental Theorem of Calculus and Substitution Rule are used above as given results. The slides do not prove them.
- Section 4.7 (Optimization): the slide proves that A'(r) < 0 when r < cube root of (500/π) and leaves the matching claim for r above that value as an exercise. The other direction is not shown in source.
- No theorem derivations were found in the Related Rates (3.9), Parametric Equations (10.1) or Polar Coordinates (10.3) slides, so nothing from those sections appears above.
