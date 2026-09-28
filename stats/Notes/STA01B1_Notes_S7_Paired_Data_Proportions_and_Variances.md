---
module: STA01B1
topic: Paired Data, Two Proportions and Two Variances
session: S7
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Paired Data, Two Proportions and Two Variances (Devore and Berk, Ch 9.3 to 9.5)

Session S6 compared two populations using independent samples (see: [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Setup: assumptions and the distribution of X̄ − Ȳ|Setup: assumptions and the distribution of X̄ − Ȳ]]). This session covers three more comparisons: two measurements on the same unit (paired data), two proportions, and two variances.

## The Paired t Test, Why Pairing Matters

Two tyre types, A and B, are compared for wear. One tyre of each type is mounted on the rear wheels of each car in a study, and the cars are driven a fixed distance before wear is measured. Each car produces one A measurement and one B measurement, five matched pairs, not two independent groups.

```
Car   Tyre A   Tyre B   d = A - B
1     10.6     10.2     0.4
2      9.8      9.4     0.4
3     12.3     11.8     0.5
4      9.7      9.1     0.6
5      8.8      8.3     0.5
```
Tyre A: mean 10.24, variance 1.733. Tyre B: mean 9.76, variance 1.763.

The same five cars, analysed two ways:
```
                        Treated as independent    Treated as paired
Correlation used?       no                        yes (r = 0.998)
degrees of freedom       8                          4
t statistic              0.574                     12.829
P-value (two tail)       0.582                      0.0002
```

> [!warning] Ignoring real pairing hides a real effect #common-mistake
> Same data, opposite conclusions. Treating the two tyres as independent throws away the fact that A and B move together within each car, mostly the same wear factors (car, driver, road) hit both tyres at once, and treats that shared noise as unexplained between-group variability. That inflates the standard error and buries a real, large difference.

Assumptions #definition
```
1. n independently selected pairs (X1, Y1), (X2, Y2), ..., (Xn, Yn)
2. Let Di = Xi - Yi, the differences within pairs
3. The Di's are assumed to be normally distributed with mean value μD and variance σD²
```
Pairing turns two samples into one. Once $D_i = X_i - Y_i$ is formed, every step downstream is a one-sample $t$ problem on $D_1,\dots,D_n$, the same machinery already built for a normal population (see: [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population#The $t$ distribution|The t distribution]]), not a new two-sample method.

Test procedure #formula #exam-flagged
$$H_0: \mu_D = \Delta_0$$
$$t = \frac{\bar{d}-\Delta_0}{s_D/\sqrt{n}}$$
$\bar{d}$ is the sample mean of the differences, $s_D$ their sample standard deviation, $n$ the number of pairs (not $2n$).

> *What pairing does and does not control: it removes whatever varies between subjects but is shared across the two measurements on that subject (driving style, road, load, for the tyres). It does nothing about a factor that differs between the two measurements themselves, and it is not "more accurate" data, it is a better match between the analysis and how the data was actually generated.*

-> Example 9.9 applies this statistic to a full worked problem, then the same reduction to a one-sample structure produces a confidence interval.

## Example 9.9, Applying the Paired t Test #worked-example

A study of musculoskeletal neck-and-shoulder disorders among office staff obtained data from $n=16$ subjects: the proportion of time during which arm elevation was below 30°, measured 18 months apart, with work conditions changed between measurements to include a wider variety of tasks. Does the data suggest true average time below 30° differs after the change? (source, slides 7 to 9)

```
Subject    1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16
Before    81  87  86  82  90  86  96  73  74  75  72  80  66  72  56  82
After     78  91  78  78  84  67  92  70  58  62  70  58  66  60  65  73
Diff       3  -4   8   4   6  19   4   3  16  13   2  22   0  12  -9   9
```
Normal probability plot of the 16 differences is reasonably straight. MINITAB: average 6.75, standard deviation 8.234.

WORKING (alpha = .05 assumed, not stated in source)
1. Parameter: $\mu_D$, true mean difference (Before minus After).
2. $H_0:\mu_D=0$
3. $H_a:\mu_D\ne0$ (two-tailed, "differs")
4. $t=\bar{d}/(s_D/\sqrt{n})$, $df=15$
5. Reject if $|t|\ge t_{.025,15}=2.131$
6. $$t=\frac{6.75}{8.234/\sqrt{16}}=\frac{6.75}{2.0585}=3.28$$
7. Since $3.28>2.131$, reject $H_0$: true average time below 30° differs after the change.

The boxplot shows the box well to the right of zero, and 13 of the 16 differences are positive against 2 negative, consistent with $\mu_D>0$.

-> This same reduction to a one-sample $t$ problem also produces a confidence interval, next.

## Paired t Confidence Interval, Example 9.10 #formula #worked-example

$$\bar{d} \pm t_{\alpha/2,\,n-1}\cdot\frac{s_D}{\sqrt{n}}$$
Requires the differences to be at least approximately normal, checked the same way as the test.

A study timed 13 medical professionals retrieving an image from a slide library and from a digital database, to compare access efficiency. (source, slide 12)
```
Subject    1   2   3   4   5   6   7   8   9  10  11  12  13
Slide     30  35  40  25  20  30  35  62  40  51  25  42  33
Digital   25  16  15  15  10  20   7  16  15  13  11  19  19
Diff       5  19  25  10  10  10  28  46  25  38  14  23  14
```
$\mu_D$ = true mean difference (slide minus digital retrieval time, seconds). MINITAB's normal probability plot supports normality (only 9 points shown, because of ties among the 13 differences).

WORKING (composite: the source gives the data and normality check but no worked interval; alpha = .05 assumed, matching Example 9.9)
$$n=13,\quad \bar{d}=\frac{267}{13}=20.54$$
$$\sum d_i^2 = 7201,\qquad SS=7201-\frac{267^2}{13}=1717.23,\qquad s_D^2=\frac{1717.23}{12}=143.10,\qquad s_D=11.96$$
$$t_{.025,12}=2.179$$
$$20.54\pm(2.179)\frac{11.96}{\sqrt{13}} = 20.54\pm(2.179)(3.318) = 20.54\pm7.23 = (13.31,\ 27.77)$$
With 95% confidence, the true mean difference (slide minus digital) is between about 13.3 and 27.8 seconds. Since the interval lies entirely above 0, slide retrieval takes longer on average, by a practically meaningful amount.

> [!note] Arithmetic correction #added
> This interval was first computed live with $s_D=11.61$, giving $(13.52,\,27.56)$. Recomputing directly from the 13 differences gives $s_D=11.96$ and $(13.31,\,27.77)$. The number above is the corrected one.

Do not forget, paired procedures
- Form $D_i=X_i-Y_i$ first; every step after that is one-sample $t$, not two-sample.
- $n$ is the number of pairs, not the number of individual measurements.
- Ignoring real pairing inflates the standard error and can hide a genuine effect.

-> The next section moves to a genuinely two-sample structure again: two population proportions.

## Difference of Two Proportions, Mean and Variance of p̂1 − p̂2

$$X\sim\text{Bin}(m,p_1),\qquad Y\sim\text{Bin}(n,p_2),\qquad X,Y\text{ independent}$$
$\hat{p}_1=X/m$, $\hat{p}_2=Y/n$, parameter of interest $p_1-p_2$. (source, slide 15)

Proposition #theorem #exam-flagged
$$E(\hat{p}_1-\hat{p}_2)=p_1-p_2$$
$$V(\hat{p}_1-\hat{p}_2)=\frac{p_1(1-p_1)}{m}+\frac{p_2(1-p_2)}{n}$$
The slide defers the proof to textbook page 492 without reproducing it. Short derivation, added:
$$E(\hat{p}_1-\hat{p}_2)=\frac{E(X)}{m}-\frac{E(Y)}{n}=p_1-p_2$$
$$V(\hat{p}_1)=\frac{V(X)}{m^2}=\frac{p_1(1-p_1)}{m},\qquad V(\hat{p}_2)=\frac{p_2(1-p_2)}{n}$$
Independence lets the variances add: $V(\hat{p}_1-\hat{p}_2)=V(\hat{p}_1)+V(\hat{p}_2)$.

A proportion is a sample mean of 0/1 indicators (defined in: [[STA01B1_Notes_S2_Point_Estimation#Point estimate and point estimator|Point estimate and point estimator]]), so this is the means result from [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Setup: assumptions and the distribution of X̄ − Ȳ|Setup: assumptions and the distribution of X̄ − Ȳ]] with $\sigma^2$ replaced by $p(1-p)$.

> *For a mean, the variance $\sigma^2$ is a separate parameter that has to be estimated, and estimating it is where $t$ comes from. For a proportion, the variance is built from $p$ itself, so once $p$ (or an estimate) is known, the variance follows. This is why every proportion procedure below uses $Z$ and never $t$.*

Large-sample condition (source: user-supplied textbook excerpt, not on the slides). Slide 16 says only "Large samples". The textbook states the two-proportion test can safely be used when
$$m\hat{p}_1\ge10,\quad m\hat{q}_1\ge10,\quad n\hat{p}_2\ge10,\quad n\hat{q}_2\ge10,\qquad \hat{q}=1-\hat{p}$$
The matching one-sample condition is $np_0\ge10$ and $n(1-p_0)\ge10$. #struggle

-> Two Proportion z Test, Example 9.11 (below) standardises $\hat{p}_1-\hat{p}_2$ under $H_0:p_1=p_2$.

## Two Proportion z Test, Example 9.11

$$H_0:p_1-p_2=0 \qquad Z=\frac{\hat{p}_1-\hat{p}_2}{\sqrt{\hat{p}\hat{q}\left(\dfrac{1}{m}+\dfrac{1}{n}\right)}},\qquad \hat{p}=\frac{X+Y}{m+n},\ \hat{q}=1-\hat{p}$$
$\hat{p}$ pools both samples into one combined estimate of the common success proportion under $H_0$.

P-value determination (source: user-supplied textbook excerpt), $z$ the computed statistic:
```
Ha: p1 - p2 > 0     P-value = P(Z > z)
Ha: p1 - p2 < 0     P-value = P(Z < z)
Ha: p1 - p2 ≠ 0     P-value = 2 P(Z > |z|)
```

Under $H_0$, $p_1=p_2=p$, so the best estimate of that common $p$ uses all $m+n$ observations, the same idea as the pooled variance $S_p^2$ in [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Pooled Two Sample t Test and Confidence Interval|Pooled Two Sample t Test and Confidence Interval]], except the pooling here follows from $H_0$ itself rather than an equal-variance assumption. The CI in the next section makes no such assumption and does not pool.

Example 9.11 (plea and sentencing, source, slides 17 to 19). Defendants who plead guilty are sentenced without a trial; others plead innocent and are sentenced only if subsequently found guilty. Data are San Francisco County robbery defendants with prior prison records. Does the proportion sent to prison differ between the two groups?
```
                            Plea
                        Guilty      Not Guilty
Number judged guilty     m = 191      n = 64
Number sent to prison    x = 101      y = 56
Sample proportion        p̂1 = .529    p̂2 = .875
```

WORKING (source, slides 18 to 19; level .01)
1. Parameters: $p_1,p_2$, true proportions sent to prison in each plea group.
2. $H_0:p_1-p_2=0$
3. $H_a:p_1-p_2\ne0$
4. $Z=(\hat{p}_1-\hat{p}_2)/\sqrt{\hat{p}\hat{q}(1/m+1/n)}$
5. $\alpha/2=.005$, $z_{.005}=2.58$. Reject if $z\ge2.58$ or $z\le-2.58$.
6. $$\hat{p}=\frac{101+56}{191+64}=.616,\quad \hat{q}=.384$$
$$z=\frac{.529-.875}{\sqrt{(.616)(.384)(1/191+1/64)}}=\frac{-.346}{.070}=-4.94$$
7. Since $-4.94\le-2.58$, reject $H_0$.

$$\text{P-value}=2[1-\Phi(|z|)]=2[1-\Phi(4.94)]<2[1-\Phi(3.49)]=.0004$$

> [!note] Where 3.49 comes from #added
> The printed standard normal table stops at $z=3.49$. Since $\Phi$ is increasing, $\Phi(4.94)>\Phi(3.49)$, so $1-\Phi(4.94)<1-\Phi(3.49)$, giving an upper bound of .0004 on the two-tailed P-value, already far below any reasonable $\alpha$. A more extensive table gives the actual value, about .0000006. The bound proves the P-value is small enough to reject; it is not itself a measurement of how small.

The data strongly suggest $p_1\ne p_2$: initially pleading guilty may be a good strategy for avoiding prison. The cited study found the same pattern across county, crime type, and prior record.

> [!warning] Example 9.11 fails the textbook's own validity check #common-mistake #struggle
> $m\hat{p}_1=101$, $m\hat{q}_1=90$, $n\hat{p}_2=56$, $n\hat{q}_2=64(.125)=8$. Three of four counts clear 10, but $n\hat{q}_2=8$ does not. The slides make no comment on this. With $z=-4.94$ the conclusion is not remotely in doubt, but it is a genuine inconsistency between the lecture's own worked example and the validity condition, unresolved pending the lecturer's answer.

-> The confidence interval for $p_1-p_2$ does not pool, and is worked next.

## Confidence Interval for p1 − p2, Example 9.13 #formula

$$\hat{p}_1-\hat{p}_2 \pm z_{\alpha/2}\sqrt{\frac{\hat{p}_1\hat{q}_1}{m}+\frac{\hat{p}_2\hat{q}_2}{n}}$$
No pooled $\hat{p}$: the test pools because $H_0$ asserts $p_1=p_2$, but an interval makes no such claim, its job is to estimate how far apart $p_1$ and $p_2$ actually are. Each sample keeps its own $\hat{p}$ and $\hat{q}$, the same pattern as the pooled $t$ needing equal variances while the large-sample $Z$ interval in S6 did not.

Example 9.13 (chemotherapy vs chemotherapy plus radiation, source, slides 21 to 22). Comparing 15-year survival after chemotherapy alone (76 of 154 survived) versus chemotherapy plus radiation (98 of 164 survived). $\hat{p}_1=76/154=.494$, $\hat{p}_2=98/164=.598$.

WORKING (source, slide 22), 99% CI, $z_{.005}=2.58$:
$$.494-.598 \pm (2.58)\sqrt{\frac{(.494)(.506)}{154}+\frac{(.598)(.402)}{164}} = -.104\pm.143 = (-.247,\ .039)$$
At 99% confidence, $-.247<p_1-p_2<.039$. The interval is wide, reflecting sample sizes that are not large for this type of interval, and it contains 0, so neither treatment can be judged superior. Since 0 is inside a 99% interval, a two-tailed test at the matching $\alpha=.01$ would not reject, agreeing with the interval.

Validity check (added, no lecture condition given for the CI): $m\hat{p}_1=76$, $m\hat{q}_1=78$, $n\hat{p}_2=98$, $n\hat{q}_2=66$, all above 10.

-> The F distribution and the test for two variances close this session.

## The F Distribution and the Test for Two Population Variances, Example 9.14

Theorem #theorem #exam-flagged (source, slide 23). $X_1,\dots,X_m$ a random sample from a normal population with variance $\sigma_1^2$; $Y_1,\dots,Y_n$ an independent random sample from a normal population with variance $\sigma_2^2$; $S_1^2,S_2^2$ the sample variances. Then
$$F=\frac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2}$$
has an $F$ distribution with $df_1=m-1$, $df_2=n-1$.

> [!warning] Normality matters more here than anywhere else this module #common-mistake
> Both populations must be normal; the F test is much more sensitive to non-normality than any t test in this module. Slide 25 stresses this, and Example 9.14 checks a normal plot before anything else.

Test procedure #formula (source, slide 24)
$$H_0:\sigma_1^2=\sigma_2^2 \qquad f=\frac{s_1^2}{s_2^2}$$
Under $H_0$ the two variances cancel in the theorem's ratio, leaving a statistic with no unknown parameter.

Rejection regions (added, standard forms matching how Example 9.14 uses them)
```
Ha: σ1² > σ2²    reject if f ≥ F(α, m-1, n-1)
Ha: σ1² < σ2²    reject if f ≤ F(1-α, m-1, n-1)
Ha: σ1² ≠ σ2²    reject if f ≥ F(α/2, m-1, n-1) or f ≤ F(1-α/2, m-1, n-1)
```
Tables list only upper-tail values; a lower-tail value uses the reciprocal rule, with the degrees of freedom swapped:
$$F_{1-\alpha,\,\nu_1,\,\nu_2}=\frac{1}{F_{\alpha,\,\nu_2,\,\nu_1}}$$

Example 9.14 (baked goods weight, source, slides 25 to 26). Bagel weights (grams): 99.8, 105.4, 94.7, 107.8, 114.3, 106.3 ($m=6$, mean 104.7, sd 6.765). Muffin weights: 99.0, 98.2, 98.1, 102.1, 102.9, 104.1, 98.8, 99.5 ($n=8$, mean 100.3, sd 2.338). A normal plot shows no reason to doubt normality; the two groups' plotted slopes differ visibly, consistent with different variability, since the slope is the reciprocal of the standard deviation when score (z-score) is plotted against grams.

$$f=\frac{s_1^2}{s_2^2}=\frac{6.765^2}{2.338^2}=8.37,\qquad df=(5,7)$$

Version A, the slide's working, $\alpha=.02$ (source, slide 26)
$$F_{.01,5,7}=7.46,\qquad F_{.99,5,7}=\frac{1}{F_{.01,7,5}}=\frac{1}{10.46}=.0956$$
Reject if $f\ge7.46$ or $f\le.0956$. Since $8.37\ge7.46$, reject $H_0$: there is a difference in weight variation, and the muffins are less variable.

Version B, the lecture's illustration, $\alpha=.10$ (source: lecture, confirmed by the user against their textbook table). The lecture's own printed table had no .01 column, so the example was finished at $\alpha=.10$ (the .05 column) to show how it would work.
$$F_{.05,5,7}=3.97$$
Since $8.37\ge3.97$, reject $H_0$, the same conclusion.

The shortcut (source, slide 26, not only a lecturer convention) #exam-flagged
It is not necessary to use the lower-tail critical value if the group with the larger variance is put on top, so $f\ge1$ and the only comparison needed is with the upper critical value. This does not change the result, so it is not cheating to simplify the test this way.
```
1. Put the larger sample variance on top, so f >= 1.
2. Numerator df = (sample size of the group on top) - 1
   Denominator df = (sample size of the group on the bottom) - 1
3. Two-tailed test: compare f only with F(α/2, df_top, df_bottom).
4. Reject H0 if f is at least that value.
```
In Example 9.14 the bagels already have the larger variance, so no swap is needed.

> *Checking the orientation cannot change the answer: with the muffins on top instead, $f'=2.338^2/6.765^2=.1195$ with $df=(7,5)$, and $F_{.01,7,5}=10.46$, $F_{.99,7,5}=1/7.46=.134$. Since $.1195\le.134$, reject again, same conclusion. The degrees of freedom and critical values both change when the orientation flips, which is why the shortcut has to carry the df swap with the variance swap.*

> *On exam marking (unconfirmed with the lecturer): if the setup, orientation, degrees of freedom, and substitution are all correct but the table value or $\alpha$ is read wrong, the working still shows understanding and should cost at most one mark, provided the final decision follows correctly from the (wrong) number written down, not from the right answer known in advance.*

Reference (source, slide 27): Chapter 9, sections 9.3 to 9.5.

Do not forget, F test
- Larger sample variance on top; its group's sample size minus 1 is the numerator df.
- Two-tailed: use $F_{\alpha/2}$, not $F_\alpha$.
- One-sided $H_a$: do not swap, let the direction of $H_a$ fix the orientation and use $F_\alpha$.
- Requires both populations normal; check a normal plot first.
- The group with the larger variance is the more variable one; a rejection can be read directly.

## The n > 30 vs n > 40 Threshold, a Running Reference

Both numbers gate the same move, using $S$ in place of an unknown $\sigma$, and the underlying calculation does not change between them, only the label attached to the statistic, the table read, and the stated justification. #struggle

| Procedure | Session | Cutoff as stated in the source | Statistic |
|---|---|---|---|
| One-sample large-sample test for a mean | S5, Lecture 5 slide 9 | $n>30$ | $Z=(\bar{X}-\mu_0)/(S/\sqrt{n})$ |
| One-sample large-sample CI for a mean | S3 | $n>40$ | $\bar{x}\pm z_{\alpha/2}\,s/\sqrt{n}$ |
| Two-sample large-sample test for $\mu_1-\mu_2$ | S6, Lecture 7 slide 3 | $m>40$ and $n>40$ | $Z=(\bar{X}-\bar{Y}-\Delta_0)/\sqrt{S_1^2/m+S_2^2/n}$ |
| Two-sample large-sample CI for $\mu_1-\mu_2$ | S6, Lecture 7 slide 4 | $m>40$ and $n>40$ | $\bar{x}-\bar{y}\pm z_{\alpha/2}\sqrt{s_1^2/m+s_2^2/n}$ |
| Pooled two-sample $t$ test | S6, Lecture 7 slide 6 | $m<40$ and $n<40$ | $t=(\bar{X}-\bar{Y}-\Delta_0)/\sqrt{S_p^2(1/m+1/n)}$ |
| Pooled two-sample $t$ CI | S6, Lecture 7 slide 7 | $m<40$ and/or $n<40$ | as above, $\pm t_{\alpha/2,m+n-2}$ |
| Paired $t$ test and CI | S7, Lecture 8 | none stated; needs $D_i$ approximately normal | $t=(\bar{d}-\Delta_0)/(s_D/\sqrt{n})$ |
| Two-proportion $z$ test | S7, Lecture 8 slide 16 | none stated ("Large samples" only); textbook: all of $m\hat{p}_1,m\hat{q}_1,n\hat{p}_2,n\hat{q}_2\ge10$ | $Z=(\hat{p}_1-\hat{p}_2)/\sqrt{\hat{p}\hat{q}(1/m+1/n)}$ |
| Two-proportion $z$ CI | S7, Lecture 8 slide 20 | none stated | $\hat{p}_1-\hat{p}_2\pm z_{\alpha/2}\sqrt{\hat{p}_1\hat{q}_1/m+\hat{p}_2\hat{q}_2/n}$ |
| $F$ test for two variances | S7, Lecture 8 | none; exact under normality, no sample-size rule | $f=s_1^2/s_2^2$ |

> [!note] The 30 vs 40 split is an unreconciled source inconsistency #common-mistake #struggle
> The vault's S3 and S4 material gives a reason for 40 (substituting $S$ for $\sigma$ adds variability beyond what the CLT alone handles), and that reasoning is sound. What it does not explain is why the S5 test slide still says 30 while the CI and every two-sample large-sample slide say 40. Nothing in the source reconciles this, and it is one of four items in a clarification email drafted this session, pending the lecturer's answer. Until then, use whichever cutoff the specific procedure's own slide states, not a single number applied everywhere.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — the variance-addition step for independent sums, used here for $\hat{p}_1-\hat{p}_2$.
- [[STA01B1_Notes_S2_Point_Estimation]] — $\hat{p}$ as $\bar{X}$ of 0/1 indicators, why proportion procedures parallel mean procedures.
- [[STA01B1_Notes_S3_Statistical_Intervals]] — the one-sample proportion CI and its $n>10$ validity condition, extended here to two samples.
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] — the one-sample $t$ machinery that the paired test reduces to.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] — the seven-step test procedure and the $n>30$ large-sample cutoff, contrasted with $n>40$ above.
- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]] — the two-sample mean fork (known variance, large-sample, pooled $t$) that this session's proportion and variance forks parallel.
