---
module: STA01B1
topic: Inferences Based on Two Samples
session: S6
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Inferences Based on Two Samples (Devore and Berk, Ch 9.1 and 9.2)

Every earlier session in this module compared a single sample against a claimed value (see: [[STA01B1_Notes_S5_Hypothesis_Testing]]). This session compares two populations directly against each other, using one independent sample drawn from each.

## Setup: assumptions and the distribution of X̄ − Ȳ

The parameter of interest throughout this note is $\mu_1-\mu_2$, and the natural estimator is $\bar{X}-\bar{Y}$. Three conditions hold for every procedure below.

```
1. X1, X2, ..., Xm is a random sample from a population with mean mu1
   and variance sigma1^2
2. Y1, Y2, ..., Yn is a random sample from a population with mean mu2
   and variance sigma2^2
3. The X and Y samples are independent of one another
```
N.B The sample sizes are named differently on purpose, $m$ for the X sample, $n$ for the Y sample. They are not assumed equal anywhere in this note.

Because $\bar{X}$ and $\bar{Y}$ are independent, their variances add when combined:
$$E(\bar{X}-\bar{Y}) = E(\bar{X})-E(\bar{Y}) = \mu_1-\mu_2$$
$$\sigma_{\bar{X}-\bar{Y}}^2 = V(\bar{X}-\bar{Y}) = V(\bar{X})+V(\bar{Y}) = \frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}$$
$$\sigma_{\bar{X}-\bar{Y}} = \sqrt{\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}}$$

This is the same variance-addition step used for the sample total $T_o$ (see: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]), applied here to a difference of two means instead of a sum of observations from one population. Every test and interval in this note standardises using this mean and this standard deviation, the way the one-sample case standardised using $\sigma/\sqrt{n}$ (see: [[STA01B1_Notes_S5_Hypothesis_Testing]]).

> [!note] Why a difference, not a sum, product, or ratio (added) #added
> The mean and variance of a linear combination of independent random variables, $a\bar{X}+b\bar{Y}$, have simple exact formulas regardless of the underlying distributions: $E(a\bar{X}+b\bar{Y})=aE(\bar{X})+bE(\bar{Y})$ and $V(a\bar{X}+b\bar{Y})=a^2V(\bar{X})+b^2V(\bar{Y})$ under independence. A difference is $a=1,b=-1$, which is why the derivation above is a two-line consequence of linearity. A sum ($a=b=1$) would work exactly the same way but rarely answers the interesting question, a difference near 0 means "about the same," and its sign says which population is larger. A product or a quotient of two means has no such clean formula in general, not even under normality and independence, and $\bar{X}/\bar{Y}$ does not have a standard named sampling distribution, so testing a ratio needs different machinery entirely, not a variant of what is covered here.

-> This mean and variance are what get standardized into a Z or t statistic in every procedure that follows.

## z Test for a Difference between Two Population Means (known variances)

This case assumes $\sigma_1^2$ and $\sigma_2^2$ are already known values, not estimated from the samples.

```
Test procedure

H0: mu1 - mu2 = Delta0

Z = (Xbar - Ybar - Delta0) / sqrt(sigma1^2/m + sigma2^2/n)

Applies when the population variances are known.
```
$$H_0: \mu_1-\mu_2=\Delta_0$$
$$Z = \frac{\bar{X}-\bar{Y}-\Delta_0}{\sqrt{\dfrac{\sigma_1^2}{m}+\dfrac{\sigma_2^2}{n}}}$$
$\Delta_0$ is the hypothesized value of the difference $\mu_1-\mu_2$, most often 0.

N.B This is the same standardizing move as the one-sample case (see: [[STA01B1_Notes_S5_Hypothesis_Testing#Case I: known variance]]), numerator is estimate minus hypothesized value, denominator is that estimate's own standard deviation (defined in: [[#Setup: assumptions and the distribution of X̄ − Ȳ]]). The three rejection region forms from Case I carry over unchanged, only the test statistic's shape has changed.

### Example 9.1 (GPA and study hours, source, slide 2)
21 students reported GPA and whether they studied less than 10 hours per week or at least 10 hours per week. GPAs for the under-10 group: 2.80, 3.40, 4.00, 3.60, 2.00, 3.00, 3.47, 2.80, 2.60, 2.00. GPAs for the 10-plus group: 3.00, 3.00, 2.20, 2.40, 4.00, 2.96, 3.41, 3.27, 3.80, 3.10, 2.50. Normal plots for both groups are reasonably linear, so normality is tenable. The population standard deviation of GPA campus-wide is known to be .6, taken as $\sigma_1=\sigma_2=.6$. Sample means: $\bar{x}=2.97$ for the under-10 group, $\bar{y}=3.06$ for the 10-plus group. Is there evidence true average GPA differs between the two study time groups, at significance level .05?

WORKING
1. Parameter of interest: $\mu_1-\mu_2$, the difference between true mean GPA for the under-10 (conceptual) population and true mean GPA for the 10-plus population.
2. $H_0: \mu_1-\mu_2=0$
3. $H_a: \mu_1-\mu_2\ne0$. Although it would seem unlikely that $\mu_1-\mu_2>0$, it is allowed as a possibility, so a two-tailed test is used.
4. With $\Delta_0=0$: $z = \dfrac{\bar{x}-\bar{y}}{\sqrt{\sigma_1^2/m+\sigma_2^2/n}}$
5. Two-tailed at $\alpha=.05$ means $\alpha/2=.025$, $z_{.025}=1.96$. $H_0$ is rejected if $z\ge1.96$ or $z\le-1.96$.
6. Substituting $m=10$, $\bar{x}=2.97$, $\sigma_1^2=.36$, $n=11$, $\bar{y}=3.06$, $\sigma_2^2=.36$:
$$z = \frac{2.97-3.06}{\sqrt{.36/10+.36/11}} = \frac{-.09}{.262} = -.34$$
7. Because $z=-.34$ is not even close to the rejection region, there is no reason to reject $H_0$. This test shows no evidence of any relationship between study hours and GPA.

-> The next fork relaxes the "variance known" assumption: when $\sigma_1^2$ and $\sigma_2^2$ are unknown but both samples are large, $S_1^2$ and $S_2^2$ substitute directly into this same Z formula.

## Large Sample z Test (unknown variances, m and n both large)

```
Test procedure

H0: mu1 - mu2 = Delta0

Z = (Xbar - Ybar - Delta0) / sqrt(S1^2/m + S2^2/n)

Applies when m > 40 and n > 40.
```
$$H_0: \mu_1-\mu_2=\Delta_0$$
$$Z = \frac{\bar{X}-\bar{Y}-\Delta_0}{\sqrt{\dfrac{S_1^2}{m}+\dfrac{S_2^2}{n}}}$$
$m>40$ and $n>40$.

N.B The only change from the known-variance case is $\sigma_1^2,\sigma_2^2 \to S_1^2,S_2^2$. The threshold here, $m>40$ and $n>40$, both samples must clear it, is stricter than the one-sample large-sample rule of $n>30$ (see: [[STA01B1_Notes_S5_Hypothesis_Testing#Case II: large sample tests]]), and matches the same $n>40$ threshold already used for a one-sample large-sample confidence interval (see: [[STA01B1_Notes_S3_Statistical_Intervals]]).

### Example 9.4 (final exam scores, control vs experimental teaching method, source, slide 3)
A low-level university mathematics course had many students fail or drop out. A study assigned students to sections by odd or even social security number, avoiding assignment by student choice, attitude, or ability. Half the sections were taught traditionally (control group), the other half with frequent assignments, quizzes, and exam retakes (experimental group). Final exam scores were recorded for 79 control students and 85 experimental students.

| Group | Sample Size | Sample Mean | Sample SD |
|---|---|---|---|
| Control | 79 | 23.87 | 11.60 |
| Experimental | 85 | 27.34 | 8.85 |

Does this data suggest true mean score for the experimental condition exceeds that for the control condition? Use $\alpha=.05$.

WORKING
Let $\mu_1,\mu_2$ denote true mean scores for control and experimental respectively.
$$H_0:\mu_1-\mu_2=0 \qquad H_a:\mu_1-\mu_2<0$$
$H_0$ is rejected if $z\le -z_{.05}=-1.645$ (lower-tailed form, defined in: [[STA01B1_Notes_S5_Hypothesis_Testing#Case I: known variance]], applied here to $\mu_1-\mu_2$).
$$z = \frac{23.87-27.34}{\sqrt{11.60^2/79+8.85^2/85}} = \frac{-3.47}{1.620} = -2.14$$
Since $-2.14\le-1.645$, $H_0$ is rejected at $\alpha=.05$.
$$\text{P-value} = \Phi(z) = \Phi(-2.14) = .016$$
which implies rejection at $\alpha=.05$, matching the rejection region decision. If two-tailed, the P-value would be $2(.016)=.032$.

> [!tip] P-value doubling in a two-tailed test (struggle, resolved S6) #struggle
> This is the first P-value in the course material on file. A P-value is the probability, computed under $H_0$, of a result at least as extreme as the one observed. For a one-tailed test it is the tail area beyond $z$ in that one direction, $\Phi(z)$ for a lower tail or $1-\Phi(z)$ for an upper tail. A two-tailed test doubles that one-tailed area, since either tail counts as "at least as extreme" when $H_a$ allows departure in both directions. Here $\Phi(-2.14)=.016$ is the lower-tail area alone; doubling it to $.032$ accounts for an equally extreme result in the upper tail too. Decision rule either way: reject $H_0$ if P-value $\le\alpha$.

-> The next procedure uses this same $S_1^2/m+S_2^2/n$ standard error, but for a confidence interval on $\mu_1-\mu_2$ instead of a test.

## Large Sample Confidence Interval for μ1 − μ2

```
100(1-alpha)% Confidence Interval

Xbar - Ybar +- z(alpha/2) * sqrt(S1^2/m + S2^2/n)

Applies when m > 40 and n > 40.
```
$$\bar{x}-\bar{y} \pm z_{\alpha/2}\sqrt{\frac{s_1^2}{m}+\frac{s_2^2}{n}}$$

### Example 9.5 (ACT math scores, fall vs spring calculus students, source, slide 4)
Students taking Calculus I in the fall semester are often better prepared than those in the spring. Data comes from a study on predictors of calculus performance, using ACT math scores for both groups.

| Group | Sample Size | Sample Mean | Sample SD |
|---|---|---|---|
| Fall | 80 | 28.25 | 3.25 |
| Spring | 74 | 25.88 | 4.59 |

A boxplot/dotplot comparison shows more high scorers in the fall group and more low scorers in the spring group. Calculate a 95% confidence interval for the difference between true average fall and spring ACT score.

WORKING
$$28.25-25.88 \pm (1.96)\sqrt{\frac{3.25^2}{80}+\frac{4.59^2}{74}} = 2.37 \pm (1.96)(.6456) = 2.37 \pm 1.265 = (1.10,\ 3.64)$$
With 95% confidence, $1.10<\mu_1-\mu_2<3.64$. The true fall average exceeds the true spring average by between 1.10 and 3.64 points. This makes sense, since students judged less prepared in the fall (by an algebra placement test) were required to take a fall-semester college algebra course before taking Calculus I in the spring, filtering the spring group's incoming preparation differently.

N.B Since the interval (1.10, 3.64) is entirely above 0, this agrees in direction with Example 9.4's test, a test and a CI on the same data agree on direction, they are two views of the same evidence.

-> The final procedure drops the large-sample requirement entirely, at the cost of needing both populations normal with equal variances.

## Pooled Two Sample t Test and Confidence Interval

```
Assumptions

1. X1, X2, ..., Xm is a random sample from a normal population
2. Y1, Y2, ..., Yn is a random sample from a normal population
3. Equal population variances (sigma1^2 = sigma2^2)
```
This is stricter than every procedure above, both populations must be normal and share one variance, so it is meant for small samples where the large-sample Z test does not apply.

### Where the pooled variance comes from (source: user-transcribed, Devore and Berk section 9.2)
Standardizing $\bar{X}-\bar{Y}$ under equal variances gives
$$Z = \frac{\bar{X}-\bar{Y}-(\mu_1-\mu_2)}{\sqrt{\sigma^2\left(\dfrac{1}{m}+\dfrac{1}{n}\right)}}$$
where $\sigma^2$ is the single common population variance. Either $S_1^2$ or $S_2^2$ alone would estimate it, but a better estimator combines both, weighted by the degrees of freedom each sample contributes:
$$S_p^2 = \frac{m-1}{m+n-2}\cdot S_1^2 + \frac{n-1}{m+n-2}\cdot S_2^2$$
The first sample contributes $m-1$ degrees of freedom, the second $n-1$, for a total of $m+n-2$. Replacing $\sigma^2$ with $S_p^2$ changes the distribution from standard normal to $t$ on $m+n-2$ degrees of freedom.

```
Test procedure

H0: mu1 - mu2 = Delta0

t = (Xbar - Ybar - Delta0) / sqrt(Sp^2 * (1/m + 1/n))

Applies when m < 40 and n < 40.
```
$$H_0: \mu_1-\mu_2=\Delta_0 \qquad t = \frac{\bar{X}-\bar{Y}-\Delta_0}{\sqrt{S_p^2\left(\dfrac{1}{m}+\dfrac{1}{n}\right)}}$$

```
Confidence interval

(Xbar - Ybar) +- t(alpha/2, m+n-2) * sqrt(Sp^2 * (1/m + 1/n))

Applies when m < 40 and/or n < 40.
```
$$(\bar{x}-\bar{y}) \pm t_{\alpha/2,(m+n-2)}\sqrt{S_p^2\left(\frac{1}{m}+\frac{1}{n}\right)}$$

> [!warning] Source mismatch: "and" vs "and/or" (common mistake) #common-mistake
> The test procedure's condition slide states $m<40$ **and** $n<40$; the confidence interval's condition slide states $m<40$ **and/or** $n<40$. Both are reproduced exactly as the source presented them. The lecture slides do not reconcile this, so treat it as an open notational inconsistency rather than resolving it silently.

> [!note] When to prefer the two-sample t over the pooled t (source: user-transcribed, section 9.2) #added
> The pooled t test is very sensitive to departures from normality and to unequal variances, it may not give correct results if either assumption fails. One way to check the equal-variance assumption is the F test for variances (section 9.5, not covered in this lecture). In general, the two-sample t test (the non-pooled, unequal-variance version) is safer unless both populations are confidently normal with equal variances. This caution does not appear anywhere in Lecture 7's own slides, only in the textbook section supplying $S_p^2$.

### Example 9.7 (liner tensile strength, no fusion vs fused, composite)
Municipal pipeline networks are increasingly rehabilitated using a flexible liner threaded through the existing pipe. A study on the effect of welding on a high-density polyethylene liner reported tensile strength (psi) both when a fusion process was used and when it was not.

No fusion: 2748, 2700, 2655, 2822, 2511, 3149, 3257, 3213, 3220, 2753. $m=10$, $\bar{x}=2902.8$, $s_1=277.3$.
Fused: 3027, 3356, 3359, 3297, 3125, 2910, 2889, 2902. $n=8$, $\bar{y}=3108.1$, $s_2=205.9$.

Normal probability plots for both groups (shown on the slides) are reasonably linear, supporting normality for both conditions.

WORKING (composite: the source gives the data and plots on slides 17 to 18 but no worked solution; $\alpha=.05$ assumed, not stated in the source)
1. Parameter: $\mu_1-\mu_2$, $\mu_1$ = true average tensile strength without fusion, $\mu_2$ = true average tensile strength with fusion.
2. $H_0:\mu_1-\mu_2=0$
3. $H_a:\mu_1-\mu_2<0$ (testing whether fusion increased strength)
4. $t = \dfrac{\bar{x}-\bar{y}}{\sqrt{S_p^2(1/m+1/n)}}$, $df=m+n-2=16$
5. Lower-tailed, reject if $t\le-t_{.05,16}=-1.746$.
6. $$S_p^2 = \frac{9}{16}(277.3)^2+\frac{7}{16}(205.9)^2 = 43254.0+18547.7 = 61801.7$$
$$t = \frac{2902.8-3108.1}{\sqrt{61801.7(1/10+1/8)}} = \frac{-205.3}{117.9} = -1.74$$
7. Since $-1.74>-1.746$, $t$ falls just short of the rejection region. $H_0$ is not rejected at $\alpha=.05$, though the result is very close to significant.

95% CI for $\mu_1-\mu_2$, same data:
$$-205.3 \pm t_{.025,16}(117.9) = -205.3\pm(2.120)(117.9) = -205.3\pm250.0 = (-455.3,\ 44.7)$$
The interval contains 0, consistent with failing to reject $H_0$, and agrees with the source's own boxplot (slide 19), described there as "not all that clear."

COVERS
Replaces the source's unworked Example 9.7: pooled variance calculation, the test decision, and the matching CI, none of which appear worked in Lecture_7.pdf.

> [!note] Why a difference of two means, and what happens with more than two (added) #added
> See: [[#Why a difference, not a sum, product, or ratio (added)]] above for the sum/product/ratio question. When there are more than two population means to compare, the natural extension is not to run pairwise difference tests for every pair, it is analysis of variance (ANOVA), which tests whether all $k$ means are equal using a single $F$ statistic, a ratio of two variances. This is expected to be the subject of Lecture 9.

## Do not forget
- Variances of $\bar{X}$ and $\bar{Y}$ add under independence, they never subtract, even though the means themselves are subtracted.
- Known variance: $Z$ with $\sigma_1^2/m+\sigma_2^2/n$. Unknown variance, both samples large ($m,n>40$): same $Z$ form with $S_1^2,S_2^2$ substituted.
- Unknown but equal variance, small samples: pooled $t$ on $m+n-2$ df, using $S_p^2$, the degrees-of-freedom-weighted average of $S_1^2$ and $S_2^2$.
- The pooled $t$ test is sensitive to non-normality and unequal variances, prefer the (non-pooled) two-sample $t$ test unless both are confidently satisfied.
- A P-value is the tail area under $H_0$ at least as extreme as the observed statistic; double it for a two-tailed test. Reject $H_0$ if P-value $\le\alpha$.
- The source itself is inconsistent on $m<40$ and $n<40$ versus $m<40$ and/or $n<40$ for the pooled procedures, both quoted as shown, not reconciled.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — the variance-addition step for independent sums, used here for $\bar{X}-\bar{Y}$.
- [[STA01B1_Notes_S3_Statistical_Intervals]] — the $z_{\alpha/2}$ convention and the $n>40$ large-sample threshold for substituting $S$, both carried over directly.
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] — the $t$ distribution itself, used here for the pooled procedure.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] — the seven-step test procedure, the three rejection region forms, and Case I/II for one sample, both extended in this note to two samples.
