---
module: STA01A1
topic: Discrete Random Variables
session: S3
tags: [definition, formula, theorem, worked-example, added]
---

# STA01A1 Notes S3: Discrete Random Variables

Source: Lecture 6 (19 slides), Lecture 7 (9 slides), Lecture 8 (9 slides) and Lecture 11 (13 slides), slide numbers as printed; textbook Chapter 3 (sections 3.1 to 3.4 and 3.6). Short revision notes written from the slides, not from a teaching session.

Scope: SA1 covered random variables, the Bernoulli rv, pmf, cdf, expected value and variance. SA2 covered the binomial, Poisson and moment generating functions. The final took all of it, including all proofs; section 3.5 was left out.

Checked: every number below was recomputed in Python on 15 Nov 2026.

## Random variables (source, Lecture 6 slides 2 to 6)

> **Definition:** For a given sample space $S$ of some experiment, a random variable (rv) is any rule that associates a number with each outcome in $S$. In mathematical language, a random variable is a function whose domain is the sample space and whose range is the set of real numbers.

- Uppercase $X$ is the rv; lowercase $x$ is one of its values. $X(s) = x$ means $x$ is the value $X$ gives the outcome $s$.

> **Definition:** Any random variable whose only possible values are 0 and 1 is called a Bernoulli random variable.

> **Definition:** A discrete random variable is an rv whose possible values either constitute a finite set or else can be listed in an infinite sequence in which there is a first element, a second element, and so on.
> A random variable is continuous if both of the following apply:
> 1. Its set of possible values consists either of all numbers in a single interval on the number line (possibly infinite in extent, e.g., from $-\infty$ to $\infty$) or all numbers in a disjoint union of such intervals (e.g., $[0, 10] \cup [20, 30]$).
> 2. No possible value of the variable has positive probability, that is, $P(X = c) = 0$ for any possible value $c$.

## The pmf (source, Lecture 6 slides 7 to 9)

> **Definition:** The probability distribution or probability mass function (pmf) of a discrete rv is defined for every number $x$ by:

$$p(x) = P(X = x) = P(\text{all } s \in S : X(s) = x)$$

- We must have $p(x) \ge 0$ and $\sum p(x) = 1$.

> **Definition:** Suppose $p(x)$ depends on a quantity that can be assigned any one of a number of possible values, with each different value determining a different probability distribution. Such a quantity is called a parameter of the distribution. The collection of all probability distributions for different values of the parameter is called a family of probability distributions.

## The cdf (source, Lecture 6 slides 10 to 11)

> **Definition:** The cumulative distribution function (cdf) $F(x)$ of a discrete rv variable $X$ with pmf $p(x)$ is defined for every number $x$ by

$$F(x) = P(X \le x) = \sum_{y:\, y \le x} p(y)$$

> For any number $x$, $F(x)$ is the probability that the observed value of $X$ will be at most $x$.

> **Proposition:** For any two numbers $a$ and $b$ with $a \le b$, $P(a \le X \le b) = F(b) - F(a^-)$. For any two integers $a$ and $b$ with $a \le b$, $P(a \le X \le b) = F(b) - F(a - 1)$.

- (added) $a^-$ is the largest possible value of $X$ strictly less than $a$.
- (added) Drawing a discrete cdf: a step graph. It is 0 left of the smallest value, jumps up by $p(x)$ at each possible value, stays flat in between, and is 1 from the largest value on. Each step includes its left end (closed dot) and not its right end (open dot).

## Expected value and variance (source, Lecture 6 slides 12 to 18)

> Let $X$ be a discrete rv with set of possible values $D$ and pmf $p(x)$. The expected value or mean value of $X$, denoted by $E(X)$ or $\mu_X$ is

$$E(X) = \mu_X = \sum_{x \in D} x \cdot p(x) \quad \text{provided that } \sum_{x \in D} |x| \cdot p(x) < \infty$$

- Meaning: the value you would expect to observe on average if the experiment is repeated over and over again.

> **Proposition:** If the rv $X$ has a set of possible values $D$ and pmf $p(x)$, then the expected value of any function $h(X)$, denoted by $E[h(X)]$ or $\mu_{h(X)}$, is computed by

$$E[h(X)] = \sum_{D} h(x) \cdot p(x) \quad \text{assuming that } \sum_{D} |h(x)| \cdot p(x) < \infty$$

> **Definition:** Let $X$ have pmf $p(x)$ and expected value $\mu$. Then the variance of $X$, denoted by $V(X)$ or $\sigma_X^2$ is

$$V(X) = \sum_{D} (x - \mu)^2 \cdot p(x) = E\left[(X - \mu)^2\right]$$

The standard deviation is $\sigma_X = \sqrt{\sigma_X^2}$.

Three propositions, each marked PROOF! on the slides:

$$E(aX + b) = aE(X) + b$$

$$V(X) = \left[\sum_{D} x^2 \cdot p(x)\right] - \mu^2 = E(X^2) - [E(X)]^2$$

$$V(aX + b) = \sigma^2_{aX+b} = a^2 \cdot \sigma_X^2 \qquad \sigma_{aX+b} = |a| \cdot \sigma_X$$

Proofs (added):
1. $\sum (ax + b)p(x) = a\sum x\,p(x) + b\sum p(x) = aE(X) + b$, since $\sum p(x) = 1$.
2. Expand: $\sum (x - \mu)^2 p(x) = \sum x^2 p(x) - 2\mu \sum x\,p(x) + \mu^2 \sum p(x) = E(X^2) - 2\mu^2 + \mu^2$.
3. The mean of $aX + b$ is $a\mu + b$, so $(aX + b) - (a\mu + b) = a(X - \mu)$. Squaring gives $a^2(X - \mu)^2$, so $V(aX + b) = a^2 V(X)$.

Example (composite, pmf from Lecture 11 slide 4)
Quiz points $X$ have $p(0) = .1$, $p(1) = .2$, $p(2) = .3$, $p(3) = .4$. Find the cdf, $P(1 \le X \le 2)$, $E(X)$ and $V(X)$.

WORKING
$F(0) = .1$, $F(1) = .3$, $F(2) = .6$, $F(3) = 1$.
$P(1 \le X \le 2) = F(2) - F(0) = .6 - .1 = .5$.
$E(X) = 0 + .2 + .6 + 1.2 = 2$. $E(X^2) = 0 + .2 + 1.2 + 3.6 = 5$. $V(X) = 5 - 2^2 = 1$.

## Binomial distribution (source, Lecture 7 slides 2 to 8)

> **Definition:** An experiment satisfying the following 4 conditions, is called a Binomial experiment:
> - The experiment consists of a sequence of $n$ trials, where $n$ is fixed in advance of the experiment
> - Each trial can result in one of the same two possible outcomes (dichotomous trials), which we denote by success (S) or failure (F)
> - The trials are independent, so that the outcome on any particular trial does not influence the outcome on any other trial
> - The probability of success is constant from trial to trial; we denote this probability by $p$

> **Definition:** Given a binomial experiment consisting of $n$ trials, the binomial random variable $X$ associated with this experiment is defined as $X$ = the number of S's among the $n$ trials. We will write $X \sim \text{Bin}(n, p)$ to indicate that $X$ is a binomial rv based on $n$ trials with success probability $p$.

$$b(x; n, p) = \begin{cases} \dbinom{n}{x} p^x (1 - p)^{n - x} & x = 0, 1, 2, \ldots, n \\[1ex] 0 & \text{otherwise} \end{cases}$$

The cdf, which the binomial tables give:

$$P(X \le x) = B(x; n, p) = \sum_{y=0}^{x} b(y; n, p) \qquad x = 0, 1, \ldots, n$$

$$E(X) = np \qquad V(X) = np(1 - p) \qquad M_X(t) = (pe^t + 1 - p)^n$$

$n$ is the number of trials and $p$ the success probability. The mgf has no proof, only application. With $n = 1$ the binomial is the Bernoulli, with mean $p$.

Example (composite)
$X \sim \text{Bin}(10, 0.2)$. Write the pmf for this question, then find $P(X = 2)$, $P(X \ge 3)$ and $E(X)$.

WORKING
$p(x) = \binom{10}{x}(0.2)^x(0.8)^{10 - x}$ for $x = 0, 1, \ldots, 10$, and 0 otherwise.
$P(X = 2) = 45(0.04)(0.8)^8 = 0.302$. $P(X \ge 3) = 1 - B(2; 10, 0.2) = 1 - 0.678 = 0.322$.
$E(X) = 10(0.2) = 2$: over many sets of 10 trials, 2 successes on average.

## Poisson distribution (source, Lecture 8 slides 2 to 8, Lecture 11 slide 12)

> **Definition:** A random variable $X$ is said to have a Poisson distribution with parameter $\lambda$ ($\lambda > 0$) if the pmf of $X$ is:

$$p(x; \lambda) = \frac{e^{-\lambda}\lambda^x}{x!} \qquad x = 0, 1, 2, \ldots$$

The value of $\lambda$ is frequently a rate per unit time or per unit area.

$$E(X) = V(X) = \lambda \qquad M_X(t) = e^{\lambda(e^t - 1)}$$

The mean and variance carry a proof (NB on the slide); the mgf has no proof, only application.

Proof of $E(X) = V(X) = \lambda$ (added):
- $E(X) = \sum_{x=1}^{\infty} x\dfrac{e^{-\lambda}\lambda^x}{x!} = \lambda\sum_{x=1}^{\infty}\dfrac{e^{-\lambda}\lambda^{x-1}}{(x-1)!} = \lambda$, because the last sum is a whole Poisson pmf.
- In the same way $E[X(X - 1)] = \lambda^2$, so $E(X^2) = \lambda^2 + \lambda$ and $V(X) = \lambda^2 + \lambda - \lambda^2 = \lambda$.

> **Proposition:** Suppose that in the Binomial pmf $b(x; n, p)$ we let $n \to \infty$ and $p \to 0$ in such a way that $np$ approaches a value $\lambda > 0$. Then $b(x; n, p) \to p(x; \lambda)$.

- Rule of thumb: $n > 50$ and $np < 5$. No proof, only application. Example: $n = 100$, $p = 0.02$ gives $P(X = 1) = 0.2707$ exactly, and $e^{-2}(2) = 0.2707$ by Poisson.

Poisson process assumptions (pulses on a Geiger counter):
> 1. For a short interval of time, the probability of receiving a single pulse is approximately proportional to the length of the time interval
> 2. The probability of more than one pulse being received during the time interval is negligible
> 3. The number of pulses received during the time interval is independent of the number received prior to this time interval

$$P_k(t) = \frac{e^{-\alpha t}(\alpha t)^k}{k!} \qquad k = 0, 1, 2, \ldots$$

$\alpha$ is the rate of the process and $t$ the length of the interval, so the count is Poisson with $\lambda = \alpha t$ and the expected count is $\alpha t$. (The slide writes $x = 0, 1, 2, \ldots$ beside this formula; the variable is $k$.)

Example (composite): calls arrive at $\alpha = 2$ per minute. Find P(exactly 3 calls in 2 minutes).
   $\lambda = 2 \times 2 = 4$, so $e^{-4}4^3/3! = 0.195$.

## Moment generating functions (source, Lecture 11 slides 3 to 12)

> Expected values of powers of $X$ are called moments about 0. Expected values of powers of $(X - \mu)$ are called moments about the mean.

$$E(X) = \mu \qquad E\left[(X - \mu)^2\right] = V(X) \qquad \frac{E\left[(X - \mu)^3\right]}{\sigma^3} = \text{skewness}$$

> **Definition:** The moment generating function (mgf) of a discrete random variable $X$ is defined to be

$$M_X(t) = E\left(e^{tX}\right) = \sum_{x \in D} e^{tx}p(x)$$

> where $D$ is the set of possible values of $X$. The mgf exists if $M_X(t)$ is defined for an interval of numbers that includes 0, positive and negative numbers.

> **Proposition:** If the mgf exists and is the same for two distributions, then the two distributions are the same. That is, the moment generating function uniquely specifies the probability distribution; there is a one-to-one correspondence between distributions and mgf's.

> **Theorem:** If the mgf exists:

$$E(X^r) = M_X^{(r)}(0)$$

Proof for $r = 1$ and $r = 2$ (added): $M_X'(t) = \sum x e^{tx}p(x)$ and $M_X''(t) = \sum x^2 e^{tx}p(x)$. At $t = 0$, $e^0 = 1$, leaving $\sum x\,p(x) = E(X)$ and $\sum x^2 p(x) = E(X^2)$.

- Bernoulli with success probability $p$ (added, from the definition): $M_X(t) = (1 - p)e^{0} + pe^{t} = 1 - p + pe^t$. The slide's case $p(0) = \frac{1}{3}$, $p(1) = \frac{2}{3}$ gives $\frac{1}{3} + \frac{2}{3}e^t$.

Example (source, Lecture 11 slide 10)
Insurance claims $X$ have $p(0) = .7$, $p(1) = .2$, $p(2) = .1$ and mgf $M_X(t) = .7 + .2e^t + .1e^{2t}$. Use the mgf to find $E(X)$ and $V(X)$.

WORKING
$M_X'(t) = .2e^t + .2e^{2t}$, so $E(X) = M_X'(0) = .4$.
$M_X''(t) = .2e^t + .4e^{2t}$, so $E(X^2) = M_X''(0) = .6$.
$V(X) = .6 - .4^2 = .44$.

## Do not forget

- A binomial needs all four conditions: fixed $n$, two outcomes, independent trials, constant $p$.
- Poisson: mean and variance are both $\lambda$; in a process, $\lambda = \alpha t$ for the interval asked about.
- $V(aX + b) = a^2 V(X)$: the $b$ disappears and $a$ is squared.
- $E(X^r)$ is the $r$th derivative of the mgf at $t = 0$.

## See also

- [[STA01A1_Notes_S1_Describing_Data]]
- [[STA01A1_Notes_S2_Probability]]

---
*CDG v13 | written S3 | 2026-11-15*
