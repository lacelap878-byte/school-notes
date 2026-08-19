---
module: STA01B1
topic: Statistics and Sampling Distributions
session: S1
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Statistics and Sampling Distributions (Devore & Berk, Ch 6)

> [!note] Where this sits (added)
> Probability starts from a known model and asks what data it should produce. Statistics runs the other way: the truth is unknown, and a real sample of data is used to infer it. Sampling distribution theory is the bridge between the two, it takes a rule from probability (a distribution has a mean and variance) and applies it not to a single observation, but to a quantity computed from a whole sample.

## Statistic and sampling distribution

Before a sample is collected, each observation is uncertain. Once collected, a sample of size $n$ is written $x_1, x_2, \ldots, x_n$ (lowercase, fixed numbers). Before collection, the same sample is written $X_1, X_2, \ldots, X_n$ (uppercase, random variables), because until the data exists there is no way to know what values will result. Any function computed from the sample, the mean, the standard deviation, the fourth spread, therefore also varies from sample to sample.

**Example (source, slides 5 to 6)**
Material strength from a Weibull population has $\mu = 4.4311$, $\sigma = 2.316$. Six independent samples of size 10 were drawn from this same population. Their sample means came out as 4.401, 5.928, 4.229, 4.132, 3.620, 6.342, no two the same, none equal to $\mu$. This is the entire point of the chapter: the population parameters are fixed, but any statistic computed from a sample is itself a random quantity.

### Statistic (defined in: this note)
```
A statistic is any quantity whose value can be calculated from sample data.
Prior to obtaining data, there is uncertainty as to what value of any
particular statistic will result. Therefore, a statistic is a random
variable and will be denoted by an uppercase letter; a lowercase letter
is used to represent the calculated or observed value of the statistic.
```

**Notation**

| | Statistic | Calculated value |
|---|---|---|
| Sample mean | $\bar{X}$ | $\bar{x}$ |
| Sample standard deviation | $S$ | $s$ |

### Sampling distribution
```
Any statistic, being a random variable, has a probability distribution.
The probability distribution of a statistic is sometimes referred to as
its sampling distribution to emphasize that it describes how the
statistic varies in value across all samples that might be selected.
```

> [!warning] Probability distribution vs sampling distribution (struggle)
> A probability distribution is the general concept: it describes how *any* random variable behaves, including a single observation $X_i$. A sampling distribution is not a separate kind of object, it is the same concept applied to a specific random variable, namely a statistic like $\bar{X}$ or $T_o$ built out of an entire sample.
>
> The confusion usually comes from imagining that as $n$ grows, the sampling distribution "collapses" to the true value $\mu$, as if it stopped being a distribution. It does not. $\bar{X}$ is a random variable for every $n$, and it keeps a full distribution with a mean and a variance no matter how large the sample gets. What happens is that the variance $\sigma^2/n$ shrinks as $n$ grows, so the distribution gets narrower and more concentrated around $\mu$, but it never becomes a single point for any finite $n$. The population parameters $\mu, \sigma^2$ are fixed and unknown; the sample statistics $\bar{x}, s^2$ are one number each, computed from one realised sample; the sampling distribution of $\bar{X}$ sits between the two, it is the full distribution of the statistic across every sample that could have been drawn.

## Random samples

### Definition (defined in: this note)
```
The rv's X1, X2, . . . , Xn are said to form a (simple) random sample of
size n if:
1. the Xi's are independent rv's
2. every Xi has the same probability distribution
```
Conditions 1 and 2 together are called independent and identically distributed (iid).

N.B If sampling is with replacement, or from an infinite population, both conditions hold exactly. If sampling is without replacement, they hold only approximately, and only when at most 5% of the population is sampled.

## Deriving the sampling distribution

Two ways to find a statistic's sampling distribution exist. Probability rules work directly when the statistic is a fairly simple function of the $X_i$'s and either the population has few distinct values or a distribution with a "nice" closed form. When the derivation by probability rules gets too difficult, a simulation experiment (almost always run on a computer) is used instead to approximate the same distribution numerically.

## Sampling distribution of the sample mean and sample total

### Proposition, general case
$$E(\bar{X}) = \mu_{\bar{X}} = \mu$$
$$V(\bar{X}) = \sigma^2_{\bar{X}} = \frac{\sigma^2}{n}$$
Holds for a random sample $X_1, \ldots, X_n$ from *any* distribution with mean $\mu$ and standard deviation $\sigma$, no normality needed here.

### Proposition, sample total
Let $T_o = X_1 + X_2 + \cdots + X_n$.
$$E(T_o) = n\mu$$
$$V(T_o) = n\sigma^2$$

(added) The sample total is not a rescaled sample mean chasing the same question. $\bar{X}$ answers "what does one unit typically look like", $T_o$ answers "what happens in aggregate across all $n$ units", the quantity that matters for capacity planning, total risk exposure, or total cost. $E(T_o)$ and $V(T_o)$ are the theoretical center and spread of that aggregate outcome, not an estimate of anything, they describe how $T_o$ behaves before any data exists.

**Example (source, slide 17)**
Days in shop for an American car: $\mu = 4.5$, $\sigma = 2$, sample of $n = 25$ cars.
$$E(\bar{X}) = \mu = 4.5, \qquad E(T_o) = n\mu = 25(4.5) = 112.5$$
$$\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}} = \frac{2}{\sqrt{25}} = .4, \qquad \sigma_{T_o} = \sqrt{n}\,\sigma = \sqrt{25}(2) = 10$$
N.B If $n$ increases to 100, $E(\bar{X})$ is unchanged, but $\sigma_{\bar{X}} = .2$, half its previous value, the sample size must quadruple to halve the standard deviation of $\bar{X}$.

### Proposition, population itself normal (exam-flagged)
Let $X_1, \ldots, X_n$ be a random sample from a **normal** distribution with mean $\mu$ and standard deviation $\sigma$. Then for **any** $n$:
$$\bar{X} \sim N\left(\mu, \frac{\sigma^2}{n}\right)$$
$$T_o \sim N(n\mu, n\sigma^2)$$

> [!warning] Not standard normal (common mistake)
> These are normal distributions with their own mean and variance, not the standard normal. Before reading a probability off a Z table, standardize first: subtract the mean of the statistic and divide by its own standard deviation, e.g. $Z = \dfrac{T_o - \mu_{T_o}}{\sigma_{T_o}}$. Plugging raw $\bar{x}$ or $t_o$ values straight into $\Phi(\cdot)$ is the single most common slip here.

**Example (source, slide 19)**
Rat maze time, normal population, $\mu = 1.5$ min, $\sigma = .35$ min, sample of 5 rats.

$T_o$ has $\mu_{T_o} = n\mu = 5(1.5) = 7.5$ and $\sigma^2_{T_o} = n\sigma^2 = 5(.1225) = .6125$, so $\sigma_{T_o} = .783$.
$$P(6 \le T_o \le 8) = P\left(\frac{6-7.5}{.783} \le Z \le \frac{8-7.5}{.783}\right) = P(-1.92 \le Z \le .64) = \Phi(.64) - \Phi(-1.92) = .7115$$

For $\bar{X}$: $\mu_{\bar{X}} = 1.5$, $\sigma_{\bar{X}} = \sigma/\sqrt{n} = .35/\sqrt{5} = .1565$.
$$P(\bar{X} \le 2.0) = P\left(Z \le \frac{2.0-1.5}{.1565}\right) = P(Z \le 3.19) = \Phi(3.19) = .9993$$

-> What happens when the population is *not* normal is the open question the slides leave hanging here, and it leads straight into the Central Limit Theorem below.

## Galton Board (aside, mechanism behind the CLT)

A Galton board (bean machine) is a pinboard that drops balls through rows of pegs, each peg bounces the ball left or right, and the balls collect at the bottom in a bell shaped pile. It was described by Francis Galton in *Natural Inheritance* (1889); the board pictured in the source slides was built at Princeton in 1981.

If a ball bounces right $k$ times over $n$ rows, it lands in the $k$th bin from the left. The number of distinct paths to that bin is $\binom{n}{k}$, and if the probability of bouncing right on any peg is $p$ (0.5 on an unbiased board):
$$\binom{n}{k}p^k(1-p)^{n-k}$$
which is the binomial pmf. The normal curve approximates this binomial distribution once $n$ (the number of peg rows) is large.

> [!example] Why the middle fills up faster than the edges (added)
> Counting binomial outcomes by hand for small $n$ shows the mechanism directly. The ratio of the center count to the outer edge count (from Pascal's triangle) grows fast: 2 at $n=2$, 3 at $n=3$, 6 at $n=4$, up to 252 at $n=10$. There are simply far more distinct left/right paths that land near the middle than paths that land at either extreme, and that imbalance is what piles the mass toward the center as $n$ grows, the same mechanism the CLT formalises below.

## The Central Limit Theorem (exam-flagged)

Let $X_1, X_2, \ldots, X_n$ be a random sample from a non-normal distribution with mean $\mu$ and standard deviation $\sigma$. Then, when $n$ is sufficiently large, $\bar{X}$ has approximately a normal distribution with
$$\mu_{\bar{X}} = \mu$$
$$\sigma^2_{\bar{X}} = \frac{\sigma^2}{n}$$

Equivalently, when $n$ is sufficiently large, $T_o$ has approximately a normal distribution with
$$\mu_{T_o} = n\mu$$
$$\sigma^2_{T_o} = n\sigma^2$$

> [!note] Scope of this statement (added)
> The Galton board only demonstrates the binary, binomial special case (bounce left or right). The general CLT, that this same normal approximation holds for sums of iid variables from essentially any distribution, needs machinery beyond this course (characteristic functions, cumulants) to prove properly. Treat the board as an illustration of the mechanism, not a proof of the general theorem.

**Example (source, slide 29)**
Chemical impurity per batch: $\mu = 4.0$g, $\sigma = 1.5$g, 50 independent batches. $n = 50$ is large enough for the CLT rule of thumb. $\bar{X}$ approximately $N(\mu_{\bar{X}} = 4.0, \sigma_{\bar{X}} = 1.5/\sqrt{50} = .2121)$.
$$P(3.5 \le \bar{X} \le 3.8) \approx \Phi(-.94) - \Phi(-2.36) = .1645$$

**Example (source, slide 30)**
Major defects per car: $\mu = 3.2$, $\sigma = 2.4$, $n = 100$. $X_i$ is a discrete random variable here, but the CLT is not limited to continuous variables. The population is positively skewed, but the large sample size still gives $\bar{X}$ an approximately normal distribution, $\mu_{\bar{X}} = 3.2$, $\sigma_{\bar{X}} = .24$.
$$P(\bar{X} > 4) \approx P(Z > 3.33) = 1 - \Phi(3.33) = .0004$$

## How large is large? (exam-flagged)

```
If the population is normal, then the sampling distribution of the
sample mean will also be normal, no matter what the sample size.

When the sample population is skewed, the sample size must be at
least 30 before the sampling distribution of the sample mean becomes
approximately normal.
```

## Do not forget

- Statistic = random variable before data, fixed number after (uppercase vs lowercase).
- Sampling distribution is not a different category from probability distribution, it is a probability distribution applied to a statistic, and it stays a full distribution for every $n$, it never collapses to a point.
- $E(\bar{X}) = \mu$, $V(\bar{X}) = \sigma^2/n$ hold for any population. The $N(\mu, \sigma^2/n)$ result only holds exactly if the population itself is normal.
- Always standardize a sampling-distribution statistic before using a Z table.
- CLT rule of thumb: $n \ge 30$ needed only when the population is skewed; a normal population needs no minimum $n$.

## See also
First note for this module, no linked notes yet.
