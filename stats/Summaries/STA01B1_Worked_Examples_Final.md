# STA01B1 Final, worked examples for phone use (Mon 9 Nov, 08:30)

Twenty-seven fully worked examples, one for each calculation type in scope. Examples 1 to 15 are Part 1; Examples 16 to 27 (Part 2) cover the types that Part 1 missed. The numbers are new, so nothing here is from Set C. Every example follows Dr H's order: **formula, substitute, simplify, interpret**. Every interpretation is in plain words.

Table values used (check each one against the table you are given on the day): $z_{0.025}=1.96$, $z_{0.05}=1.645$, $z_{0.10}=1.28$, $t_{0.025,15}=2.131$, $t_{0.025,20}=2.086$, $t_{0.025,7}=2.365$, $\chi^2_{0.05,3}=7.815$, $\chi^2_{0.05,2}=5.991$, $F_{0.05,2,12}=3.89$, $Q_{0.05,3,12}=3.77$, $t_{0.025,20}=2.086$, $F_{0.025,10,8}=4.30$, $F_{0.025,8,10}=3.85$, $\chi^2_{0.025,14}=26.12$, $\chi^2_{0.975,14}=5.63$.

Reminders: the standard error of $\bar x$ is $\frac{\sigma}{\sqrt n}$, never $\frac{\sigma}{n}$. Reject when $p\le\alpha$. Round sample sizes **up**.

## Contents

- [[#Example 1. Sampling distribution of the sample mean and the total]] probability for the sample mean, mean and sd of the total
- [[#Example 2. Checking whether an estimator is unbiased]] expected value check and variance comparison
- [[#Example 3. Confidence interval for a mean, sigma unknown]] t interval from a small sample
- [[#Example 4. Confidence interval for a proportion]] interval for a proportion
- [[#Example 5. Pooled t confidence interval for two means]] interval for the difference of two means, equal variances
- [[#Example 6. Paired t test]] test on paired differences
- [[#Example 7. Type I and Type II error from a given rejection region]] alpha and beta from a given rejection rule
- [[#Example 8. Finding the cut-off and beta from alpha, upper-tailed]] cut-off and beta for an upper-tailed test
- [[#Example 9. Sample size from alpha and beta for a mean]] n from alpha and beta for a mean
- [[#Example 10. Type II error for a proportion]] beta for a proportion
- [[#Example 11. Sample size for a confidence interval]] n for a given width or margin of error
- [[#Example 12. ANOVA and Tukey]] F test, then Tukey with the underlined means
- [[#Example 13. Chi-square goodness of fit]] testing a 9 3 3 1 ratio
- [[#Example 14. Chi-square test of independence]] two-way table, expected counts and conclusion
- [[#Example 15. Regression printout, interpretation and prediction]] slope, R squared, prediction and extrapolation
- [[#Part 2, the types that were missing]] examples 16 to 27, the types Part 1 did not cover
  - [[#Example 16. Pooled t test for two means]] two-sided test with the pooled variance
  - [[#Example 17. z test and interval for two means, large samples]] large-sample test and interval
  - [[#Example 18. Two-proportion z test and interval]] pooled test, unpooled interval
  - [[#Example 19. F test for two variances]] two-sided test, upper and lower critical values
  - [[#Example 20. Confidence interval for a mean with sigma known, and a bound]] z interval, upper bound, link to a lower-tailed claim
  - [[#Example 21. Confidence interval for a variance]] interval for the variance and the standard deviation
  - [[#Example 22. Prediction interval for one new value]] between, at most and at least wording
  - [[#Example 23. Sample size from alpha and beta for a proportion]] n from alpha and beta for a proportion
  - [[#Example 24. Two-sided beta and the sample size]] rejection region, beta and n for a two-sided test
  - [[#Example 25. Numerical bias and MSE]] bias and mean squared error of two estimators
  - [[#Example 26. The Central Limit Theorem with a non-normal population]] normal probability for a large sample from a skewed population
  - [[#Example 27. Reading a p-value]] lower, two-sided and upper p-values and decisions

---

## Example 1. Sampling distribution of the sample mean and the total
**Question.** Packets have mean mass $\mu=250$ g and standard deviation $\sigma=12$ g. A random sample of $n=36$ packets is taken. (a) Find $P(248\le\bar X\le253)$. (b) Find the mean and standard deviation of the total mass $T_0$.

**Working.**
Standard error: $\sigma_{\bar X}=\frac{\sigma}{\sqrt n}=\frac{12}{\sqrt{36}}=\frac{12}{6}=2$ g. Here $n=36<40$, so we need the population to be normal (assume it is).

(a)
$$P(248\le\bar X\le253)=P\!\left(\frac{248-250}{2}\le Z\le\frac{253-250}{2}\right)=P(-1\le Z\le1.5)$$
$$=\Phi(1.5)-\Phi(-1)=0.9332-0.1587=0.7745$$

(b)
$$E(T_0)=n\mu=36(250)=9000\text{ g},\qquad \sigma_{T_0}=\sqrt n\,\sigma=6(12)=72\text{ g}$$

**In words.** About 77% of random samples of 36 packets will have an average mass between 248 g and 253 g. The total mass of 36 packets is typically 9000 g, give or take 72 g.

---

## Example 2. Checking whether an estimator is unbiased
**Question.** $X_1,X_2,X_3$ is a random sample with mean $\mu$ and variance $\sigma^2$. Is $\hat\theta=\frac{X_1+2X_2+3X_3}{6}$ unbiased for $\mu$? Compare it with $\bar X$.

**Working.**
$$E(\hat\theta)=\frac{E(X_1)+2E(X_2)+3E(X_3)}{6}=\frac{\mu+2\mu+3\mu}{6}=\frac{6\mu}{6}=\mu$$
So $\hat\theta$ is unbiased. The observations are independent, so constants come out squared:
$$V(\hat\theta)=\frac{V(X_1)+4V(X_2)+9V(X_3)}{36}=\frac{14\sigma^2}{36}=\frac{7\sigma^2}{18}$$
$$V(\bar X)=\frac{\sigma^2}{3}=\frac{6\sigma^2}{18}$$

**In words.** Both estimators are correct on average, but $\bar X$ has the smaller variance ($\frac{6}{18}<\frac{7}{18}$), so it is the better estimator because it is more likely to land close to $\mu$.

---

## Example 3. Confidence interval for a mean, sigma unknown
**Question.** A sample of $n=16$ gives $\bar x=52.4$ and $s=6.8$. Assuming a normal population, find a 95% confidence interval for $\mu$.

**Working.** $df=n-1=15$, so $t_{0.025,15}=2.131$.
$$\bar x\pm t_{\alpha/2,n-1}\frac{s}{\sqrt n}=52.4\pm2.131\cdot\frac{6.8}{\sqrt{16}}=52.4\pm2.131(1.7)=52.4\pm3.62$$
$$(48.78,\ 56.02)$$

**In words.** We are 95% confident that the true population mean lies between 48.78 and 56.02.

---

## Example 4. Confidence interval for a proportion
**Question.** In a random sample of 200 customers, 56 said they would buy the product. Find a 95% confidence interval for the true proportion $p$ of all customers who would buy.

**Working.** $\hat p=\frac{56}{200}=0.28$ and $\hat q=1-\hat p=0.72$.
$$\hat p\pm z_{\alpha/2}\sqrt{\frac{\hat p\hat q}{n}}=0.28\pm1.96\sqrt{\frac{0.28(0.72)}{200}}=0.28\pm1.96(0.03175)=0.28\pm0.062$$
$$(0.218,\ 0.342)$$

**In words.** We are 95% confident that between 21.8% and 34.2% of all customers would buy the product.

---

## Example 5. Pooled t confidence interval for two means
**Question.** Supplier A: $m=12$, $\bar x=30.5$, $s_1^2=9$. Supplier B: $n=10$, $\bar y=27.8$, $s_2^2=11$. Assume normal populations with equal variances. Find a 95% confidence interval for $\mu_1-\mu_2$.

**Working.** Pooled variance:
$$s_p^2=\frac{(m-1)s_1^2+(n-1)s_2^2}{m+n-2}=\frac{11(9)+9(11)}{20}=\frac{198}{20}=9.9,\qquad s_p=3.146$$
$df=m+n-2=20$, so $t_{0.025,20}=2.086$.
$$(\bar x-\bar y)\pm t_{\alpha/2,m+n-2}\,s_p\sqrt{\frac1m+\frac1n}=2.7\pm2.086(3.146)\sqrt{\frac1{12}+\frac1{10}}=2.7\pm2.086(1.347)=2.7\pm2.81$$
$$(-0.11,\ 5.51)$$

**In words.** We are 95% confident that Supplier A's true mean is between 0.11 lower and 5.51 higher than Supplier B's. The interval contains 0, so at the 5% level there is not sufficient evidence of a difference between the two suppliers' means.

---

## Example 6. Paired t test
**Question.** Eight workers are timed before and after training. The differences (before minus after) have $\bar d=2.6$ and $s_d=2.4$. Test at the 5% level whether training reduces the mean time (that is, $\mu_D>0$). Assume the differences are normal.

**Working.** The same workers are measured twice, so we work with the differences. $H_0:\mu_D=0$ against $H_a:\mu_D>0$. $df=n-1=7$, so the critical value is $t_{0.05,7}=1.895$.
$$t=\frac{\bar d-0}{s_d/\sqrt n}=\frac{2.6}{2.4/\sqrt8}=\frac{2.6}{0.8485}=3.06$$
Since $3.06>1.895$, reject $H_0$.

**In words.** At the 5% level there is sufficient evidence that training reduces the mean time. Training shortens the time by 2.6 on average, and the data show this is more than chance. (A two-sided 95% interval for $\mu_D$ is $2.6\pm2.365(0.8485)=(0.59,\ 4.61)$, which does not contain 0, so it agrees.)

---

## Example 7. Type I and Type II error from a given rejection region
**Question.** Test $H_0:\mu=100$ against $H_a:\mu>100$ with $\sigma=15$ and $n=25$. The rule is: reject $H_0$ if $\bar x>105$. (a) Find $\alpha$. (b) Find $\beta$ when the true mean is $\mu'=108$.

**Working.** Standard error: $\frac{15}{\sqrt{25}}=3$.

(a) $\alpha$ is the chance of rejecting when $H_0$ is true ($\mu=100$):
$$\alpha=P(\bar X>105\mid\mu=100)=P\!\left(Z>\frac{105-100}{3}\right)=P(Z>1.67)=1-0.9525=0.0475$$

(b) $\beta$ is the chance of **not** rejecting when the true mean is $108$:
$$\beta(108)=P(\bar X\le105\mid\mu=108)=P\!\left(Z\le\frac{105-108}{3}\right)=P(Z\le-1)=0.1587$$

**In words.** If the true mean really is 100, this rule wrongly rejects about 4.75% of the time. If the true mean is 108, the rule misses it (fails to reject) about 15.9% of the time.

---

## Example 8. Finding the cut-off and beta from alpha, upper-tailed
**Question.** Test $H_0:\mu=40$ against $H_a:\mu>40$ with $\sigma=8$, $n=25$ and $\alpha=0.05$. (a) Give the rejection region in terms of $\bar x$. (b) Find $\beta(43)$.

**Working.** Standard error: $\frac{8}{\sqrt{25}}=1.6$.

(a) The $\alpha$ condition puts the cut-off $c$ at $z_{0.05}=1.645$ standard errors above $\mu_0$:
$$c=\mu_0+z_\alpha\frac{\sigma}{\sqrt n}=40+1.645(1.6)=42.63$$
Reject $H_0$ if $\bar x>42.63$.

(b)
$$\beta(43)=P(\bar X\le42.63\mid\mu=43)=P\!\left(Z\le\frac{42.63-43}{1.6}\right)=P(Z\le-0.23)=0.4090$$

**In words.** If the true mean is 43, this test misses the increase about 41% of the time.

---

## Example 9. Sample size from alpha and beta for a mean
**Question.** Same test as Example 8 ($H_0:\mu=40$, $H_a:\mu>40$, $\sigma=8$, $\alpha=0.05$). How large must $n$ be so that $\beta(43)=0.10$?

**Working.** The cut-off $c$ must satisfy both conditions:
$$c=\mu_0+z_\alpha\frac{\sigma}{\sqrt n}\quad(\alpha),\qquad c=\mu'-z_\beta\frac{\sigma}{\sqrt n}\quad(\beta)$$
Set them equal: $40+1.645\frac{8}{\sqrt n}=43-1.28\frac{8}{\sqrt n}$. Collect the $\frac{8}{\sqrt n}$ terms:
$$(1.645+1.28)\frac{8}{\sqrt n}=3\quad\Rightarrow\quad\sqrt n=\frac{8(2.925)}{3}=7.80\quad\Rightarrow\quad n=60.8$$
(With more decimals, $n=60.9$.) Round **up**: $n=61$.

**In words.** At least 61 observations are needed so that the test has a 5% chance of a false alarm and only a 10% chance of missing a true mean of 43.

---

## Example 10. Type II error for a proportion
**Question.** Test $H_0:p=0.30$ against $H_a:p>0.30$ with $n=120$ and $\alpha=0.05$. Find the probability of a Type II error when the true proportion is $p'=0.40$.

**Working.** Under $H_0$: standard error $\sqrt{\frac{0.3(0.7)}{120}}=0.0418$.
$$c=p_0+z_\alpha\sqrt{\frac{p_0q_0}{n}}=0.30+1.645(0.0418)=0.3688$$
Reject $H_0$ if $\hat p>0.3688$. Under the true value, standard error $\sqrt{\frac{0.4(0.6)}{120}}=0.0447$:
$$\beta(0.40)=P(\hat p\le0.3688\mid p=0.40)=P\!\left(Z\le\frac{0.3688-0.40}{0.0447}\right)=P(Z\le-0.70)=0.2420$$

**In words.** If the true proportion is 40%, the test fails to detect that it is above 30% about 24% of the time. Note that the standard error changes from $H_0$ to the true value.

---

## Example 11. Sample size for a confidence interval
**Question.** (a) $\sigma=10$. How large must $n$ be so that a 95% confidence interval for $\mu$ has a width of at most 4? (b) How large must $n$ be to estimate a proportion to within 0.05 with 95% confidence if no estimate of $p$ is available?

**Working.**
(a) A width of 4 means the half-width is $E=2$.
$$n=\left(\frac{z_{\alpha/2}\,\sigma}{E}\right)^2=\left(\frac{1.96(10)}{2}\right)^2=(9.8)^2=96.04\ \Rightarrow\ n=97$$

(b) No estimate means we use $\hat p=0.5$ (the worst case):
$$n=\frac{z_{\alpha/2}^2\,\hat p\hat q}{E^2}=\frac{(1.96)^2(0.5)(0.5)}{(0.05)^2}=\frac{0.9604}{0.0025}=384.16\ \Rightarrow\ n=385$$

**In words.** (a) We need at least 97 observations for the 95% interval to be no wider than 4. (b) We need at least 385 people to be 95% confident that the sample proportion is within 0.05 of the true proportion, whatever that proportion is. Round up, always, because rounding down would leave the interval slightly too wide. "Within" means half-width $E$; "width" means $2E$.

---

## Example 12. ANOVA and Tukey
**Question.** Three fertilisers ($I=3$) are each used on $J=5$ plots. The sample means are $12$, $15$ and $19$, and $MSE=6$. Test at the 5% level whether the mean yields are equal. If not, use Tukey's procedure.

**Working.** $H_0:\mu_1=\mu_2=\mu_3$ against $H_a$: at least two means differ. Grand mean: $\bar x_{\cdot\cdot}=\frac{12+15+19}{3}=15.33$.
$$SSTr=J\sum(\bar x_{i\cdot}-\bar x_{\cdot\cdot})^2=5\left[(12-15.33)^2+(15-15.33)^2+(19-15.33)^2\right]=5(24.67)=123.3$$
Degrees of freedom: treatments $I-1=2$, error $I(J-1)=12$, total $IJ-1=14$.
$$MSTr=\frac{123.3}{2}=61.67,\qquad F=\frac{MSTr}{MSE}=\frac{61.67}{6}=10.28$$
Critical value $F_{0.05,2,12}=3.89$. Since $10.28>3.89$, reject $H_0$.

Tukey (only because we rejected): the second subscript of $Q$ is $I$, the third is the error df.
$$w=Q_{0.05,3,12}\sqrt{\frac{MSE}{J}}=3.77\sqrt{\frac65}=3.77(1.095)=4.13$$
Differences between means: $15-12=3<4.13$ (not significant); $19-15=4<4.13$ (not significant); $19-12=7>4.13$ (significant).

Order the means and join those not significantly different:
$$\underline{12\quad\ 15}\qquad\quad\underline{15\quad\ 19}$$

**In words.** At the 5% level there is sufficient evidence that at least two fertiliser means differ. Fertiliser 1 and Fertiliser 3 differ significantly. Fertiliser 2 cannot be separated from either of the others, which is not the same as saying it is equal to them.

---

## Example 13. Chi-square goodness of fit
**Question.** A breeding theory says offspring appear in the ratio $9:3:3:1$. In a sample of $n=160$ the counts are $85,\ 33,\ 28,\ 14$. Test the theory at the 5% level.

**Working.** $H_0$: the proportions are $\frac9{16},\frac3{16},\frac3{16},\frac1{16}$. $H_a$: at least one proportion is different.
Expected counts under $H_0$, $E_i=n\,p_{i0}$: $90,\ 30,\ 30,\ 10$. All are at least 5, so the test is valid.
$$\chi^2=\sum\frac{(O-E)^2}{E}=\frac{(85-90)^2}{90}+\frac{(33-30)^2}{30}+\frac{(28-30)^2}{30}+\frac{(14-10)^2}{10}$$
$$=0.278+0.300+0.133+1.600=2.31$$
$df=k-1=4-1=3$, so the critical value is $\chi^2_{0.05,3}=7.815$. Since $2.31<7.815$, do not reject $H_0$.

**In words.** At the 5% level there is not sufficient evidence that the offspring ratio differs from $9:3:3:1$.

---

## Example 14. Chi-square test of independence
**Question.** 150 people were classified by gender and by preferred brand (A, B, C). Test at the 5% level whether brand preference is independent of gender.

| | Brand A | Brand B | Brand C | Total |
|---|---|---|---|---|
| Female | 30 | 20 | 10 | 60 |
| Male | 20 | 30 | 40 | 90 |
| Total | 50 | 50 | 50 | 150 |

**Working.** $H_0$: gender and brand preference are independent. $H_a$: they are not independent.
Expected count $=\frac{\text{row total}\times\text{column total}}{n}$. Female: $\frac{60\times50}{150}=20$ in each column. Male: $\frac{90\times50}{150}=30$ in each column. All are at least 5.
$$\chi^2=\frac{(30-20)^2}{20}+\frac{(20-20)^2}{20}+\frac{(10-20)^2}{20}+\frac{(20-30)^2}{30}+\frac{(30-30)^2}{30}+\frac{(40-30)^2}{30}$$
$$=5+0+5+3.33+0+3.33=16.67$$
$df=(I-1)(J-1)=(2-1)(3-1)=2$, so the critical value is $\chi^2_{0.05,2}=5.991$. Since $16.67>5.991$, reject $H_0$.

**In words.** At the 5% level there is sufficient evidence that brand preference depends on gender. Women lean toward Brand A and men toward Brand C.

---

## Example 15. Regression printout, interpretation and prediction
**Question.** Exam mark $y$ (%) is regressed on study hours $x$ for 20 students whose study hours ranged from 2 to 14. The printout gives:

```
Predictor   Coef    SE Coef   T      P
Constant    41.2    3.1       13.3   0.000
Hours       3.45    0.51      6.70   0.000

R-Sq = 71.4%
```

(a) Test whether there is a linear relationship. (b) Interpret the slope. (c) Interpret $R^2$. (d) Predict the mark for 10 hours. (e) Can we predict for 20 hours?

**Working.**
(a) $H_0:\beta_1=0$ against $H_a:\beta_1\ne0$. The $p$-value is $0.000\le0.05$, so reject $H_0$. (Also $F=t^2=6.70^2=44.9$.)

(b) For each additional hour of study, the exam mark increases by 3.45 percentage points on average.

(c) 71.4% of the variation in exam marks is explained by the linear relationship with study hours. The percentage **not** explained is $100\%-71.4\%=28.6\%$.

(d) $\hat y=41.2+3.45(10)=41.2+34.5=75.7$. Ten hours is inside the data range (2 to 14), so the prediction is allowed. The predicted mark is about 75.7%.

(e) No. 20 hours is outside the range of the data (2 to 14), so this is extrapolation and the line cannot be trusted there.

**In words.** There is sufficient evidence of a linear relationship between study hours and exam mark at the 5% level, and the more hours a student studies, the higher the predicted mark, within the range of the data.

---

# Part 2, the types that were missing

## Example 16. Pooled t test for two means
**Question.** Method A: $m=10$, $\bar x=78.4$, $s_1=6.1$. Method B: $n=12$, $\bar y=72.9$, $s_2=5.5$. Assume normal populations with equal variances. Test at the 5% level whether the two methods have different mean scores.

**Working.** $H_0:\mu_1-\mu_2=0$ against $H_a:\mu_1-\mu_2\ne0$ (two-sided). Pooled variance:
$$s_p^2=\frac{(m-1)s_1^2+(n-1)s_2^2}{m+n-2}=\frac{9(37.21)+11(30.25)}{20}=\frac{667.6}{20}=33.38,\qquad s_p=5.778$$
$$t=\frac{(\bar x-\bar y)-0}{s_p\sqrt{\frac1m+\frac1n}}=\frac{5.5}{5.778\sqrt{\frac1{10}+\frac1{12}}}=\frac{5.5}{5.778(0.4282)}=\frac{5.5}{2.474}=2.22$$
$df=m+n-2=20$, two-sided critical value $t_{0.025,20}=2.086$. Since $2.22>2.086$, reject $H_0$.

**In words.** At the 5% level there is sufficient evidence that the two methods have different mean scores, and Method A's mean is higher. The $p$-value is about 0.04: if the two true means were equal, a difference this large (in either direction) would happen only about 4% of the time.

---

## Example 17. z test and interval for two means, large samples
**Question.** Group 1: $m=50$, $\bar x=104.2$, $s_1=9.5$. Group 2: $n=60$, $\bar y=100.1$, $s_2=11.2$. Both samples are larger than 40, so the sample variances can stand in for the population variances. (a) Test $H_0:\mu_1-\mu_2=0$ against $H_a:\mu_1-\mu_2\ne0$ at the 5% level. (b) Find a 95% confidence interval for $\mu_1-\mu_2$.

**Working.** Standard error:
$$\sqrt{\frac{s_1^2}{m}+\frac{s_2^2}{n}}=\sqrt{\frac{90.25}{50}+\frac{125.44}{60}}=\sqrt{1.805+2.091}=1.974$$

(a)
$$z=\frac{(\bar x-\bar y)-0}{1.974}=\frac{4.1}{1.974}=2.08$$
Critical value $z_{0.025}=1.96$. Since $2.08>1.96$, reject $H_0$. ($p$-value $=2(1-0.9812)=0.0376\le0.05$.)

(b)
$$(\bar x-\bar y)\pm z_{0.025}(1.974)=4.1\pm1.96(1.974)=4.1\pm3.87=(0.23,\ 7.97)$$

**In words.** At the 5% level there is sufficient evidence that the two group means differ. The $p$-value of 0.0376 means that if the two true means were equal, a difference this large (in either direction) would happen only about 3.8% of the time. We are 95% confident that Group 1's true mean is between 0.23 and 7.97 higher than Group 2's. The interval does not contain 0, which agrees with the test.

---

## Example 18. Two-proportion z test and interval
**Question.** Town A: $54$ of $m=150$ households recycle. Town B: $50$ of $n=200$ households recycle. (a) Test at the 5% level whether the proportion is higher in Town A. (b) Find a 95% confidence interval for $p_1-p_2$. Assume the conditions for the test are met.

**Working.** $\hat p_1=\frac{54}{150}=0.36$ and $\hat p_2=\frac{50}{200}=0.25$.

(a) $H_0:p_1-p_2=0$ against $H_a:p_1-p_2>0$. Under $H_0$ the two proportions are equal, so we **pool**:
$$\hat p=\frac{54+50}{150+200}=0.2971,\qquad \hat q=0.7029$$
$$z=\frac{\hat p_1-\hat p_2}{\sqrt{\hat p\hat q\left(\frac1m+\frac1n\right)}}=\frac{0.11}{\sqrt{0.2971(0.7029)\left(\frac1{150}+\frac1{200}\right)}}=\frac{0.11}{0.04936}=2.23$$
Critical value $z_{0.05}=1.645$. Since $2.23>1.645$, reject $H_0$. ($p$-value $=1-0.9871=0.0129\le0.05$.)

(b) The interval does **not** pool:
$$(\hat p_1-\hat p_2)\pm z_{0.025}\sqrt{\frac{\hat p_1\hat q_1}{m}+\frac{\hat p_2\hat q_2}{n}}=0.11\pm1.96\sqrt{\frac{0.36(0.64)}{150}+\frac{0.25(0.75)}{200}}=0.11\pm1.96(0.0497)$$
$$(0.013,\ 0.207)$$

**In words.** At the 5% level there is sufficient evidence that a higher proportion of households recycle in Town A. The $p$-value of 0.0129 means that if the two towns really recycled at the same rate, a difference this large in Town A's favour would happen only about 1.3% of the time. We are 95% confident that Town A's proportion is between 1.3 and 20.7 percentage points higher.

---

## Example 19. F test for two variances
**Question.** Sample 1: $m=11$, $s_1^2=24.5$. Sample 2: $n=9$, $s_2^2=9.8$. Assume normal populations. Test at the 5% level whether the population variances are different.

**Working.** $H_0:\sigma_1^2=\sigma_2^2$ against $H_a:\sigma_1^2\ne\sigma_2^2$ (two-sided, so $\frac\alpha2=0.025$ in each tail).
$$F=\frac{s_1^2}{s_2^2}=\frac{24.5}{9.8}=2.5,\qquad df=(m-1,\ n-1)=(10,\ 8)$$
Upper critical value $F_{0.025,10,8}=4.30$. Lower critical value $\frac{1}{F_{0.025,8,10}}=\frac{1}{3.85}=0.26$. Reject $H_0$ if $F\ge4.30$ or $F\le0.26$. Since $0.26<2.5<4.30$, do not reject $H_0$.

**In words.** At the 5% level there is not sufficient evidence that the two population variances are different. The sample variances differ by a ratio of 2.5, but with samples this small a ratio of that size can easily happen by chance, so it is reasonable to treat the variances as equal. (This is the check used before a pooled $t$ test.)

---

## Example 20. Confidence interval for a mean with sigma known, and a bound
**Question.** A sample of $n=36$ has $\bar x=120.5$ and the population standard deviation is known to be $\sigma=9$. (a) Find a 95% confidence interval for $\mu$. (b) Find a 95% upper confidence bound for $\mu$ and use it to say whether $\mu=125$ is plausible against $\mu<125$.

**Working.** Standard error: $\frac{9}{\sqrt{36}}=1.5$.

(a)
$$\bar x\pm z_{\alpha/2}\frac{\sigma}{\sqrt n}=120.5\pm1.96(1.5)=120.5\pm2.94=(117.56,\ 123.44)$$

(b) All of $\alpha=0.05$ goes in one tail, so use $z_{0.05}=1.645$:
$$\mu<\bar x+z_\alpha\frac{\sigma}{\sqrt n}=120.5+1.645(1.5)=122.97$$

**In words.** (a) We are 95% confident that the true mean lies between 117.56 and 123.44. (b) We are 95% confident that the true mean is below 122.97. The value 125 is above that bound, so $\mu=125$ is not plausible, and the data support $\mu<125$. A lower-tailed alternative ($\mu<\mu_0$) is checked with an **upper** bound; an upper-tailed alternative ($\mu>\mu_0$) with a **lower** bound; a two-sided alternative with the two-sided interval. (This uses the interval only. One-sample tests are not examined.)

---

## Example 21. Confidence interval for a variance
**Question.** A sample of $n=15$ from a normal population has $s^2=16$. Find a 95% confidence interval for $\sigma^2$ and for $\sigma$.

**Working.** $df=n-1=14$. From the chi-square table: $\chi^2_{0.025,14}=26.12$ (area $0.025$ to its right) and $\chi^2_{0.975,14}=5.63$ (area $0.975$ to its right).
$$\left(\frac{(n-1)s^2}{\chi^2_{\alpha/2,n-1}},\ \frac{(n-1)s^2}{\chi^2_{1-\alpha/2,n-1}}\right)=\left(\frac{14(16)}{26.12},\ \frac{14(16)}{5.63}\right)=\left(\frac{224}{26.12},\ \frac{224}{5.63}\right)=(8.58,\ 39.80)$$
Take square roots for $\sigma$: $(\sqrt{8.58},\ \sqrt{39.80})=(2.93,\ 6.31)$.

**In words.** We are 95% confident that the true population variance is between 8.58 and 39.80, which means the true standard deviation is between 2.93 and 6.31. The **lower** bound uses the **larger** chi-square value.

---

## Example 22. Prediction interval for one new value
**Question.** Using the sample in Example 3 ($n=16$, $\bar x=52.4$, $s=6.8$, normal population), find a 95% prediction interval for **one new** observation.

**Working.** $t_{0.025,15}=2.131$.
$$\bar x\pm t_{\alpha/2,n-1}\,s\sqrt{1+\frac1n}=52.4\pm2.131(6.8)\sqrt{1+\frac1{16}}=52.4\pm2.131(6.8)(1.0308)=52.4\pm14.94$$
$$(37.46,\ 67.34)$$

One-sided bounds put all of $\alpha=0.05$ in one tail, so use $t_{0.05,15}=1.753$. The margin is $1.753(6.8)(1.0308)=12.29$:
$$\text{upper bound}=52.4+12.29=64.69,\qquad\text{lower bound}=52.4-12.29=40.11$$

**In words.** A prediction interval is about **one single future value**, not the true mean.
- Between: we are 95% confident that one new observation will be **between** 37.46 and 67.34.
- Upper bound: we are 95% confident that one new observation will be **at most** 64.69.
- Lower bound: we are 95% confident that one new observation will be **at least** 40.11.

Compare the wording with a confidence interval, which is about the **true mean**: "we are 95% confident that the true mean lies between 48.78 and 56.02" (Example 3). The prediction interval is much wider ($\pm14.94$ against $\pm3.62$), because a single value varies far more than an average does. The extra "$1+$" under the root is the difference.

---

## Example 23. Sample size from alpha and beta for a proportion
**Question.** Test $H_0:p=0.30$ against $H_a:p>0.30$ at $\alpha=0.05$. How large must $n$ be so that $\beta(0.40)=0.10$?

**Working.** The cut-off $c$ for $\hat p$ must satisfy both conditions. Note that each condition uses its own standard error:
$$c=p_0+z_\alpha\sqrt{\frac{p_0q_0}{n}}\quad(\alpha),\qquad c=p'-z_\beta\sqrt{\frac{p'q'}{n}}\quad(\beta)$$
Set them equal and collect the terms with $\frac{1}{\sqrt n}$:
$$p'-p_0=\frac{z_\alpha\sqrt{p_0q_0}+z_\beta\sqrt{p'q'}}{\sqrt n}\quad\Rightarrow\quad n=\left[\frac{z_\alpha\sqrt{p_0q_0}+z_\beta\sqrt{p'q'}}{p'-p_0}\right]^2$$
$$n=\left[\frac{1.645\sqrt{0.3(0.7)}+1.28\sqrt{0.4(0.6)}}{0.40-0.30}\right]^2=\left[\frac{1.645(0.4583)+1.28(0.4899)}{0.10}\right]^2=\left[\frac{0.7539+0.6271}{0.10}\right]^2=(13.81)^2=190.7$$
Round up: $n=191$.

**In words.** At least 191 observations are needed so that the test has a 5% chance of a false alarm and only a 10% chance of missing a true proportion of 0.40.

---

## Example 24. Two-sided beta and the sample size
**Question.** Test $H_0:\mu=50$ against $H_a:\mu\ne50$ with $\sigma=10$, $n=25$ and $\alpha=0.05$. (a) Give the rejection region. (b) Find $\beta(54)$. (c) How large must $n$ be for $\beta(54)=0.10$?

**Working.** Standard error: $\frac{10}{\sqrt{25}}=2$.

(a) $\frac\alpha2=0.025$ in each tail, so $z_{0.025}=1.96$:
$$50\pm1.96(2)=50\pm3.92\quad\Rightarrow\quad\text{reject if }\bar x<46.08\text{ or }\bar x>53.92$$

(b) $\beta$ is the chance $\bar X$ lands **between** the two cut-offs when the true mean is $54$:
$$\beta(54)=P(46.08\le\bar X\le53.92\mid\mu=54)=P\!\left(\frac{46.08-54}{2}\le Z\le\frac{53.92-54}{2}\right)=P(-3.96\le Z\le-0.04)$$
$$=0.4840-0.0000=0.4840$$

(c) Use the boundary nearer to $\mu'$ with $z_{\alpha/2}$ (the far tail is negligible):
$$n=\left[\frac{\sigma(z_{\alpha/2}+z_\beta)}{\lvert\mu'-\mu_0\rvert}\right]^2=\left[\frac{10(1.96+1.28)}{4}\right]^2=(8.10)^2=65.6\ \Rightarrow\ n=66$$

**In words.** If the true mean is 54, this test misses the difference about 48% of the time. About 66 observations are needed to bring that down to 10%.

---

## Example 25. Numerical bias and MSE
**Question.** Two estimators of a parameter $\theta=50$ have $E(\hat\theta_1)=50$, $V(\hat\theta_1)=8$ and $E(\hat\theta_2)=52$, $V(\hat\theta_2)=3$. Find the bias and the mean squared error of each and say which is better.

**Working.**
$$\text{bias}(\hat\theta_1)=E(\hat\theta_1)-\theta=50-50=0,\qquad \text{bias}(\hat\theta_2)=52-50=2$$
$$MSE(\hat\theta)=V(\hat\theta)+[\text{bias}(\hat\theta)]^2$$
$$MSE(\hat\theta_1)=8+0^2=8,\qquad MSE(\hat\theta_2)=3+2^2=7$$

**In words.** $\hat\theta_1$ is unbiased and $\hat\theta_2$ is biased, but $\hat\theta_2$ has the smaller mean squared error ($7<8$), so on average it lands closer to the true value. Unbiased is not automatically better.

---

## Example 26. The Central Limit Theorem with a non-normal population
**Question.** A skewed (non-normal) population has mean $\mu=30$ and standard deviation $\sigma=12$. A random sample of $n=64$ is taken. Find $P(\bar X>32)$ and say why it is allowed.

**Working.** Standard error: $\frac{12}{\sqrt{64}}=1.5$. Since $n=64>40$, the Central Limit Theorem says $\bar X$ is approximately $N(30,\ 1.5^2)$.
$$P(\bar X>32)=P\!\left(Z>\frac{32-30}{1.5}\right)=P(Z>1.33)=1-0.9082=0.0918$$

**In words.** There is about a 9.2% chance that the sample mean exceeds 32. We could use the normal curve even though the population is not normal, because the sample is large ($n>40$). With a small sample from a non-normal population, we could not.

---

## Example 27. Reading a p-value
**Question.** Three tests give the following $z$ statistics. Find each $p$-value and decide at $\alpha=0.05$. (a) Lower-tailed, $z=-2.1$. (b) Two-sided, $z=1.8$. (c) Upper-tailed, $z=2.5$.

**Working.** The rule is the same every time: **reject $H_0$ if $p\le\alpha$**. Only the area changes with $H_a$.

(a) Lower tail: $p=P(Z\le-2.1)=0.0179$. Since $0.0179\le0.05$, reject $H_0$.

(b) Two-sided: double the smaller tail: $p=2P(Z\ge1.8)=2(0.0359)=0.0718$. Since $0.0718>0.05$, do not reject $H_0$.

(c) Upper tail: $p=P(Z\ge2.5)=0.0062$. Since $0.0062\le0.05$, reject $H_0$.

**In words.** (a) At the 5% level there is sufficient evidence against $H_0$. (b) At the 5% level there is not sufficient evidence against $H_0$, although it would be rejected at the 10% level. (c) At the 5% level there is sufficient evidence against $H_0$. The $p$-value is the chance of data at least this extreme if $H_0$ were true. It is not the chance that $H_0$ is true.
