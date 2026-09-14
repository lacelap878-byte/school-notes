---
module: MAT01B1
topic: The Binomial Theorem
session: S19
tags: [theorem, formula, worked-example]
---

# The Binomial Theorem

Source: lecture notes, "The Binomial Theorem" (October 2023).

## Motivation: expanding $(a+b)^n$

A **binomial** is a two-term expression, e.g. $a+b$. Expanding successive powers by hand:

$$
(a+b)^0=1,\qquad(a+b)^1=a+b,\qquad(a+b)^2=a^2+2ab+b^2.
$$

$(a+b)^3$ follows by multiplying $(a+b)^2$ by $(a+b)$ and collecting terms:

$$
(a+b)^3=(a^2+2ab+b^2)(a+b)=a^3+2a^2b+ab^2+a^2b+2ab^2+b^3=a^3+3a^2b+3ab^2+b^3.
$$

## The pattern

Rewriting the first few expansions with every term shown as $a^{\text{power}}b^{\text{power}}$:

$$
(a+b)^1=a^1b^0+a^0b^1
$$
$$
(a+b)^2=a^2b^0+2a^1b^1+a^0b^2
$$
$$
(a+b)^3=a^3b^0+3a^2b^1+3a^1b^2+a^0b^3
$$
$$
(a+b)^4=a^4b^0+4a^3b^1+6a^2b^2+4a^1b^3+a^0b^4
$$

In every term of $(a+b)^n$, the exponents of $a$ and $b$ add up to $n$: if $a$'s exponent is $n-k$, $b$'s exponent is $k$. Starting from $a^n$ (all $a$, $k=0$) and ending at $b^n$ (all $b$, $k=n$), the exponent of $a$ decreases while the exponent of $b$ increases. Writing $C_k$ for the coefficient attached to the term $a^{n-k}b^k$,

$$
(a+b)^n=\sum_{k=0}^n C_k\,a^{n-k}b^k.
$$

The remaining question is how to find the coefficients $C_k$.

## Pascal's triangle

Listing just the coefficients from the expansions above:

$$
1
$$
$$
1\quad1
$$
$$
1\quad2\quad1
$$
$$
1\quad3\quad3\quad1
$$
$$
1\quad4\quad6\quad4\quad1
$$

This is **Pascal's triangle**. The edge entries in every row are $1$; any other entry is the sum of the two entries diagonally above it in the previous row (e.g. the second entry of row 3, $3$, is $1+2$ from row 2... more precisely, the second entry of the row for $n=3$, namely $3$, is the sum of the two entries above it, $1$ and $2$, from the row for $n=2$).

N.B Pascal's triangle works for any $n$, but building it row by row becomes impractical once $n$ is large, which is exactly the motivation for finding a direct formula for $C_k$ instead.

## Combinations give the coefficients

**Definition.** For a natural number $n$ and $0\le k\le n$,

$$
{}_nC_k=\frac{n!}{(n-k)!\,k!}.
$$

From this definition, ${}_nC_0={}_nC_n=1$ and ${}_nC_1={}_nC_{n-1}=n$.

**Checking against the known coefficients.** For $n=1$: ${}_1C_0=\dfrac{1!}{1!\,0!}=1$, ${}_1C_1=\dfrac{1!}{0!\,1!}=1$, matching $(a+b)^1=a+b$. For $n=2$: ${}_2C_0=1$, ${}_2C_1=\dfrac{2!}{1!\,1!}=2$, ${}_2C_2=1$, matching $(a+b)^2=a^2+2ab+b^2$. This pattern confirms $C_k={}_nC_k$.

## The Binomial Theorem

**Theorem.**

$$
(a+b)^n=\sum_{k=0}^n{}_nC_k\,a^{n-k}b^k.
$$

**Hypotheses**
- $n$ a natural number

**Alternative notation.** ${}_nC_k$ is also written $\dbinom nk$, giving the equivalent form

$$
(a+b)^n=\sum_{k=0}^n\binom nk a^{n-k}b^k.
$$

## Worked example: expanding $(a+b)^3$

$$
(a+b)^3=\sum_{k=0}^3{}_3C_k\,a^{3-k}b^k={}_3C_0a^3b^0+{}_3C_1a^2b^1+{}_3C_2a^1b^2+{}_3C_3a^0b^3=a^3+3a^2b+3ab^2+b^3.
$$

## Worked example: expanding $(2x-y)^5$

Here $a=2x$, $b=-y$, $n=5$:

$$
(2x-y)^5=\sum_{k=0}^5(2x)^{5-k}(-y)^k=32x^5-16x^4y+8x^3y^2-4x^2y^3+2xy^4-y^5.
$$

## Worked example: expanding $(2x-3)^4$, using $\binom nk$ notation

Here $a=2x$, $b=-3$:

$$
(2x-3)^4=\sum_{k=0}^4\binom4k(2x)^{4-k}(-3)^k=1\cdot16x^4+4\cdot8x^3(-3)+6\cdot4x^2\cdot9+4\cdot2x\cdot(-27)+1\cdot81,
$$

$$
=16x^4-96x^3+216x^2-216x+81.
$$

## Worked example: finding one coefficient without a full expansion

Find the coefficient $a$ in the term $ax^8y^5$ of the expansion of $(2x^2-5y)^9$.

By the Binomial Theorem, with $a=2x^2$, $b=-5y$, $n=9$:

$$
(2x^2-5y)^9=\sum_{k=0}^9\binom9k(2x^2)^{9-k}(-5y)^k=\sum_{k=0}^9\binom9k2^{9-k}x^{18-2k}(-5y)^k.
$$

The term wanted has $x^8$, so $18-2k=8\Rightarrow k=5$. The required term is

$$
\binom95 2^{9-5}x^8(-5y)^5=126\cdot16\cdot(-3125)\,x^8y^5,
$$

so $a=126\cdot16\cdot(-3125)=-6\,300\,000$.

N.B This is the payoff of having a direct formula rather than Pascal's triangle: picking out a single term needs only the value of $k$ that matches the wanted exponent, not the full expansion.

## Worked example: a binomial with fractional exponents

Expand $(3\sqrt t+\sqrt[4]t)^4$ (a plain square root in the first term, a fourth root in the second).

Since $\sqrt t=t^{1/2}=\left(t^{1/4}\right)^2=(\sqrt[4]t)^2$, the first term rewrites as $3\sqrt t=3(\sqrt[4]t)^2$, so

$$
3\sqrt t+\sqrt[4]t=3(\sqrt[4]t)^2+\sqrt[4]t=\sqrt[4]t\left(3\sqrt[4]t+1\right).
$$

Raising to the 4th power:

$$
(3\sqrt t+\sqrt[4]t)^4=\left[\sqrt[4]t\left(3\sqrt[4]t+1\right)\right]^4=\left(\sqrt[4]t\right)^4\left(3\sqrt[4]t+1\right)^4=t\left(3\sqrt[4]t+1\right)^4.
$$

Expanding $\left(3\sqrt[4]t+1\right)^4$ by the Binomial Theorem, with $X=3\sqrt[4]t$:

$$
t\sum_{k=0}^4\binom4kX^{4-k}=t\sum_{k=0}^4\binom4k3^{4-k}\left(\sqrt[4]t\right)^{4-k}.
$$

Working out each term with its binomial coefficient:

$$
=t\left[\binom40 3^4t+\binom413^3\sqrt[4]{t^3}+\binom423^2\sqrt[4]{t^2}+\binom433\sqrt[4]t+\binom441\right]
$$
$$
=t\left(81t+108\sqrt[4]{t^3}+54\sqrt[4]{t^2}+12\sqrt[4]t+1\right).
$$

(added, flagging a discrepancy) The source's own final line states this as $t(81t+27\sqrt[4]{t^3}+9\sqrt[4]{t^2}+3\sqrt[4]t+1)$, matching only the $k=0$ and $k=4$ terms ($81$ and $1$) and appearing to have dropped the binomial coefficients $\binom41=4$, $\binom42=6$, $\binom43=4$ from the three middle terms. Recomputing directly from the Binomial Theorem gives the coefficients $108,54,12$ shown above instead of the source's $27,9,3$. Worth checking against your lecturer's own working rather than taking either version on faith.

## See also
- No other session currently in this vault uses the Binomial Theorem; cross-links will be added if a later topic (e.g. binomial-series expansions) calls back to it.
