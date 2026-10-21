---
module: MAT01B1
topic: Final exam proof sheet
test: Final
tags: [theorem, formula, exam-flagged, added]
---

# MAT01B1 Proofs Final

The exam proof sheet. It ranks every proof and derivation by how close it is to a question in the 15 past papers you supplied, and writes the likely ones out in full so they can be memorised from one place. Everything lower down is linked, not repeated. The summary for the same exam is [[MAT01B1_Summary_Final]].

Labels used below:
- `(source: past papers)` means the question or statement comes from a supplied paper.
- `(source: ST1 proofs)` and `(source: ST2 proofs)` mean the proof is copied from [[MAT01B1_Proofs_ST1]] or [[MAT01B1_Proofs_ST2]].
- `(added)` means it was built during revision from the notes, not copied from a proof in the slides.

## Priority list

Memorise in this order. The evidence is the 15 supplied papers, searched for prove, proof, show that, derive and state.

1. Mean Value Theorem proof via Rolle. Asked as a 4 mark proof in the 2018 supplementary, the 2023 Exam A (as steps (a) to (e)) and the 2024 final. Also asked as a statement and as hypothesis questions in multiple choice.
2. Mean Value Theorem for Integrals, proof 1 and proof 2. Asked as a proof in the ST2 papers, and as a statement in the 2022 Exam A and the 2020 supplementary. Your own view is that these first two are the likely ones.
3. Fermat's Theorem proof. Asked as a 3 mark proof in the 2022 Exam A, and as a statement in the 2020 supplementary and in several multiple choice questions.
4. Rolle's Theorem. Statement asked in the 2018 supplementary and the 2022 Exam C, with a "use Rolle to show exactly one root" question in the 2022 Exam C.
5. Polar slope derivation. A "show that $dy/dx=\ldots$" question in the 2023 Exams A, B and C.
6. Binomial sigma form. A "show that" question in the 2023 Exam A and the 2024 final.
7. Circumference as an improper integral. A "show that" question in the 2023 Exam A.
8. Everything else: see Lower priority proofs. Not asked as a proof in the papers searched.

## Statements to know word for word

Fermat's Theorem (source: ST1 proofs): if $f$ has a local maximum or minimum at $c$, and $f'(c)$ exists, then $f'(c)=0$.

Rolle's Theorem (source: ST1 proofs): let $f$ be continuous on $[a,b]$, differentiable on $(a,b)$, with $f(a)=f(b)$. Then there exists $c\in(a,b)$ such that $f'(c)=0$.

Mean Value Theorem (source: ST1 proofs): let $f$ be continuous on $[a,b]$ and differentiable on $(a,b)$. Then there exists $c\in(a,b)$ such that

$$f'(c)=\frac{f(b)-f(a)}{b-a}.$$

Mean Value Theorem for Integrals (source: ST2 proofs): if $f$ is continuous on $[a,b]$, then there exists $c\in[a,b]$ such that

$$f(c)=f_{ave}=\frac{1}{b-a}\int_a^b f(x)\,dx.$$

Extreme Value Theorem (source: ST1 proofs, the parenthetical in the proof of Rolle's Theorem): a continuous function on a closed interval attains a maximum and a minimum on that interval.

Intermediate Value Theorem (added, standard statement): if $f$ is continuous on $[a,b]$ and $N$ is any number between $f(a)$ and $f(b)$, then there exists $c\in[a,b]$ with $f(c)=N$.

N.B The hypotheses are marks. Rolle needs continuous on the closed interval, differentiable on the open interval, and equal values at the ends. The Mean Value Theorem drops the equal values condition. The Mean Value Theorem for Integrals needs only continuity.

## Sketch for the Mean Value Theorem proof

(added) The 2018 paper asks for a sketch in the proof, and the 2023 paper asks how $h$ is defined in words.

- Draw the graph of $f$ on $[a,b]$ and the straight line (the secant) through $(a,f(a))$ and $(b,f(b))$.
- $h(x)$ is the vertical gap between the graph and that line.
- The gap is $0$ at both ends, so $h(a)=h(b)=0$. That is why Rolle's Theorem applies to $h$.
- Where $h'(c)=0$, the graph has the same slope as the secant.

## Fermat's Theorem proof

**Statement.** If $f$ has a local maximum or minimum at $c$, and $f'(c)$ exists, then $f'(c) = 0$.

**Proof.** Assume $f$ has a local maximum at $c$. By definition,

$$
f'(c) = \lim_{h \to 0} \frac{f(c+h) - f(c)}{h}.
$$

For $h$ small, $f(c+h) \le f(c)$.

If $h > 0$:
$$
\frac{f(c+h) - f(c)}{h} \le 0 \quad \Rightarrow \quad f'(c) = \lim_{h \to 0^+} (\cdots) \le 0.
$$

If $h < 0$:
$$
\frac{f(c+h) - f(c)}{h} \ge 0 \quad \Rightarrow \quad f'(c) = \lim_{h \to 0^-} (\cdots) \ge 0.
$$

Since $f'(c)$ exists, both one sided limits are equal, so $0 \le f'(c) \le 0$, giving $f'(c) = 0$. The local minimum case is symmetric.

> [!note] Converse is false
> $f'(c) = 0$ does not imply an extremum. For example $f(x) = x^3$ at $c = 0$ is an inflection point (a point where the curve changes concavity), not an extremum.

## Rolle's Theorem proof

**Statement.** Let $f$ be continuous on $[a,b]$, differentiable on $(a,b)$, with $f(a) = f(b)$. Then there exists $c \in (a,b)$ such that $f'(c) = 0$.

**Hypotheses**
- $f$ continuous on $[a,b]$
- $f$ differentiable on $(a,b)$
- $f(a) = f(b)$

**Proof.**

*Case I: $f$ is constant on $[a,b]$.* Then $f'(x) = 0$ for every $x$, so any $c \in (a,b)$ works.

*Case II: $f(x) > f(a)$ for some $x \in (a,b)$.* By the Extreme Value Theorem (a continuous function on a closed interval attains a maximum and minimum on that interval), $f$ attains a maximum on $[a,b]$. Since that maximum exceeds $f(a) = f(b)$, it cannot occur at either endpoint, so it occurs at some $c \in (a,b)$. Then $c$ is a local maximum, and Fermat's Theorem gives $f'(c) = 0$.

*Case III: $f(x) < f(a)$ for some $x \in (a,b)$.* Symmetric to Case II using the minimum: $f'(c) = 0$ for some $c \in (a,b)$.

-> feeds directly into the Mean Value Theorem (see: Mean Value Theorem proof via Rolle), which is Rolle's Theorem applied to a tilted helper function.

## Mean Value Theorem proof via Rolle

**Statement.** Let $f$ be continuous on $[a,b]$ and differentiable on $(a,b)$. Then there exists $c \in (a,b)$ such that

$$
f'(c) = \frac{f(b) - f(a)}{b-a}.
$$

**Hypotheses**
- $f$ continuous on $[a,b]$
- $f$ differentiable on $(a,b)$

**Proof.** Define

$$
h(x) = f(x) - \left[ f(a) + \frac{f(b)-f(a)}{b-a}(x-a) \right],
$$

the vertical gap between $f$ and the secant line (the straight line joining the two endpoints) through $(a, f(a))$ and $(b, f(b))$.

Since $f$ is continuous on $[a,b]$ and differentiable on $(a,b)$, and the bracketed term is linear (continuous and differentiable everywhere), $h$ is continuous on $[a,b]$ and differentiable on $(a,b)$.

$$
h(a) = f(a) - [f(a) + 0] = 0,
$$
$$
h(b) = f(b) - \left[ f(a) + \frac{f(b)-f(a)}{b-a}(b-a) \right] = f(b) - f(b) = 0.
$$

So $h(a) = h(b)$, and Rolle's Theorem (see: Rolle's Theorem proof) gives $c \in (a,b)$ with $h'(c) = 0$. Since

$$
h'(x) = f'(x) - \frac{f(b)-f(a)}{b-a},
$$

setting $h'(c) = 0$ gives

$$
f'(c) = \frac{f(b)-f(a)}{b-a}.
$$

## Mean Value Theorem for Integrals proof 1, EVT and IVT

#theorem

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

## Mean Value Theorem for Integrals proof 2, FTC and MVT

#theorem

Statement: same as in Mean Value Theorem for Integrals proof 1, EVT and IVT.

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

## Polar slope derivation

#formula

(added, from the parametric slope formula in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Tangents]]; the questions are from the 2023 Exams A, B and C, source: past papers)

Statement: for a polar curve $r=f(\theta)$, with $r'=\dfrac{dr}{d\theta}$,

$$\frac{dy}{dx}=\frac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}.$$

Hypotheses:
- $r=f(\theta)$ is differentiable
- the denominator $\dfrac{dx}{d\theta}=r'\cos\theta-r\sin\theta$ is not $0$

Derivation:
- Use $\theta$ as the parameter in $x=r\cos\theta$ and $y=r\sin\theta$, where $r=f(\theta)$.
- By the product rule:

$$\frac{dx}{d\theta}=r'\cos\theta-r\sin\theta,\qquad \frac{dy}{d\theta}=r'\sin\theta+r\cos\theta.$$

- The parametric slope formula $\dfrac{dy}{dx}=\dfrac{dy/d\theta}{dx/d\theta}$ gives the statement.

Check 1 (2023 Exam C, Question 4b): $r=\dfrac{2}{1+\cos\theta}$, so $r'=\dfrac{2\sin\theta}{(1+\cos\theta)^2}$. The numerator is $\dfrac{2\sin^2\theta+2\cos\theta(1+\cos\theta)}{(1+\cos\theta)^2}=\dfrac{2}{1+\cos\theta}$ and the denominator is $\dfrac{2\sin\theta\cos\theta-2\sin\theta(1+\cos\theta)}{(1+\cos\theta)^2}=\dfrac{-2\sin\theta}{(1+\cos\theta)^2}$. So

$$\frac{dy}{dx}=-\frac{1+\cos\theta}{\sin\theta}=-\cot\frac\theta2.$$

Check 2 (2023 Exam B, Question 10b): $r=2(\cos\theta-\sin\theta)$, so $r'=-2(\sin\theta+\cos\theta)$. The numerator is $2\cos2\theta-2\sin2\theta$ and the denominator is $-2\sin2\theta-2\cos2\theta$. Dividing top and bottom by $-2\cos2\theta$:

$$\frac{dy}{dx}=\frac{\tan2\theta-1}{\tan2\theta+1}.$$

## Binomial sigma form

#theorem

(added; questions from the 2023 Exam A Question 4 and the 2024 final Question 9, source: past papers)

Statement (source: [[MAT01B1_Notes_S21_BinomialTheorem#The Binomial Theorem]]):

$$(a+b)^n=\sum_{k=0}^n\binom nk a^{n-k}b^k,\qquad \binom nk=\frac{n!}{(n-k)!\,k!}.$$

Hypotheses:
- $n$ is a natural number

Pattern for a "show that" question: put $a$ and $b$ in, then combine the powers of $x$ in each term.

- 2024 final, Question 9: $a=x$, $b=\dfrac1x$, $n=5$.

$$\left(x+\frac1x\right)^5=\sum_{k=0}^5\frac{5!}{k!\,(5-k)!}\,x^{5-k}x^{-k}=\sum_{k=0}^5\frac{5!}{k!\,(5-k)!}\,x^{5-2k}.$$

For the coefficient of $x^3$: $5-2k=3$, so $k=1$ and the coefficient is $\dfrac{5!}{1!\,4!}=5$.

- 2023 Exam A, Question 4: the printed exponent $x^{12-3k}$ with $(-2)^k$ fits $a=x^2$, $b=-\dfrac2x$, $n=6$.

$$\left(x^2-\frac2x\right)^6=\sum_{k=0}^6\frac{6!}{(6-k)!\,k!}\,(x^2)^{6-k}\left(-\frac2x\right)^k=\sum_{k=0}^6\frac{6!}{(6-k)!\,k!}\,x^{12-3k}(-2)^k.$$

For the constant term: $12-3k=0$, so $k=4$ and the term is $\dfrac{6!}{2!\,4!}(-2)^4=15\cdot16=240$.

## Circumference as an improper integral

#theorem

(added; the question is from the 2023 Exam A, Question 3, source: past papers)

Statement: for the unit circle $x^2+y^2=1$, the circumference is

$$L=2\int_{-1}^{1}\frac{dx}{\sqrt{1-x^2}},$$

an improper integral, not to be evaluated.

Derivation, using the arc length formula $L=\int\sqrt{1+(dy/dx)^2}\,dx$:
- The upper semicircle is $y=\sqrt{1-x^2}$ for $-1\le x\le1$, and $\dfrac{dy}{dx}=\dfrac{-x}{\sqrt{1-x^2}}$.
- Then $1+\left(\dfrac{dy}{dx}\right)^2=1+\dfrac{x^2}{1-x^2}=\dfrac{1}{1-x^2}$, so $ds=\dfrac{dx}{\sqrt{1-x^2}}$.
- The circumference is twice the length of the upper semicircle.
- The integrand is undefined at $x=\pm1$, where the slope is vertical, so the integral is improper.

## Rolle's Theorem and exactly one root

#theorem

(added; the question is from the 2022 Exam C, Question 3b, source: past papers: use Rolle's Theorem to show that $x^3+x-3=0$ has exactly one root)

Let $f(x)=x^3+x-3$, which is continuous and differentiable everywhere.

- At least one root: $f(0)=-3<0$ and $f(2)=7>0$, so by the Intermediate Value Theorem there is a root in $(0,2)$.
- At most one root: suppose there were two roots $r_1<r_2$, so $f(r_1)=f(r_2)=0$. Rolle's Theorem then gives a $c\in(r_1,r_2)$ with $f'(c)=0$. But $f'(x)=3x^2+1\ge1>0$ for every $x$, a contradiction.
- Therefore the equation has exactly one root.

Pattern: show a root exists with the Intermediate Value Theorem, then show two roots are impossible with Rolle's Theorem and the sign of $f'$.

## Lower priority proofs

Not asked as a proof in the papers searched. In rough order of how often the topic itself appears:

- Theorem 5, Corollary 7 and the increasing and decreasing test: [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7]] and [[MAT01B1_Proofs_ST1#Increasing/Decreasing Test]]. Theorem 5 and the test both use the Mean Value Theorem as above.
- Derivatives of inverse trig and inverse hyperbolic functions: [[MAT01B1_Proofs_ST1#Derivatives of inverse trig functions (added, absent from the source entirely)|inverse trig]] (one move: write the plain trig equation, differentiate implicitly, convert with a Pythagorean identity).
- Arc length, surface area, shells, volumes, average value, area between curves, integrating factor, separable equations, parametric formulas: all in [[MAT01B1_Proofs_ST2]]. The headings in that file carry tags, so these links are to the whole file. Each of those proofs is a Riemann sum argument: slice, approximate each piece, let the number of pieces grow, recognise an integral.
