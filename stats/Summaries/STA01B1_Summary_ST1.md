---
module: STA01B1
topic: Revision Summary
test: ST1
range: S1 to S5
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# STA01B1 Summary (ST1, sessions S1 to S5)

Fast-review pass over the whole ST1 range, from sampling distributions through hypothesis testing. Every result is stated in a sentence or two and linked back to its session note for the full treatment, and every derivation lives in [[STA01B1_Proofs_ST1]] rather than being repeated here.

## Material covered
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]
- [[STA01B1_Notes_S2_Point_Estimation]]
- [[STA01B1_Notes_S3_Statistical_Intervals]]
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]]
- [[STA01B1_Notes_S5_Hypothesis_Testing]]
- [[STA01B1_Proofs_ST1]] (all derivations for this range)

## Condensed concept pass

The five sessions are one continuous argument. Sampling distribution theory says a statistic computed from a sample is itself a random variable with its own distribution. Point estimation asks which single number to report for an unknown parameter and how to judge the method that produced it. Interval estimation wraps that number in a range with a stated confidence level. Small-sample normal theory rebuilds those intervals when the large-sample justification fails. Hypothesis testing turns the same machinery toward deciding whether the data contradicts a specific claimed value. One thread runs through all of it: the sampling distribution of $\bar{X}$, and what happens once the unknown $\sigma$ has to be replaced by $S$.

### From probability to a sampling distribution (S1)

A statistic is any quantity computed from the sample, and because the sample is random before it is collected, the statistic is a random variable with a distribution called its sampling distribution. This is not a new kind of object, it is an ordinary probability distribution applied to a statistic, and it stays a full distribution for every $n$, narrowing but never collapsing to a point. For any population, $E(\bar{X}) = \mu$ and $V(\bar{X}) = \sigma^2/n$, and for the total $E(T_o) = n\mu$, $V(T_o) = n\sigma^2$. If the population is itself normal, then $\bar{X} \sim N(\mu, \sigma^2/n)$ exactly for any $n$. If it is not, the Central Limit Theorem makes $\bar{X}$ approximately normal once $n$ is large, where "large" means $n \ge 30$ only when the population is skewed and no minimum at all when it is already normal. (see: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]])

### Building and judging a point estimate (S2)

A point estimator $\hat{\theta}$ is the rule (a random variable built from the sample), the estimate is the number it produces on real data. An estimator is unbiased when $E(\hat{\theta}) = \theta$, meaning it is centered on the truth on average, and bias is the technical gap $E(\hat{\theta}) - \theta$, not a value judgment. The sample variance $S^2$ with divisor $n-1$ is unbiased for $\sigma^2$, while the divisor-$n$ version carries bias $-\sigma^2/n$ and underestimates on average. Unbiasedness alone does not pick a winner, so the MVUE criterion adds a second demand: among unbiased estimators, take the one with minimum variance, which for a normal population is $\bar{X}$. The standard error is the estimator's own standard deviation, and if its formula contains unknown parameters, substituting estimates gives the estimated standard error. A proportion needs nothing new, since $\hat{p} = X/n$ is just $\bar{X}$ of 0/1 indicators. (see: [[STA01B1_Notes_S2_Point_Estimation]])

### Wrapping the estimate in an interval (S3)

A confidence interval replaces the single number with a range of plausible values carrying a stated confidence level. With a normal population and known $\sigma$, the interval is $\bar{x} \pm z_{\alpha/2}\,\sigma/\sqrt{n}$, and the confidence level describes the long-run success rate of the procedure, not a probability about the one interval already computed. The critical value $z_{\alpha/2}$ is read at cumulative area $1 - \alpha/2$. When $\sigma$ is unknown but $n$ is large, $S$ replaces $\sigma$ and the same $z$ interval holds, now needing $n > 40$ because the substitution adds variability. A proportion follows the same pattern, $\hat{p} \pm z_{\alpha/2}\sqrt{\hat{p}\hat{q}/n}$. Sample-size planning inverts the half-width: solve $n = (z_{\alpha/2}\sigma/E)^2$ for a mean, or $n = z_{\alpha/2}^2\hat{p}\hat{q}/E^2$ for a proportion, using $\hat{p} = 0.5$ as the worst case when no prior estimate exists. One-sided bounds put all of $\alpha$ in one tail with $z_\alpha$, giving a tighter bound than the matching side of a two-sided interval. (see: [[STA01B1_Notes_S3_Statistical_Intervals]])

### When the sample is small and the population is normal (S4)

The large-sample interval leans on the CLT, which needs $n$ large, so for small $n$ that justification disappears and the population is instead assumed normal outright. The pivot $T = (\bar{X} - \mu)/(S/\sqrt{n})$ then follows a $t$ distribution with $n-1$ degrees of freedom exactly, and the CI becomes $\bar{x} \pm t_{\alpha/2,n-1}\,s/\sqrt{n}$. The $t$ curve is wider than $z$ precisely because $S$ replacing $\sigma$ adds uncertainty, the same reason the large-sample threshold rose from $30$ to $40$, and it converges to $z$ as $n$ grows. A prediction interval, which targets one new observation rather than the mean, is wider still, carrying $\sqrt{1 + 1/n}$ instead of $\sqrt{1/n}$. A confidence interval for $\sigma^2$ uses the chi-squared pivot $(n-1)S^2/\sigma^2$ and is asymmetric, so the larger critical value produces the lower endpoint. (see: [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]])

### Testing a claim rather than estimating (S5)

Hypothesis testing sets up two contradictory claims, the null $H_0$ assumed true until contradicted and the alternative $H_a$, and the only outcomes are reject $H_0$ or fail to reject $H_0$, never prove it true. A Type I error rejects a true $H_0$ with probability $\alpha$, a Type II error fails to reject a false $H_0$ with probability $\beta$, and $\beta$ is not a single number since it depends on which alternative value is true. Shrinking the rejection region lowers $\alpha$ but raises $\beta$, so the two trade off directly for fixed $n$. For a composite null the worst-case $\alpha$ sits at the boundary value. The test statistic $Z = (\bar{X} - \mu_0)/(\sigma/\sqrt{n})$ handles a normal population with known $\sigma$ (Case I, any $n$), and substituting $S$ handles unknown $\sigma$ with $n > 30$ (Case II), with the rejection region set by whether $H_a$ points up, down, or both ways. (see: [[STA01B1_Notes_S5_Hypothesis_Testing]])

## Worked example notebook

One representative example per principle, in minimal form, each labelled with its source slide. Full working is in the linked session notes.

- CLT applied to a mean (source, S1 slide 29). Impurity $\mu = 4.0$, $\sigma = 1.5$, $n = 50$, so $\bar{X} \approx N(4.0, 0.2121^2)$ and $P(3.5 \le \bar{X} \le 3.8) \approx 0.1645$.
- Standardising a total (source, S1 slide 19). Normal population, $n = 5$, $\mu_{T_o} = 7.5$, $\sigma_{T_o} = 0.783$, giving $P(6 \le T_o \le 8) = 0.7115$.
- Point estimate of a proportion (source, S2 slide 3). $15$ of $25$ crashes undamaged, $\hat{p} = 15/25 = 0.60$.
- Sample variance (source, S2 slides 5 to 6). Eight rat lifetimes give $s^2 = 95315$ with divisor $n-1$, versus $83401$ with divisor $n$ on the same data.
- Estimated standard error of a proportion (source, S2 slide 21). $\hat{p} = 0.6$, $n = 25$, so $\sqrt{(0.6)(0.4)/25} = 0.098$.
- CI for the mean, known $\sigma$ (source, S3 slide 14). $\sigma = 13$, $n = 40$, $\bar{x} = 70.7$, at 90 percent gives $70.7 \pm 3.4 = (67.3, 74.1)$.
- Sample size for a mean (source, S3 slide 16). $\sigma = 25$, width at most $10$ at 95 percent gives $n = 97$.
- Large-sample CI, unknown $\sigma$ (source, S3 slide 19). $n = 50$, $\bar{x} = 19.82$, $s = 4.50$ gives $19.82 \pm 1.25 = (18.6, 21.1)$.
- One-sample $t$ interval (source, S4 slides 7 to 9). $n = 16$, $\bar{x} = 5.34$, $s = 0.8483$, $t_{.025,15} = 2.131$ gives $5.34 \pm 0.45 = (4.89, 5.79)$.
- Prediction interval (source, S4 slide 14). $n = 10$, $\bar{x} = 21.90$, $s = 4.134$ gives $21.90 \pm 9.81 = (12.09, 31.71)$, far wider than the CI on the same data.
- CI for the variance (source, S4 slides 17 to 18). $n = 16$, $s^2 = 0.7196$, $\chi^2_{.025,15} = 27.488$, $\chi^2_{.975,15} = 6.262$ gives $(0.393, 1.724)$ for $\sigma^2$.
- Two-tailed test, known $\sigma$ (source, S5 Example 8.6). $\mu_0 = 130$, $\sigma = 1.5$, $n = 9$, $\bar{x} = 131.08$ gives $z = 2.16$, inside $\pm 2.58$, so fail to reject at $\alpha = 0.01$.
- Upper-tailed large-sample test (source, S5 Example 8.8). $\mu_0 = 15$, $n = 70$, $\bar{x} = 17.99$, $s = 5.937$ gives $z = 4.21 \ge 1.645$, so reject $H_0$.
- Type I and Type II errors (source, S5 Example 8.5). Paint drying, cutoff $c = 70.8$ gives $\alpha = 0.01$ but $\beta(72) = 0.7486$, moving to $c = 72$ gives $\alpha \approx 0.05$ and $\beta(72) = 0.5$, showing the trade-off.

## Common mistakes

Patterns pulled from the struggle and warning callouts across the five notes.

- Treating a sampling-distribution statistic as already standard normal. It has its own mean and standard deviation, standardise first before using a $Z$ table. (see: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]])
- Imagining the sampling distribution collapses to $\mu$ as $n$ grows. It stays a full distribution for every finite $n$, only its variance $\sigma^2/n$ shrinks.
- Reading "bias" as a value judgment. It is the technical gap $E(\hat{\theta}) - \theta$, a property of a formula.
- Letting "accurate" hide two properties. Unbiasedness is where the distribution is centered, precision is how tightly it is spread, an estimator can have one without the other.
- Calling the confidence level a probability about the one computed interval. It is the long-run coverage of the procedure. (see: [[STA01B1_Notes_S3_Statistical_Intervals]])
- Looking up $z_{\alpha/2}$ at the wrong area. Use cumulative $1 - \alpha/2$, not $1 - \alpha$ and not $\alpha$.
- Confusing "within" and "width" in sample-size problems. "Within" is $E$ directly, "width" is $2E$, so halve it first.
- Reading $\hat{p} = 0.5$ as a claim about the true $p$. It is the worst-case choice that maximises the required $n$.
- Mixing up a PI and a CI. A CI estimates $\mu$, a PI predicts one new observation and is always wider. (see: [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]])
- Placing the chi-squared critical values on the wrong endpoints. The larger value makes the lower endpoint.
- Reading "fail to reject" as "proven true." It only means the evidence was not strong enough to reject. (see: [[STA01B1_Notes_S5_Hypothesis_Testing]])
- Expecting a single $\beta$. There is one $\beta$ per alternative value, and $\alpha$ and $\beta$ trade off against each other.

## Tips

- Sample-size question dissection. Identify what is being solved for (usually $n$), extract the error of estimation $E$ (watching within versus width), convert the confidence level to $z_{\alpha/2}$, then pick the spread estimate: a given $\sigma$ or $\hat{p}$, the range rule $\sigma \approx \text{range}/4$ when nothing exists yet, or $\hat{p} = 0.5$ for a bound irrespective of $p$. (see: [[STA01B1_Notes_S3_Statistical_Intervals]])
- Reading a bias expression. The sign gives the direction of the systematic error, and the way $n$ enters gives how fast the error vanishes as the sample grows. (see: [[STA01B1_Notes_S2_Point_Estimation]])
- Range rule versus CLT. The range rule guesses the population spread before any data exists, the CLT describes the shape of the sampling distribution of $\bar{X}$, they answer different questions and must not be swapped.
- Hat propagation. A hat appears wherever an unknown parameter inside a formula has been replaced by an estimate, including inside a standard error, so $\hat{\sigma}_{\hat{\theta}}$ is a different (estimated) quantity from $\sigma_{\hat{\theta}}$.
- Probability mode versus statistics mode. Proving a property like $E(\bar{X}) = \mu$ treats the estimator as a random variable before any data, computing $\hat{p} = 0.60$ reports one fixed number from one sample.
- CI and test duality (added). A two-sided level-$\alpha$ test of $H_0: \mu = \mu_0$ rejects exactly when $\mu_0$ falls outside the $100(1-\alpha)\%$ confidence interval for $\mu$. The interval is the set of null values the data would not reject, which is why the same critical value $z_{\alpha/2}$ drives both. (see: [[STA01B1_Notes_S5_Hypothesis_Testing]])

## See also
- [[STA01B1_Proofs_ST1]]
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]
- [[STA01B1_Notes_S2_Point_Estimation]]
- [[STA01B1_Notes_S3_Statistical_Intervals]]
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]]
- [[STA01B1_Notes_S5_Hypothesis_Testing]]
