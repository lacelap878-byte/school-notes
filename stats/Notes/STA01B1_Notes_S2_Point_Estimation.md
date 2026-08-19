---
module: STA01B1
topic: Point Estimation
session: S2
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Point Estimation (Devore & Berk, Ch 6)

A point estimate answers "what single number should I report for this unknown population parameter." Everything in this note is about how to build that number, and how to judge whether the method used to build it is any good.

## Point estimate and point estimator

### Definition (page 248)
```
A point estimate of a population parameter is a single number that can
be regarded as a sensible value for the population parameter.
A point estimate is obtained by selecting a suitable statistic and
computing its value from the given sample data.
The selected statistic is called the point estimator of the parameter
(and indicated as such using "^").
```

### General parameter notation
The Greek letter $\theta$ is used as a placeholder for whatever parameter is of interest ($\mu$, $\sigma^2$, $p$, etc). Its estimator is written $\hat\theta$.

> [!note] Reading $\hat\theta$ and $\sigma_{\hat\theta}$ correctly (added)
> $\theta$ is not a function being evaluated, it is just a name for the unknown number. A hat appears on a quantity specifically when an unknown parameter inside its formula has been replaced by an estimator or an estimate, this is the hat propagation rule: $\hat\theta$ is the estimator of $\theta$, and later $\sigma_{\hat\theta}$ means "the standard deviation of $\hat\theta$", not $\sigma$ treated as a function taking $\theta$ as input. Keep the subscript reading as a possessive, not an argument.

In the best possible world an estimator would satisfy $\hat\theta = \theta$ always, but $\hat\theta$ is a function of the sample $X_i$'s, so it is a random variable (defined in: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]). For some samples $\hat\theta$ overestimates $\theta$, for others it underestimates it.

> [!note] $\hat{p}$ is $\bar{X}$ in disguise (added)
> If each $X_i$ is an indicator variable, 1 if the trial shows the outcome of interest, 0 otherwise, then $\hat{p} = X/n$ is literally the sample mean of those indicators. Proportions and means are not two separate ideas here, a proportion is just what the sample mean becomes when the underlying variable is binary. Everything already established for $\bar{X}$ (unbiasedness, standard error) carries over to $\hat{p}$ for that reason.

**Example 6.1 (source, slide 3)**
25 controlled bumper crashes, $X$ = number resulting in no visible damage. Parameter $p$ = proportion of crashes with no damage. Observed $x = 15$.
$$\text{estimator } \hat{p} = \frac{X}{n} \qquad \text{estimate} = \frac{x}{n} = \frac{15}{25} = .60$$

**Example 6.2 (source, slide 4)**
20 dielectric breakdown voltage observations, assumed normal with mean $\mu$ (also the median, since normal is symmetric). Four different estimators of the same $\mu$, applied to the same data ($\sum x_i = 555.86$):

| Estimator | Estimate |
|---|---|
| a. $\bar{X}$ | $\bar{x} = 555.86/20 = 27.793$ |
| b. $[\min(X_i)+\max(X_i)]/2$ | $(27.94+27.98)/2 = 27.960$ |
| c. sample median | $(27.94+27.98)/2 = 27.960$ |
| d. 10% trimmed mean $\bar{X}_{tr(10)}$ | $(555.86-24.46-25.61-29.50-30.88)/16 = 27.838$ |

N.B four different, individually reasonable estimators applied to the same data give four different numbers. Choosing between them is exactly the problem the rest of this note solves.

**Example, similar to 6.3 (source, slides 5 to 6)**
Eight rat lifetimes on a restricted diet: 716, 1144, 1017, 1138, 389, 1221, 530, 958. Estimating population variance $\sigma^2$ with the sample variance:
$$\hat\sigma^2 = S^2 = \frac{\sum X_i^2 - \left(\sum X_i\right)^2/n}{n-1}$$
$$\hat\sigma^2 = s^2 = \frac{6{,}991{,}551 - (7113)^2/8}{7} = \frac{667{,}205}{7} = 95{,}315, \qquad \hat\sigma = s = \sqrt{95{,}315} = 309$$
Using divisor $n$ instead of $n-1$ (the average squared deviation) on the same data gives $\hat\sigma^2 = 667{,}205/8 = 83{,}401$, a different answer from the same data. The next section explains why the divisor-$n$ version is the one to avoid.

## Unbiased estimators

### Definition (page 251)
```
A point estimator is said to be an unbiased estimator if

E(theta hat) = theta

for every possible value of the parameter. If the point estimator is
not unbiased, the difference

E(theta hat) - theta

is called the bias of the estimator.
```

> [!warning] "Bias" is a technical gap, not a judgment (common mistake)
> Statistical bias means the average value of the estimator, across every sample that could be drawn, misses the true parameter by a fixed amount. It has nothing to do with favoring a particular group or outcome, it is a mathematical property of a formula.

### Proposition (page 252)
When $X$ is a binomial rv with parameters $n$ and $p$, the sample proportion
$$\hat{p} = \frac{X}{n}$$
is an unbiased estimator of $p$.

### Proposition (page 253)
$$S^2 = \frac{1}{n-1}\left(\sum X_i^2 - \frac{\left(\sum X_i\right)^2}{n}\right)$$
is an unbiased estimator of $\sigma^2$.

**BUT:**
$$\hat\sigma^2 = \frac{1}{n}\left(\sum X_i^2 - \frac{\left(\sum X_i\right)^2}{n}\right)$$
is a **biased** estimator of $\sigma^2$.

> [!example] Why the divisor-$n$ version is biased, worked in full (added)
> The divisor-$n$ estimator relates to $S^2$ by $\hat\sigma^2 = \dfrac{n-1}{n}S^2$. Since $E(S^2) = \sigma^2$ (the proposition above),
> $$E(\hat\sigma^2) = \frac{n-1}{n}E(S^2) = \frac{n-1}{n}\sigma^2$$
> $$\text{bias} = E(\hat\sigma^2) - \sigma^2 = \left(\frac{n-1}{n} - 1\right)\sigma^2 = -\frac{\sigma^2}{n}$$
> Reading this expression tells you everything without knowing $\sigma^2$'s numeric value: the negative sign means the divisor-$n$ estimator systematically *underestimates* $\sigma^2$ on average, and the $1/n$ factor means that underestimate shrinks toward zero as $n$ grows, the bias is worst for small samples and becomes negligible for large ones. This sign-and-$n$ reading is the general skill: the sign of a bias expression gives the direction of the systematic error, and how $n$ enters it gives the rate at which that error disappears as the sample grows.

### Proposition (page 254)
If $X_1, X_2, \ldots, X_n$ is a random sample from a distribution with mean $\mu$, then $\bar{X}$ is an unbiased estimator of $\mu$. If in addition the distribution is continuous and symmetric, then the median and any trimmed mean are also unbiased estimators of $\mu$.

N.B this is exactly why Example 6.2 above had multiple unbiased-looking candidates for the same $\mu$, unbiasedness alone doesn't pick a winner between them, the next section is what does.

## Minimum variance unbiased estimation

### Principle of MVU Estimation (page 256)
```
Among all estimators of theta that are unbiased, choose the one that
has minimum variance. The resulting estimator is called the minimum
variance unbiased estimator (MVUE) of theta.
```
$$\text{MSE} = \text{variance} + (\text{bias})^2$$
Since an unbiased estimator has bias 0, seeking an unbiased estimator with minimum variance is the same as seeking an unbiased estimator with minimum MSE.

> [!warning] "Accurate" hides two separate properties (common mistake)
> Casual language uses "accurate" for both of these at once, but they are different technical properties. Unbiasedness is about where the estimator's distribution is centered, on average it hits $\theta$. Precision (variance) is about how tightly that distribution is spread around its center. An estimator can be unbiased and imprecise, or biased and very precise. MVUE asks for both: unbiased first, then the tightest spread among the unbiased options.

### Theorem, MVUE for $\mu$ under normality (exam-flagged)
Let $X_1, X_2, \ldots, X_n$ be a random sample from a normal distribution with parameters $\mu$ and $\sigma$. Then the estimator
$$\hat\mu = \bar{X}$$
is the MVUE for $\mu$.

### Complications
The best estimator for $\mu$ depends on which distribution is being sampled:
1. If the sample comes from a normal distribution, the mean is the best of the four estimators seen in Example 6.2 (mean, median, trimmed mean, average of two extremes), since it has minimum variance among all unbiased estimators.
2. If the sample does not come from a normal distribution, the trimmed mean with a small trimming percentage works reasonably well in most situations, even with outliers present. It is called a robust estimator.

## The standard error

Besides reporting a point estimate, some indication of its precision should be given.

### Definition (page 259)
$$\sigma_{\hat\theta} = \sqrt{V(\hat\theta)}$$
The standard error of an estimator is its standard deviation.

If the standard error itself involves unknown parameters that can be estimated, substituting those estimates gives the **estimated standard error**:
$$\hat\sigma_{\hat\theta} = \sqrt{\hat{V}(\hat\theta)}$$

**Example 6.9 (source, slide 20)**
Breakdown voltage assumed normal, $\hat\mu = \bar{X}$ is the best estimator of $\mu$.
Known $\sigma = 1.5$: $\sigma_{\bar{X}} = \sigma/\sqrt{n} = 1.5/\sqrt{20} = .335$.
Unknown $\sigma$, estimated by $s = 1.462$: $\hat\sigma_{\bar{X}} = s/\sqrt{n} = 1.462/\sqrt{20} = .327$.

**Example 6.10 (source, slide 21)**
Standard error of $\hat{p} = X/n$:
$$\sigma_{\hat{p}} = \sqrt{V(X/n)} = \sqrt{\frac{V(X)}{n^2}} = \sqrt{\frac{npq}{n^2}} = \sqrt{\frac{pq}{n}}$$
Since $p$ and $q = 1-p$ are unknown (else why estimate?), substitute $\hat{p} = x/n$ and $\hat{q} = 1-x/n$: $\hat\sigma_{\hat{p}} = \sqrt{\hat{p}\hat{q}/n} = \sqrt{(.6)(.4)/25} = .098$. Alternatively, since $pq$ is largest when $p=q=.5$, an upper bound on the standard error is $\sqrt{1/(4n)} = .10$.

## Two more terminology traps (added)

> [!warning] "Prediction" is the wrong word here (common mistake)
> Point estimation concerns a parameter that already exists but is unknown, $\mu$, $\sigma^2$, $p$ are all fixed facts about a population that sampling has not revealed yet. "Prediction" wrongly implies a future, not-yet-determined event. An estimate is a best guess at something that is already true, not a forecast of something that hasn't happened.

> [!note] Probability mode vs statistics mode (added)
> Deriving and proving properties like unbiasedness (e.g. showing $E(\bar{X}) = \mu$) is done in probability mode: the parameter is fixed but unknown, and the estimator is treated as the random variable being reasoned about in general, before any data exists. Plugging real numbers into a formula to report $\hat{p} = .60$ or $s = 309$ is statistics mode: a single fixed number computed from one particular sample. Sampling distribution theory (see: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]) is the hybrid that makes this work at all, it borrows probability tools ($E$, $V$) to evaluate statistical tools (estimators) before they're ever applied to real data.

> [!note] Biased estimators still get used (added)
> Unbiasedness is not a strict requirement for every estimator seen in practice. Maximum likelihood estimators are sometimes biased but still widely used; in large samples the bias of an estimator like the divisor-$n$ variance formula becomes negligible anyway; and some computational contexts trade a small bias for other advantages (simplicity, stability). Unbiased is the default preference here, not an absolute rule.

## Do not forget

- $\hat\theta$ is the estimator (random variable, built from the sample); the reported number computed from actual data is the estimate.
- A hat appears wherever an unknown parameter has been replaced by an estimate, including inside standard error formulas.
- Bias $= E(\hat\theta) - \theta$. Sign gives direction of the systematic error, how $n$ enters gives how fast it shrinks.
- $S^2$ with divisor $n-1$ is unbiased for $\sigma^2$; the divisor-$n$ version is biased, with bias $-\sigma^2/n$.
- MVUE = unbiased first, then minimum variance among the unbiased options. Normal population: $\bar{X}$ wins. Non-normal: a small-trim trimmed mean is the robust choice.
- $\hat{p}$ is just $\bar{X}$ for 0/1 data, nothing new needed to handle it separately.
- Standard error is a standard deviation of an estimator; if that formula contains unknown parameters, substituting estimates gives the *estimated* standard error, a different (hatted) quantity.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — sampling distribution concept and the probability/statistics distinction this session builds directly on.
