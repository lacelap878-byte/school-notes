---
module: STA01B1
topic: Proofs and Derivations
test: ST1
range: S1 to S5
tags: [theorem, formula, exam-flagged, added]
---

# STA01B1 Proofs (ST1, sessions S1 to S5)

Every derivation the ST1 range can test, collected for memorisation. Each heading names the result being proven. A line marked `(shown in source)` reproduces working that appears on the session page; a line marked `(added)` reconstructs a standard derivation of a result that the page only states, and links back to where it is stated. Results that cannot be derived at this course level are listed honestly at the end as statement only.

Standing notation for the whole file: $X_1, \ldots, X_n$ is a random sample (iid) with $E(X_i) = \mu$ and $V(X_i) = \sigma^2$. The sample mean is $\bar{X} = \frac{1}{n}\sum X_i$, the sample total is $T_o = \sum X_i$, and the sample variance is $S^2 = \frac{1}{n-1}\sum (X_i - \bar{X})^2$.

---

## 1. Mean and variance of the sample mean

Result: $E(\bar{X}) = \mu$ and $V(\bar{X}) = \dfrac{\sigma^2}{n}$. #formula #added

(added; result stated in [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] under "Sampling distribution of the sample mean and sample total".)

Mean, by linearity of expectation:
$$E(\bar{X}) = E\!\left(\frac{1}{n}\sum_{i=1}^{n} X_i\right) = \frac{1}{n}\sum_{i=1}^{n} E(X_i) = \frac{1}{n}\,(n\mu) = \mu$$

The constant $\frac{1}{n}$ leaves the expectation as a constant, and no independence is needed for the mean.

Variance:
$$V(\bar{X}) = V\!\left(\frac{1}{n}\sum_{i=1}^{n} X_i\right) = \frac{1}{n^2}\sum_{i=1}^{n} V(X_i) = \frac{1}{n^2}\,(n\sigma^2) = \frac{\sigma^2}{n}$$

N.B the constant $\frac{1}{n}$ comes out of a variance squared, as $\frac{1}{n^2}$, and the step $V(\sum X_i) = \sum V(X_i)$ needs independence (all covariances zero).

-> This proves $\bar{X}$ is unbiased for $\mu$, and gives its standard error $\sigma/\sqrt{n}$ used in section 7.

---

## 2. Mean and variance of the sample total

Result: $E(T_o) = n\mu$ and $V(T_o) = n\sigma^2$. #formula #added

(added; result stated in [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] under "Sampling distribution of the sample mean and sample total".)

$$E(T_o) = E\!\left(\sum_{i=1}^{n} X_i\right) = \sum_{i=1}^{n} E(X_i) = n\mu$$
$$V(T_o) = V\!\left(\sum_{i=1}^{n} X_i\right) = \sum_{i=1}^{n} V(X_i) = n\sigma^2 \qquad \text{(independence)}$$

Consistency check with section 1: since $\bar{X} = T_o/n$,
$$V(\bar{X}) = \frac{V(T_o)}{n^2} = \frac{n\sigma^2}{n^2} = \frac{\sigma^2}{n}$$

---

## 3. The sample proportion is unbiased for p

Result: for $X \sim \text{Bin}(n, p)$ and $\hat{p} = X/n$, $E(\hat{p}) = p$. #theorem #added

(added; proposition stated in [[STA01B1_Notes_S2_Point_Estimation]] under "Unbiased estimators".)

Using $E(X) = np$:
$$E(\hat{p}) = E\!\left(\frac{X}{n}\right) = \frac{1}{n}\,E(X) = \frac{np}{n} = p$$

N.B this is section 1 in disguise: if each $X_i$ is a 0/1 indicator (1 for the outcome of interest), then $\hat{p}$ is the sample mean of those indicators with $\mu = p$, so unbiasedness carries over for free. (see: [[STA01B1_Notes_S2_Point_Estimation]] note that $\hat{p}$ is $\bar{X}$ in disguise.)

---

## 4. The sample variance is unbiased for the population variance

Result: $E(S^2) = \sigma^2$. #theorem #exam-flagged #added

(added; proposition stated in [[STA01B1_Notes_S2_Point_Estimation]] under "Unbiased estimators", page 253. This is the central derivation of the ST1 range.)

Start from the numerator and split each deviation about $\bar{X}$ into a deviation about $\mu$ minus the error in $\bar{X}$:
$$\sum_{i=1}^{n} (X_i - \bar{X})^2 = \sum_{i=1}^{n} \big[(X_i - \mu) - (\bar{X} - \mu)\big]^2$$

Expand the square term by term:
$$= \sum_{i=1}^{n} (X_i - \mu)^2 \; - \; 2(\bar{X} - \mu)\sum_{i=1}^{n} (X_i - \mu) \; + \; \sum_{i=1}^{n} (\bar{X} - \mu)^2$$

Simplify the last two pieces. The final sum has no index $i$ inside it, so it equals $n(\bar{X} - \mu)^2$. In the middle piece,
$$\sum_{i=1}^{n} (X_i - \mu) = n\bar{X} - n\mu = n(\bar{X} - \mu)$$
so the middle piece is $-2(\bar{X} - \mu)\cdot n(\bar{X} - \mu) = -2n(\bar{X} - \mu)^2$. Combining the middle and last pieces, $-2n(\bar{X}-\mu)^2 + n(\bar{X}-\mu)^2 = -n(\bar{X}-\mu)^2$:
$$\sum_{i=1}^{n} (X_i - \bar{X})^2 = \sum_{i=1}^{n} (X_i - \mu)^2 - n(\bar{X} - \mu)^2$$

Now take expectations of both sides:
$$E\!\left[\sum_{i=1}^{n} (X_i - \bar{X})^2\right] = \sum_{i=1}^{n} E\big[(X_i - \mu)^2\big] - n\,E\big[(\bar{X} - \mu)^2\big]$$

Evaluate the two expectations. Since $E(X_i) = \mu$, $E[(X_i - \mu)^2] = V(X_i) = \sigma^2$, so the sum is $n\sigma^2$. Since $E(\bar{X}) = \mu$ from section 1, $E[(\bar{X} - \mu)^2] = V(\bar{X}) = \sigma^2/n$. Substitute:
$$= n\sigma^2 - n\cdot\frac{\sigma^2}{n} = n\sigma^2 - \sigma^2 = (n-1)\sigma^2$$

Divide by the $n-1$ in the definition of $S^2$:
$$E(S^2) = \frac{1}{n-1}\,E\!\left[\sum_{i=1}^{n} (X_i - \bar{X})^2\right] = \frac{1}{n-1}\,(n-1)\sigma^2 = \sigma^2$$

N.B the divisor $n-1$ is precisely what cancels the factor $(n-1)$ that the algebra produces, this is the whole reason the divisor is $n-1$ and not $n$.

(added, intuition) The deviations are measured from $\bar{X}$, not from the unknown $\mu$. Because $\sum (X_i - \bar{X}) = 0$ always holds, only $n-1$ of the $n$ deviations can vary freely, one degree of freedom is spent locating the center with $\bar{X}$. Dividing by that count of free deviations is what removes the bias.

-> Section 5 uses this result to show what happens when the divisor is $n$ instead.

---

## 5. The divisor-n variance estimator is biased

Result: $\hat{\sigma}^2 = \frac{1}{n}\sum (X_i - \bar{X})^2$ has $E(\hat{\sigma}^2) = \frac{n-1}{n}\sigma^2$, so bias $= -\dfrac{\sigma^2}{n}$. #theorem #exam-flagged

(shown in source: worked in full in [[STA01B1_Notes_S2_Point_Estimation]] under "Unbiased estimators".)

The two estimators share the same numerator and differ only in divisor, so
$$\hat{\sigma}^2 = \frac{n-1}{n}\,S^2$$

Take the expectation, using $E(S^2) = \sigma^2$ from section 4:
$$E(\hat{\sigma}^2) = \frac{n-1}{n}\,E(S^2) = \frac{n-1}{n}\,\sigma^2$$

The bias is the expected value minus the target:
$$\text{bias} = E(\hat{\sigma}^2) - \sigma^2 = \left(\frac{n-1}{n} - 1\right)\sigma^2 = -\frac{\sigma^2}{n}$$

Conclusions, read straight off the expression without any numeric value of $\sigma^2$:

- The sign is negative, so the divisor-$n$ estimator systematically underestimates $\sigma^2$ on average.
- The magnitude is $\sigma^2/n$, so the underestimate is worst for small $n$ and shrinks toward zero as $n$ grows. The estimator is asymptotically unbiased, and the two divisors agree for large samples.

(source, S2) On the eight rat lifetimes, divisor $n-1$ gives $s^2 = 95315$ while divisor $n$ gives $83401$ from the same data. The divisor-$n$ number is the smaller of the two, exactly the downward pull this bias predicts.

N.B general skill: the sign of a bias expression gives the direction of the systematic error, and the way $n$ enters gives the rate at which the error vanishes as the sample grows.

---

## 6. Mean squared error decomposition

Result: $\text{MSE}(\hat{\theta}) = V(\hat{\theta}) + [\text{bias}(\hat{\theta})]^2$. #theorem #added

(added; identity stated in [[STA01B1_Notes_S2_Point_Estimation]] under "Minimum variance unbiased estimation".)

Write $\mu_{\hat{\theta}} = E(\hat{\theta})$ and add and subtract it inside the squared error:
$$\text{MSE}(\hat{\theta}) = E\big[(\hat{\theta} - \theta)^2\big] = E\big[(\hat{\theta} - \mu_{\hat{\theta}}) + (\mu_{\hat{\theta}} - \theta)\big]^2$$

Expand the square:
$$= E\big[(\hat{\theta} - \mu_{\hat{\theta}})^2\big] + 2(\mu_{\hat{\theta}} - \theta)\,E\big[\hat{\theta} - \mu_{\hat{\theta}}\big] + (\mu_{\hat{\theta}} - \theta)^2$$

The quantity $\mu_{\hat{\theta}} - \theta$ is a constant (the bias), pulled outside the expectation. The middle expectation vanishes, $E[\hat{\theta} - \mu_{\hat{\theta}}] = E(\hat{\theta}) - \mu_{\hat{\theta}} = 0$. The first term is $V(\hat{\theta})$ by definition. So
$$\text{MSE}(\hat{\theta}) = V(\hat{\theta}) + (\mu_{\hat{\theta}} - \theta)^2 = V(\hat{\theta}) + [\text{bias}(\hat{\theta})]^2$$

-> For an unbiased estimator the bias is 0, so MSE equals variance. That is why "minimum MSE among unbiased estimators" and "minimum variance among unbiased estimators" are the same request, which is the MVUE criterion. (see: [[STA01B1_Notes_S2_Point_Estimation]] under "Minimum variance unbiased estimation".)

---

## 7. Standard errors of the point estimators

The standard error of an estimator is its standard deviation, $\sigma_{\hat{\theta}} = \sqrt{V(\hat{\theta})}$. #formula

Sample mean, from section 1:
$$\sigma_{\bar{X}} = \sqrt{V(\bar{X})} = \sqrt{\frac{\sigma^2}{n}} = \frac{\sigma}{\sqrt{n}}$$
When $\sigma$ is unknown, substituting $s$ gives the estimated standard error $\hat{\sigma}_{\bar{X}} = s/\sqrt{n}$.

Sample total, from section 2:
$$\sigma_{T_o} = \sqrt{V(T_o)} = \sqrt{n\sigma^2} = \sqrt{n}\,\sigma$$

Sample proportion (shown in source: [[STA01B1_Notes_S2_Point_Estimation]] under "The standard error", Example 6.10). With $X \sim \text{Bin}(n,p)$, $V(X) = npq$ where $q = 1-p$:
$$\sigma_{\hat{p}} = \sqrt{V\!\left(\frac{X}{n}\right)} = \sqrt{\frac{V(X)}{n^2}} = \sqrt{\frac{npq}{n^2}} = \sqrt{\frac{pq}{n}}$$
Since $p$ and $q$ are unknown, substitute $\hat{p}$ and $\hat{q}$ to get the estimated standard error $\sqrt{\hat{p}\hat{q}/n}$. Because $pq$ is largest at $p = q = 0.5$, an upper bound is
$$\sigma_{\hat{p}} \le \sqrt{\frac{1}{4n}}$$

-> These standard errors are the interval half-widths (before the critical value) in every confidence interval below.

---

## 8. Confidence interval for the mean, sigma known

Result: a $100(1-\alpha)\%$ CI for $\mu$ is $\bar{x} \pm z_{\alpha/2}\,\dfrac{\sigma}{\sqrt{n}}$. #theorem #exam-flagged

(shown in source: derived in full in [[STA01B1_Notes_S3_Statistical_Intervals]] under "Basic properties of confidence intervals".)

The population is normal, so $\bar{X} \sim N(\mu, \sigma^2/n)$ (section 1 gives the parameters), and the standardised pivot is exactly standard normal:
$$Z = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \sim N(0,1)$$

By definition of the critical value, $P(-z_{\alpha/2} \le Z \le z_{\alpha/2}) = 1-\alpha$. Substitute the pivot:
$$P\!\left(-z_{\alpha/2} \le \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \le z_{\alpha/2}\right) = 1-\alpha$$

Multiply all three parts by $\sigma/\sqrt{n}$:
$$P\!\left(-z_{\alpha/2}\frac{\sigma}{\sqrt{n}} \le \bar{X} - \mu \le z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right) = 1-\alpha$$

Subtract $\bar{X}$ from all three parts, then multiply by $-1$, which reverses both inequalities and swaps the two bounds:
$$P\!\left(\bar{X} - z_{\alpha/2}\frac{\sigma}{\sqrt{n}} \le \mu \le \bar{X} + z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right) = 1-\alpha$$

Replacing the random $\bar{X}$ with its observed value $\bar{x}$ gives the interval
$$\left(\bar{x} - z_{\alpha/2}\frac{\sigma}{\sqrt{n}}, \ \ \bar{x} + z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)$$

N.B the probability statement holds for the random interval before the sample is drawn. Once $\bar{x}$ is a fixed number, the $1-\alpha$ describes the long-run coverage of the procedure, not a probability about the one interval in hand. (see: [[STA01B1_Notes_S3_Statistical_Intervals]] under "Interpreting the confidence level".)

The quantity $z_{\alpha/2}$ is read at cumulative table area $1-\alpha/2$, since area $\alpha/2$ remains in the upper tail beyond it.

---

## 9. Confidence interval for the mean, sigma unknown

#theorem #exam-flagged

Large sample (added; algebra reused from section 8; result stated in [[STA01B1_Notes_S3_Statistical_Intervals]] under "Large sample confidence intervals"). For $n$ large, replacing $\sigma$ by the sample standard deviation $S$ leaves
$$Z = \frac{\bar{X} - \mu}{S/\sqrt{n}}$$
approximately standard normal (the CLT supplies approximate normality of $\bar{X}$, and $S \approx \sigma$ for large $n$). The identical isolation of $\mu$ from section 8 gives
$$\left(\bar{x} - z_{\alpha/2}\frac{s}{\sqrt{n}}, \ \ \bar{x} + z_{\alpha/2}\frac{s}{\sqrt{n}}\right)$$
Generally $n > 40$ is required here, stricter than the CLT rule of thumb $n \ge 30$, because substituting $S$ for $\sigma$ adds variability on top of what the CLT already handles.

Small sample, normal population (added; algebra reused from section 8; result stated in [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] under "One-sample $t$ confidence interval"). Here the same ratio is not approximately normal but follows a $t$ distribution exactly:
$$T = \frac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}$$
(distributional result stated in the source, see section 14). The isolation of $\mu$ is unchanged except that $t_{\alpha/2,\,n-1}$ replaces $z_{\alpha/2}$:
$$\left(\bar{x} - t_{\alpha/2,\,n-1}\frac{s}{\sqrt{n}}, \ \ \bar{x} + t_{\alpha/2,\,n-1}\frac{s}{\sqrt{n}}\right)$$

N.B the $t$ critical value is larger than the matching $z$ for small $n$, which widens the interval. That extra width is the price of not knowing $\sigma$, and it disappears as $n$ grows and $t_{n-1}$ approaches $N(0,1)$.

---

## 10. Confidence interval for a proportion

Result: an approximate $100(1-\alpha)\%$ CI for $p$ is $\hat{p} \pm z_{\alpha/2}\sqrt{\dfrac{\hat{p}\hat{q}}{n}}$. #theorem #exam-flagged #added

(added; result stated in [[STA01B1_Notes_S3_Statistical_Intervals]] under "Confidence interval for a population proportion".)

For large $n$ the CLT applied to the 0/1 indicators makes $\hat{p}$ approximately normal, with $E(\hat{p}) = p$ (section 3) and standard error $\sqrt{pq/n}$ (section 7). The pivot is
$$Z = \frac{\hat{p} - p}{\sqrt{pq/n}} \approx N(0,1)$$
The isolation of $p$ mirrors section 8. Because $p$ appears inside the standard error and is unknown, the endpoints substitute $\hat{p}$ and $\hat{q} = 1 - \hat{p}$:
$$\left(\hat{p} - z_{\alpha/2}\sqrt{\frac{\hat{p}\hat{q}}{n}}, \ \ \hat{p} + z_{\alpha/2}\sqrt{\frac{\hat{p}\hat{q}}{n}}\right)$$
Large-sample validity: $n\hat{p} > 10$ and $n\hat{q} > 10$.

---

## 11. Sample size formulas

#formula

For the mean (rearranging the section 8 half-width). The error of estimation is $E = z_{\alpha/2}\,\sigma/\sqrt{n}$. Solve for $n$:
$$\sqrt{n} = \frac{z_{\alpha/2}\,\sigma}{E} \quad\Longrightarrow\quad n = \left(\frac{z_{\alpha/2}\,\sigma}{E}\right)^2$$
If a full width $w$ is specified instead of the half-width, then $w = 2E$, so substitute $E = w/2$ first. Round the result up to the next integer.

For a proportion (rearranging the section 10 half-width). From $E = z_{\alpha/2}\sqrt{\hat{p}\hat{q}/n}$,
$$n = \frac{z_{\alpha/2}^2\,\hat{p}\hat{q}}{E^2}$$
When no prior estimate of $p$ exists, use $\hat{p} = 0.5$: the product $\hat{p}\hat{q}$ is a downward parabola in $\hat{p}$ peaking at $0.5$ with value $\tfrac14$, so $\hat{p} = 0.5$ produces the largest required $n$. Whatever the true $p$ turns out to be, this $n$ is guaranteed large enough. (Rearrangements shown via examples in [[STA01B1_Notes_S3_Statistical_Intervals]] under "Confidence level, precision, sample size" and "Confidence interval for a population proportion".)

N.B "within" gives $E$ directly, "width" gives $2E$ so divide by 2 first. This course uses the traditional proportion CI formula, not the adjusted one, for sample size work.

---

## 12. Confidence interval for the variance

Result: a $100(1-\alpha)\%$ CI for $\sigma^2$ is $\left(\dfrac{(n-1)s^2}{\chi^2_{\alpha/2,\,n-1}}, \ \dfrac{(n-1)s^2}{\chi^2_{1-\alpha/2,\,n-1}}\right)$. #theorem #exam-flagged #added

(added; result stated in [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] under "Confidence interval for the variance".)

Start from the pivotal quantity, which for a normal sample follows a chi-squared distribution (theorem stated in the source, see section 14):
$$\frac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1}$$

Let $\chi^2_{\alpha/2,\,n-1}$ be the upper critical value (area $\alpha/2$ to its right) and $\chi^2_{1-\alpha/2,\,n-1}$ the lower critical value (area $\alpha/2$ to its left). Then
$$P\!\left(\chi^2_{1-\alpha/2,\,n-1} \le \frac{(n-1)S^2}{\sigma^2} \le \chi^2_{\alpha/2,\,n-1}\right) = 1-\alpha$$

Take the reciprocal of all three parts, which reverses both inequalities:
$$P\!\left(\frac{1}{\chi^2_{\alpha/2,\,n-1}} \le \frac{\sigma^2}{(n-1)S^2} \le \frac{1}{\chi^2_{1-\alpha/2,\,n-1}}\right) = 1-\alpha$$

Multiply all three parts by $(n-1)S^2$:
$$P\!\left(\frac{(n-1)S^2}{\chi^2_{\alpha/2,\,n-1}} \le \sigma^2 \le \frac{(n-1)S^2}{\chi^2_{1-\alpha/2,\,n-1}}\right) = 1-\alpha$$

Replacing $S^2$ with the observed $s^2$ gives the stated interval.

N.B the reciprocal step is what sends the larger critical value $\chi^2_{\alpha/2,\,n-1}$ into the denominator of the smaller (lower) endpoint. The chi-squared distribution is not symmetric, so the two critical values are genuinely different numbers, unlike the $z$ and $t$ cases. A confidence interval for $\sigma$ itself is the square root of each endpoint.

---

## 13. Prediction interval for a single future observation

Result: a $100(1-\alpha)\%$ PI is $\bar{x} \pm t_{\alpha/2,\,n-1}\,s\sqrt{1 + \dfrac{1}{n}}$. #theorem #exam-flagged #added

(added; result stated in [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] under "A prediction interval".)

Let $X_{n+1} \sim N(\mu, \sigma^2)$ be a new observation, independent of the sample. It is predicted by $\bar{X}$, and the prediction error is $X_{n+1} - \bar{X}$. Its mean is
$$E(X_{n+1} - \bar{X}) = \mu - \mu = 0$$
and, using independence to add variances,
$$V(X_{n+1} - \bar{X}) = V(X_{n+1}) + V(\bar{X}) = \sigma^2 + \frac{\sigma^2}{n} = \sigma^2\!\left(1 + \frac{1}{n}\right)$$

So $X_{n+1} - \bar{X} \sim N\!\big(0, \ \sigma^2(1 + 1/n)\big)$. Standardising and replacing $\sigma$ with $S$ produces a $t_{n-1}$ variable:
$$\frac{X_{n+1} - \bar{X}}{S\sqrt{1 + \frac{1}{n}}} \sim t_{n-1}$$

The same isolation as section 9 gives the interval
$$\left(\bar{x} - t_{\alpha/2,\,n-1}\,s\sqrt{1 + \tfrac{1}{n}}, \ \ \bar{x} + t_{\alpha/2,\,n-1}\,s\sqrt{1 + \tfrac{1}{n}}\right)$$

N.B the CI for $\mu$ carries $\sqrt{1/n}$ but the PI carries $\sqrt{1 + 1/n}$. The extra $1$ under the root is the individual variability of the single new observation about the mean, so a PI is always wider than the matching CI on the same data.

---

## 14. Results stated without proof at this level

These are used above but are not derived on the page, and cannot be proven with course-level tools, so they are recorded as statement only, per R4. #theorem

- $T = \dfrac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}$ for a normal sample. Proof not shown in source. A full proof writes $T$ as a standard normal divided by $\sqrt{\chi^2_{n-1}/(n-1)}$ with the two independent, which is the definition of a $t$ variable. Stated in [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] under "The $t$ distribution".

- $\dfrac{(n-1)S^2}{\sigma^2} \sim \chi^2_{n-1}$ for a normal sample. Proof not shown in source. Stated in [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] under "Confidence interval for the variance".

- $\hat{\mu} = \bar{X}$ is the MVUE for $\mu$ under normality. Optimality proof not shown in source (needs tools such as the Cramer-Rao bound or completeness). Stated in [[STA01B1_Notes_S2_Point_Estimation]] under "Minimum variance unbiased estimation".

- Central Limit Theorem: $\bar{X}$ is approximately normal for large $n$ from almost any population. Proof not shown in source (needs characteristic functions). Stated in [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] under "The Central Limit Theorem".

---

## Do not forget

- $E(\bar{X}) = \mu$ needs only linearity, $V(\bar{X}) = \sigma^2/n$ needs independence, the constant leaves the variance as $1/n^2$.
- $E(S^2) = \sigma^2$ hinges on $\sum(X_i - \bar{X})^2 = \sum(X_i - \mu)^2 - n(\bar{X} - \mu)^2$, then $E[(\bar{X}-\mu)^2] = \sigma^2/n$. The $n-1$ divisor cancels the $(n-1)$ that appears.
- Divisor-$n$ bias is exactly $-\sigma^2/n$: negative means underestimate, $1/n$ means it fades as $n$ grows.
- MSE $= V + \text{bias}^2$, so among unbiased estimators minimum variance is minimum MSE (the MVUE).
- Every CI derivation is the same three moves: standardise to a pivot, bracket the pivot between critical values, isolate the parameter.
- Known $\sigma$ uses $z$ exactly (normal population); unknown $\sigma$ uses $z$ for large $n$ or $t_{n-1}$ exactly for small $n$ normal.
- The $\sigma^2$ interval is asymmetric: the larger $\chi^2$ value makes the lower endpoint.
- The PI carries $\sqrt{1 + 1/n}$, always wider than the CI's $\sqrt{1/n}$.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]
- [[STA01B1_Notes_S2_Point_Estimation]]
- [[STA01B1_Notes_S3_Statistical_Intervals]]
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]]
- [[STA01B1_Notes_S5_Hypothesis_Testing]]
- [[STA01B1_Summary_ST1]]
