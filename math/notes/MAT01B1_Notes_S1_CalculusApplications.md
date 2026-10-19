---
module: MAT01B1
topic: Calculus Applications
session: S1
tags: [definition, theorem, formula, worked-example, common-mistake]
---

# Calculus Applications

## Extremum values and what they let you do

A **local maximum** at a point $c$ means $f(c)$ is at least as large as $f(x)$ for every $x$ near $c$, not necessarily on the whole domain, just in a neighbourhood of $c$. A **local minimum** is the mirror image. A point where the derivative is zero or doesn't exist is called a **critical point**, and every local extremum of a differentiable function occurs at a critical point (that's Fermat's Theorem, full derivation in [[MAT01B1_Proofs_ST1#Fermat's Theorem]]). The reverse isn't true: a critical point doesn't have to be an extremum at all, $f(x)=x^3$ has a critical point at $x=0$ that's neither a max nor a min, just a flat spot the curve passes straight through.

Rolle's Theorem is the special case where the function starts and ends at the same height, $f(a)=f(b)$, over $[a,b]$. If it does, somewhere in between the curve has to level out, $f'(c)=0$ for some $c$ strictly inside the interval. It's really just Fermat's Theorem plus one observation: if $f$ isn't flat the whole way, it must climb above or dip below its starting height somewhere, and that peak or trough is an interior extremum. Full derivation in [[MAT01B1_Proofs_ST1#Rolle's Theorem]].

The **Mean Value Theorem** drops the requirement that the endpoints match. It says the instantaneous rate of change (the derivative) equals the average rate of change (the slope of the secant line joining the endpoints) at at least one point in between:

$$
f'(c) = \frac{f(b)-f(a)}{b-a}.
$$

The proof tilts the whole picture so the secant line becomes horizontal, which turns it back into Rolle's Theorem, full derivation in [[MAT01B1_Proofs_ST1#Mean Value Theorem]]. Concretely: if you drive 120 km in 2 hours, your average speed is 60 km/h, and the MVT guarantees that at some instant your speedometer actually read exactly 60 km/h, not more, not less.

**Theorem 5** and **Corollary 7** are the reason indefinite integrals carry a $+C$. If a function's derivative is zero everywhere on an interval, the function can't be doing anything but sitting still, it has to be constant, and that follows from the MVT applied to any two points. Stack that on top of Corollary 7 (two functions with the same derivative differ only by a constant) and you get the actual justification for writing $\int f(x)\,dx = F(x)+C$: any two antiderivatives of $f$ have equal derivatives (both equal $f$), so by Corollary 7 they differ by a constant. Full derivation in [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7]].

The **Increasing/Decreasing Test** converts the sign of $f'$ directly into the shape of $f$: positive derivative means climbing, negative means falling, and this too is just the MVT, since $f(x_2)-f(x_1)=f'(c)(x_2-x_1)$ forces the sign of the left side to match the sign of $f'(c)$. Full derivation in [[MAT01B1_Proofs_ST1#Increasing/Decreasing Test]].

### Absolute and local extreme values

Source: Dr K, §4.1 Maximum and Minimum Values.

**Definition (source).** Let $c$ be a number in the domain $D$ of a function $f$. Then $f(c)$ is the **absolute maximum** value of $f$ on $D$ if $f(c)\ge f(x)$ for all $x$ in $D$, and the **absolute minimum** value of $f$ on $D$ if $f(c)\le f(x)$ for all $x$ in $D$. An absolute maximum or minimum is sometimes called a **global** maximum or minimum, and the maximum and minimum values of $f$ are called its **extreme values**.

**Definition (source).** The number $f(c)$ is a **local maximum** value of $f$ if $f(c)\ge f(x)$ when $x$ is near $c$, and a **local minimum** value if $f(c)\le f(x)$ when $x$ is near $c$. "Near $c$" means on some open interval containing $c$.

N.B Because "near $c$" needs an open interval around $c$, an endpoint of the domain can be an absolute extreme but never a local one.

**Worked examples (source, §4.1).**
- $f(x)=\cos x$ takes its (local and absolute) maximum value $1$ infinitely many times ($\cos2n\pi=1$) and its (local and absolute) minimum value $-1$ infinitely many times ($\cos(2n+1)\pi=-1$), because $-1\le\cos x\le1$.
- $f(x)=x^2$: $f(0)=0$ is the absolute (and local) minimum since $x^2\ge0$. There is no maximum value, since the parabola has no highest point.
- $f(x)=x^3$ has no absolute maximum or minimum, and no local extreme values either.
- $f(x)=3x^4-16x^3+18x^2$ on $-1\le x\le4$: $f(-1)=37$ is the absolute maximum, and it is not a local maximum because it occurs at an endpoint. $f(1)=5$ is a local maximum, $f(0)=0$ is a local minimum, and $f(3)=-27$ is both a local minimum and the absolute minimum. At $x=4$ there is neither a local nor an absolute maximum.

### Extreme Value Theorem

**Theorem (source).** If $f$ is continuous on a closed interval $[a,b]$, then $f$ attains an absolute maximum value $f(c)$ and an absolute minimum value $f(d)$ at some numbers $c$ and $d$ in $[a,b]$.

**Hypotheses**
- $f$ continuous on $[a,b]$
- the interval $[a,b]$ closed (both endpoints included)

An extreme value can be attained more than once. The source omits the proof, saying only that the theorem is intuitively plausible but difficult to prove. It shows why both hypotheses are needed. A function on $[0,2]$ with a jump has no maximum value (its values get arbitrarily close to $3$ but never reach it), which doesn't contradict the theorem because the function is not continuous. A function continuous on the open interval $(0,2)$ that grows without bound has neither a maximum nor a minimum, which doesn't contradict the theorem because $(0,2)$ is not closed.

N.B The theorem says extreme values exist, not how to find them.

### Fermat's Theorem, critical numbers and the Closed Interval Method

Fermat's Theorem is stated at the start of this note, with its proof in [[MAT01B1_Proofs_ST1#Fermat's Theorem]]. <span style="color:#f08c00">Exam: the lecture flags it with "You must know the statement and proof of this theorem."</span> The slides prove the local maximum case and leave the local minimum case as an exercise. #exam-flagged

**Two ways Fermat's Theorem misleads (source, Examples 5 and 6).**
- $f(x)=x^3$ has $f'(0)=0$ but no maximum or minimum at $0$: the curve crosses its horizontal tangent there. So the converse of Fermat's Theorem is false.
- $f(x)=|x|$ has its (local and absolute) minimum at $0$, yet $f'(0)$ does not exist. So an extreme value can occur where $f'(c)$ does not exist.

**Definition (source).** A **critical number** of $f$ is a number $c$ in the domain of $f$ such that either $f'(c)=0$ or $f'(c)$ does not exist. Fermat's Theorem can then be rephrased: if $f$ has a local maximum or minimum at $c$, then $c$ is a critical number of $f$. So the search for extreme values starts at the critical numbers.

**Worked example (source, §4.1, Example 7).** Find the critical numbers of $f(x)=x^{3/5}(4-x)$. By the Product Rule,

$$
f'(x)=-x^{3/5}+(4-x)\cdot\frac35x^{-2/5}=\frac{12-8x}{5x^{2/5}}.
$$

$f'(x)=0$ when $x=\frac32$, and $f'(x)$ does not exist when $x=0$ (which is in the domain). The critical numbers are $\frac32$ and $0$.

**The Closed Interval Method (source).** To find the absolute maximum and minimum values of a continuous function $f$ on a closed interval $[a,b]$:

1. Find the values of $f$ at the critical numbers of $f$ in $(a,b)$.
2. Find the values of $f$ at the endpoints of the interval.
3. The largest of the values from steps 1 and 2 is the absolute maximum value, and the smallest is the absolute minimum value.

Why it works: by the Extreme Value Theorem the extremes exist, and each one either is local, so it occurs at a critical number by Fermat's Theorem, or occurs at an endpoint (source).

**Worked example (source, §4.1, Example 8, flagged as a test question).** Find the absolute maximum and minimum values of $f(x)=x^3-3x^2+1$ on $-\frac12\le x\le4$. $f$ is continuous, so the Closed Interval Method applies. $f'(x)=3x^2-6x=3x(x-2)$, which exists everywhere, so the only critical numbers are $0$ and $2$, both in $\left(-\frac12,4\right)$. Then

$$
f(0)=1,\qquad f(2)=-3,\qquad f\!\left(-\tfrac12\right)=\tfrac18,\qquad f(4)=17.
$$

The absolute maximum is $f(4)=17$, which occurs at an endpoint, and the absolute minimum is $f(2)=-3$, which occurs at a critical number. N.B Compare all the values together, the endpoints included. Here the maximum is at an endpoint and the minimum at a critical number. The method is used throughout [[MAT01B1_Notes_S5_OptimizationProblems#The Closed Interval Method (source, §4.1)|optimization problems]].

### Rolle's Theorem and the Mean Value Theorem, worked examples

Source: Dr K, §4.2 Mean Value Theorem. The statements and proofs are in [[MAT01B1_Proofs_ST1]] (Rolle's Theorem, Mean Value Theorem, Theorem 5 and Corollary 7). What follows are the lecture's examples and remarks.

**Rolle's Theorem as a statement about motion (source).** For a position function $s=f(t)$: if an object is in the same place at two instants $t=a$ and $t=b$, then $f(a)=f(b)$, and Rolle's Theorem gives an instant $c$ between them with $f'(c)=0$, that is, zero velocity. A ball thrown straight up is momentarily at rest at the top.

**Worked example (source, §4.2).** Prove that $x^3+x-1=0$ has exactly one real root.

*Existence.* $f(x)=x^3+x-1$ is a polynomial, so it is continuous. $f(0)=-1<0$ and $f(1)=1>0$, so by the Intermediate Value Theorem there is a number $c$ between $0$ and $1$ with $f(c)=0$.

*Uniqueness, by contradiction.* Suppose there were two roots $a<b$, so $f(a)=0=f(b)$. $f$ is continuous on $[a,b]$ and differentiable on $(a,b)$, so Rolle's Theorem gives a number $c$ between $a$ and $b$ with $f'(c)=0$. But $f'(x)=3x^2+1\ge1$ for all $x$, so $f'$ is never $0$. This is a contradiction, so there is no second root.

(added) The slide's proof of Rolle's Theorem has a slip in Case 3: it says $f(x)>f(a)$ where it should say $f(x)<f(a)$, since Case 3 is the minimum case. The Proofs file has it right.

**Worked example (source, §4.2), finding $c$.** $f(x)=x^3-x$ on $[0,2]$. It is a polynomial, so the Mean Value Theorem applies. $f(2)=6$, $f(0)=0$, $f'(x)=3x^2-1$, so $f(2)-f(0)=f'(c)(2-0)$ becomes

$$
6=(3c^2-1)\cdot2=6c^2-2\;\Rightarrow\;c^2=\frac43\;\Rightarrow\;c=\pm\frac{2}{\sqrt3}.
$$

$c$ must be in $(0,2)$, so $c=\dfrac{2}{\sqrt3}$. Geometrically, the tangent at that point is parallel to the secant line through $(0,0)$ and $(2,6)$.

**Worked example (source, §4.2), bounding a function.** Suppose $f(0)=-3$ and $f'(x)\le5$ for all $x$. How large can $f(2)$ be? $f$ is differentiable, hence continuous, so the Mean Value Theorem on $[0,2]$ gives a number $c$ with $f(2)-f(0)=f'(c)(2-0)$, so

$$
f(2)=f(0)+2f'(c)\le-3+2(5)=7.
$$

The largest possible value of $f(2)$ is $7$. This is the main use of the theorem: information about a function from information about its derivative.

**Caution for Theorem 5 (source).** Let $f(x)=\dfrac{x}{|x|}$, which is $1$ for $x>0$ and $-1$ for $x<0$. Its domain is $\{x\mid x\neq0\}$ and $f'(x)=0$ for every $x$ in the domain, yet $f$ is not constant. This does not contradict Theorem 5 because the domain is not an interval. $f$ is constant on $(0,\infty)$ and on $(-\infty,0)$ separately. N.B The word "interval" in Theorem 5 is doing real work.

**Worked example (source, §4.2), using Corollary 7.** Prove the identity $\tan^{-1}x+\cot^{-1}x=\dfrac\pi2$. Let $f(x)=\tan^{-1}x+\cot^{-1}x$. Then

$$
f'(x)=\frac{1}{1+x^2}-\frac{1}{1+x^2}=0\quad\text{for all }x\in\mathbb R,
$$

so $f(x)=C$ for some constant $C$. To find $C$, evaluate at a convenient point, $x=1$, where both angles are special: $C=f(1)=\tan^{-1}1+\cot^{-1}1=\dfrac\pi4+\dfrac\pi4=\dfrac\pi2$. Hence $\tan^{-1}x+\cot^{-1}x=\dfrac\pi2$. (The source notes this could be proved with trigonometry, but calculus is simpler here.)

## L'Hospital's Rule and indeterminate forms

Source: Dr K, §4.4 Indeterminate Forms and L'Hospital's Rule, Part 1 (slides 1 to 34). Part 2 of that lecture (the forms $\infty-\infty$, $0^0$, $\infty^0$, $1^\infty$) isn't in the vault yet.

<span style="color:#f08c00">Exam: L'Hospital's Rule is examined in the final exam.</span> #exam-flagged

**Why it exists.** Some limits can't be settled by the usual limit laws because the answer depends on how fast each piece moves. In $\displaystyle\lim_{x\to1}\frac{\ln x}{x-1}$ the numerator and denominator both go to $0$, so the quotient could end up as anything. That is an **indeterminate form**, here of type $\tfrac00$. The other two types handled in this lecture are $\tfrac{\infty}{\infty}$ and $0\cdot\infty$. (added) The idea behind the rule: if $f(a)=g(a)=0$, then near $a$ we have $f(x)\approx f'(a)(x-a)$ and $g(x)\approx g'(a)(x-a)$, so the ratio $f/g$ behaves like $f'(a)/g'(a)$. This is only a heuristic for the friendliest case, not a proof (the source doesn't prove the rule).

**Statement (source).** Suppose $f$ and $g$ are differentiable and $g'(x)\neq0$ when $x$ is near $a$. Suppose that $\lim_{x\to a}f(x)=0$ and $\lim_{x\to a}g(x)=0$, or $\lim_{x\to a}f(x)=\pm\infty$ and $\lim_{x\to a}g(x)=\pm\infty$. Then

$$
\lim_{x\to a}\frac{f(x)}{g(x)}=\lim_{x\to a}\frac{f'(x)}{g'(x)}
$$

if the limit on the right exists (or is $\pm\infty$).

**Hypotheses**
- $f$ and $g$ differentiable
- $g'(x)\neq0$ near $a$
- the limit has the form $\tfrac00$ or $\tfrac{\pm\infty}{\pm\infty}$

The rule also holds for one-sided limits ($x\to a^+$, $x\to a^-$) and for limits at infinity ($x\to\infty$, $x\to-\infty$).

N.B Differentiate the numerator and the denominator **separately**. This is not the Quotient Rule.

N.B Every solution needs two visible steps: first check that the limit really is $\tfrac00$ or $\tfrac{\pm\infty}{\pm\infty}$ and write down the type, then write L'H over the equals sign where the rule is applied.

> [!warning] Check the form before using the rule
> $\displaystyle\lim_{x\to\pi^-}\frac{\sin x}{1-\cos x}$: the numerator goes to $\sin\pi=0$ but the denominator goes to $1-\cos\pi=2$, so this is not indeterminate and the rule must not be used. Plug in directly: $\dfrac{0}{2}=0$. (source) <span style="color:#e03131">Wrong:</span> differentiating anyway gives $\cos x/\sin x\to-\infty$ as $x\to\pi^-$ (added). <span style="color:#2f9e44">Right:</span> the limit is $0$. #common-mistake

**Worked example (source, §4.4 Part 1).** $\displaystyle\lim_{x\to1}\frac{\ln x}{x-1}$, type $\tfrac00$:

$$
\lim_{x\to1}\frac{\ln x}{x-1}\overset{\text{L'H}}{=}\lim_{x\to1}\frac{1/x}{1}=1.
$$

**Worked example (source, §4.4 Part 1), applying the rule twice.** $\displaystyle\lim_{x\to\infty}\frac{e^x}{x^2}$, type $\tfrac\infty\infty$, and still $\tfrac\infty\infty$ after one step:

$$
\lim_{x\to\infty}\frac{e^x}{x^2}\overset{\text{L'H}}{=}\lim_{x\to\infty}\frac{e^x}{2x}\overset{\text{L'H}}{=}\lim_{x\to\infty}\frac{e^x}{2}=\infty.
$$

**Worked example (source, §4.4 Part 1), simplify before going again.** $\displaystyle\lim_{x\to\infty}\frac{\ln x}{\sqrt[3]{x}}$, type $\tfrac\infty\infty$:

$$
\lim_{x\to\infty}\frac{\ln x}{x^{1/3}}\overset{\text{L'H}}{=}\lim_{x\to\infty}\frac{1/x}{\tfrac13x^{-2/3}}=\lim_{x\to\infty}\frac{3}{x^{1/3}}=0.
$$

Here the fraction was tidied after one step and the limit read off, so no second application was needed.

**Worked example (source, §4.4 Part 1), three applications.** $\displaystyle\lim_{x\to0}\frac{\tan x-x}{x^3}$, type $\tfrac00$:

$$
\lim_{x\to0}\frac{\tan x-x}{x^3}\overset{\text{L'H}}{=}\lim_{x\to0}\frac{\sec^2x-1}{3x^2}\overset{\text{L'H}}{=}\lim_{x\to0}\frac{2\sec^2x\tan x}{6x}=\lim_{x\to0}\frac{\sec^2x\tan x}{3x}
$$

$$
\overset{\text{L'H}}{=}\lim_{x\to0}\frac{2\sec^2x\tan^2x+\sec^4x}{3}=\frac13.
$$

The source needs $\tan0=0$, $\sec0=1$, $\frac{d}{dx}\tan x=\sec^2x$ and $\frac{d}{dx}\sec x=\sec x\tan x$ at every step.

**Type $0\cdot\infty$ (source).** If $\lim_{x\to a}f(x)=0$ and $\lim_{x\to a}g(x)=\pm\infty$, the product $f\cdot g$ is an indeterminate form of type $0\cdot\infty$. Turn it into a quotient first, which is plain algebra and not yet the rule:

$$
f\cdot g=\frac{f}{1/g}\qquad\text{or}\qquad f\cdot g=\frac{g}{1/f}.
$$

That gives $\tfrac00$ or $\tfrac\infty\infty$, and now the rule applies. N.B The choice matters: first try leaving the function with the more complicated reciprocal in the numerator.

**Worked example (source, §4.4 Part 1).** $\displaystyle\lim_{x\to0^+}x\ln x$. Put $1/x$ in the denominator, since $1/x$ is much easier to differentiate than $1/\ln x$:

$$
\lim_{x\to0^+}x\ln x=\lim_{x\to0^+}\frac{\ln x}{1/x}\overset{\text{L'H}}{=}\lim_{x\to0^+}\frac{1/x}{-1/x^2}=\lim_{x\to0^+}(-x)=0.
$$

<span style="color:#e03131">Wrong:</span> the other choice, $\dfrac{x}{1/\ln x}$, leads after one step to $\lim_{x\to0^+}-x(\ln x)^2$, which is again of type $0\cdot\infty$ and no closer to an answer. <span style="color:#2f9e44">Right:</span> $\dfrac{\ln x}{1/x}$.

**Where the rule is used elsewhere in this vault.** Two improper integral examples below need it for the boundary term, $\int_{-\infty}^0xe^x\,dx$ and $\int_0^1\ln x\,dx$ (see: Worked examples from the lecture, section 7.8). The vertical tangents of the cycloid in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: tangent to the cycloid (source, slides 9 to 11)|S16]] also need it.

## Curve sketching (added)

Source: Dr K, §4.3 How Derivatives affect the shape of a Graph and §4.5 Summary of curve sketching, plus the §4.5 textbook slides (2023 deck), wherever marked (source). The "reading a curve" paragraph and the $x^3-3x^2$ example below are added context, the standard way these results get used together, gathered here because Abs Max/Min, MVT, and the Inc/Dec Test only really click once you use them on an actual curve.

**Reading a curve from $f'$ and $f''$.** Find the critical points (where $f'=0$ or is undefined), then use the Inc/Dec Test on the intervals between them to say where $f$ rises and falls. A critical point where $f'$ switches from positive to negative is a local maximum, negative to positive is a local minimum, no switch means neither (the $x^3$ situation from Fermat's Theorem above). **Concavity** describes which way the curve bends: $f''(x)>0$ means the curve bends upward (concave up, like a cup), $f''(x)<0$ means it bends downward (concave down, like a frown). A point where concavity switches is called an **inflection point**. Limits at the ends of the domain (to find asymptotes) sometimes need [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]], for example $\lim_{x\to-\infty}xe^x=0$ gives the $x$-axis as a horizontal asymptote of $y=xe^x$ (source, §4.5 summary of curve sketching).

**(composite) Worked example.** Let $f(x) = x^3 - 3x^2$. Then $f'(x) = 3x^2-6x = 3x(x-2)$, zero at $x=0$ and $x=2$. Testing signs: $f'>0$ on $(-\infty,0)$, $f'<0$ on $(0,2)$, $f'>0$ on $(2,\infty)$. So $x=0$ is a local maximum ($f(0)=0$) and $x=2$ is a local minimum ($f(2)=-4$). $f''(x)=6x-6$, zero at $x=1$, negative before and positive after, so $x=1$ is an inflection point.

```desmos-graph
left=-2; right=4;
top=6; bottom=-6;
---
y=x^{3}-3x^{2}
```

### First Derivative Test, concavity and the Second Derivative Test

**The First Derivative Test (source, §4.3).** Suppose that $c$ is a critical number of a continuous function $f$.

(a) If $f'$ changes from positive to negative at $c$, then $f$ has a local maximum at $c$.

(b) If $f'$ changes from negative to positive at $c$, then $f$ has a local minimum at $c$.

(c) If $f'$ is positive to the left and right of $c$, or negative to the left and right of $c$, then $f$ has no local maximum or minimum at $c$.

**Hypotheses**
- $f$ continuous
- $c$ a critical number of $f$

This is the Inc/Dec Test read across one point: in (a), $f$ is increasing to the left of $c$ and decreasing to the right, so $c$ is a peak.

**Worked example (source, §4.3, Example 1).** $f(x)=3x^4-4x^3-12x^2+5$. Then $f'(x)=12x^3-12x^2-24x=12x(x-2)(x+1)$, with critical numbers $-1,0,2$. Signs of $f'$: negative on $(-\infty,-1)$, positive on $(-1,0)$, negative on $(0,2)$, positive on $(2,\infty)$. So $f$ is decreasing on $(-\infty,-1)$ and $(0,2)$, increasing on $(-1,0)$ and $(2,\infty)$. By the First Derivative Test, $f(-1)=0$ and $f(2)=-27$ are local minimum values and $f(0)=5$ is a local maximum value.

**Concavity (source).** If the graph of $f$ lies above all of its tangents on an interval $I$, it is **concave upward** (CU) on $I$. If it lies below all of its tangents on $I$, it is **concave downward** (CD) on $I$.

**Concavity Test (source).**

(1) If $f''(x)>0$ for all $x$ in $I$, the graph of $f$ is concave upward on $I$.

(2) If $f''(x)<0$ for all $x$ in $I$, the graph of $f$ is concave downward on $I$.

Why it holds: on a CU curve the tangent slope increases from left to right, so $f'$ is increasing, so its derivative $f''$ is positive (source).

**Definition (source).** A point $P$ on a curve $y=f(x)$ is an **inflection point** if $f$ is continuous there and the curve changes from concave upward to concave downward, or from concave downward to concave upward, at $P$. If the curve has a tangent at an inflection point, the curve crosses its tangent there. By the Concavity Test, there is an inflection point wherever $f''$ changes sign.

N.B $f''(c)=0$ is not enough, the sign of $f''$ has to change. (added) $f(x)=x^4$ has $f''(0)=0$, but $f''(x)=12x^2\ge0$ on both sides, so the curve is concave up throughout and $x=0$ is not an inflection point.

**The Second Derivative Test (source).** Suppose $f''$ is continuous near $c$.

(a) If $f'(c)=0$ and $f''(c)>0$, then $f$ has a local minimum at $c$.

(b) If $f'(c)=0$ and $f''(c)<0$, then $f$ has a local maximum at $c$.

**Hypotheses**
- $f''$ continuous near $c$
- $f'(c)=0$

In (a), $f''>0$ near $c$ means $f$ is concave up near $c$, so the graph lies above its horizontal tangent at $c$ and $c$ is a local minimum.

N.B The test says nothing when $f''(c)=0$ (the point could be a maximum, a minimum or neither) or when $f''(c)$ does not exist. Then use the First Derivative Test. Even when both tests apply, the First Derivative Test is often the easier one (source).

**Worked example (source, §4.3).** $y=x^4-4x^3$. Then $f'(x)=4x^3-12x^2=4x^2(x-3)$ and $f''(x)=12x^2-24x=12x(x-2)$, with critical numbers $0$ and $3$. At $3$: $f''(3)=36>0$, so $f(3)=-27$ is a local minimum. At $0$: $f''(0)=0$, so the Second Derivative Test is silent. $f'$ is negative on both sides of $0$ (since $4x^2\ge0$ and $x-3<0$), so by the First Derivative Test there is no extremum at $0$. $f''$ is positive on $x<0$, negative on $(0,2)$ and positive on $x>2$, so the inflection points are $(0,0)$ and $(2,-16)$.

### Curve sketching checklist

Source: Dr K, §4.5 Summary of curve sketching, and the §4.5 guidelines in the 2023 deck. The lecture's examples label the steps A to H:

- **A. Domain.** Where is the function defined?
- **B. Intercepts.** The $y$-intercept is $f(0)$, the $x$-intercepts come from $f(x)=0$.
- **C. Symmetry.** Even if $f(-x)=f(x)$ for all $x$ in the domain (symmetric about the $y$-axis). Odd if $f(-x)=-f(x)$ (symmetric about the origin). Periodic if $f(x+p)=f(x)$ for all $x$ (repeats after every interval of length $p$, so sketch one period and translate).
- **D. Asymptotes.** Horizontal: as $x\to\pm\infty$, does $f$ approach a line $y=L$? Vertical: as $x\to a^\pm$, does $f$ go to $\pm\infty$ (check the endpoints of the domain)? Slant: see below.
- **E. Intervals of increase and decrease.** Where is $f'>0$ and where is $f'<0$ (Inc/Dec Test)?
- **F. Local maximum and minimum values.** Where is $f'=0$ or undefined, classified by the First Derivative Test.
- **G. Concavity and inflection points.** Where is $f''>0$, $f''=0$, $f''<0$?
- **H. Sketch.** Use everything found to draw a graph showing the most important features.

> [!warning] Symmetry: the §4.5 summary slides misstate it
> <span style="color:#e03131">Wrong (as printed in the §4.5 summary slides):</span> an odd function is "mirrored by the line $y=x$", and $y=\ln(4-x^2)$ is called symmetric "about the origin". <span style="color:#2f9e44">Right:</span> an even function is symmetric about the $y$-axis, an odd function about the origin (a $180^\circ$ rotation). So $\ln(4-x^2)$, which is even, is symmetric about the $y$-axis, and $x^3/(x^2+1)$, which is odd, is symmetric about the origin. The 2023 textbook deck states both correctly. (source error, noted so it isn't copied) #common-mistake

### Slant asymptotes

**Definition (source).** If $\displaystyle\lim_{x\to\infty}\big[f(x)-(mx+b)\big]=0$ with $m\neq0$, the line $y=mx+b$ is a **slant asymptote** of $y=f(x)$, because the vertical distance between the curve and the line approaches zero. The same holds for $x\to-\infty$.

For a rational function, a slant asymptote occurs when the degree of the numerator is exactly one more than the degree of the denominator (2023 deck). Long division then gives the line.

**Worked example (source, §4.5).** $f(x)=\dfrac{x^3}{x^2+1}$. Long division gives $f(x)=x-\dfrac{x}{x^2+1}$, which suggests $y=x$. Confirm:

$$
\lim_{x\to\pm\infty}\big[f(x)-x\big]=\lim_{x\to\pm\infty}-\frac{x}{x^2+1}=\lim_{x\to\pm\infty}-\frac{1/x}{1+1/x^2}=0.
$$

So $y=x$ is a slant asymptote. The rest of the sketch:
- Domain $\mathbb R$, intercept $(0,0)$, odd (symmetric about the origin), no vertical or horizontal asymptote.
- $f'(x)=\dfrac{x^2(x^2+3)}{(x^2+1)^2}>0$ for $x\neq0$, so $f$ is increasing on $(-\infty,0)\cup(0,\infty)$. $f'(0)=0$ but $f'$ does not change sign, so there is no local maximum or minimum.
- $f''(x)=\dfrac{2x(3-x^2)}{(x^2+1)^3}$ is zero at $0$ and $\pm\sqrt3$, and changes sign at each. Inflection points $\left(-\sqrt3,-\frac{3\sqrt3}{4}\right)$, $(0,0)$, $\left(\sqrt3,\frac{3\sqrt3}{4}\right)$.

N.B The long division only suggests the candidate line. The limit is what confirms it.

```desmos-graph
left=-5; right=5;
top=5; bottom=-5;
---
y=\frac{x^{3}}{x^{2}+1}
y=x
```

### Worked sketches from the lecture, section 4.5

**Example 1 (source, 2023 deck): $y=\dfrac{2x^2}{x^2-1}$.**
- Domain $x\neq\pm1$, intercept $(0,0)$, even (symmetric about the $y$-axis).
- $\displaystyle\lim_{x\to\pm\infty}\frac{2x^2}{x^2-1}=\lim\frac{2}{1-1/x^2}=2$, so $y=2$ is a horizontal asymptote. The denominator is $0$ at $x=\pm1$ and $\lim_{x\to1^+}=\infty$, $\lim_{x\to1^-}=-\infty$, $\lim_{x\to-1^+}=-\infty$, $\lim_{x\to-1^-}=\infty$, so $x=1$ and $x=-1$ are vertical asymptotes.
- $f'(x)=\dfrac{-4x}{(x^2-1)^2}$. Increasing on $(-\infty,-1)$ and $(-1,0)$, decreasing on $(0,1)$ and $(1,\infty)$. The only critical number is $0$ ($\pm1$ is not in the domain), and $f(0)=0$ is a local maximum.
- $f''(x)=\dfrac{12x^2+4}{(x^2-1)^3}$. CU on $(-\infty,-1)$ and $(1,\infty)$, CD on $(-1,1)$. No inflection points, since $\pm1$ is not in the domain.

```desmos-graph
left=-5; right=5;
top=6; bottom=-6;
---
y=\frac{2x^{2}}{x^{2}-1}
y=2
x=1
x=-1
```

**Example 2 (source): $y=\dfrac{x^2}{\sqrt{x+1}}$.**
- Domain $(-1,\infty)$, intercept $(0,0)$, no symmetry. $\lim_{x\to\infty}f(x)=\infty$, so no horizontal asymptote ($x\to-\infty$ is not considered, it is outside the domain). As $x\to-1^+$, $\sqrt{x+1}\to0$ and $f>0$, so $\lim=\infty$ and $x=-1$ is a vertical asymptote.
- $f'(x)=\dfrac{x(3x+4)}{2(x+1)^{3/2}}$. The only critical number in the domain is $0$ ($-\tfrac43$ is outside it). Decreasing on $(-1,0)$, increasing on $(0,\infty)$, and $f(0)=0$ is a local (and absolute) minimum.
- $f''(x)=\dfrac{3x^2+8x+8}{4(x+1)^{5/2}}$. The numerator has discriminant $64-96=-32<0$ and positive leading coefficient, so it is always positive. $f''>0$ on the whole domain: CU throughout, no inflection point.

**Example 3 (source): $y=xe^x$.**
- Domain $\mathbb R$, intercept $(0,0)$, no symmetry. $\lim_{x\to\infty}xe^x=\infty$. As $x\to-\infty$ the product is $0\cdot\infty$ type, so rewrite and use [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]]: $\displaystyle\lim_{x\to-\infty}\frac{x}{e^{-x}}\overset{\text{L'H}}{=}\lim_{x\to-\infty}\frac{1}{-e^{-x}}=\lim_{x\to-\infty}(-e^x)=0$. The $x$-axis is a horizontal asymptote on the left.
- $f'(x)=(x+1)e^x$. Decreasing on $(-\infty,-1)$, increasing on $(-1,\infty)$, and $f(-1)=-e^{-1}$ is a local (and absolute) minimum.
- $f''(x)=(x+2)e^x$. CD on $(-\infty,-2)$, CU on $(-2,\infty)$, inflection point $(-2,-2e^{-2})$.

**Example 4 (source): $y=\dfrac{\cos x}{2+\sin x}$.**
- Domain $\mathbb R$, $y$-intercept $\tfrac12$, $x$-intercepts at $x=\tfrac\pi2+n\pi$. Neither even nor odd, but $f(x+2\pi)=f(x)$, so periodic with period $2\pi$: sketch $0\le x\le2\pi$ and extend by translation. No asymptotes.
- $f'(x)=-\dfrac{2\sin x+1}{(2+\sin x)^2}$. The denominator is always positive, so $f'>0$ when $\sin x<-\tfrac12$, that is $\tfrac{7\pi}{6}<x<\tfrac{11\pi}{6}$. Increasing on $\left(\tfrac{7\pi}{6},\tfrac{11\pi}{6}\right)$, decreasing on $\left(0,\tfrac{7\pi}{6}\right)\cup\left(\tfrac{11\pi}{6},2\pi\right)$. Local minimum $f\!\left(\tfrac{7\pi}{6}\right)=-\tfrac{1}{\sqrt3}$, local maximum $f\!\left(\tfrac{11\pi}{6}\right)=\tfrac{1}{\sqrt3}$.
- $f''(x)=-\dfrac{2\cos x\,(1-\sin x)}{(2+\sin x)^3}$. Since $1-\sin x\ge0$ and $(2+\sin x)^3>0$, $f''>0$ exactly when $\cos x<0$. CU on $\left(\tfrac\pi2,\tfrac{3\pi}2\right)$, CD on $\left(0,\tfrac\pi2\right)\cup\left(\tfrac{3\pi}2,2\pi\right)$, inflection points $\left(\tfrac\pi2,0\right)$ and $\left(\tfrac{3\pi}2,0\right)$.

**Example 5 (source): $y=\ln(4-x^2)$.**
- Domain $(-2,2)$, $y$-intercept $\ln4$, $x$-intercepts $\pm\sqrt3$ (from $4-x^2=1$). Even, symmetric about the $y$-axis. No horizontal asymptotes (see the domain). Since $4-x^2\to0^+$ as $x\to\pm2$ from inside the domain, $\lim\ln(4-x^2)=-\infty$ and $x=\pm2$ are vertical asymptotes.
- $f'(x)=\dfrac{-2x}{4-x^2}$. Increasing on $(-2,0)$, decreasing on $(0,2)$, and $f(0)=\ln4$ is a local maximum.
- $f''(x)=\dfrac{-8-2x^2}{(4-x^2)^2}<0$ for all $x$ in the domain: CD throughout, no inflection point.

## Integration techniques

All formulas referenced here (the exact statements of IBP, trig substitutions, partial fractions, and the reduction cases) live in [[MAT01B1_Notes_S2_DerivativeIntegralReference]], worked examples for each live in [[MAT01B1_Notes_S3_IntegrationExamples]], this section is about when and why to reach for each one, not the formulas or the worked mechanics.

**Integration by Parts** is the product rule run in reverse. It's the tool when the integrand is a product of two functions of different types (a polynomial times an exponential, a log by itself, an inverse trig function by itself) where no substitution collapses it into something simpler. See [[MAT01B1_Notes_S2_DerivativeIntegralReference#Integration by Parts]] for the formula and the LIATE guide for picking $u$. Worked examples, including the repeated, cyclic and definite cases, are in [[MAT01B1_Notes_S3_IntegrationExamples#Integration by Parts]].

**Trig substitution** is the tool specifically for a square root of a sum or difference of squares sitting under the integral sign, $\sqrt{a^2-b^2x^2}$, $\sqrt{b^2x^2-a^2}$, or $\sqrt{a^2+b^2x^2}$. The substitution turns the root into a single trig function via a Pythagorean identity, removing it entirely. See [[MAT01B1_Notes_S2_DerivativeIntegralReference#Trig substitutions]]. Worked examples, including the definite, completing-the-square and preliminary-substitution cases, are in [[MAT01B1_Notes_S3_IntegrationExamples#Worked examples from the lecture, section 7.3]].

**Partial fractions** is for a rational function (one polynomial divided by another) where nothing simplifies directly. The idea: any such fraction can be broken back apart into the simpler fractions that would have been added together to make it, and each of those simpler pieces integrates using the log or arctan patterns already in the reference tables. See [[MAT01B1_Notes_S2_DerivativeIntegralReference#Partial fractions]] for the decomposition table, and [[MAT01B1_Notes_S3_IntegrationExamples#Partial Fractions]] for a worked example. All four cases, completing the square, avoiding partial fractions and rationalizing substitutions are worked in [[MAT01B1_Notes_S3_IntegrationExamples#Worked examples from the lecture, section 7.4]].

**Products and quotients of trig functions** ($\sin^n x\cos^m x$, $\tan^n x\sec^m x$) get handled by stripping one factor out to serve as the substitution's $du$, then converting everything else to match the remaining variable using a Pythagorean identity. The full case breakdown, including the case the original reference sheet left unexplained ($\tan^n x\sec^m x$ with $n$ even and $m$ odd, which needs the secant reduction formula), is in [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products and quotients of trig functions]]. Worked examples are in [[MAT01B1_Notes_S3_IntegrationExamples#Worked examples from the lecture, section 7.2, sine and cosine]] and [[MAT01B1_Notes_S3_IntegrationExamples#Worked examples from the lecture, section 7.2, tangent and secant]], and products of different angles use the identities in [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products of sines and cosines of different angles (source, §7.2)|Products of sines and cosines of different angles]].

### Strategy for integration

Source: Dr K, §7.5 Strategy for Integration. There are no hard and fast rules, but there is a recognition order. It assumes the basic integration formulas are known (the table in [[MAT01B1_Notes_S2_DerivativeIntegralReference]]). The asterisked table formulas, 19 and 20, need not be memorised: 19 can be avoided with partial fractions and 20 with a trigonometric substitution.

1. **Simplify the integrand if possible.** Algebra or a trig identity may make the method obvious: $\int\sqrt x(1+\sqrt x)\,dx=\int(\sqrt x+x)\,dx$, $\int\frac{\tan\theta}{\sec^2\theta}\,d\theta=\int\frac{\sin\theta}{\cos\theta}\cos^2\theta\,d\theta$, $\int\sin\theta\cos\theta\,d\theta=\frac12\int\sin2\theta\,d\theta$, and $\int(\sin x+\cos x)^2\,dx=\int(1+\sin2x)\,dx$.
2. **Look for an obvious substitution.** Find a $u=g(x)$ whose differential $g'(x)\,dx$ also appears, apart from a constant factor. In $\int\frac{x}{x^2-1}\,dx$, $u=x^2-1$ is better than partial fractions.
3. **Classify the integrand by its form.**
   - Powers of $\sin x,\cos x$, or of $\tan x,\sec x$, or of $\cot x,\csc x$: the strip-a-factor substitutions above.
   - A rational function: partial fractions (dividing first if it is improper).
   - A product of a power of $x$ (or a polynomial) and a transcendental function (trigonometric, exponential, logarithmic): integration by parts, choosing $u$ and $dv$.
   - Radicals: $\sqrt{\pm x^2\pm a^2}$ calls for a trigonometric substitution, and $\sqrt[n]{ax+b}$ calls for the rationalizing substitution $u=\sqrt[n]{ax+b}$ (more generally this sometimes works for $\sqrt[n]{g(x)}$).
4. **Try again.** There are basically only two methods, substitution and parts. Try a substitution even if none is obvious. Try parts, which sometimes works on a single function ($\int\ln x\,dx$). Manipulate the integrand algebraically, for example $\int\frac{dx}{1-\cos x}=\int\frac{1+\cos x}{\sin^2x}\,dx=\int\left(\csc^2x+\frac{\cos x}{\sin^2x}\right)dx$. Relate the problem to an earlier one: $\int\tan^2x\sec x\,dx=\int\sec^3x\,dx-\int\sec x\,dx$ reuses the $\sec^3$ result. Or combine several methods in one integral.

**Examples (source: method of attack).** The lecture sets out the plan for most of these and does not finish them. The final answers marked (added) are completed here.

- $\displaystyle\int\frac{\tan^3x}{\cos^3x}\,dx$: step 1 rewrites it as $\int\tan^3x\sec^3x\,dx$, the $\tan^m\sec^n$ form with $m$ odd. Alternatively $\int\frac{\sin^3x}{\cos^6x}\,dx$ with $u=\cos x$ leads to $\int(u^{-4}-u^{-6})\,du$. (added) Either way the answer is $\frac{\sec^5x}{5}-\frac{\sec^3x}{3}+C$, the same as the $\tan^3x\sec^3x$ example in S3.
- $\displaystyle\int e^{\sqrt x}\,dx$: the rationalizing substitution $u=\sqrt x$, $x=u^2$, $dx=2u\,du$ gives $2\int ue^u\,du$, a product of $u$ and a transcendental function, so integrate by parts. (added) $2(\sqrt x-1)e^{\sqrt x}+C$.
- $\displaystyle\int\frac{x^5+1}{x^3-3x^2-10x}\,dx$: no simplification or substitution is obvious, and the fraction is rational and improper, so divide first and then use partial fractions. (added) The quotient is $x^2+3x+19$ with remainder $87x^2+190x+1$, the denominator is $x(x-5)(x+2)$, and the result is $\frac{x^3}{3}+\frac{3x^2}{2}+19x-\frac1{10}\ln|x|+\frac{3126}{35}\ln|x-5|-\frac{31}{14}\ln|x+2|+C$.
- $\displaystyle\int\frac{dx}{x\sqrt{\ln x}}$: only step 2 is needed. $u=\ln x$ has $du=\frac{dx}{x}$, which is in the integral. (added) $2\sqrt{\ln x}+C$.
- $\displaystyle\int\sqrt{\frac{1-x}{1+x}}\,dx$ (worked in full in the source): the rationalizing substitution $u=\sqrt{\frac{1-x}{1+x}}$ works but leads to a very complicated rational function. Algebra is easier: multiply the numerator and denominator by $\sqrt{1-x}$, giving $\int\frac{1-x}{\sqrt{1-x^2}}\,dx=\int\frac{dx}{\sqrt{1-x^2}}-\int\frac{x}{\sqrt{1-x^2}}\,dx$, which is $\sin^{-1}x+\sqrt{1-x^2}+C$ (the second piece by $u=1-x^2$).

### Elementary functions and non-elementary integrals

The **elementary functions** are the polynomials, rational functions, power functions $x^a$, exponential functions $a^x$, logarithmic functions, trigonometric and inverse trigonometric functions, hyperbolic and inverse hyperbolic functions, and everything built from these by addition, subtraction, multiplication, division and composition (source, §7.5).

If $f$ is elementary, then $f'$ is elementary, but $\int f(x)\,dx$ need not be. For example, $f(x)=e^{x^2}$ is continuous, so $F(x)=\int_0^xe^{t^2}\,dt$ exists and $F'(x)=e^{x^2}$ by Part 1 of the Fundamental Theorem of Calculus. But $F$ has been proved not to be elementary, so no amount of effort will evaluate $\int e^{x^2}\,dx$ in terms of known functions. The same holds for $\int\frac{e^x}{x}\,dx$, $\int\sin(x^2)\,dx$, $\int\cos(e^x)\,dx$, $\int\sqrt{x^3+1}\,dx$, $\int\frac{1}{\ln x}\,dx$ and $\int\frac{\sin x}{x}\,dx$. In fact most elementary functions have no elementary antiderivative.

This is why [[MAT01B1_Notes_S14_LinearDifferentialEquations#Worked example: a non-elementary integral (source, slides 12 to 13)|S14's example]] leaves $\int e^{x^2}\,dx$ as a definite integral, and why the Comparison Theorem below is useful (see: Comparison Theorem).

## Improper integrals (added)

Source: the Comparison Theorem and every example marked (source, §7.8) are from Dr K, §7.8 Improper Integrals. The rest of this section is added context.

Every integral formula above assumes a finite interval and a function with no breaks in it. An **improper integral** is one where that assumption fails, either the interval runs out to infinity (**Type I**), or the function has a discontinuity, usually a vertical asymptote (a value the function shoots off to infinity near, without ever reaching it), somewhere in the interval (**Type II**).

**Type I: infinite interval.**

$$
\int_a^{\infty} f(x)\,dx = \lim_{t\to\infty} \int_a^t f(x)\,dx.
$$

If the limit exists (is a finite number), the integral is called **convergent** and that limit is its value. If the limit doesn't exist or is infinite, the integral is **divergent**. The same idea applies to $\int_{-\infty}^b f(x)\,dx$ with $t\to-\infty$, and $\int_{-\infty}^{\infty}f(x)\,dx$ is split at any point $c$ into $\int_{-\infty}^c + \int_c^{\infty}$, both pieces have to converge separately for the whole thing to converge.

**(composite) Worked example.** $\displaystyle\int_1^{\infty} \frac{1}{x^2}\,dx = \lim_{t\to\infty}\int_1^t x^{-2}\,dx = \lim_{t\to\infty}\left[-\frac{1}{x}\right]_1^t = \lim_{t\to\infty}\left(1-\frac{1}{t}\right) = 1.$ Convergent, value $1$, even though the region extends forever, the area under it is finite.

```desmos-graph
left=0; right=10;
top=3; bottom=-1;
---
y=1/x^{2}
```

**Type II: discontinuity in the interval.** If $f$ has a vertical asymptote at $b$ (or at $a$, or at an interior point $c\in(a,b)$), the integral is again defined as a limit approaching that point:

$$
\int_a^b f(x)\,dx = \lim_{t\to b^-} \int_a^t f(x)\,dx \quad \text{(asymptote at } b\text{)}.
$$

If the asymptote is at the left endpoint $a$, use $\lim_{t\to a^+}\int_t^b f(x)\,dx$ instead. If it sits at an interior point $c$ with $a<c<b$, split the integral at $c$ and treat each piece as its own limit:

$$
\int_a^b f(x)\,dx=\int_a^c f(x)\,dx+\int_c^b f(x)\,dx.
$$

The whole integral converges only if **both** pieces converge (source, §7.8).

> [!warning] Spot the asymptote before integrating
> $\displaystyle\int_0^3\frac{dx}{x-1}$ has a vertical asymptote at $x=1$, inside the interval. <span style="color:#e03131">Wrong:</span> treating it as an ordinary integral gives $\ln|x-1|\Big|_0^3=\ln2-\ln1=\ln2$. <span style="color:#2f9e44">Right:</span> split at $1$. Already $\displaystyle\int_0^1\frac{dx}{x-1}=\lim_{t\to1^-}\ln|t-1|=-\infty$, so the integral is divergent. (source, §7.8, Example 7 and its warning) #common-mistake


**(composite) Worked example.** $\displaystyle\int_0^1 \frac{1}{\sqrt{x}}\,dx = \lim_{t\to0^+}\int_t^1 x^{-1/2}\,dx = \lim_{t\to0^+}\Big[2\sqrt{x}\Big]_t^1 = \lim_{t\to0^+}\big(2-2\sqrt{t}\big) = 2.$ Convergent, value $2$, despite the function blowing up at $x=0$.

**The $p$-integral test.** Two families come up constantly enough to be worth memorising outright rather than re-deriving every time:

$$
\int_1^{\infty} \frac{1}{x^p}\,dx \text{ converges} \iff p>1, \qquad \int_0^1 \frac{1}{x^p}\,dx \text{ converges} \iff p<1.
$$

Notice these point in opposite directions: for the infinite interval, a *steeper* fall-off (larger $p$) is what saves it. For the interval shrinking toward a vertical asymptote, a *gentler* blow-up (smaller $p$) is what saves it. For $p>1$ the value is $\int_1^\infty\frac{1}{x^p}\,dx=\frac{1}{p-1}$, and for $p=1$ it is $\lim_{t\to\infty}\ln t=\infty$, divergent (source, §7.8, Examples 1 and 4).

### Worked examples from the lecture, section 7.8

**Type I.** $\displaystyle\int_1^\infty\frac{dx}{x}=\lim_{t\to\infty}\ln t=\infty$, divergent (source, §7.8, Example 1). Compare $\int_1^\infty\frac{dx}{x^2}=1$ above: both integrands go to $0$, but $1/x^2$ goes to $0$ fast enough and $1/x$ doesn't.

$\displaystyle\int_{-\infty}^0xe^x\,dx=\lim_{t\to-\infty}\int_t^0xe^x\,dx=\lim_{t\to-\infty}\big(-te^t-1+e^t\big)=-1$ (source, §7.8, Example 2). Integration by parts with $u=x$, $dv=e^x\,dx$ gives the antiderivative, and $te^t\to0$ comes from rewriting $te^t=\dfrac{t}{e^{-t}}$ and using [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]] (type $\tfrac\infty\infty$).

$\displaystyle\int_{-\infty}^{\infty}\frac{dx}{1+x^2}=\pi$ (source, §7.8, Example 3). Split at $0$: each half is $\lim\tan^{-1}$ and equals $\tfrac\pi2$, and both converge.

**Type II.** $\displaystyle\int_2^5\frac{dx}{\sqrt{x-2}}=\lim_{t\to2^+}2\big(\sqrt3-\sqrt{t-2}\big)=2\sqrt3$, convergent (source, §7.8, Example 5). The asymptote is at the left endpoint, so the limit is $t\to2^+$.

$\displaystyle\int_0^{\pi/2}\sec x\,dx=\lim_{t\to(\pi/2)^-}\ln|\sec t+\tan t|=\infty$, divergent (source, §7.8, Example 6).

$\displaystyle\int_0^1\ln x\,dx=\lim_{t\to0^+}\big(-t\ln t-1+t\big)=-1$ (source, §7.8, Example 8). Integration by parts with $u=\ln x$, $dv=dx$, and $t\ln t\to0$ from the $0\cdot\infty$ case of [[#L'Hospital's Rule and indeterminate forms|L'Hospital's Rule]].

### Comparison Theorem

**Comparison Theorem (source, §7.8)**, also called the Comparison Test. Suppose $f$ and $g$ are continuous with $f(x)\ge g(x)\ge0$ for $x\ge a$.

(a) If $\displaystyle\int_a^\infty f(x)\,dx$ is convergent, then $\displaystyle\int_a^\infty g(x)\,dx$ is convergent.

(b) If $\displaystyle\int_a^\infty g(x)\,dx$ is divergent, then $\displaystyle\int_a^\infty f(x)\,dx$ is divergent.

**Hypotheses**
- $f$ and $g$ continuous
- $f(x)\ge g(x)\ge0$ for $x\ge a$

The source states it for Type I integrals and says a similar theorem holds for Type II. It omits the proof and gives only the picture: if the area under the top curve $y=f(x)$ is finite, so is the area under the bottom curve $y=g(x)$, and if the area under the bottom curve is infinite, so is the area under the top. This is useful exactly when the actual antiderivative is hard or impossible to find, but the integral can still be pinned between something easy and a known $p$-integral.

> [!warning] Only two directions work
> <span style="color:#2f9e44">Right:</span> a smaller nonnegative function under a convergent bigger one converges, and a bigger function over a divergent smaller one diverges. <span style="color:#e03131">Wrong:</span> concluding $\int f$ converges because $\int g$ does, or that $\int g$ diverges because $\int f$ does. If $\int_a^\infty g$ converges, $\int_a^\infty f$ may or may not; if $\int_a^\infty f$ diverges, $\int_a^\infty g$ may or may not. (source) #common-mistake

**Worked example (source, §7.8, Example 9), convergence.** Show $\displaystyle\int_0^\infty e^{-x^2}\,dx$ is convergent. The antiderivative of $e^{-x^2}$ isn't elementary, so split:

$$
\int_0^\infty e^{-x^2}\,dx=\int_0^1e^{-x^2}\,dx+\int_1^\infty e^{-x^2}\,dx.
$$

The first integral is an ordinary definite integral. For the second, $x\ge1$ gives $x^2\ge x$, so $-x^2\le-x$ and $e^{-x^2}\le e^{-x}$. Also

$$
\int_1^\infty e^{-x}\,dx=\lim_{t\to\infty}\big(-e^{-t}+e^{-1}\big)=e^{-1},
$$

convergent. Taking $f(x)=e^{-x}$ and $g(x)=e^{-x^2}$ in the Comparison Theorem, $\int_1^\infty e^{-x^2}\,dx$ converges, so $\int_0^\infty e^{-x^2}\,dx$ converges. (added) The split at $1$ is not optional: on $(0,1)$ we have $x^2<x$, so $e^{-x^2}>e^{-x}$ and the inequality needed for the theorem points the wrong way there.

**Worked example (source, §7.8, Example 10), divergence.** Show $\displaystyle\int_1^\infty\frac{1+e^{-x}}{x}\,dx$ is divergent. For $x\ge1$, $\dfrac{1+e^{-x}}{x}>\dfrac1x$, and $\displaystyle\int_1^\infty\frac{dx}{x}$ is divergent (the $p$-integral test with $p=1$). By part (b) with $g(x)=\dfrac1x$ and $f(x)=\dfrac{1+e^{-x}}{x}$, the given integral is divergent.

**(composite) Worked example.** Does $\displaystyle\int_1^{\infty} \frac{1}{\sqrt{x^3+1}}\,dx$ converge? The antiderivative isn't elementary, so compare instead: for $x\ge1$, $\sqrt{x^3+1} > \sqrt{x^3} = x^{3/2}$, so $\dfrac{1}{\sqrt{x^3+1}} < \dfrac{1}{x^{3/2}}$. Since $p=3/2>1$, $\int_1^\infty x^{-3/2}\,dx$ converges (by the $p$-integral test), and the original integrand is smaller and nonnegative, so by the Comparison Theorem the original integral converges too, without ever finding its actual value.

## See also
- [[MAT01B1_Proofs_ST1]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S3_IntegrationExamples]]
- [[MAT01B1_Notes_S5_OptimizationProblems]] (the extremum theory above applied directly to optimization problems)
- [[MAT01B1_Notes_S6_MVTForIntegrals]] (integral counterpart of the Mean Value Theorem)
- [[MAT01B1_Notes_S14_LinearDifferentialEquations]] (a different non-elementary integral, $\int e^{x^2}\,dx$, handled via the Fundamental Theorem of Calculus rather than the Comparison Theorem used above)
- [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Worked example: tangent to the cycloid (source, slides 9 to 11)]] (L'Hospital's Rule applied to the cycloid's vertical tangents)
