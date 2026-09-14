---
module: MAT01B1
topic: Matrices and Matrix Operations
session: S18
tags: [definition, theorem, formula, worked-example]
---

# Matrices and Matrix Operations

Source: Dr K, §1.3 Matrices and matrix operations, University of Johannesburg, cross-checked against the course's linear algebra textbook (Anton, *Elementary Linear Algebra*, §1.3), supplied by the lecturer.

## Matrix notation and terminology

**Definition.** A **matrix** is a rectangular array of numbers. The numbers in the array are its **entries**.

(added, from the textbook) Matrices don't only arise as augmented matrices for linear systems: any table of numbers organised into rows and columns is a matrix, for instance a table recording how many hours a student spent on each of three subjects across a week has one row per subject and one column per day.

**Definition.** The **size** of a matrix is $m\times n$ if it has $m$ rows and $n$ columns. A $1\times n$ matrix is a **row matrix** (or **row vector**); an $m\times1$ matrix is a **column matrix** (or **column vector**). Row and column vectors are denoted with a bar, e.g. $\bar a=\begin{bmatrix}1&2&3\end{bmatrix}$.

**Notation.** The entry of $A$ in row $i$, column $j$ is $a_{ij}$:

$$
A=\begin{bmatrix}a_{11}&a_{12}&\cdots&a_{1n}\\a_{21}&a_{22}&\cdots&a_{2n}\\\vdots&\vdots&\ddots&\vdots\\a_{m1}&a_{m2}&\cdots&a_{mn}\end{bmatrix},\qquad A=[a_{ij}]_{m\times n}=[a_{ij}],\qquad (A)_{ij}=a_{ij}.
$$

**Definition.** A **square matrix** is an $m\times n$ matrix with $m=n$. Its **main diagonal** consists of the entries $a_{11},a_{22},a_{33},\dots$. An **identity matrix** is a square matrix with $1$'s on the main diagonal and $0$'s everywhere else.

## Operations on matrices

**Definition (equality).** $A=[a_{ij}]_{m\times n}$ and $B=[b_{ij}]_{r\times s}$ are **equal** if and only if $m=r$, $n=s$, and $a_{ij}=b_{ij}$ for all $i,j$: same size, same entries in every position.

**Definition (sum and difference).** If $A,B$ have the same size, $A+B=[a_{ij}+b_{ij}]$ and $A-B=[a_{ij}-b_{ij}]$. Matrices of different sizes cannot be added or subtracted.

**Worked example (source, slide 8).** $A=\begin{bmatrix}2&1&0&3\\-1&0&2&4\\4&-2&7&0\end{bmatrix}$, $B=\begin{bmatrix}-4&3&5&1\\2&2&0&-1\\3&2&-4&5\end{bmatrix}$:

$$
A+B=\begin{bmatrix}-2&4&5&4\\1&2&2&3\\7&0&3&5\end{bmatrix},\qquad A-B=\begin{bmatrix}6&-2&-5&2\\-3&-2&2&5\\1&-4&11&-5\end{bmatrix}.
$$

**Worked example (source, slide 9).** With $A$ as above and $C=\begin{bmatrix}3&2\\1&6\end{bmatrix}$, is $C+A$ defined? (added, following directly from the definition) $C$ is $2\times2$ and $A$ is $3\times4$, different sizes, so $C+A$ is undefined.

**Definition (scalar multiple).** If $A=[a_{ij}]$ and $c$ is a scalar, $cA=[ca_{ij}]$. $(-1)B$ is written $-B$, the **negative** of $B$.

**Worked example (source, slide 10).** $A=\begin{bmatrix}2&3&4\\1&3&1\end{bmatrix}$, $B=\begin{bmatrix}0&2&7\\-1&3&-5\end{bmatrix}$: $2A=\begin{bmatrix}4&6&8\\2&6&2\end{bmatrix}$, $(-1)B=\begin{bmatrix}0&-2&-7\\1&-3&5\end{bmatrix}$.

## Worked example: addition and scalar multiplication exercises (source, slide 11)

$A=\begin{bmatrix}3&-1&0\\1&2&-4\end{bmatrix}$, $B=\begin{bmatrix}1&-1&1\\-2&0&6\end{bmatrix}$, $C=\begin{bmatrix}1&0&-2\\3&1&1\end{bmatrix}$: $A+B-C=\begin{bmatrix}3&-2&3\\-4&1&1\end{bmatrix}$.

Solve for $a,b,c,d,e,f$ if $A=\begin{bmatrix}3&-1&4\\2&0&6\end{bmatrix}$, $B=\begin{bmatrix}a&b&c\\d&e&f\end{bmatrix}$, $3A-2B=\begin{bmatrix}7&-7&14\\6&-6&14\end{bmatrix}$: $B=\begin{bmatrix}1&2&-1\\0&3&2\end{bmatrix}$.

**Unsolved practice (source, slide 12).** Let $B=\begin{bmatrix}1&-1\\-2&0\end{bmatrix}$, $C=\begin{bmatrix}2&0\\3&1\end{bmatrix}$. Solve for $A$ if $2A+B=I+C$ (no answer given in the source).

## Matrix multiplication

**Definition.** If $A$ is $m\times r$ and $B$ is $r\times n$, the **product** $AB$ is the $m\times n$ matrix with

$$
(AB)_{ij}=a_{i1}b_{1j}+a_{i2}b_{2j}+\cdots+a_{ir}b_{rj}.
$$

The number of columns of $A$ **must** equal the number of rows of $B$ for $AB$ to be defined.

**Worked example (source, slide 14).** $A=\begin{bmatrix}3&0\\-1&2\\1&1\end{bmatrix}$, $B=\begin{bmatrix}4&-1\\0&2\end{bmatrix}$: $AB=\begin{bmatrix}12&-3\\-4&5\\4&1\end{bmatrix}$; $BA$ is undefined ($B$ is $2\times2$, $A$ is $3\times2$, columns of $B\ne$ rows of $A$).

**Worked example (source, slide 15).**

1. $\begin{bmatrix}3&1\\5&2\end{bmatrix}\begin{bmatrix}2&-1\\-5&3\end{bmatrix}=\begin{bmatrix}1&0\\0&1\end{bmatrix}$
2. $\begin{bmatrix}5&0&-7\\1&5&9\end{bmatrix}\begin{bmatrix}3\\1\\-1\end{bmatrix}=\begin{bmatrix}22\\-1\end{bmatrix}$
3. $\begin{bmatrix}1&3&-3\end{bmatrix}\begin{bmatrix}3&0\\-2&1\\0&6\end{bmatrix}=\begin{bmatrix}-3&-15\end{bmatrix}$
4. $\begin{bmatrix}1\\1\\-3\end{bmatrix}\begin{bmatrix}4&0&1\end{bmatrix}=\begin{bmatrix}4&0&1\\4&0&1\\-12&0&-3\end{bmatrix}$
5. $\begin{bmatrix}4&0&1\end{bmatrix}\begin{bmatrix}1\\1\\-3\end{bmatrix}=\begin{bmatrix}1\end{bmatrix}$

## Transpose of a matrix

**Definition.** The **transpose** of an $m\times n$ matrix $A$ is the $n\times m$ matrix $A^T$ obtained by interchanging the rows and columns of $A$: the $i$th column of $A^T$ is the $i$th row of $A$. Equivalently, $(A^T)_{ij}=(A)_{ji}$, the subscripts reverse.

**Worked example (source, slide 16).** $A=\begin{bmatrix}2&1&0&3\\-1&0&2&4\\4&-2&7&0\end{bmatrix}$, $B=\begin{bmatrix}4&-2&1\\0&2&3\end{bmatrix}$, $C=\begin{bmatrix}3&5&2\end{bmatrix}$:

$$
A^T=\begin{bmatrix}2&-1&4\\1&0&-2\\0&2&7\\3&4&0\end{bmatrix},\qquad B^T=\begin{bmatrix}4&0\\-2&2\\1&3\end{bmatrix},\qquad C^T=\begin{bmatrix}3\\5\\2\end{bmatrix}.
$$

(added, from the textbook) For a square matrix, $A^T$ can also be pictured as "reflecting" $A$ about its main diagonal, swapping every pair of entries symmetric about that diagonal.

## Trace of a matrix

**Definition.** If $A$ is square, the **trace** of $A$, $\operatorname{tr}(A)$, is the sum of the entries on its main diagonal. The trace is undefined if $A$ isn't square.

**Worked example (source, slide 17).** $\operatorname{tr}\!\left(\begin{bmatrix}1&2&3\\4&5&6\\7&8&9\end{bmatrix}\right)=1+5+9=15.$

## Partitioned matrices

A matrix can be **partitioned** into smaller matrices, called **submatrices**, by inserting horizontal and vertical rules between selected rows and columns. A general $3\times4$ matrix $A$ can be partitioned, for example, into four submatrices $A_{11},A_{12},A_{21},A_{22}$, or into its three row vectors, or into its four column vectors:

$$
A=\begin{bmatrix}A_{11}&A_{12}\\A_{21}&A_{22}\end{bmatrix}=\begin{bmatrix}\bar r_1\\\bar r_2\\\bar r_3\end{bmatrix}=\begin{bmatrix}\bar c_1&\bar c_2&\bar c_3&\bar c_4\end{bmatrix}.
$$

## Matrix multiplication by columns and by rows

If $B=\begin{bmatrix}\bar b_1&\bar b_2&\cdots&\bar b_r\end{bmatrix}$ (partitioned into columns), then $AB=\begin{bmatrix}A\bar b_1&A\bar b_2&\cdots&A\bar b_r\end{bmatrix}$: the $j$th column of $AB$ is $A$ times the $j$th column of $B$. Similarly, if $A$ is partitioned into rows $\bar a_1,\dots,\bar a_m$, the $i$th row of $AB$ is $\bar a_iB$.

**Worked example (source, slides 19 to 20).** $A=\begin{bmatrix}3&0\\-1&5\end{bmatrix}$, $B=\begin{bmatrix}4&-2&1\\0&2&3\end{bmatrix}$, $AB=\begin{bmatrix}12&-6&3\\-4&12&14\end{bmatrix}$.

3rd column of $AB$: $A\begin{bmatrix}1\\3\end{bmatrix}=\begin{bmatrix}3&0\\-1&5\end{bmatrix}\begin{bmatrix}1\\3\end{bmatrix}=\begin{bmatrix}3\\14\end{bmatrix}$.

2nd row of $AB$: $\begin{bmatrix}-1&5\end{bmatrix}B=\begin{bmatrix}-1&5\end{bmatrix}\begin{bmatrix}4&-2&1\\0&2&3\end{bmatrix}=\begin{bmatrix}-4&12&14\end{bmatrix}$.

## Matrix products as linear combinations

**Definition.** If $A_1,\dots,A_r$ are matrices of the same size and $c_1,\dots,c_r$ are scalars, $c_1A_1+c_2A_2+\cdots+c_rA_r$ is a **linear combination** of $A_1,\dots,A_r$ with **coefficients** $c_1,\dots,c_r$.

**Worked example (source, slide 22).** $2\begin{bmatrix}1&1\\-1&2\end{bmatrix}-3\begin{bmatrix}-1&1\\-1&5\end{bmatrix}=\begin{bmatrix}5&-1\\1&-11\end{bmatrix}$, expressing $\begin{bmatrix}5&-1\\1&-11\end{bmatrix}$ as a linear combination of the other two.

**Theorem 1.3.1.** If $A$ is an $m\times n$ matrix and $\bar x$ is an $n\times1$ column vector, then $A\bar x$ can be expressed as a linear combination of the columns of $A$ in which the coefficients are the entries of $\bar x$.

**Hypotheses**
- $A$ is $m\times n$
- $\bar x$ is $n\times1$

**Derivation.**

$$
A\bar x=\begin{bmatrix}a_{11}&\cdots&a_{1n}\\\vdots&&\vdots\\a_{m1}&\cdots&a_{mn}\end{bmatrix}\begin{bmatrix}x_1\\\vdots\\x_n\end{bmatrix}=x_1\begin{bmatrix}a_{11}\\\vdots\\a_{m1}\end{bmatrix}+x_2\begin{bmatrix}a_{12}\\\vdots\\a_{m2}\end{bmatrix}+\cdots+x_n\begin{bmatrix}a_{1n}\\\vdots\\a_{mn}\end{bmatrix}.
$$

**Worked example (source, slide 23).** $\begin{bmatrix}-1&3&2\\1&2&-3\\2&1&-2\end{bmatrix}\begin{bmatrix}2\\-1\\3\end{bmatrix}=\begin{bmatrix}1\\-9\\-3\end{bmatrix}$, written as the linear combination $2\begin{bmatrix}-1\\1\\2\end{bmatrix}-1\begin{bmatrix}3\\2\\1\end{bmatrix}+3\begin{bmatrix}2\\-3\\-2\end{bmatrix}=\begin{bmatrix}1\\-9\\-3\end{bmatrix}$.

**Worked example: columns of $AB$ as linear combinations of the columns of $A$ (source, slide 24).** Reusing $AB=\begin{bmatrix}12&27&30&13\\8&-4&26&12\end{bmatrix}$ from the row-column multiplication example above, each column of $AB$ is the same linear combination of the columns of $A$ as the corresponding column of $B$ is of the standard basis, with coefficients read straight from that column of $B$:

$$
\begin{bmatrix}12\\8\end{bmatrix}=4\begin{bmatrix}1\\2\end{bmatrix}+0\begin{bmatrix}2\\6\end{bmatrix}+2\begin{bmatrix}4\\0\end{bmatrix},\quad
\begin{bmatrix}27\\-4\end{bmatrix}=1\begin{bmatrix}1\\2\end{bmatrix}-1\begin{bmatrix}2\\6\end{bmatrix}+7\begin{bmatrix}4\\0\end{bmatrix},
$$
$$
\begin{bmatrix}30\\26\end{bmatrix}=4\begin{bmatrix}1\\2\end{bmatrix}+3\begin{bmatrix}2\\6\end{bmatrix}+5\begin{bmatrix}4\\0\end{bmatrix},\quad
\begin{bmatrix}13\\12\end{bmatrix}=3\begin{bmatrix}1\\2\end{bmatrix}+1\begin{bmatrix}2\\6\end{bmatrix}+2\begin{bmatrix}4\\0\end{bmatrix}.
$$

## Matrix form of a linear system

A system of $m$ linear equations in $n$ unknowns can be written as the single matrix equation

$$
A\bar x=\bar b,
$$

where $A=[a_{ij}]$ is the **coefficient matrix**, $\bar x$ is the column of unknowns, and $\bar b$ is the column of constants. Adjoining $\bar b$ to $A$ as a final column recovers the [[MAT01B1_Notes_S16_IntroductionToLinearSystems#Augmented matrices|augmented matrix]] $[A\mid\bar b]$ already defined in S16, this section just names the coefficient matrix $A$ and the vector form $A\bar x=\bar b$ explicitly.

## Self-check (source, slides 26, 30)

Concepts to know: matrix, entries, column/row vector, square matrix, main diagonal, equal matrices, matrix operations (sum, difference, scalar multiplication), linear combination of matrices, product of matrices, partitioned matrices, submatrices, row-column/column/row methods, coefficient matrix of a linear system, transpose, trace.

Skills to have: determine the size of a matrix; identify its row and column vectors; perform matrix addition, subtraction, scalar multiplication, multiplication; determine whether a product is defined; compute a matrix product by the row-column, column, or row method; express $A\bar x$ as a linear combination of the columns of $A$; express a linear system as a matrix equation and identify its coefficient matrix; compute a transpose; compute a trace.

## Self-test, true or false (source: the textbook's end-of-section review, paraphrased, no answers given there either)

1. A matrix with equal numbers of rows and columns always has a main diagonal, even if it isn't literally square-shaped on the page.
2. An $m\times n$ matrix has $m$ column vectors and $n$ row vectors.
3. If $AB=BA$, then $A$ must equal $B$.
4. If $A\bar x=\bar b$, then $\bar b$ must be a linear combination of the columns of $A$.
5. For every matrix $A$, $(A^T)^T=A$.
6. If $A,B$ are square matrices of the same order, $\operatorname{tr}(AB)=\operatorname{tr}(A)\operatorname{tr}(B)$.
7. If $A,B$ are square matrices of the same order, $(AB)^T=A^TB^T$.
8. For every square matrix $A$, $\operatorname{tr}(A^T)=\operatorname{tr}(A)$.
9. If $A$ is $6\times4$ and $B$ is $m\times n$ with $B^TA^T$ a $2\times6$ matrix, then $m=4$, $n=2$.
10. If $A$ is $n\times n$ and $c$ is a scalar, $\operatorname{tr}(cA)=c\operatorname{tr}(A)$.
11. If $A,B,C$ are matrices of the same size with $A-C=B-C$, then $A=B$.
12. If $A,B,C$ are square matrices of the same order with $AC=BC$, then $A=B$.
13. If $AB+BA$ is defined, then $A$ and $B$ must be square matrices of the same size.
14. If $B$ has a column of zeros, then so does $AB$, whenever this product is defined.
15. If $B$ has a column of zeros, then so does $BA$, whenever this product is defined.

## See also
- [[MAT01B1_Notes_S16_IntroductionToLinearSystems]]
- [[MAT01B1_Notes_S17_GaussianElimination]]
