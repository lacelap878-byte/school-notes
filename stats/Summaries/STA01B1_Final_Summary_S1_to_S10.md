# STA01B1 Final: Revise S1 to S10 (Mon 9 Nov, 08:30)

Read tonight, read again tomorrow morning. Built from your own ST1/ST2 summaries, proofs and S10 notes, re-scoped for the final. Dr H gives no formulas on the proofs and no formula for $n$. One- or two-sided is decided by the board on the day.

## Definitions

Each term has a **Short** version (one line) and a **Long** version (3 to 4 sentences, the size Dr H asks for). The Long versions say what the thing is and why it matters, not how it is calculated. Alphabetical order.

### Analysis of variance (ANOVA)
**Short:** A test of whether three or more population means are all equal, made by comparing the variation between the group means with the variation within the groups.

**Long:** ANOVA is a hypothesis test for comparing the means of three or more populations at the same time, where $H_0$ says that all the population means are equal. It asks whether the differences between the group averages are bigger than the ordinary variation among the individual observations inside each group. We use one overall test instead of many two-sample tests because it keeps the risk of a false alarm under control. A significant result tells us that at least two means differ, but not which ones.

### Bias
**Short:** The gap between the average value of an estimator and the true parameter: $\text{bias}(\hat\theta)=E(\hat\theta)-\theta$.

**Long:** Bias describes whether an estimator is aimed at the right target. If we could use the estimator on every possible sample, bias is the gap between the average of all those estimates and the true value of the parameter. A positive bias means the estimator tends to be too high, a negative bias means it tends to be too low, and zero means it hits the target on average. It describes systematic error only, so an estimator with zero bias can still be far off for the one sample we have.

### Central Limit Theorem
**Short:** For a large random sample from any population, the sample mean (and the sample total) is approximately normal.

**Long:** The Central Limit Theorem says that the average of a large random sample behaves in a predictable, bell-shaped way, whatever the shape of the population it came from. It tells us that $\bar X$ is approximately normal with mean $\mu$ and variance $\frac{\sigma^2}{n}$, and that the total $T_0$ is approximately normal with mean $n\mu$ and variance $n\sigma^2$. In this course "large" means $n>40$, and if the population is already normal then $\bar X$ is exactly normal for any $n$. It is the reason we can use normal probabilities for confidence intervals and tests about $\mu$ without knowing the shape of the population.

### Chi-square, t and F distributions, how they are built
**Short:** All three are built from standard normal variables: $\chi^2$ from squared normals, $t$ from a normal divided by the root of a chi-square, $F$ from a ratio of two chi-squares.

**Long:** These are three families of probability distributions that all come from standard normal random variables. A chi-square variable is a sum of squared independent standard normals, a $t$ variable is a standard normal divided by the square root of an independent chi-square over its degrees of freedom, and an $F$ variable is the ratio of two independent chi-squares, each over its degrees of freedom. They matter because they are the sampling distributions of the quantities we use most: $\frac{(n-1)S^2}{\sigma^2}$ is chi-square, $\frac{\bar X-\mu}{S/\sqrt n}$ is $t$, and the ANOVA statistic is $F$. In every case the pieces being combined must be independent.

### Confidence interval
**Short:** A range of plausible values for a parameter, built so that a stated percentage of such intervals would contain the true value.

**Long:** A confidence interval is a range of values that we report for an unknown population parameter instead of a single number. The confidence level, such as 95%, is a statement about the method: if we repeated the sampling many times, about 95% of the intervals built this way would contain the true value. It is not the probability that the one interval we have contains the parameter, because the parameter is fixed and the interval either contains it or it does not. The width of the interval shows how precise our estimate is, since a narrow interval means a precise estimate and a wide one means a lot of uncertainty.

### Hypothesis testing
**Short:** A procedure that uses sample data to decide between two competing claims about a population parameter.

**Long:** Hypothesis testing is a way of using sample data to decide between two competing claims about a population parameter. The null hypothesis $H_0$ is the claim we keep unless the data give strong evidence against it, usually "no difference" or "no effect", and the alternative $H_a$ is the claim we are trying to find evidence for. The test asks how likely data like ours would be if $H_0$ were true, and if that is very unlikely, at most the significance level $\alpha$, we reject $H_0$. Because a sample can mislead us, the conclusion is only ever "sufficient evidence against $H_0$" or "not sufficient evidence against $H_0$", and never that $H_0$ is proven.

### Least squares regression line
**Short:** The straight line $\hat y=b_0+b_1x$ that makes the sum of the squared vertical distances from the data points as small as possible.

**Long:** The least squares regression line is the straight line that best describes how a response variable $y$ changes with an explanatory variable $x$. "Best" means that it makes the total of the squared vertical gaps between the observed points and the line as small as possible. It is our estimate of the true population line $E(y)=\beta_0+\beta_1x$, which gives the average value of $y$ at each value of $x$. Its slope is the average change in $y$ for each one-unit increase in $x$, and the line can be trusted for predictions only inside the range of the data.

### Point estimation
**Short:** Using one number calculated from the sample, a point estimate, to estimate an unknown population parameter.

**Long:** Point estimation is the problem of using sample data to give one best guess for an unknown population parameter. The rule or formula is the point estimator $\hat\theta$, which is a random variable because it changes from sample to sample, and the number we get from our own data is the point estimate. Examples are $\bar X$ for $\mu$, $S^2$ for $\sigma^2$ and $\hat p$ for $p$. Because many rules are possible, we judge an estimator by whether it is unbiased and by how little it varies, and the mean squared error combines the two.

### R squared
**Short:** The percentage of the variation in $y$ that is explained by the linear relationship with $x$.

**Long:** $R^2$ measures how much of the variation in the response $y$ is accounted for by its straight-line relationship with $x$. It is the proportion of the total variation that the regression explains, so it lies between $0\%$ and $100\%$. In the exam it must be stated in the words of the question, for example "82.8% of the variation in monthly electricity cost is explained by the linear relationship with floor area", and the rest, $100\%-R^2$, is not explained. It does not show that $x$ causes $y$, and a high $R^2$ alone does not show that a straight line is the right model.

### Sample size for a confidence interval
**Short:** The $n$ needed so that a confidence interval has the half-width $E$ you want.

**Long:** This is the number of observations we need to collect so that a confidence interval comes out as precise as we want it to be. The precision is set by the half-width $E$, the largest error we are willing to accept, and the confidence level is set through $\alpha$. A more precise interval or a higher confidence level always needs a larger sample, and so does a more variable population (a larger $\sigma$). "Within" a value means the half-width $E$, "width" means $2E$, and the answer is always rounded up to a whole number.

### Sample size from alpha and beta
**Short:** The $n$ needed so that a test with significance level $\alpha$ also has Type II error $\beta$ at a stated true value.

**Long:** This is the number of observations needed so that a hypothesis test has both of its error risks under control at once: a chance of Type I error of $\alpha$, and a chance of Type II error of only $\beta$ when the true value is a stated $\mu'$. It exists because $\alpha$ and $\beta$ pull against each other for a fixed sample size, and only a larger $n$ can make both small. The further the true value $\mu'$ is from $\mu_0$, the smaller the sample needed, and the more variable the population, the larger. It applies to a single mean or a single proportion, and the answer is always rounded up.

### Sampling distribution
**Short:** The probability distribution of a statistic, describing how its value varies from sample to sample.

**Long:** A sampling distribution is the probability distribution of a statistic, such as $\bar X$, across all the samples we could possibly draw. It exists because a statistic is calculated from a random sample, so before the data are collected it is itself a random variable whose value changes from sample to sample. It describes the centre, the spread (the standard error) and the shape of those values; for example $\bar X$ has mean $\mu$ and variance $\frac{\sigma^2}{n}$. It stays a full distribution for every $n$ and only narrows as $n$ grows, and it is the foundation of confidence intervals and tests.

### Type I error
**Short:** Rejecting $H_0$ when $H_0$ is true.

**Long:** A Type I error is a false alarm: the data lead us to reject $H_0$ even though $H_0$ is actually true. The probability of making it is the significance level $\alpha$, which we choose before looking at the data, commonly $0.05$. With $\alpha=0.05$ we accept that about 5 in every 100 tests of a true $H_0$ would wrongly reject it. We can lower $\alpha$ to make false alarms rarer, but for a fixed sample size that makes Type II errors more likely.

### Type II error
**Short:** Failing to reject $H_0$ when $H_0$ is false.

**Long:** A Type II error is a miss: the data fail to lead us to reject $H_0$ even though $H_0$ is actually false. Its probability is $\beta$, and unlike $\alpha$ it depends on what the true value is, so we always state it at a particular value such as $\beta(47)$. $\beta$ is smaller when the true value is further from the hypothesised one, when the sample is larger, or when $\alpha$ is larger. In words, $\beta$ is the chance that the test misses a real difference.

### Unbiased estimator
**Short:** An estimator whose average value over all possible samples equals the parameter: $E(\hat\theta)=\theta$.

**Long:** An unbiased estimator is one that is correct on average: if we used it on every possible sample, the average of its values would equal the true parameter, $E(\hat\theta)=\theta$. Being unbiased says nothing about any single sample, which can still be well off the target. Known examples are $\bar X$ for $\mu$, $\hat p$ for $p$, and $S^2$ with divisor $n-1$ for $\sigma^2$. Among unbiased estimators we prefer the one with the smallest variance, because it is the most likely to be close to the truth.

## 0. Your five slips (never again)
1. Standard error is $\frac{\sigma}{\mathbf{\sqrt n}}$, not $\frac{\sigma}{n}$. Write $E(\bar X)=\mu$ with the symbol, then the number.
2. Reject iff **$p\le\alpha$** for every $H_a$. Only the side of the curve changes (upper tail: area to the right, lower tail: area to the left, two-sided: double the smaller tail).
3. $\beta$ is the area of the **true-mean curve** on the side of $c$ that is **not** the rejection region. $\alpha$ is the area of the $H_0$ curve inside the rejection region.
4. Chi-square goodness of fit: **$df=k-1$** ($k$ groups, never $n-1$). Expected counts come from $H_0$: $E_i=n\,p_{i0}$.
5. After a non-rejection write: "not sufficient evidence that ..." at the stated level, with context. Never "accept $H_0$", never "the alternative is rejected", and a significance level is not a confidence level.

Also: the 15 copies of $\bar x$ are already inside $\frac{x_{\cdot\cdot}^2}{IJ}$ in ANOVA; a negative $SS$ is an alarm.

## 1. Sampling distribution of the sample mean (S1)
- $E(\bar X)=\mu$, $V(\bar X)=\frac{\sigma^2}{n}$, $\text{sd}=\frac{\sigma}{\sqrt n}$. Total $T_0$: mean $n\mu$, sd $\sqrt n\,\sigma$.
- Normal population: $\bar X$ is exactly normal. Otherwise the CLT: $\bar X$ is approximately normal when $n>40$ (Dr H's cut, the tutor says 30).
- Standardise: $Z=\frac{\bar X-\mu}{\sigma/\sqrt n}$. For the probability of a range for $\bar X$, use the sd of $\bar X$, never the sd of $X$.

## 2. Point estimation (S2)
- $\text{Bias}=E(\hat\theta)-\theta$. Unbiased means bias $0$. $MSE=V(\hat\theta)+[\text{bias}]^2$.
- Point estimate means a number from the data; point estimator means the random variable (the formula). This is a true or false trap.
- Compare two unbiased estimators: choose the smaller variance.
- Useful: $V(\hat p)=\frac{pq}{n}$, $V(\hat p_1-\hat p_2)=\frac{p_1q_1}{m}+\frac{p_2q_2}{n}$, $E(\hat p_1-\hat p_2)=p_1-p_2$.

## 3. Proofs (skeletons, write every symbol, a mark per missing dot or bar)
- **MSE equals variance plus bias squared:** add and subtract $E(\hat\theta)$, square, and the cross term has $E[\hat\theta-E(\hat\theta)]=0$.
- **$E(S^2)=\sigma^2$:** $\sum(X_i-\bar X)^2=\sum X_i^2-n\bar X^2$; $E(X_i^2)=\sigma^2+\mu^2$ and $E(\bar X^2)=\frac{\sigma^2}{n}+\mu^2$; this gives $(n-1)\sigma^2$. Divisor $n$ gives bias $-\frac{\sigma^2}{n}$.
- **$\bar X^2-\frac{S^2}{n}$ is unbiased for $\mu^2$:** $E(\bar X^2)=\mu^2+\frac{\sigma^2}{n}$ and $E\!\left(\frac{S^2}{n}\right)=\frac{\sigma^2}{n}$.
- **Bias of $\hat p^2$:** $E(\hat p^2)=p^2+\frac{pq}{n}$, so bias $=\frac{pq}{n}$.
- **$S_p^2$ is unbiased:** weights $(m-1)$ and $(n-1)$, each $S^2$ is unbiased, and the weights sum to $m+n-2$.
- **CI for $\mu_1-\mu_2$ (known $\sigma$):** $\bar X_1-\bar X_2\sim N\!\left(\mu_1-\mu_2,\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}\right)$, standardise, $P(-z\le Z\le z)=1-\alpha$, rearrange.
- **$SST=SSTr+SSE$:** add and subtract $\bar x_{i\cdot}$, expand, the cross term is $\sum_i(\bar x_{i\cdot}-\bar x_{\cdot\cdot})\sum_j(x_{ij}-\bar x_{i\cdot})=0$, and the two ends become $SSE$ and $SSTr$ (the one carrying the $J$). Dots: $x_{ij}$ none, $\bar x_{i\cdot}$ one, $\bar x_{\cdot\cdot}$ two. The grand mean has a bar, the grand total does not.
- **Chi-square:** $E_{ij}=\frac{n_{i\cdot}\,n_{\cdot j}}{n}$ (independence gives $p_{i\cdot}\,p_{\cdot j}$, times $n$). $\chi^2=\sum\frac{O^2}{E}-n$ (expand the square, $\sum O=\sum E=n$).
- **Building distributions (Practical 2):** $\chi^2_\nu=\sum Z_i^2$ ($\nu$ standard normals squared); $t=\frac{Z}{\sqrt{X/\nu}}$; $F=\frac{X_1/\nu_1}{X_2/\nu_2}$. Independence of numerator and denominator is a condition.

## 4. Confidence intervals (S3, S4, S6, S7)
| Parameter | Interval | Notes |
|---|---|---|
| $\mu$, $\sigma$ known | $\bar x\pm z_{\alpha/2}\frac{\sigma}{\sqrt n}$ | |
| $\mu$, $\sigma$ unknown | $\bar x\pm t_{\alpha/2,n-1}\frac{s}{\sqrt n}$ | normal population |
| $p$ | $\hat p\pm z_{\alpha/2}\sqrt{\frac{\hat p\hat q}{n}}$ | |
| $\sigma^2$ | $\left(\frac{(n-1)s^2}{\chi^2_{\alpha/2,n-1}},\ \frac{(n-1)s^2}{\chi^2_{1-\alpha/2,n-1}}\right)$ | lower bound uses the upper chi-square |
| $\mu_1-\mu_2$, $\sigma$ known | $(\bar x_1-\bar x_2)\pm z_{\alpha/2}\sqrt{\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}}$ | |
| $\mu_1-\mu_2$, pooled $t$ | $(\bar x_1-\bar x_2)\pm t_{\alpha/2,m+n-2}\,s_p\sqrt{\frac1m+\frac1n}$ | $s_p^2=\frac{(m-1)s_1^2+(n-1)s_2^2}{m+n-2}$; equal variances assumed |
| paired $\mu_D$ | $\bar d\pm t_{\alpha/2,n-1}\frac{s_d}{\sqrt n}$ | one sample of differences |
| $p_1-p_2$ | $(\hat p_1-\hat p_2)\pm z_{\alpha/2}\sqrt{\frac{\hat p_1\hat q_1}{m}+\frac{\hat p_2\hat q_2}{n}}$ | |
| prediction (one new value) | $\bar x\pm t\,s\sqrt{1+\frac1n}$ | wider than the CI |

- Sample size for width: $n=\left(\frac{z_{\alpha/2}\sigma}{E}\right)^2$ for a mean; $n=\frac{z_{\alpha/2}^2\,\hat p\hat q}{E^2}$ for a proportion ($\hat p=0.5$ if unknown). "Within" means $E$; "width" means $2E$. Round up.
- df rule from Dr H: if the exact df is not in the table, use the closest listed value.

## 5. Type I, Type II, sample size (S5, the concept you cracked)
- $\alpha=P(\text{reject }H_0\mid H_0\text{ true})$ = area of the $H_0$ curve in the rejection region.
- $\beta=P(\text{fail to reject}\mid H_0\text{ false at the true value }\mu')$ = area of the $\mu'$ curve in the **complement** of the rejection region.
- $c$ is a vertical line in the overlap of the two curves, between $\mu_0$ and $\mu'$ (halfway only if $\alpha=\beta$). It is the $\bar x$ whose $p$-value is exactly $\alpha$.
- Direction decides the picture. $H_a:\mu<\mu_0$ has the rejection region left of $c$ and $\beta$ to the right. $H_a:\mu>\mu_0$ has the rejection region right of $c$ and $\beta$ to the left. Two-sided: $\frac\alpha2$ in each tail ($z_{\alpha/2}$); $\beta$ uses the true mean's curve and the nearer boundary.
- Given a rejection region (for example $\bar X>32$, true mean $31$): Type II error $=P(\bar X\le32\mid\mu=31)$.
- **Find $n$ (derive it, no formula given).** Start at $\mu_0$ and walk toward $\mu'$ by $z_\alpha\cdot se$; start at $\mu'$ and walk toward $\mu_0$ by $z_\beta\cdot se$. Both reach $c$, so equate and solve. Round $n$ up.

| $H_a$ | $c$ from $\alpha$ | $c$ from $\beta$ | $n$ |
|---|---|---|---|
| $\mu<\mu_0$ | $\mu_0-z_\alpha\frac{\sigma}{\sqrt n}$ | $\mu'+z_\beta\frac{\sigma}{\sqrt n}$ | $\left[\frac{\sigma(z_\alpha+z_\beta)}{\mu_0-\mu'}\right]^2$ |
| $\mu>\mu_0$ | $\mu_0+z_\alpha\frac{\sigma}{\sqrt n}$ | $\mu'-z_\beta\frac{\sigma}{\sqrt n}$ | $\left[\frac{\sigma(z_\alpha+z_\beta)}{\mu'-\mu_0}\right]^2$ |
| $\mu\ne\mu_0$ | use $z_{\alpha/2}$ and the boundary nearer $\mu'$ | | $\left[\frac{\sigma(z_{\alpha/2}+z_\beta)}{\lvert\mu'-\mu_0\rvert}\right]^2$ |

  Key: $\mu_0$ is the $H_0$ mean, $\mu'$ is the true mean asked about, $se=\frac{\sigma}{\sqrt n}$, $c$ is the cut-off in $\bar x$ units, and $z_\alpha$ and $z_\beta$ are the $z$ values leaving $\alpha$ or $\beta$ to the right (always positive). Proportion: the same, with $\sqrt{p_0q_0}$ beside $z_\alpha$ and $\sqrt{p'q'}$ beside $z_\beta$, over $(p'-p_0)$.
- Worked check (Set C, question B5): $c=47.5325$, $\beta(47)=0.3594$, $n=34.2$, so $n=35$.

## 6. Pooled t and paired t (S6, S7)
- Pooled $t$: $H_0:\mu_1-\mu_2=\Delta_0$, $df=m+n-2$, assumptions: equal variances (sample sds within a factor of 2) and normality.
- Paired: two measurements on the same unit, so take differences and do a one-sample $t$ on $\bar d$ with $df=n-1$. Independent groups: pooled. State which, and why.

## 7. ANOVA and Tukey (S8)
- $H_0:\mu_1=\dots=\mu_I$; $H_a$: at least two differ. Assumptions (say both): normal populations, equal variances (largest sd not more than $2\times$ the smallest).
- $SST=\sum x^2-\frac{x_{\cdot\cdot}^2}{IJ}$; $SSTr=\frac{\sum x_{i\cdot}^2}{J}-\frac{x_{\cdot\cdot}^2}{IJ}$; $SSE=SST-SSTr$. Order check: grand piece $<$ group piece $<$ every-value piece.
- df: $I-1$, $I(J-1)$, $IJ-1$. $MSTr=\frac{SSTr}{I-1}$, $MSE=\frac{SSE}{I(J-1)}$, $F=\frac{MSTr}{MSE}$; reject if $F\ge F_{\alpha,I-1,I(J-1)}$.
- Tukey only after rejecting: $w=Q_{\alpha,I,I(J-1)}\sqrt{\frac{MSE}{J}}$. The second subscript is $I$, not $I-1$; the third is the error df. Means differing by more than $w$ differ; joined means are "not shown to differ", not "equal".

## 8. Regression: interpretation only (S9, Practical 10)
- Slope $b_1$: "for each one-unit increase in $x$, $y$ changes by $b_1$ on average" (use variable names and units).
- $R^2$: "$R^2$% of the variation in $y$ is explained by the linear relationship with $x$"; **not explained $=100\%-R^2$**.
- $t$, df and $p$ are on the printout; $F=t^2$ for the slope.
- Predict only inside the data range (outside is extrapolation).
- Residuals against fitted values: constant variance. Normal probability plot: normality.
- No hand-calculated coefficients, no scatter plots.

## 9. Chi-square (S10)
- Counts in categories only. Statistic $\chi^2=\sum\frac{(O-E)^2}{E}$, upper tail, reject if $\chi^2\ge\chi^2_{\alpha,df}$.
- **Goodness of fit:** $H_0:p_i=p_{i0}$; $E_i=n\,p_{i0}$; $df=k-1$.
- **Independence:** $H_0$: the two classifications are independent; $E=\frac{\text{row total}\times\text{column total}}{n}$; $df=(I-1)(J-1)$.
- Assumption: **every expected count $\ge5$** (the expected, not the observed, not the df). Fix: larger $n$ or combine cells.
- Write: hypotheses, then expected counts and the $\ge5$ check, then the statistic in a table, then df and cut-off, then the decision, then a plain-words conclusion.
- Which test? A number measured on each person: $t$ or ANOVA. Only labels: chi-square. Three groups alone do not make it ANOVA.
- Table A.7 prints $3.843$ ($df=1$) and $5.992$ ($df=2$) in the $.05$ column. Homogeneity is out.
- Example: $52,38,21,9$ against $40,30,20,10\%$ of $120$ gives $E=48,36,24,12$ and $\chi^2=1.57<7.815$ with $df=3$, so do not reject.

## 10. Wording bank
- Slope: "On average, each additional [$x$ unit] is associated with a change of [$b_1$] [$y$ unit]."
- $R^2$: "[$R^2$]% of the variation in [$y$] is explained by the linear relationship with [$x$]."
- Reject: "At the [$\alpha$] level there is sufficient evidence that ..."
- Fail to reject: "At the [$\alpha$] level there is not sufficient evidence that ..."
- CI meaning: "We are [95]% confident that the true [parameter] lies between $a$ and $b$."
- ANOVA: "At least two population means differ"; Tukey: "[A] and [B] differ significantly."

## 11. Out of scope (do not spend time)
One-sample hypothesis tests (Lecture 6, Tutorial 6), chi-square homogeneity, hand-calculated regression coefficients, scatter plots.

## 12. Tomorrow morning, in this order (20 minutes)
1. Section 0, aloud.
2. Draw the two curves for a lower-tailed and an upper-tailed test, shade $\alpha$ and $\beta$, write both descriptions of $c$.
3. Write the $SST=SSTr+SSE$ and $E(S^2)=\sigma^2$ proofs from a blank page.
4. Tables A.3, A.5, A.7, A.9, A.10: find one value in each.
