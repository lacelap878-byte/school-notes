---
module: MAT01B1
topic: Introduction to Systems of Linear Equations
session: S16
tags: [definition, formula, worked-example]
---

# Introduction to Systems of Linear Equations

Source: Dr K, §1.1 Introduction to systems of linear equations (slides 1 to 29), University of Johannesburg.

## Linear equations

**Definition.** A linear equation in the $n$ variables $x_1,x_2,\dots,x_n$ is

$$
a_1x_1+a_2x_2+\cdots+a_nx_n=b,
$$

where $a_1,\dots,a_n,b$ are constants and not all the $a$'s are zero. In two or three variables (written without subscripts), this is $a_1x+a_2y=b$ (a line, $a_1,a_2$ not both $0$) or $a_1x+a_2y+a_3z=b$ (a plane, $a_1,a_2,a_3$ not all $0$).

**Definition.** A **homogeneous** linear equation is one with $b=0$: $a_1x_1+\cdots+a_nx_n=0$.

## Worked example: identifying linear equations (source, slide 6)

Which of the following are linear in $x,y,z,w,x_1,x_2,x_3$?

| Equation | Linear? |
|---|---|
| $x-3y+4z-17w=6$ | Linear |
| $\sin x+7y=6$ | Not linear (trig function of a variable) |
| $xy+6z=4$ | Not linear (product of two variables) |
| $-3x^2+y=0$ | Not linear (squared variable) |
| $5x_3+4x_1-x_2=1$ | Linear |
| $\pi x_1-x_2=6$ | Linear ($\pi$ is just a constant coefficient) |

## Systems of linear equations

**Definition.** A **system of linear equations** (or **linear system**) is a finite collection of linear equations; the variables are called **unknowns**. A system of $m$ equations in $n$ unknowns $x_1,\dots,x_n$ has the general form

$$
\begin{aligned}
a_{11}x_1+a_{12}x_2+\cdots+a_{1n}x_n&=b_1\\
a_{21}x_1+a_{22}x_2+\cdots+a_{2n}x_n&=b_2\\
&\;\;\vdots\\
a_{m1}x_1+a_{m2}x_2+\cdots+a_{mn}x_n&=b_m.
\end{aligned}
$$

## Solutions

**Definition.** A **solution** of a linear system in $n$ unknowns is a sequence of $n$ numbers $s_1,\dots,s_n$ such that substituting $x_1=s_1,\dots,x_n=s_n$ makes every equation true, written as the **ordered $n$-tuple** $(s_1,\dots,s_n)$ (ordered pair if $n=2$, ordered triple if $n=3$). A system is **consistent** if it has at least one solution, **inconsistent** if it has none.

## Geometric picture: two and three unknowns

For a system of two equations in two unknowns, each equation graphs as a line, and a solution is a point where the lines meet. There are only three possibilities: the lines are parallel and distinct (**no solution**), the lines meet at exactly one point (**exactly one solution**), or the lines coincide (**infinitely many solutions**, every point on the common line).

The same three-way split holds for three equations in three unknowns, now with planes instead of lines: no solution, exactly one solution, or infinitely many solutions (where all three planes meet).

## Worked example: the three cases (source, slides 15 to 17)

1. $x+y=1,\ 2x-y=11$: exactly one solution, $(x,y)=(4,-3)$.
2. $x+y=4,\ 3x+3y=6$: no solution (tripling the first equation would give $3x+3y=12$, contradicting $3x+3y=6$).
3. $4x-2y=1,\ 16x-8y=4$: infinitely many solutions (the second equation is exactly $4\times$ the first, so they're the same line).

## Augmented matrices

**Definition.** The system above abbreviates to the **augmented matrix**

$$
\left[\begin{array}{cccc|c}
a_{11}&a_{12}&\cdots&a_{1n}&b_1\\
a_{21}&a_{22}&\cdots&a_{2n}&b_2\\
\vdots&\vdots&&\vdots&\vdots\\
a_{m1}&a_{m2}&\cdots&a_{mn}&b_m
\end{array}\right].
$$

**Worked example (source, slide 19).** $x_1+x_2+2x_3=9,\ 2x_1+4x_2-3x_3=1,\ 3x_1+6x_2-5x_3=0$ has augmented matrix

$$
\left[\begin{array}{ccc|c}1&1&2&9\\2&4&-3&1\\3&6&-5&0\end{array}\right].
$$

## Elementary row operations

The basic method for solving a linear system is to perform algebraic operations on it that don't change the solution set, producing successively simpler equivalent systems. The three operations are: multiply an equation by a nonzero constant, interchange two equations, add a constant times one equation to another. Since the rows of the augmented matrix correspond exactly to the equations, these become:

**Definition.** The **elementary row operations** on a matrix are:
1. Multiply a row by a nonzero constant: $cR_i$ (e.g. $-3R_2$).
2. Interchange two rows: $R_i\leftrightarrow R_j$ (e.g. $R_1\leftrightarrow R_3$).
3. Add a constant times one row to another: $R_i+kR_j$ (e.g. $R_2+4R_1$).

$R_i$ denotes the $i$th row; in operation 3, the row being changed is written first.

## Worked example: solving by row operations (source, slides 23 to 26)

$x+y+2z=9,\ 2x+4y-3z=1,\ 3x+6y-5z=0$.

$$
\left[\begin{array}{ccc|c}1&1&2&9\\2&4&-3&1\\3&6&-5&0\end{array}\right]
\xrightarrow{R_2-2R_1}
\left[\begin{array}{ccc|c}1&1&2&9\\0&2&-7&-17\\3&6&-5&0\end{array}\right]
\xrightarrow{R_3-3R_1}
\left[\begin{array}{ccc|c}1&1&2&9\\0&2&-7&-17\\0&3&-11&-27\end{array}\right]
$$

$$
\xrightarrow{\frac12R_2}
\left[\begin{array}{ccc|c}1&1&2&9\\0&1&-\frac72&-\frac{17}2\\0&3&-11&-27\end{array}\right]
\xrightarrow{R_3-3R_2}
\left[\begin{array}{ccc|c}1&1&2&9\\0&1&-\frac72&-\frac{17}2\\0&0&-\frac12&-\frac32\end{array}\right]
$$

$$
\xrightarrow{-2R_3}
\left[\begin{array}{ccc|c}1&1&2&9\\0&1&-\frac72&-\frac{17}2\\0&0&1&3\end{array}\right]
\xrightarrow{R_1-R_2}
\left[\begin{array}{ccc|c}1&0&\frac{11}2&\frac{35}2\\0&1&-\frac72&-\frac{17}2\\0&0&1&3\end{array}\right]
$$

$$
\xrightarrow[R_2+\frac72R_3]{R_1-\frac{11}2R_3}
\left[\begin{array}{ccc|c}1&0&0&1\\0&1&0&2\\0&0&1&3\end{array}\right]
$$

The solution $x=1,\ y=2,\ z=3$ is now evident just by reading the matrix. N.B This last step, clearing out everything above each leading $1$, is exactly the extra work that turns row echelon form into the more powerful *reduced* row echelon form used throughout [[MAT01B1_Notes_S17_GaussianElimination]].

## Self-check (source, slides 27 to 28)

Concepts to know: linear equation, homogeneous linear equation, system of linear equations, solution of a linear system, consistent/inconsistent linear system, augmented matrix, elementary row operations.

Skills to have: determine whether an equation is linear; determine whether a given $n$-tuple is a solution; find the augmented matrix of a system (and vice versa); perform elementary row operations on a system and its augmented matrix; determine consistency; find the solution of a consistent system.

## Practice problems (source, slide 29)

Solve (answers as given in the source, no worked derivation shown there):

(a) $x+3y+z=5,\ 2x+7y+2z=4,\ x+2y+2z=3$ $\Rightarrow (x,y,z)=(31,-6,-8)$

(b) $3y-z=4,\ x+3y+z=1,\ x+2z=4$ $\Rightarrow$ inconsistent

(c) $2x+4y-6z=2,\ -x-2y+3z=-1,\ x+y+z=3$ $\Rightarrow (x,y,z)=(5,-2,0)+t(-5,4,1)$

## See also
- [[MAT01B1_Notes_S17_GaussianElimination]]
- [[MAT01B1_Notes_S18_MatricesAndMatrixOperations]] (names the coefficient matrix $A$ and the vector form $A\bar x=\bar b$ for the systems introduced here)
