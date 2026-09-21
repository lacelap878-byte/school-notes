---
module: MAT01B1
topic: Gaussian Elimination
session: S19
tags: [definition, theorem, formula, worked-example]
---

# Gaussian Elimination

Source: Dr K, §1.2 Gaussian Elimination (slides 1 to 41), University of Johannesburg.

## Goal

Develop a systematic procedure, built entirely from [[MAT01B1_Notes_S18_IntroductionToLinearSystems#Elementary row operations|elementary row operations]], for reducing an augmented matrix so that the solution of the corresponding system can be read off by inspection.

## Row echelon form

**Definition.** A matrix is in **row echelon form** if:
1. In every row that isn't entirely zeros, the first nonzero number is a $1$ (a **leading 1**).
2. Rows consisting entirely of zeros are grouped at the bottom.
3. In any two consecutive non-zero rows, the leading $1$ of the lower row sits strictly further right than the leading $1$ of the row above it.

**Definition.** A matrix is in **reduced row echelon form** if, in addition, every column containing a leading $1$ has zeros everywhere else in that column.

N.B The point of the extra condition is purely practical: reduced row echelon form lets the solution be read straight off the matrix, without doing back-substitution, exactly the payoff seen at the end of [[MAT01B1_Notes_S18_IntroductionToLinearSystems#Worked example: solving by row operations (source, slides 23 to 26)|S18's worked example]].

## Worked example: classifying matrices (source, slide 7)

| Matrix | Classification |
|---|---|
| $\begin{bmatrix}7&0&1&0\\0&1&-1&4\\0&0&0&0\end{bmatrix}$ | Neither (leading entry in row 1 is $7$, not $1$) |
| $\begin{bmatrix}0&0&0\\0&0&0\\0&0&0\end{bmatrix}$ | Row echelon and reduced row echelon |
| $\begin{bmatrix}0&0&1\\0&1&0\\1&0&0\end{bmatrix}$ | Neither (leading $1$'s move left going down, not right) |
| $\begin{bmatrix}1&1&3&5\\0&0&1&-1\\0&0&0&1\\0&0&0&0\end{bmatrix}$ | Row echelon but not reduced |
| $\begin{bmatrix}1&0&1&0\\0&1&-1&4\\0&0&0&0\end{bmatrix}$ | Row echelon and reduced row echelon |

## Reading the solution off a reduced row echelon form

**Unique solution (source, slide 9).** If the augmented matrix in $x_1,x_2,x_3,x_4$ reduces to $\begin{bmatrix}1&0&0&0&|&3\\0&1&0&0&|&-1\\0&0&1&0&|&0\\0&0&0&1&|&5\end{bmatrix}$, the corresponding equations are just $x_1=3$, $x_2=-1$, $x_3=0$, $x_4=5$: a unique solution.

**Inconsistent (source, slide 10).** If the last row of a reduced augmented matrix reads $[0\ \ 0\ \ 0\ \ |\ \ 1]$, this corresponds to $0x+0y+0z=1$, which no values of $x,y,z$ can satisfy, so the system is inconsistent.

## Worked example: infinitely many solutions, one free variable (source, slides 11 to 13)

$\begin{bmatrix}1&0&3&|&-1\\0&1&-4&|&2\\0&0&0&|&0\end{bmatrix}$ in unknowns $x,y,z$. The last row, $0x+0y+0z=0$, imposes no restriction and can be dropped, leaving

$$
x+3z=-1,\qquad y-4z=2.
$$

$x$ and $y$ correspond to leading $1$'s and are the **leading variables**; $z$, left over, is the **free variable**. Solving the leading variables in terms of $z$:

$$
x=-1-3z,\qquad y=2+4z.
$$

Setting the free variable $z=t$ (an arbitrary parameter) gives the **parametric equations** of the solution set:

$$
x=-1-3t,\qquad y=2+4t,\qquad z=t.
$$

$t=0$ gives $(x,y,z)=(-1,2,0)$; $t=1$ gives $(-4,6,1)$; every choice of $t$ gives another point in the (infinite) solution set.

## Worked example: infinitely many solutions, two free variables (source, slides 14 to 15)

$\begin{bmatrix}1&-5&1&|&4\\0&0&0&|&0\\0&0&0&|&0\end{bmatrix}$ in $x,y,z$: the zero rows drop out, leaving the single equation $x-5y+z=4$, whose solution set is a plane in three-dimensional space. Solving for the leading variable $x$ in terms of the free variables $y,z$: $x=4+5y-z$. Setting $y=s$, $z=t$:

$$
x=4+5s-t,\qquad y=s,\qquad z=t.
$$

**Definition.** When a system has infinitely many solutions, a set of parametric equations that produces every solution by assigning numerical values to the parameters is called the **general solution**.

## Gaussian Elimination

**Method.**
1. Write the augmented matrix of the system.
2. Use elementary row operations to reduce it to row echelon form.
3. Solve by back-substitution.

## Worked example (source, slides 18 to 19)

$x-y+z=0,\ 3x+y+2z=2,\ -2x+y-z=1$.

$$
\left[\begin{array}{ccc|c}1&-1&1&0\\3&1&2&2\\-2&1&-1&1\end{array}\right]
\xrightarrow[R_3+2R_1]{R_2-3R_1}
\left[\begin{array}{ccc|c}1&-1&1&0\\0&4&-1&2\\0&-1&1&1\end{array}\right]
\xrightarrow{R_2\leftrightarrow R_3}
\left[\begin{array}{ccc|c}1&-1&1&0\\0&-1&1&1\\0&4&-1&2\end{array}\right]
$$

$$
\xrightarrow{R_3+4R_2}
\left[\begin{array}{ccc|c}1&-1&1&0\\0&-1&1&1\\0&0&3&6\end{array}\right]
\xrightarrow[\frac13R_3]{-R_2}
\left[\begin{array}{ccc|c}1&-1&1&0\\0&1&-1&-1\\0&0&1&2\end{array}\right]
$$

Reading off: $x-y+z=0$, $y-z=-1$, $z=2$. Back-substitution: $z=2$, $y=z-1=1$, $x=y-z=-1$.

## Worked example: a free variable in Gaussian elimination (source, slide 20)

$x+2y-z=5,\ -x-y+z=-2,\ 2x+y-2z=1$.

$$
\left[\begin{array}{ccc|c}1&2&-1&5\\-1&-1&1&-2\\2&1&-2&1\end{array}\right]
\xrightarrow{R_2+R_1}
\left[\begin{array}{ccc|c}1&2&-1&5\\0&1&0&3\\2&1&-2&1\end{array}\right]
\xrightarrow{R_3-2R_1}
\left[\begin{array}{ccc|c}1&2&-1&5\\0&1&0&3\\0&-3&0&-9\end{array}\right]
\xrightarrow{R_3+3R_2}
\left[\begin{array}{ccc|c}1&2&-1&5\\0&1&0&3\\0&0&0&0\end{array}\right]
$$

So $x+2y-z=5$, $y=3$, and the third row drops out ($z$ is free). With $z=t$: $y=3$, $x=5-2y+z=t-1$.

## Worked example: a messier reduction (source, slides 21 to 22)

$2y-z=-4,\ 2x-y+2z=7,\ -x+3y+z=-2$.

$$
\left[\begin{array}{ccc|c}0&2&-1&-4\\2&-1&2&7\\-1&3&1&-2\end{array}\right]
\xrightarrow{R_1\leftrightarrow R_3}
\left[\begin{array}{ccc|c}-1&3&1&-2\\2&-1&2&7\\0&2&-1&-4\end{array}\right]
\xrightarrow{R_2+2R_1}
\left[\begin{array}{ccc|c}-1&3&1&-2\\0&5&4&3\\0&2&-1&-4\end{array}\right]
$$

$$
\xrightarrow{R_3-\frac25R_2}
\left[\begin{array}{ccc|c}-1&3&1&-2\\0&5&4&3\\0&0&-\frac{13}5&-\frac{26}5\end{array}\right]
\xrightarrow[\frac15R_2,\,-\frac5{13}R_3]{-R_1}
\left[\begin{array}{ccc|c}1&-3&-1&2\\0&1&\frac45&\frac35\\0&0&1&2\end{array}\right]
$$

Reading off: $x-3y-z=2$, $y+\tfrac45z=\tfrac35$, $z=2$. Back-substitution: $z=2$, $y=\tfrac35-\tfrac45(2)=-1$, $x=2+3y+z=1$.

## Gauss-Jordan Elimination

**Method.**
1. Write the augmented matrix.
2. Perform Gaussian elimination to reach row echelon form.
3. Locate the rightmost leading $1$; add multiples of its row to the rows above to clear out everything above it.
4. Repeat with each leading $1$, working from the bottom of the matrix to the top.
5. Read the solution off directly, no back-substitution needed.

**Practical tips for row reduction (source, slide 24).** If any rows are entirely zeros, swap them to the bottom first. Find the leftmost column that isn't all zeros and, swapping rows if needed, make its top entry nonzero, this is the first leading entry (a leading $1$ is most convenient). Use it to clear out everything below it, then mentally cover that row and repeat on the remaining submatrix. Scale each row by a constant at the end so every leading entry is exactly $1$.

**Definition (recap).** Variables under a leading $1$'s column are **leading variables**; the rest are **free variables**, each needing its own parameter in the general solution.

Every system of linear equations has exactly zero, one, or infinitely many solutions, there are no other possibilities.

## Worked example: redoing the first Gaussian elimination example (source, slides 26 to 27)

Starting from the row echelon form already found above, $\begin{bmatrix}1&-1&1&|&0\\0&1&-1&|&-1\\0&0&1&|&2\end{bmatrix}$:

$$
\xrightarrow{R_2+R_3}
\left[\begin{array}{ccc|c}1&-1&1&0\\0&1&0&1\\0&0&1&2\end{array}\right]
\xrightarrow{R_1-R_3}
\left[\begin{array}{ccc|c}1&-1&0&-2\\0&1&0&1\\0&0&1&2\end{array}\right]
\xrightarrow{R_1+R_2}
\left[\begin{array}{ccc|c}1&0&0&-1\\0&1&0&1\\0&0&1&2\end{array}\right]
$$

$x=-1,\ y=1,\ z=2$, the same solution as by Gaussian elimination above, but read directly with no back-substitution needed.

## Worked example: redoing the free-variable example (source, slides 28 to 29)

Continuing the row echelon form $\begin{bmatrix}1&2&-1&|&5\\0&1&0&|&3\\0&0&0&|&0\end{bmatrix}$ found earlier:

$$
\xrightarrow{R_1-2R_2}
\left[\begin{array}{ccc|c}1&0&-1&-1\\0&1&0&3\\0&0&0&0\end{array}\right]
$$

$x-z=-1$, $y=3$; with $z=t$: $y=3$, $x=z-1=t-1$.

## Practice problems (source, slide 30)

Given (already reduced) augmented matrices in $x,y,z$, answers as given in the source:

(a) $\begin{bmatrix}1&0&0&|&-1\\0&1&0&|&4\\0&0&1&|&2\end{bmatrix}\Rightarrow(x,y,z)=(-1,4,2)$

(b) $\begin{bmatrix}1&2&1&|&6\\0&1&-1&|&1\\0&0&1&|&1\end{bmatrix}\Rightarrow(x,y,z)=(1,2,1)$

(c) $\begin{bmatrix}1&1&1&|&0\\0&1&-1&|&2\\0&0&0&|&0\end{bmatrix}\Rightarrow(x,y,z)=(-2,2,0)+t(-2,1,1)$

(d) $\begin{bmatrix}1&3&2&|&0\\0&1&1&|&4\\0&0&0&|&1\end{bmatrix}\Rightarrow$ no solution

## Homogeneous linear systems

**Definition.** A system of linear equations is **homogeneous** if every constant term is zero:

$$
a_{11}x_1+\cdots+a_{1n}x_n=0,\ \dots,\ a_{m1}x_1+\cdots+a_{mn}x_n=0.
$$

**Definition.** The solution that assigns $0$ to every variable is the **trivial solution**; any other solution is **nontrivial**. A homogeneous system always has the trivial solution, so there are only two possibilities: only the trivial solution, or infinitely many solutions in addition to it (never "no solution").

## Worked example: a homogeneous system with nontrivial solutions (source, slide 33)

$x+2y-z=0,\ -x-y+z=0$.

$$
\left[\begin{array}{ccc|c}1&2&-1&0\\-1&-1&1&0\end{array}\right]
\xrightarrow{R_2+R_1}
\left[\begin{array}{ccc|c}1&2&-1&0\\0&1&0&0\end{array}\right]
$$

$x+2y-z=0$, $y=0$; with $z=t$: $y=0$, $x=-2y+z=t$, a nontrivial family (every $t\ne0$ gives a nontrivial solution).

## Worked example: two free parameters (source, slide 34)

$x_1-x_2+2x_3-x_4=0,\ -x_1-x_2-x_3+2x_4=0,\ -x_1-3x_2+3x_4=0$, general solution (source states the result without showing the row reduction):

$$
(x_1,x_2,x_3,x_4)=s\left(-\tfrac32,\tfrac12,1,0\right)+t\left(\tfrac32,\tfrac12,0,1\right).
$$

N.B A homogeneous system stays homogeneous under elementary row operations, the constant column is always zero, so no operation can ever introduce a nonzero constant into it.

## Two theorems about homogeneous systems

**Theorem 1.2.1 (Free Variable Theorem for Homogeneous Systems).** If a homogeneous linear system has $n$ unknowns, and the reduced row echelon form of its augmented matrix has $r$ nonzero rows, then the system has $n-r$ free variables.

**Hypotheses**
- the system is homogeneous
- $n$ = number of unknowns, $r$ = number of nonzero rows in the reduced row echelon form

**Theorem 1.2.2.** A homogeneous linear system with more unknowns than equations has infinitely many solutions.

**Hypotheses**
- the system is homogeneous
- number of unknowns $>$ number of equations

## Worked example: nontrivial solutions by inspection (source, slide 36)

By Theorem 1.2.2, a homogeneous system with more unknowns than equations is guaranteed nontrivial solutions, no row reduction needed:

1. $2x_1-3x_2+4x_3-x_4=0,\ 7x_1+x_2-8x_3+9x_4=0,\ 2x_1+8x_2+x_3-x_4=0$: 4 unknowns, 3 equations $\Rightarrow$ nontrivial solutions.
2. $3x_1-2x_2=0,\ 6x_1-4x_2=0$: 2 unknowns, 2 equations, Theorem 1.2.2 doesn't directly apply by unknown-count alone here, but the two equations are proportional (the second is exactly twice the first), so they carry only one independent condition on two unknowns $\Rightarrow$ nontrivial solutions.

## Remarks on row echelon forms (source, slide 37)

The reduced row echelon form of a matrix is unique, there's only one. The (plain) row echelon form is *not* unique, different sequences of row operations can lead to different-looking row echelon forms. However, every row echelon form of a given matrix has the same number of zero rows and the same leading-1 positions (**pivot positions** or **pivot columns**), regardless of the path taken to get there.

## Extra exercises, unsolved (source, slides 38, 41)

No answers are given in the source for these, included here as practice rather than worked examples:

(a) If $A$ is a $4\times6$ matrix, what is the maximum possible number of leading $1$'s in its reduced row echelon form?

(b) If $B$ is a $4\times7$ matrix whose last column is all zeros, what is the maximum possible number of parameters in the general solution of the system with augmented matrix $B$?

(c) If $C$ is a $6\times3$ matrix, what is the minimum possible number of zero rows in any row echelon form of $C$?

(d) Find $a,b,c$ so that the graph of $p(x)=ax^2+bx+c$ passes through $(1,2)$, $(-1,6)$, and $(2,3)$.

(e) $2R_3-4R_1$ (changing row $3$) is *not* an elementary row operation. Explain why, and rewrite it as an equivalent sequence of elementary row operations.

(f) Find the value(s) of $k$ for which $x+ky=4,\ kx+9y=6$ has a unique solution.

(g) Find (if possible) conditions on $a,b,c$ such that $x+ay=0,\ y+bz=0,\ z+cx=0$ has no solution, one solution, or infinitely many solutions.

(h) Solve for $\alpha,\beta,\gamma$ (with $0\le\alpha\le2\pi$, $0\le\beta\le2\pi$, $0\le\gamma\le\pi$): $2\sin\alpha-\cos\beta+3\tan\gamma=3,\ 4\sin\alpha+2\cos\beta-2\tan\gamma=2,\ 6\sin\alpha-3\cos\beta+\tan\gamma=9$ (treat $\sin\alpha,\cos\beta,\tan\gamma$ as three linear unknowns first).

## Self-check (source, slides 39 to 40)

Concepts to know: reduced row echelon form, row echelon form, leading $1$, leading variables, free variables, general solution, Gaussian elimination, Gauss-Jordan elimination, forward phase, backward phase, augmented matrix, homogeneous linear system, trivial/non-trivial solution, back-substitution.

Skills to have: recognise row echelon form vs. reduced row echelon form vs. neither; construct solutions from an augmented matrix already in (reduced) row echelon form; use Gaussian elimination and Gauss-Jordan elimination to find the general solution of a system; analyse homogeneous systems using the Free Variable Theorem.

## See also
- [[MAT01B1_Notes_S18_IntroductionToLinearSystems]]
- [[MAT01B1_Notes_S20_MatricesAndMatrixOperations]] (matrix algebra: addition, multiplication, transpose, trace, on the same matrices row-reduced here)
