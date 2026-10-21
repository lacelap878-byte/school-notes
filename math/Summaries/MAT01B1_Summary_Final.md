---
module: MAT01B1
test: Final
topic: Final exam summary
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, added]
---

# MAT01B1 Summary Final

Built for the morning before the final, for fast review and not first learning. It sits on top of [[MAT01B1_Summary_ST1]] and [[MAT01B1_Summary_ST2]], which are linked and not copied, and it adds the material taught after ST2: linear systems, matrices and the Binomial Theorem. The exam proof sheet is [[MAT01B1_Proofs_Final]].

Labels: `(source: past papers)` means taken from the 15 papers you supplied. `(source: revision session)` and `(your words)` come from your own revision and reports. `(added)` means built during revision from the notes. Orange text marked Open is something still shaky.

## Contents

- [[#Definitions]]: terms used in this file, with look alike pairs separated
  - [[#Volume and strip terms]]: strip, washer, shell, radius, height, depth
  - [[#Length, surface and curve terms]]: ds, surface of revolution, parameter, polar
  - [[#Linear systems terms]]: augmented matrix, leading and free variables, homogeneous
  - [[#Matrix terms]]: size, product, transpose, trace, partition, linear combination
  - [[#Binomial terms]]: binomial coefficient, general term, constant term
- [[#Material covered]]: what the module covered, grouped by test
  - [[#Material from ST1]]: ST1 notes, summary and proofs
  - [[#Material from ST2]]: ST2 summary and proofs
  - [[#Material after ST2]]: linear systems, matrices, binomial notes
- [[#Condensed concept pass]]: one short entry per result, linked
  - [[#Calculus up to ST1]]: ST1 results, linked
  - [[#Calculus in ST2]]: ST2 results, linked by topic
  - [[#Polar slope, new since the notes]]: slope of a polar curve
  - [[#Linear systems and Gaussian elimination]]: methods and what the answers mean
  - [[#Matrices]]: operations, products, linear combinations
  - [[#Binomial Theorem]]: the theorem and picking out one term
- [[#Worked example notebook]]: one example per new principle
  - [[#Free variable example]]: a system with one free variable
  - [[#Product sizes and the column method]]: sizes, columns and rows of a product
  - [[#Linear combination example]]: A times a column as a mix of columns
  - [[#Binomial given term and sigma form]]: coefficient of a given power, show that
  - [[#Polar slope example]]: 2023 Exam C slope question
  - [[#Volume and surface area examples from revision]]: washers, shells, arc length worked in revision
- [[#What the tests showed]]: your account of how the tests went
  - [[#ST2]]: ST2 in your own words
  - [[#ST1]]: ST1 account still to be added
- [[#Common mistakes]]: slips grouped by pattern, open ones in orange
  - [[#Strips, radius and height]]: volume and surface area slips
  - [[#Algebra and simplifying]]: arithmetic and simplification slips
  - [[#Multiple choice]]: traps in the multiple choice
  - [[#Trig integrals]]: odd and even power rules
  - [[#Linear systems and matrices]]: free variables, products, linear combinations
- [[#Decision aids]]: short procedures for choosing a method
  - [[#Washer or shell]]: how to choose and set up
  - [[#Surface area, choosing r and ds]]: radius table and ds forms
  - [[#Which variable and which differential]]: dx or dy or dt
  - [[#Trig integral sorting]]: which rule for which trig integral
  - [[#Free variable test and reading a solution]]: leading versus free, writing the answer
  - [[#Matrix pieces and sizes]]: product sizes, columns, rows, trace
  - [[#Binomial term finder]]: find a named, power or constant term
  - [[#Multiple choice routine]]: order of attack for question 1
- [[#Exam procedure]]: format, recurring questions, in the paper
  - [[#Paper format, as far as the supplied papers show]]: question 1 and the written questions
  - [[#Questions that recur in the 15 supplied papers]]: what came up, with years
  - [[#In the paper]]: timing, blanking, checking
- [[#Tips]]: short takeaways from revision
- [[#See also]]: the proof sheet and earlier summaries

## Definitions

Cumulative across the module. Only terms this file uses, and the ones that were confused in revision. Where two terms look alike, the difference is stated.

### Volume and strip terms

- Strip: a thin slice of the region, drawn as a rectangle, whose thickness is $dx$ (a vertical strip) or $dy$ (a horizontal strip).
- Washer: the ring a strip makes when it is perpendicular to the axis and spins. Area $\pi(R^2-r^2)$.
- Shell: the tube a strip makes when it is parallel to the axis and spins. Volume piece $2\pi(\text{radius})(\text{height})\,d(\cdot)$.
- Radius: always the distance from the strip to the axis of rotation, never just the coordinate.
- Outer radius $R$ and inner radius $r$: the far and the near edge of the washer, measured from the axis. If the region does not touch the axis, the gap is the inner radius.
- Height of a shell: far end of the strip minus near end of the strip, along the strip. Not the same as depth.
- Depth versus height: depth is measured from the top of a container, height from the bottom. In a cone tank with the tip at the bottom, "2 m deep" means $h=2$ in $V=\tfrac1{12}\pi h^3$.

### Length, surface and curve terms

- Arc length element $ds$: the length of a tiny piece of curve, from the tiny right triangle with sides $dx$ and $dy$.
- Surface of revolution: the surface made by spinning a curve about an axis. Each piece of the curve sweeps a band.
- Parameter: the third variable, for example $t$, that both $x$ and $y$ depend on.
- Polar coordinates $(r,\theta)$: distance from the pole and angle from the polar axis. The same point has many polar representations.

### Linear systems terms

- Linear equation: $a_1x_1+\cdots+a_nx_n=b$, no products, powers or trig of the unknowns.
- Consistent and inconsistent: a system with at least one solution, and with none. A row $[0\ 0\ 0\ |\ 1]$ means inconsistent.
- Augmented matrix: the coefficients and the constants written together, with a bar before the constants.
- Elementary row operations: swap two rows, scale a row by a nonzero number, add a multiple of one row to another.
- Leading 1 or pivot: the first nonzero entry in a row, made equal to 1.
- Row echelon form: leading 1s step to the right going down, zero rows at the bottom.
- Reduced row echelon form: row echelon form plus zeros above every leading 1.
- Gaussian elimination: reduce to row echelon form, then back substitute. Gauss Jordan: reduce all the way to reduced row echelon form and read the answer off.
- Leading variable: its column has a leading 1. Free variable: its column has no leading 1.
- Parameter in a solution: the letter, such as $t$, you give a free variable.
- Homogeneous system: every constant is $0$. Trivial solution: all unknowns $0$. Nontrivial: any other solution.

### Matrix terms

- Size $m\times n$: $m$ rows and $n$ columns. Row vector: $1\times n$. Column vector: $m\times 1$.
- Square matrix, main diagonal, identity matrix: same number of rows and columns; entries $a_{11},a_{22},\dots$; ones on the diagonal and zeros elsewhere.
- Product defined: columns of $A$ equal rows of $B$. The product has the rows of $A$ and the columns of $B$.
- Transpose $A^T$: swap rows and columns, so an $m\times n$ matrix becomes $n\times m$.
- Trace: sum of the main diagonal entries. Only defined for a square matrix.
- Partitioned matrix: a matrix cut by lines into blocks. The useful cuts are into columns or into rows.
- Linear combination: numbers times matrices of the same size, added. For $A\bar x$, the entries of $\bar x$ say how many of each column of $A$ to take.
- Coefficient matrix: the part of the augmented matrix left of the bar, written $A$ in $A\bar x=\bar b$.

### Binomial terms

- Binomial: a two term expression such as $a+b$.
- $\binom nk$ (also ${}_nC_k$): $\dfrac{n!}{(n-k)!\,k!}$, the coefficient of the term with $b^k$.
- General term of $(a+b)^n$, with the anatomy:

$$\binom nk\,a^{\,n-k}\,b^{\,k}$$

  - $k$ runs from $0$ to $n$ and the $(k+1)$th term has $b^k$, so the 4th term has $k=3$.
  - The exponents of $a$ and $b$ always add to $n$.
  - Constant term: add the exponents of $x$ from $a^{n-k}$ and $b^k$, set the total to $0$, solve for $k$. It must be a whole number from $0$ to $n$, otherwise there is no constant term.

## Material covered

### Material from ST1

- [[MAT01B1_Summary_ST1]] (the ST1 summary)
- [[MAT01B1_Notes_S1_CalculusApplications]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S3_IntegrationExamples]]
- [[MAT01B1_Proofs_ST1]]

### Material from ST2

- [[MAT01B1_Summary_ST2]] (the ST2 summary, which links to every ST2 note S4 to S17)
- [[MAT01B1_Proofs_ST2]]

### Material after ST2

- [[MAT01B1_Notes_S18_IntroductionToLinearSystems]]
- [[MAT01B1_Notes_S19_GaussianElimination]]
- [[MAT01B1_Notes_S20_MatricesAndMatrixOperations]]
- [[MAT01B1_Notes_S21_BinomialTheorem]]

## Condensed concept pass

One short entry per major result. Entries already in an earlier summary are linked, not copied.

### Calculus up to ST1

- Fermat, Rolle, Mean Value Theorem, Theorem 5 with Corollary 7, and the increasing and decreasing test: see [[MAT01B1_Summary_ST1#Condensed concept pass]]. Full proofs on the exam proof sheet: [[MAT01B1_Proofs_Final]].
- Curve sketching, integration by parts, trig substitution, partial fractions, $\sin^n\cos^m$, $\tan^n\sec^m$, improper integrals and the comparison theorem: same section of the ST1 summary.

### Calculus in ST2

- Related rates: [[MAT01B1_Summary_ST2#Related rates (§3.9)]]
- Optimization: [[MAT01B1_Summary_ST2#Optimization (§4.7)]]
- Average value and the MVT for integrals: [[MAT01B1_Summary_ST2#Average value and the Mean Value Theorem for Integrals (§6.5 and MVT deck)]]
- Area between curves: [[MAT01B1_Summary_ST2#Area between curves (§6.1)]]
- Disks and washers: [[MAT01B1_Summary_ST2#Volumes by cross-sections, disks and washers (§6.2)]]
- Shells: [[MAT01B1_Summary_ST2#Cylindrical shells (§6.3)]]
- Arc length: [[MAT01B1_Summary_ST2#Arc length (§8.1)]]
- Surface area: [[MAT01B1_Summary_ST2#Surface area of revolution (§8.2)]]
- Separable equations: [[MAT01B1_Summary_ST2#Differential equations and separable equations (§9.3)]]
- Linear differential equations: [[MAT01B1_Summary_ST2#Linear differential equations (§9.5)]]
- Parametric curves: [[MAT01B1_Summary_ST2#Parametric curves (§10.1)]]
- Calculus with parametric equations: [[MAT01B1_Summary_ST2#Calculus with parametric equations (§10.2)]]
- Polar coordinates: [[MAT01B1_Summary_ST2#Polar coordinates (§10.3)]]

### Polar slope, new since the notes

- For a polar curve $r=f(\theta)$, treat $\theta$ as the parameter in $x=r\cos\theta$, $y=r\sin\theta$. The parametric slope formula then gives the slope (see: Polar slope derivation in [[MAT01B1_Proofs_Final]]).
- This is asked as "show that $dy/dx=\ldots$" in the 2023 Exams A, B and C (source: past papers). The slides stop before it, so it comes from the parametric slope formula in [[MAT01B1_Notes_S16_CalculusWithParametricEquations#Tangents]]. (added)

### Linear systems and Gaussian elimination

- Every system has no solution, exactly one, or infinitely many (source: [[MAT01B1_Notes_S18_IntroductionToLinearSystems#Solutions]]).
- Method: augmented matrix, row operations to row echelon form, back substitute. Gauss Jordan goes on to reduced row echelon form (source: [[MAT01B1_Notes_S19_GaussianElimination#Gaussian Elimination]]).
- Make zeros column by column, left to right, top to bottom in each column. For Gauss Jordan then clear above each leading 1, rightmost column first and bottom to top (source: [[MAT01B1_Notes_S19_GaussianElimination#Order of the zeros]]).
- A zero row means a redundant equation. A column without a leading 1 is a free variable, so the system has infinitely many solutions. A row $[0\ 0\ 0\ |\ 1]$ means no solution.
- Homogeneous systems always have the trivial solution. More unknowns than equations forces nontrivial solutions (source: [[MAT01B1_Notes_S19_GaussianElimination#Two theorems about homogeneous systems]]).

### Matrices

- Operations need equal sizes for sum and difference. A product needs columns of $A$ equal to rows of $B$ (source: [[MAT01B1_Notes_S20_MatricesAndMatrixOperations#Matrix multiplication]]).
- Column by column and row by row products: column $j$ of $AB$ is $A$ times column $j$ of $B$, and row $i$ of $AB$ is row $i$ of $A$ times $B$ (source: [[MAT01B1_Notes_S20_MatricesAndMatrixOperations#Matrix multiplication by columns and by rows]]).
- $A\bar x$ is a linear combination of the columns of $A$ with the entries of $\bar x$ as coefficients (source: [[MAT01B1_Notes_S20_MatricesAndMatrixOperations#Matrix products as linear combinations]]).
- A system is $A\bar x=\bar b$ (source: [[MAT01B1_Notes_S20_MatricesAndMatrixOperations#Matrix form of a linear system]]). Transpose swaps rows and columns, and trace adds the diagonal (source: [[MAT01B1_Notes_S20_MatricesAndMatrixOperations#Transpose of a matrix]] and [[MAT01B1_Notes_S20_MatricesAndMatrixOperations#Trace of a matrix]]).

### Binomial Theorem

$$(a+b)^n=\sum_{k=0}^n\binom nk a^{n-k}b^k$$

- Source: [[MAT01B1_Notes_S21_BinomialTheorem#The Binomial Theorem]]. A single term needs only the right $k$, not the full expansion (source: [[MAT01B1_Notes_S21_BinomialTheorem#Worked example: finding one coefficient without a full expansion]]).

## Worked example notebook

Earlier notebooks, not repeated here: [[MAT01B1_Summary_ST1#Worked example notebook]] and [[MAT01B1_Summary_ST2#Worked example notebook]]. Below, one example for each new principle.

### Free variable example

(source: [[MAT01B1_Notes_S19_GaussianElimination]], slide 20) $x+2y-z=5,\ -x-y+z=-2,\ 2x+y-2z=1$ reduces to rows $[1\ 2\ -1\ |\ 5]$, $[0\ 1\ 0\ |\ 3]$, $[0\ 0\ 0\ |\ 0]$. Column 3 has no leading 1, so $z=t$ is free, $y=3$ and $x=5-2y+z=t-1$.

### Product sizes and the column method

(source, S20 slide 14) $A$ is $3\times2$ and $B$ is $2\times2$: $AB$ is $3\times2$, and $BA$ is undefined. (source, S20 slides 19 and 20) For $A=\begin{bmatrix}3&0\\-1&5\end{bmatrix}$, $B=\begin{bmatrix}4&-2&1\\0&2&3\end{bmatrix}$, column 3 of $AB$ is $A\begin{bmatrix}1\\3\end{bmatrix}=\begin{bmatrix}3\\14\end{bmatrix}$ and row 2 is $\begin{bmatrix}-1&5\end{bmatrix}B=\begin{bmatrix}-4&12&14\end{bmatrix}$.

### Linear combination example

(source, S20 slide 23) $\begin{bmatrix}-1&3&2\\1&2&-3\\2&1&-2\end{bmatrix}\begin{bmatrix}2\\-1\\3\end{bmatrix}=2\begin{bmatrix}-1\\1\\2\end{bmatrix}-1\begin{bmatrix}3\\2\\1\end{bmatrix}+3\begin{bmatrix}2\\-3\\-2\end{bmatrix}=\begin{bmatrix}1\\-9\\-3\end{bmatrix}$.

### Binomial given term and sigma form

(source: [[MAT01B1_Notes_S21_BinomialTheorem]]) In $(2x^2-5y)^9$, the term with $x^8$ has $18-2k=8$, so $k=5$ and the coefficient is $\binom95 2^4(-5)^5=-6\,300\,000$.

(source: 2024 final, Question 9; working added) $\left(x+\tfrac1x\right)^5=\sum_{k=0}^5\dfrac{5!}{k!\,(5-k)!}x^{5-2k}$, since $x^{5-k}\cdot x^{-k}=x^{5-2k}$. The coefficient of $x^3$ needs $5-2k=3$, so $k=1$ and the coefficient is $5$.

### Polar slope example

(source: 2023 Exam C, Question 4b; working added) For $r=\dfrac{2}{1+\cos\theta}$, $r'=\dfrac{2\sin\theta}{(1+\cos\theta)^2}$. Then $\dfrac{dy}{dx}=\dfrac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}=\dfrac{2/(1+\cos\theta)}{-2\sin\theta/(1+\cos\theta)^2}=-\dfrac{1+\cos\theta}{\sin\theta}=-\cot\dfrac\theta2$.

### Volume and surface area examples from revision

(source: revision session) Region $y=x^3$, $y=0$, $x=2$ about $x=3$: washers $\pi\int_0^8\left[(3-\sqrt[3]y)^2-1\right]dy$ and shells $2\pi\int_0^2(3-x)x^3\,dx$ both give $\dfrac{56\pi}5$.

(source: revision session, ST2 Question 7b) Region $y=x^2$, $x=\tfrac12y$, $x=0$ about $y=5$ with shells in $dy$: $V=2\pi\int_0^4(5-y)\left(\sqrt y-\tfrac y2\right)dy=\dfrac{136\pi}{15}$.

(source: revision session) Arc length of $x=\tfrac23y^{3/2}$, $0\le y\le3$: $\dfrac{dx}{dy}=y^{1/2}$, $ds=\sqrt{1+y}\,dy$, $L=\tfrac23(1+y)^{3/2}\Big|_0^3=\dfrac{14}3$.

## What the tests showed

In your own words, as you reported them. Nothing here is inferred.

### ST2

- Mark: 66 percent. Average going into the final: 75 percent (source: handoff memo).
- Main cause of lost marks: ran out of time. Question 7 was nearly blank and the multiple choice was rushed (source: handoff memo).
- On four multiple choice questions "none of the above" was chosen when the correct option was listed (source: handoff memo).
- On the integration question: "i forgot how to integrate or so i thought i was under pressure so blanked" (your words, revision session).
- On time: "i cant keep track of time inside the exam room there is no clock", you only know "30 minutes before submission", and it happened on question 6 (your words, revision session).
- On speed and accuracy: "if i listen to you i wont finish in time if i prioritise time i make silly mistakes its really double edged" (your words, revision session).

### ST1

Your account of ST1 has not been supplied. Add it here: what appeared, what you got stuck on, what you would do differently.

## Common mistakes

Grouped by pattern. Orange items are still open after revision.

### Strips, radius and height

- <span style="color:#f08c00">Open: choosing the radius and the height in washers, shells and surface area.</span> Radius is the distance to the axis. Height is far end minus near end of the strip.
- Wrong: shells about a horizontal axis with $dx$. Right: a horizontal axis means horizontal strips for shells, so $dy$ and curves written as $x$ in terms of $y$.
- Wrong: treating a bound such as $x=2$ only as a limit. Right: when the region does not reach the axis, that gap is also the inner radius.
- Wrong: swapping outer and inner radius, which gives a negative volume. Right: test one value between the limits to see which curve is farther from the axis.
- Cone tank: $h=2$ for "2 m deep", not $h=4$ (source: handoff memo).

### Algebra and simplifying

- Fractions: multiply the numerator by the same factor as the denominator, then check with decimals.
- Leave nothing half simplified, for example $(\sqrt2)^3=2\sqrt2$ gives a single term.
- Substitution $u=\cos x$ has $du=-\sin x\,dx$, so a sign must not be dropped. $\int\sec^2y\,dy=\tan y$, not a logarithm.
- Polar angle: move it into the allowed range, for example $7\pi/4$, not $-\pi/4$.
- MVT for integrals: the last step is to solve $f(c)=f_{\text{ave}}$ for $c$, in the number world, not the angle world.
- Parametric concavity with $\ln t$: the domain is $t>0$, so restrict the interval.

### Multiple choice

- Never choose "none of the above" first. Simplify your own result into the form of each option, or test one value.
- Use the constraint to eliminate a variable before optimising (the box in ST2 1.1).
- Polar to Cartesian: multiply by $r$ when you see $\sin\theta$ or $\cos\theta$ (ST2 1.8).
- Parametric circle: check radius, then direction, then laps (ST2 1.9).
- Surface of revolution: check limits and which differential belongs with $ds$ (ST2 1.10).

### Trig integrals

- <span style="color:#f08c00">Open: sorting odd and even powers.</span> Even power of $\sec$: save $\sec^2x$ and use $u=\tan x$. Odd power of $\tan$ with a $\sec$: save $\sec x\tan x$ and use $u=\sec x$. Odd power of $\sin$ or $\cos$: save one factor and use the other as $u$.
- For $\int\tan x\sec^3x\,dx$ the substitution is $u=\sec x$, not $u=\tan x$.

### Linear systems and matrices

- <span style="color:#f08c00">Open: the free variable test.</span> A free variable is a column with no leading 1. A zero below a leading 1 does not make that variable free.
- Row 1 of $A$ is not row 1 of $AB$. Row 1 of $AB$ is row 1 of $A$ times all of $B$.
- <span style="color:#f08c00">Open: linear combinations.</span> The numbers in $\bar x$ are how many of each column to take.
- Product sizes: write the sizes of $A$ and $B$ in order and compare the inner pair.
- Source slips in the slides and two vault notes that repeat them: see [[MAT01B1_Summary_ST2#Common mistakes]].

## Decision aids

(added) Each aid below was built during revision from the notes and from your questions.

### Washer or shell

1. Sketch the region and draw one strip.
2. Strip perpendicular to the axis: washer. Strip parallel to the axis: shell.
3. Horizontal axis: washer uses $dx$, shell uses $dy$. Vertical axis: washer uses $dy$, shell uses $dx$.
4. If the question names a method, follow it and the strips follow.
5. Washer: $V=\pi\int(R^2-r^2)$, with radii measured to the axis. Shell: $V=2\pi\int(\text{radius})(\text{height})$, with no inner radius because the height already covers it.
6. Limits from the corners, found by setting the curves equal. A third boundary may only be a corner.
7. Both methods agree when both are possible. Use that as a check.

### Surface area, choosing r and ds

- $r$ is the distance from the point on the curve to the axis: $y$ for the $x$ axis, $x$ for the $y$ axis, $|y-k|$ for $y=k$, $|x-k|$ for $x=k$.
- $ds$: $\sqrt{1+(dy/dx)^2}\,dx$ for $y=f(x)$, $\sqrt{1+(dx/dy)^2}\,dy$ for $x=g(y)$, $\sqrt{(dx/dt)^2+(dy/dt)^2}\,dt$ for a parametric curve.
- Then $S=2\pi\int r\,ds$ with everything in one variable and limits for that variable.
- Example: $y=x^2$, $0\le x\le1$, has $r=x^2$ about the $x$ axis, $x$ about the $y$ axis, $x^2+1$ about $y=-1$ and $3-x$ about $x=3$ (source: revision session).

### Which variable and which differential

- Curve given as $y=\ldots$: use $dx$ with $x$ limits. Curve given as $x=\ldots$: use $dy$ with $y$ limits. Curve with $t$: use $dt$.
- Everything inside the integral must be in that one variable, and the limits must belong to it. You cannot integrate a $y$ expression with respect to $x$.
- Changing variable means changing the limits too.

### Trig integral sorting

1. Same family, such as $\sin$ with $\cos$ or $\tan$ with $\sec$: use the odd and even rules in Common mistakes.
2. Mixed families such as $\cot$ with $\sec$: rewrite everything in $\sin$ and $\cos$.
3. A bare $\sqrt{1+(\ldots)^2}$, or a power of $x$ times it: trig substitution with $\tan$.
4. An extra $x$ outside the root: ordinary $u$ substitution.
5. The awkward case, even $\tan$ with odd $\sec$ such as $\sec^3$: use the reduction formula.

$$\int\sec^n x\,dx=\frac{\sec^{n-2}x\tan x}{n-1}+\frac{n-2}{n-1}\int\sec^{n-2}x\,dx$$

$$\int\sec x\,dx=\ln|\sec x+\tan x|+C,\qquad \int\csc x\,dx=-\ln|\csc x+\cot x|+C$$

### Free variable test and reading a solution

1. In each row find the first nonzero entry. That column is a leading variable.
2. Columns that never get one are free. Name each with its own letter.
3. Solve the leading variables from the bottom row up, in terms of the letters.
4. Example: rows $[1\ 2\ 0\ |\ 3]$ and $[0\ 0\ 1\ |\ 5]$ have leading variables $x$ and $z$, so $y=t$ is free and $(x,y,z)=(3-2t,\ t,\ 5)$.
5. First line to write when a leading 1 is missing: "let the free variable equal $t$".

### Matrix pieces and sizes

- $AB$ exists when the inner sizes match, and has the outer sizes.
- Column $j$ of $AB$ is $A$ times column $j$ of $B$. Row $i$ of $AB$ is row $i$ of $A$ times $B$.
- $A\bar x=x_1(\text{col }1)+x_2(\text{col }2)+\cdots$. To write $\bar b$ as a linear combination of the columns of $A$, solve $A\bar x=\bar b$ and use the solution as the coefficients.
- Trace needs a square matrix. Transpose swaps the size.

### Binomial term finder

1. General term $\binom nk a^{n-k}b^k$.
2. A named term: the $(k+1)$th term has $b^k$.
3. A power of $x$ or the constant term: add the exponents of $x$ in $a^{n-k}$ and $b^k$, set equal to the target, solve for $k$. The result must be a whole number from $0$ to $n$.
4. Coefficients include the number parts of $a$ and $b$, with their signs.

### Multiple choice routine

1. Read all five options before working.
2. Work the question yourself, then simplify into the form of each option. If the constraint gives another unknown, use it to eliminate.
3. Never choose "none of the above" first.
4. Circle a stuck question and move on. Keep about 10 minutes at the end to recheck the multiple choice (source: handoff memo).

## Exam procedure

### Paper format, as far as the supplied papers show

- Question 1 is multiple choice, 10 to 12 marks in the finals supplied, options a to e with e "none of the above", answered by a cross in a grid.
- Written questions follow, from 2 marks up to about 14 marks each.
- The supplied papers' text does not give total marks or duration. The front page of your paper does.

### Questions that recur in the 15 supplied papers

All of the following are from the papers themselves (source: past papers). Counts are of the papers I found them in.

- Binomial expansion or a term of an expansion: 2018 supplementary, 2019, 2020 supplementary, 2023 A, 2023 B, 2023 C, 2024. The sigma form "show that" appears in 2023 A and 2024.
- Augmented matrix and Gaussian or Gauss Jordan elimination: 2019, 2020 supplementary, 2022 A, 2022 B, 2023 B, 2023 C, 2024. Writing $\bar b$ as a linear combination of the columns: 2023 B, 2023 C, 2024.
- Matrix calculations, trace and transpose: 2019, 2020 supplementary, 2022 C, 2023 A.
- Mean Value Theorem proof via Rolle: 2018 supplementary, 2023 A, 2024. Fermat's Theorem proof: 2022 A.
- Statements asked: Rolle (2018 supplementary, 2022 C), Fermat and MVT for integrals (2020 supplementary), EVT and MVT (2019), MVT for integrals (2022 A).
- Polar "show that" for the slope: 2023 A, B and C.
- Finding $c$ in the MVT for derivatives: 2019, 2023 C, 2024.

### In the paper

- Time check: you have no clock, so set a phone timer to ring at the 30 minutes left mark, if the invigilator allows a phone in the room. (plan agreed in revision, check the rule on phones before the paper)
- About one minute per mark. Circle and move on. (source: handoff memo)
- If you blank, write the first line of the theorem or the setup. Setup lines earn partial marks even if the finish slips. (plan agreed in revision)
- If the "30 minutes left" panic starts: breathe once, do the cheapest marks first, then write setups for the rest. (plan agreed in revision)
- Before handing in: limits changed with every substitution, signs, radius and height, and every multiple choice option checked against your own answer.

## Tips

- If a problem hands you a constraint and a quantity to optimise, the constraint exists to remove an unknown.
- A polar equation with $\sin\theta$ or $\cos\theta$: multiply by $r$, then use $x=r\cos\theta$, $y=r\sin\theta$, $r^2=x^2+y^2$ (source: revision session).
- In $ds=\sqrt{1+(dx/dy)^2}\,dy$ the $dx$ is not lost, it is inside the derivative. The differential outside the root is the one you integrate with (source: revision session).
- For a parametric circle, the standard cos and sin form runs counterclockwise. Swap them or negate one to reverse the direction, and multiply the angle to add laps (source: revision session).
- Simplify before you stop: a half simplified answer can lose a mark.

## See also

- [[MAT01B1_Proofs_Final]]
- [[MAT01B1_Summary_ST1]] and [[MAT01B1_Summary_ST2]]
