---
module: STA01B1
topic: Revision Summary
test: ST2
range: S6 to S9
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# STA01B1 Summary (ST2, sessions S6 to S9)

Fast review for the Summative Assessment 2 theory test: Friday 9 October 2026, 09:40 to 11:15, D1 Lab 308. Be there 15 minutes early, and bring no bags. It is a fill-in paper on proofs, theory and applications. Scope is textbook 9.1 to 9.5, 10.1, 10.2, 12.1 to 12.3 and 12.5, Tutorials 7 to 10, and Lectures 7 to 10. Every derivation is in [[STA01B1_Proofs_ST2]], so this file states results and links out.

The practical test (Thursday 15 October, on Moodle, Practicals 6, 7, 9 and 10) is not covered here.

> [!note] About the links
> Many headings in the S7 to S9 notes carry an inline tag (for example `#formula`), and I can't reliably anchor a link to those headings. Those citations link the whole file and name the heading in plain text. Untagged headings are anchored directly.

## Material covered

- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]]: two means, independent samples (z known variance, large-sample z, pooled t, CIs)
- [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances]]: paired t, two proportions, F test for two variances
- [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]]: single-factor ANOVA, the $SST$ proof, Tukey's procedure
- [[STA01B1_Notes_S9_Simple_Linear_Regression]]: least squares, $r$ and $r^2$, regression ANOVA, t and F tests, CI and PI at $x_0$
- [[STA01B1_Proofs_ST2]]: all derivations for this range
- Supplied this time:
  - Tutorials 7 to 10, with Solutions 7 to 9 (Solution 10 not yet released)
  - The departmental hypothesis testing summary sheet
  - Past papers with memos: STA1B10 Semester Test 2 2011, 2012 and 2016; STA01B1 Summative Assessment 3 2024 (Section A memo)
  - Past papers without memos: STA01B1 2018 Semester Test 2; 2020 SA2 Section B; 2022 SA2; 2022 Paper C; 2023 Paper A; 2025 Deferred SA2; 2025 SA3; the SA2 mock test

Past-paper material outside this test's scope was left out. That includes one-sample tests, Type II error and power calculations, sample-size questions, chi-squared tests, randomized block and two-way designs, and the variance CI for one sample.

---

## How the paper is marked

The assessment information says: show all steps and calculations, and give evidence that you understand the work. For applications, start with the formula, then substitute, then simplify, and lastly interpret. Past papers round to 2 decimal places.

Recent papers print the hypothesis test as numbered blanks. Fill every one:

```
1. Parameter(s): Let mu1 = true average ... of ...; Let mu2 = ...
2. Null hypothesis
3. Alternative hypothesis
4. Test statistic: formula, then substitution, then value
5. Significance level
6. Rejection region and p-value
7. Decision: reject / do not reject H0
8. Conclusion: plain English, in the words of the question, naming alpha
```

N.B define the parameters in context ("true average sugar content of Caffe Latte drinks"), not as bare symbols. A conclusion that names the populations and the significance level is what earns the last mark in every memo on file.

---

## Choosing the procedure

From the departmental summary sheet and the S6 to S9 notes. Read the question in this order.

| What is being compared | Design | Procedure | Statistic follows |
|---|---|---|---|
| Two means | Same subjects or matched pairs (before/after, twins, two tyres on one car) | Paired $t$ on the differences | $t_{n-1}$, $n$ = number of pairs |
| Two means | Independent, $m>40$ and $n>40$ | Large-sample $z$ with $s_1^2, s_2^2$ | $N(0,1)$ |
| Two means | Independent, $\sigma_1, \sigma_2$ known | $z$ with $\sigma_1^2, \sigma_2^2$ | $N(0,1)$ |
| Two means | Independent, $m<40$ and/or $n<40$, both normal, equal variances | Pooled $t$ | $t_{m+n-2}$ |
| Two means | Independent, small, unequal variances | Not applicable (summary sheet) | |
| Two proportions | Independent, large (all four counts $\ge 10$) | Two-proportion $z$ | $N(0,1)$ |
| Two variances | Independent, both normal | $F$ test | $F_{m-1,n-1}$ |
| Three or more means | Independent, normal, equal variances | Single-factor ANOVA, then Tukey if $H_0$ is rejected | $F_{I-1,\,I(J-1)}$ |
| Is $y$ linearly related to $x$? | $n$ pairs $(x_i, y_i)$ | Slope $t$ test or model $F$ test | $t_{n-2}$, $F_{1,n-2}$ |

> [!warning] Paired or independent: the question to ask #struggle #common-mistake
> Do the two columns share the same subjects? If yes, take differences and run a one-sample $t$ with $n-1$ df. That holds even when a question also prints $s_p^2$ and $\bar{x}_1-\bar{x}_2$: past papers give those as distractors (2023 Paper A Q3, 2024 SA3 Q2). This slipped in S7, S8 and S9.

The cutoff is 40, confirmed by the lecturer. For two means the large-sample $z$ needs both $m>40$ and $n>40$. The pooled $t$ applies when $m<40$ and/or $n<40$. Example from 2022 SA2 Q3c: $m = 21$ heart patients and $n = 41$ athletes means pooled $t$, because one sample is under 40.

---

## Every test statistic

Each statistic is written as estimate minus hypothesised value, divided by the standard error of the estimate.

| Procedure | $H_0$ | Test statistic | Distribution, df | Assumptions |
|---|---|---|---|---|
| Two means, known variances | $\mu_1-\mu_2=\Delta_0$ | $z=\dfrac{\bar{x}-\bar{y}-\Delta_0}{\sqrt{\sigma_1^2/m+\sigma_2^2/n}}$ | $N(0,1)$ | Independent random samples; normal populations or both large; $\sigma$'s known |
| Two means, large samples | $\mu_1-\mu_2=\Delta_0$ | $z=\dfrac{\bar{x}-\bar{y}-\Delta_0}{\sqrt{s_1^2/m+s_2^2/n}}$ | $N(0,1)$ approx | Independent random samples; $m>40$ and $n>40$ |
| Pooled $t$ | $\mu_1-\mu_2=\Delta_0$ | $t=\dfrac{\bar{x}-\bar{y}-\Delta_0}{\sqrt{s_p^2(1/m+1/n)}}$ | $t_{m+n-2}$ | Independent random samples; both populations normal; equal variances |
| Paired $t$ | $\mu_D=\Delta_0$ | $t=\dfrac{\bar{d}-\Delta_0}{s_D/\sqrt{n}}$ | $t_{n-1}$ | Matched-pairs design; differences a random sample from a normal distribution |
| Two proportions | $p_1-p_2=0$ | $z=\dfrac{\hat{p}_1-\hat{p}_2}{\sqrt{\hat{p}\hat{q}(1/m+1/n)}}$ | $N(0,1)$ approx | Independent binomial samples; $m\hat{p}_1, m\hat{q}_1, n\hat{p}_2, n\hat{q}_2 \ge 10$ |
| Two variances | $\sigma_1^2=\sigma_2^2$ | $f=\dfrac{s_1^2}{s_2^2}$ | $F_{m-1,\,n-1}$ | Independent random samples; both populations normal |
| ANOVA | $\mu_1=\cdots=\mu_I$ | $f=\dfrac{MSTr}{MSE}$ | $F_{I-1,\,I(J-1)}$ | Independent random samples; normal populations; equal variances |
| Regression slope | $\beta_1=0$ | $t=\dfrac{b_1}{\sqrt{MSE/S_{xx}}}$ | $t_{n-2}$ | $\varepsilon \sim N(0,\sigma^2)$, independent, constant $\sigma^2$ |
| Regression model | slope $=0$ | $f=\dfrac{MSR}{MSE}$ | $F_{1,\,n-2}$ | As above; $t^2=f$ |

Supporting formulas:
$$s_p^2=\frac{(m-1)s_1^2+(n-1)s_2^2}{m+n-2} \qquad \hat{p}=\frac{x+y}{m+n},\ \hat{q}=1-\hat{p}$$
$$s_D=\sqrt{\frac{\sum d_i^2-(\sum d_i)^2/n}{n-1}} \qquad w=Q_{\alpha,\,I,\,I(J-1)}\sqrt{\frac{MSE}{J}}$$

($s_D$ is the ordinary sample standard deviation of the differences, written in computing form. It is added here for hand calculation.)

The ANOVA and regression pieces, with totals and no bars in the computing formulas:
$$SST=\sum_i\sum_j x_{ij}^2-\frac{x_{\cdot\cdot}^2}{IJ}\qquad SSTr=\frac{\sum_i x_{i\cdot}^2}{J}-\frac{x_{\cdot\cdot}^2}{IJ}\qquad SSE=SST-SSTr$$
$$MSTr=\frac{SSTr}{I-1}\qquad MSE=\frac{SSE}{I(J-1)}$$
$$S_{xx}=\sum x_i^2-\frac{(\sum x_i)^2}{n}\qquad S_{xy}=\sum x_iy_i-\frac{(\sum x_i)(\sum y_i)}{n}\qquad S_{yy}=\sum y_i^2-\frac{(\sum y_i)^2}{n}$$
$$b_1=\frac{S_{xy}}{S_{xx}}\qquad b_0=\bar{y}-b_1\bar{x}\qquad r=\frac{S_{xy}}{\sqrt{S_{xx}S_{yy}}}\qquad r^2=\frac{SSR}{\text{Total }SS}$$
$$SSR=b_1S_{xy}\qquad SSE=\text{Total }SS-SSR\qquad MSE=\frac{SSE}{n-2}$$

ANOVA tables:

| Source | df | SS | MS | F |
|---|---|---|---|---|
| Treatments | $I-1$ | $SSTr$ | $SSTr/(I-1)$ | $MSTr/MSE$ |
| Error | $I(J-1)$ | $SSE$ | $SSE/[I(J-1)]$ | |
| Total | $IJ-1$ | $SST$ | | |

| Source | df | SS | MS | F |
|---|---|---|---|---|
| Regression | $1$ | $SSR$ | $SSR/1$ | $MSR/MSE$ |
| Error | $n-2$ | $SSE$ | $SSE/(n-2)$ | |
| Total | $n-1$ | $S_{yy}$ | | |

---

## Rejection regions and p-values

| $H_a$ | $z$ or $t$ rejection region | p-value |
|---|---|---|
| upper-tailed ($>$) | $z\ge z_\alpha$ or $t\ge t_{\alpha,\nu}$ | $P(Z\ge z)$, the area to the right |
| lower-tailed ($<$) | $z\le -z_\alpha$ or $t\le -t_{\alpha,\nu}$ | $P(Z\le z)$, the area to the left |
| two-tailed ($\neq$) | $\lvert z\rvert\ge z_{\alpha/2}$ or $\lvert t\rvert\ge t_{\alpha/2,\nu}$ | $2P(Z\ge \lvert z\rvert)$ |

Reject $H_0$ when the p-value $\le\alpha$.

F test (S7). For a two-tailed test, put the larger sample variance on top so $f\ge1$, and compare with $F_{\alpha/2}$ using df (top group $-1$, bottom group $-1$). For a one-sided $H_a$, the direction of $H_a$ fixes which variance is on top, and you use $F_\alpha$. For lower critical values, $F_{1-\alpha,\nu_1,\nu_2}=1/F_{\alpha,\nu_2,\nu_1}$.

ANOVA and the regression $F$ are always upper-tailed: reject if $f\ge F_{\alpha}$.

Common $z$ values: $z_{.10}=1.28$, $z_{.05}=1.645$, $z_{.025}=1.96$, $z_{.01}=2.33$, $z_{.005}=2.58$.

> [!tip] Approximate p-value from a t or F table (past-paper skill; parked since S5, now has source material)
> The t table has only fixed columns, so bracket the statistic between two columns and read the tail areas. For example, 2012 memo Q1: $t=-2.82$ with 4 df lies between $t_{.025,4}=2.776$ and $t_{.01,4}=3.747$ in absolute value. That gives $.01<\text{p-value}<.025$ for a one-tailed test. For a two-tailed test, double both ends. The 2011 memo Q3 gives $0.05<\tfrac12(\text{p-value})<0.10$, so $0.10<\text{p-value}<0.20$. The same bracketing works on the F table (Solution 8 Q60).

---

## Every confidence interval, bound and prediction interval

Every interval has the form estimate $\pm$ (critical value)(standard error). For a one-sided bound, use $z_\alpha$ or $t_\alpha$ in place of $z_{\alpha/2}$ or $t_{\alpha/2}$, keep only one side, and check the direction against the wording.

| Target | Two-sided $100(1-\alpha)\%$ interval | Conditions |
|---|---|---|
| $\mu_1-\mu_2$, large | $\bar{x}-\bar{y}\pm z_{\alpha/2}\sqrt{s_1^2/m+s_2^2/n}$ | $m>40$ and $n>40$ |
| $\mu_1-\mu_2$, pooled | $\bar{x}-\bar{y}\pm t_{\alpha/2,m+n-2}\sqrt{s_p^2(1/m+1/n)}$ | normal, equal variances, $m<40$ and/or $n<40$ |
| $\mu_D$, paired | $\bar{d}\pm t_{\alpha/2,n-1}\,s_D/\sqrt{n}$ | differences approximately normal |
| $p_1-p_2$ | $\hat{p}_1-\hat{p}_2\pm z_{\alpha/2}\sqrt{\hat{p}_1\hat{q}_1/m+\hat{p}_2\hat{q}_2/n}$ | large samples; no pooled $\hat{p}$ |
| Average $y$ at $x_0$ (CI) | $\hat{y}\pm t_{\alpha/2,n-2}\sqrt{MSE\left(\dfrac1n+\dfrac{(x_0-\bar{x})^2}{S_{xx}}\right)}$ | regression assumptions |
| One new $y$ at $x_0$ (PI) | $\hat{y}\pm t_{\alpha/2,n-2}\sqrt{MSE\left(1+\dfrac1n+\dfrac{(x_0-\bar{x})^2}{S_{xx}}\right)}$ | regression assumptions |
| $\mu_i-\mu_j$ in ANOVA (past paper) | $\bar{x}_i-\bar{x}_j\pm t_{\alpha/2,I(J-1)}\sqrt{MSE(1/J+1/J)}$ | ANOVA assumptions |
| Slope $\beta_1$ (tutorial) | $b_1\pm t_{\alpha/2,n-2}\sqrt{MSE/S_{xx}}$ | regression assumptions |

Sources for the last two rows, which are not on the lecture slides:
- $\mu_i-\mu_j$: STA1B10 2012 memo Q3.4, a 90% CI for $\mu_1-\mu_3$ using $MSE$ and $t_{.05,16}=1.746$.
- Slope: Tutorial 10 Q32 asks for a CI for the true average change in $y$ per unit of $x$. A printout gives it directly as the slope's Lower 95% and Upper 95% columns. The standard error is the denominator of the slope $t$ test. (added)

Reading intervals:
- If 0 is inside a CI for a difference, you cannot conclude the parameters differ.
- If 1 is inside a CI for a ratio of variances, the variances may be equal (2023 Paper A Q9, interval $(0.5866, 4.798)$).
- A lower bound above 0 says $\mu_1>\mu_2$ by at least that amount.
- The PI and CI at the same $x_0$ share the centre $\hat{y}$. The PI is always wider because of the extra 1. Both are narrowest at $x_0=\bar{x}$.

Bound direction, from past papers:
- "By how much is A less than B" (2022 SA2 Q3d): an upper bound on $\mu_A-\mu_B$, which will be negative.
- "Estimate the difference by a lower bound" (mock Q14.2, 2023 Paper A Q3b): $\bar{d}-t_{\alpha,n-1}s_D/\sqrt{n}$ or the two-sample equivalent.
- Solution 7 Q4b: upper bound $=\bar{x}-\bar{y}+z_\alpha SE$, giving $5700+1.645(396.93)=6352.95$.

---

## Every assumption, in exam wording

Past memos award one mark per assumption. Write them as a list.

- Two means, independent, pooled $t$ (2011 memo Q3.2):
  - samples randomly and independently selected
  - from normally distributed populations
  - with equal variances
- Two means, large samples (summary sheet):
  - random samples
  - independent samples
  - $m>40$ and $n>40$
- Paired $t$ (2012 memo Q1.1):
  - the experiment is designed as matched pairs
  - the $n$ differences form a random sample
  - from a normal distribution
- Two proportions (summary sheet, and S7 for the strict rule):
  - binomial experiments
  - independent samples
  - large samples: $m\hat{p}_1\ge10$, $m\hat{q}_1\ge10$, $n\hat{p}_2\ge10$, $n\hat{q}_2\ge10$
- $F$ test:
  - independent random samples
  - from normal populations (the F test is very sensitive to non-normality)
- ANOVA (S8):
  - normality: each $X_{ij}$ is normal
  - homoscedasticity: $V(X_{ij})=\sigma^2$, the same for every group
  - independent random samples
  - Rough check: the largest sample SD is not much more than twice the smallest.
- Regression (S9):
  - $\varepsilon$ is normal with mean 0
  - common (constant) variance $\sigma^2$
  - errors independent
  - Equivalently, at each $x$, $y$ is normal with mean $\beta_0+\beta_1x$ and variance $\sigma^2$.
  - Check with the normal probability plot (normality) and residuals versus fits (equal variance).

How to verify an assumption when asked (2018 Q1.2 and 1.1):
- Normality: a normal probability plot is roughly straight, or its reported p-value exceeds $\alpha$.
- Equal variances: run the $F$ test, or apply the ANOVA rule of thumb.
- Independence: from the design. Different subjects mean independent samples; the same subjects mean paired.

---

## Sampling distributions of the statistics

"Completely describe the sampling distribution of the appropriate test statistic" appears in 2012 Q1.1, 2016 Q3.1 and Q4.1, and mock Q10.1 and Q14.1. The full answer names the distribution, its parameters or df, and the assumptions.

| Statistic | Sampling distribution |
|---|---|
| $\bar{X}-\bar{Y}$ | Normal (exactly if populations are normal, approximately by CLT if large), mean $\mu_1-\mu_2$, variance $\sigma_1^2/m+\sigma_2^2/n$ |
| Pooled $T$ | Student's $t$ with $m+n-2$ df |
| Paired $T$ | Student's $t$ with $n-1$ df (2016 memo: "$t$-distribution with 3 degrees of freedom" for 4 twin pairs) |
| $\hat{p}_1-\hat{p}_2$ | Approximately normal, mean $p_1-p_2$, variance $p_1q_1/m+p_2q_2/n$ (2016 memo Q4.1) |
| $F=S_1^2/S_2^2$ under $H_0$ | $F$ with $m-1$ and $n-1$ df |
| $F=MSTr/MSE$ under $H_0$ | $F$ with $I-1$ and $I(J-1)$ df |
| Slope $T$ under $H_0$ | $t$ with $n-2$ df |
| Regression $F$ | $F$ with 1 and $n-2$ df |

---

## Condensed concept pass

### Two independent means (S6)

The parameter is $\mu_1-\mu_2$ and the estimator is $\bar{X}-\bar{Y}$. Its mean is $\mu_1-\mu_2$, and its variances add, $\sigma_1^2/m+\sigma_2^2/n$, because the samples are independent.

Three forks:
- Known variances: $z$.
- Unknown variances with both samples over 40: the same $z$ with $s^2$ substituted.
- Small samples from normal populations with equal variances: pooled $t$ on $m+n-2$ df. $s_p^2$ is the df-weighted average of $s_1^2$ and $s_2^2$.

The hypothesised difference $\Delta_0$ is usually 0, but "exceeds by more than 5" makes it 5. Every CI is the matching statistic turned inside out.

(see: [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Pooled Two Sample t Test and Confidence Interval|Pooled Two Sample t Test and Confidence Interval]])

### Paired data, two proportions, two variances (S7)

Pairing turns two samples into one sample of differences $D_i=X_i-Y_i$. Everything after that is a one-sample $t$ with $n-1$ df. Ignoring real pairing inflates the standard error and can bury a real effect: the tyre data gave $t=0.574$ unpaired and $t=12.829$ paired.

Proportions always use $z$. The variance $pq$ is built from $p$, so there is no separate variance to estimate and no $t$. The test pools $\hat{p}=(x+y)/(m+n)$ because $H_0$ says $p_1=p_2$. The CI does not pool.

Two variances use $f=s_1^2/s_2^2$ on $(m-1, n-1)$ df. The test needs both populations normal and is very sensitive to non-normality.

(see: [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances#The Paired t Test, Why Pairing Matters|The Paired t Test, Why Pairing Matters]], [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances#Two Proportion z Test, Example 9.11|Two Proportion z Test, Example 9.11]], [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances#The F Distribution and the Test for Two Population Variances, Example 9.14|The F Distribution and the Test for Two Population Variances, Example 9.14]])

### Single-factor ANOVA and Tukey (S8)

ANOVA tests $H_0:\mu_1=\cdots=\mu_I$ against "at least two differ" with one $F$ test. It compares variation between the sample means ($MSTr$) with variation within the samples ($MSE$).

$MSE$ is the pooled estimate of $\sigma^2$, built from deviations around each group's own mean. It is unbiased whether or not $H_0$ holds, so it cannot see the means differ. $MSTr$ inflates when the means differ, so a large $F$ rejects $H_0$.

$SST=SSTr+SSE$ (the lecturer's proof), with df $IJ-1=(I-1)+I(J-1)$. When $H_0$ is rejected, Tukey's HSD $w=Q_{\alpha,I,I(J-1)}\sqrt{MSE/J}$ says which means differ. List the means in increasing order and underline groups whose range is less than $w$. Means not joined by a common line differ significantly. $\alpha$ is the family error rate.

(see: [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]], headings "Why F grows when H0 is false", "Tukey's procedure: which means differ" and "Reading the underscoring (source, slide 31)", the last at [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure#Reading the underscoring (source, slide 31)|Reading the underscoring]])

### Simple linear regression (S9)

The probabilistic model is $y=\beta_0+\beta_1x+\varepsilon$, with $\varepsilon$ normal, mean 0 and common variance $\sigma^2$. $E(y)=\beta_0+\beta_1x$ is the line of means.

Least squares picks $b_0$ and $b_1$ to minimise $SSE=\sum(y_i-\hat{y}_i)^2$. That gives $b_1=S_{xy}/S_{xx}$ and $b_0=\bar{y}-b_1\bar{x}$, and the line passes through $(\bar{x},\bar{y})$.

Total $SS=SSR+SSE$ with df $n-1=1+(n-2)$. $r^2=SSR/\text{Total }SS$ is the proportion of variation in $y$ explained by $x$. $r$ carries the sign of the slope.

Usefulness is tested by $t=b_1/\sqrt{MSE/S_{xx}}$ on $n-2$ df, or $F=MSR/MSE$ on $(1,n-2)$ df, with $t^2=F$. The null is slope $=0$. A non-significant slope does not prove "unrelated": the relationship could be nonlinear, or the result could be a Type II error.

The CI at $x_0$ is for the average $y$. The PI is for one new $y$, and it is wider by the extra 1. Avoid extrapolation and causal claims.

(see: [[STA01B1_Notes_S9_Simple_Linear_Regression#The t test for the slope (slide 19)|The t test for the slope]], [[STA01B1_Notes_S9_Simple_Linear_Regression#Diagnostic tools (source, slides 23 to 26)|Diagnostic tools]], [[STA01B1_Notes_S9_Simple_Linear_Regression#Why the prediction interval is wider, and why both flare (added)|Why the prediction interval is wider]])

---

## The four theory paragraphs

The assessment information names these four as short-paragraph questions. Each model answer below is built from the session notes, plus the 2016 memo where one exists. Past papers ask for 2 to 4 sentences worth 2 to 4 marks.

### Sampling distributions
A statistic, such as $\bar{X}$, $\bar{X}-\bar{Y}$ or $\hat{p}_1-\hat{p}_2$, is any quantity calculated from sample data. Before the sample is drawn its value is uncertain, so it is a random variable. Its probability distribution is called its sampling distribution. In repeated sampling, if we drew every possible sample of the same size from the population and computed the statistic each time, the sampling distribution would describe how those values vary: their mean, their spread (the standard error) and their shape. For example, $\bar{X}-\bar{Y}$ is centred on $\mu_1-\mu_2$ with variance $\sigma_1^2/m+\sigma_2^2/n$, and it is normal if the populations are normal or approximately normal by the CLT when the samples are large. Test statistics and confidence intervals are built from these distributions.
(source: S1 definition, which 2022 Paper C Q1a asks for "in terms of repeated sampling"; the two-sample example is from S6)

### Hypothesis testing
A hypothesis test uses sample data to decide between two contradictory claims about a population parameter. The null hypothesis $H_0$ is assumed true until the evidence contradicts it, usually a claim of no difference or no effect. The alternative $H_a$ is the claim the researcher wants to establish. A test statistic is computed from the sample, and $H_0$ is rejected if it falls in the rejection region, or equivalently if the p-value is at most the significance level $\alpha$. The only conclusions are "reject $H_0$" or "fail to reject $H_0$", never "$H_0$ is proven". A Type I error (rejecting a true $H_0$) has probability $\alpha$, and a Type II error (not rejecting a false $H_0$) has probability $\beta$.
(source: S5 definitions; 2016 memo Q1.1)

### ANOVA
Analysis of variance tests whether the means of two or more populations are all equal: $H_0:\mu_1=\cdots=\mu_I$ against $H_a$ that at least two differ. It compares the variation between the sample means ($MSTr$) with the variation within the samples ($MSE$), using $F=MSTr/MSE$. A large $F$ means the group means are further apart than within-group noise can explain, so $H_0$ is rejected. It assumes independent random samples from normal populations with equal variances. ANOVA only says that some means differ. A multiple comparison procedure such as Tukey's is needed to find which.
(source: S8; 2016 memo Q1.2. Past papers: "Explain the principle of ANOVA in no more than 3 sentences", 2022 Paper C Q8c, 2025 SA3 Q3a; four sentences in 2018 Q3.2)

### The least squares regression line
The least squares regression line $\hat{y}=b_0+b_1x$ is the straight line that best fits $n$ data pairs. "Best" means it minimises the sum of the squared vertical distances of the points from the line, $SSE=\sum(y_i-\hat{y}_i)^2$. The minimising values are $b_1=S_{xy}/S_{xx}$ and $b_0=\bar{y}-b_1\bar{x}$, so the line always passes through $(\bar{x},\bar{y})$. It estimates the population line of means $E(y)=\beta_0+\beta_1x$ in the model $y=\beta_0+\beta_1x+\varepsilon$, and is used to describe the relationship between $x$ and $y$ and to predict $y$ within the observed range of $x$.
(source: S9; 2016 memo Q1.3 for the uses; 2025 SA3 Q4a asks "what a linear regression model is" in one sentence)

### Sentence completions (2022 SA2 Q1, 2025 Deferred SA2 Q1)

- The level of significance is the probability of rejecting $H_0$ when $H_0$ is true, that is, of making a Type I error. (S5)
- The p-value is the probability, computed assuming $H_0$ is true, of obtaining a test statistic value at least as extreme as the one observed. (S6) (added) It is also the smallest $\alpha$ at which $H_0$ would be rejected.
- A Type II error is not rejecting $H_0$ when $H_0$ is false. (S5)
- Normality of the underlying distribution means each population sampled follows a normal distribution, so the observations, the paired differences or the regression errors are normally distributed. (S7, S8, S9)
- Homoscedasticity means equal variances: every population (or the error at every $x$) has the same variance $\sigma^2$. (S8, S9)

---

## Worked example notebook

Each example comes from a past paper, tutorial or memo on file. Labels:
- (memo): the working follows a departmental memo or tutorial solution.
- (working mine): no memo was supplied, so I worked it and checked every number by recomputing.

Where a memo has a mistake, it is corrected here and listed under "Memo errors".

### Large-sample z for two means (2022 Paper C Q7; also 2020 SA2 Q3 and mock Q13) (working mine)
DMFS increment: control $m=289$, $\bar{x}=12.83$, $s_1=8.31$; fluoride $n=260$, $\bar{y}=11.18$, $s_2=7.51$. Is fluoride toothpaste beneficial at $\alpha=.01$?

WORKING
1. $\mu_1$ = true average DMFS increment without fluoride, $\mu_2$ = with fluoride.
2. $H_0:\mu_1-\mu_2=0$
3. $H_a:\mu_1-\mu_2>0$ (beneficial means fewer new cavities with fluoride)
4. $z=\dfrac{\bar{x}-\bar{y}}{\sqrt{s_1^2/m+s_2^2/n}}=\dfrac{12.83-11.18}{\sqrt{8.31^2/289+7.51^2/260}}=\dfrac{1.65}{0.6752}=2.44$
5. $\alpha=.01$
6. Reject if $z\ge z_{.01}=2.33$. p-value $=P(Z\ge2.44)=.0073$.
7. Reject $H_0$.
8. There is sufficient evidence at the 1% level that the true average DMFS increment is lower with fluoride toothpaste, so it is beneficial.

Assumptions (Q7b): independent random samples; both $m$ and $n$ above 40, so no normality is needed.

N.B Tutorial 7 Q12 uses the same scenario with a fluoride mean of 9.78, and Solution 7 gives the 99% CI $(1.30, 4.80)$. The exam versions changed the mean to 11.18. Always use the numbers on the paper in front of you.

### Pooled t test (STA1B10 2011 Semester Test 2 Q3) (memo)
ABSA $m=9$, $\bar{x}=3.2$, $s_1=0.5$; FNB $n=12$, $\bar{y}=2.8$, $s_2=0.7$; times on hold are approximately normal. Is there a difference?

WORKING
$$s_p^2=\frac{8(0.5)^2+11(0.7)^2}{19}=\frac{2.0+5.39}{19}=0.3889$$
$$t=\frac{3.2-2.8}{\sqrt{0.3889(1/9+1/12)}}=\frac{0.4}{0.275}=1.455$$
(The memo subtracts the other way round and gets $-1.455$. The decision is the same.)
- $H_0:\mu_1-\mu_2=0$ against $H_a:\mu_1-\mu_2\neq0$, with $df=19$.
- Reject if $\lvert t\rvert>t_{.05,19}=1.729$. The memo uses the .05 column for a two-tailed test, which implies $\alpha=.10$; the question states no $\alpha$.
- $0.10<\text{p-value}<0.20$.
- Do not reject $H_0$. One cannot conclude there is a difference in mean time on hold.

### Pooled t with a confidence bound, and the "and/or" rule (2022 SA2 Q3c and d) (working mine)
Heart patients $m=21$, $\bar{x}_1=1.8889$, $s_1=0.8917$; marathon athletes $n=41$, $\bar{x}_2=0.9038$, $s_2=0.9010$; normal populations, equal variances, $\alpha=.01$. Do heart patients have a higher mean? By how much are the athletes lower (99% upper bound)?

WORKING
- $m=21<40$, so the pooled $t$ applies even though $n=41$.
- $s_p^2=\dfrac{20(0.8917)^2+40(0.9010)^2}{60}=0.8062$
- $SE=\sqrt{0.8062(1/21+1/41)}=0.2410$
- $H_a:\mu_1-\mu_2>0$, so $t=\dfrac{1.8889-0.9038}{0.2410}=4.09$
- Reject if $t\ge t_{.01,60}=2.390$. Reject $H_0$: heart patients have a significantly higher mean LDL level at the 1% level.
- 99% upper bound for $\mu_2-\mu_1$: $(0.9038-1.8889)+2.390(0.2410)=-0.41$. With 99% confidence, the athletes' mean is at least 0.41 mmol/L lower than the heart patients'.

### A non-zero hypothesised difference (Tutorial 7 Q32) (memo)
Steroid $m=8$, $\bar{x}=32.8$, $s_1=2.6$; control $n=10$, $\bar{y}=40.5$, $s_2=2.5$. Does the control mean exceed the steroid mean by more than 5 g, at $\alpha=.01$?

WORKING
- "$\mu_2$ exceeds $\mu_1$ by more than 5" means $\mu_1-\mu_2<-5$. So $H_0:\mu_1-\mu_2=-5$ against $H_a:\mu_1-\mu_2<-5$.
- $s_p^2=\dfrac{7(2.6)^2+9(2.5)^2}{16}=6.47$
- $t=\dfrac{(32.8-40.5)-(-5)}{\sqrt{6.47(1/8+1/10)}}=-2.24$
- The p-value is $P(t_{16}<-2.24)\approx.02>.01$, so do not reject $H_0$.

### Paired t (STA1B10 2012 Semester Test 2 Q1) (memo)
Cases bottled per hour before and after a time management programme at 5 companies: before 500, 475, 525, 490, 530; after 510, 480, 525, 495, 533. Has productivity increased, at $\alpha=.05$?

WORKING
- Assumptions: matched pairs; the 5 differences form a random sample from a normal distribution; $t$ with 4 df.
- $d=$ before $-$ after $=-10,-5,0,-5,-3$, so $\bar{d}=-4.6$ and $s_D=3.6469$.
- $H_0:\mu_D=0$ against $H_a:\mu_D<0$ (after is larger).
- $t=\dfrac{-4.6}{3.6469/\sqrt5}=-2.82$
- Reject if $t\le-2.132$. $.01<\text{p-value}<.025$.
- Reject $H_0$: the programme increased productivity.

Variant with $\Delta_0\neq0$ (2024 SA3 Q2, memo). Heart rate after minus before $=70,77,78,70$, so $\bar{d}=73.75$ and $s_D=4.35$. Test whether the after rate is more than 70 greater: $H_0:\mu_D=70$ against $H_a:\mu_D>70$.
$$t=\frac{73.75-70}{4.35/\sqrt4}=1.72<t_{.05,3}=2.353$$
Do not reject $H_0$. The question also printed $s_p^2$ and $\bar{x}_1-\bar{x}_2$; ignore them.

### Two-proportion z test (STA1B10 2016 Semester Test 2 Q4; repeated as 2025 SA3 Q1) (memo)
224 of 395 primary teachers and 126 of 266 high school teachers are very satisfied. Is the primary proportion greater, at $\alpha=.05$?

WORKING
- $\hat{p}_1=.5671$, $\hat{p}_2=.4737$, $\hat{p}=\dfrac{224+126}{395+266}=.5295$
- Validity: $224, 171, 126, 140$ are all at least 10.
- $H_0:p_1-p_2=0$ against $H_a:p_1-p_2>0$
- $$z=\frac{.5671-.4737}{\sqrt{(.5295)(.4705)(1/395+1/266)}}=\frac{.0934}{.0396}=2.36$$
- Reject if $z\ge1.645$. p-value $\approx.009$.
- Reject $H_0$: the proportion of satisfied primary school teachers is greater, at the 5% level.

### Two-proportion CI against a test at a different α (2024 SA3 Q1) (memo)
16 of 200 bolts from machine A and 8 of 200 from machine B are defective.

WORKING
- 90% CI: $(.08-.04)\pm1.645\sqrt{\dfrac{(.08)(.92)}{200}+\dfrac{(.04)(.96)}{200}}=.04\pm.0389=(.0011,\ .0789)$
- Two-tailed test at 5%: $\hat{p}=.06$, $z=\dfrac{.04}{\sqrt{(.06)(.94)(2/200)}}=1.68<1.96$, p-value $=.0921$. Do not reject.
- The CI excludes 0 but the test does not reject. Two different significance levels were used (90% CI against $\alpha=.05$). At 95% the CI is $(-.0064,\ .0864)$, which contains 0 and agrees with the test (working mine).

N.B under the lecturer's strict 10-and-10 rule, machine B has only $n\hat{p}_2=8$ defectives, so the large-sample condition fails. The memo does not comment. Say so if a question asks you to check the assumptions.

### F test for two variances (STA1B10 2012 Semester Test 2 Q2) (memo)
Pain thresholds: males $n=14$, $s^2=12.7$; females $n=10$, $s^2=26.4$. Is there a difference in variability, at $\alpha=.05$?

WORKING
- $H_0:\sigma_F^2=\sigma_M^2$ against $H_a:\sigma_F^2\neq\sigma_M^2$
- Larger variance on top: $f=26.4/12.7=2.08$ with df $(9, 13)$.
- Two-tailed, so compare with $F_{.025,9,13}=3.31$. The memo labels this value $F_{9;13;0.05}$, meaning the total $\alpha$ of .05.
- $2.08<3.31$, so do not reject $H_0$. There is insufficient evidence of a difference in variability. The p-value is above $2(0.10)=0.2$.

### The full two-sample chain: F test, then pooled t, then a bound (2018 Semester Test 2 Q1) (working mine)
Foam volume: Coke $\bar{x}=307.3$, $s_1=34.6$; Pepsi $\bar{y}=142.4$, $s_2=29.6$; 12 cans each. The normal probability plots report p-values .861 and .401.

WORKING
1. Equal variances at $\alpha=.10$. $f=34.6^2/29.6^2=1.37$ with df $(11,11)$. Compare with $F_{.05,11,11}\approx2.82$. Do not reject, so the equal-variance assumption holds.
2. Assumptions verified:
   - independent random samples (different cans)
   - normality (both plot p-values exceed .10)
   - equal variances (step 1)
   Use the pooled $t$.
3. $s_p^2=\dfrac{11(34.6)^2+11(29.6)^2}{22}=1036.66$, $SE=\sqrt{1036.66(2/12)}=13.14$
4. $H_a:\mu_1-\mu_2>0$, so $t=\dfrac{307.3-142.4}{13.14}=12.55>t_{.10,22}=1.321$. Reject $H_0$; the p-value is far below .0005.
5. Since $H_0$ was rejected, a Type I error is possible: concluding Coke foams more when it does not.
6. 99% lower bound: $164.9-t_{.01,22}(13.14)=164.9-2.508(13.14)=131.93$. Coke's mean foam volume exceeds Pepsi's by at least 131.93 ml.

N.B 2022 Paper C Q4 reprints this question with the column labels swapped (PEPSI 307.3, COKE 142.4) while the data clearly put Coke near 300. Check the summary table against the raw data before deciding which mean is which.

### ANOVA from raw data, then Tukey (2024 SA3 Q3; also 2016 Q8) (memo, labels corrected)
Service ratings: bank X 8, 7, 6, 7, 6; bank Y 9, 7, 7, 8, 7; bank Z 5, 6, 7, 5, 5. $I=3$, $J=5$; normal populations with equal variances; $\alpha=.10$.

WORKING
- Totals: $x_{1\cdot}=34$, $x_{2\cdot}=38$, $x_{3\cdot}=28$, $x_{\cdot\cdot}=100$; $\sum\sum x_{ij}^2=686$.
- $$SST=686-\frac{100^2}{15}=19.33\qquad SSTr=\frac{34^2+38^2+28^2}{5}-\frac{100^2}{15}=10.13\qquad SSE=9.20$$

| Source | SS | df | MS | F |
|---|---|---|---|---|
| Treatments | 10.13 | 2 | 5.07 | 6.61 |
| Error | 9.20 | 12 | 0.767 | |
| Total | 19.33 | 14 | | |

- $F_{.10,2,12}=2.81$. $6.61>2.81$, so reject $H_0$: mean ratings differ across the three banks.
- Tukey at $\alpha=.05$: $w=Q_{.05,3,12}\sqrt{0.7667/5}=3.77(0.3916)=1.48$.

```
Z      X      Y
5.6    6.8    7.6
-----------
       -----------
```

$6.8-5.6=1.2<1.48$ and $7.6-6.8=0.8<1.48$, so both neighbouring pairs are joined. $7.6-5.6=2.0>1.48$. Banks Y and Z differ significantly; bank X has not been shown to differ from either.

### ANOVA from a partial table (Tutorial 9 Q6, additional exercise; Solution 9) (memo)
Four brands of spark plug, five each. Given $SST=310{,}500.76$ and $MSE=14{,}713.69$.

WORKING
- df: treatments $3$, error $16$, total $19$.
- $SSE=16(14{,}713.69)=235{,}419.04$, $SSTr=310{,}500.76-235{,}419.04=75{,}081.72$, $MSTr=25{,}027.24$.
- $f=25{,}027.24/14{,}713.69=1.70<F_{.10,3,16}=2.46$, so the p-value is above .10. Do not reject $H_0$.

The same skill appears in 2020 SA2 Q6. There $I=3$, $J=8$, $MSE=0.2880$ and $f=3.529$, which gives $MSTr=1.0164$, $SSTr=2.03$, $SSE=6.05$ and $SST=8.08$ (working mine).

### Tukey grouping and choosing a treatment (Tutorial 9 Q11; Solution 9) (memo)
Five brands, $MSE=272.8$, $J=4$: $w=Q_{.05,5,15}\sqrt{272.8/4}=4.37(8.258)=36.09$.

```
3       1       4       2       5
437.5   462.0   469.3   512.8   532.1
---------------------   -------------
```

The brands split into two groups, $\{1,3,4\}$ and $\{2,5\}$. There are no significant differences within a group, and every between-group difference is significant.

For a "which should be used" question (2023 Paper A Q6d, circuit noise, low is best; working mine): $MSE=5034/16=314.65$ and $w=4.05\sqrt{314.65/5}=32.13$. Means: $\bar{x}_1=19.2$, $\bar{x}_3=49.8$, $\bar{x}_2=70.0$, $\bar{x}_4=79.8$. Lines join $\{1,3\}$ ($30.6<32.13$) and $\{3,2,4\}$ ($79.8-49.8=30.0<32.13$). Design 1 is the only design significantly quieter than designs 2 and 4. Design 3 is not shown to differ from any of the others. Choose design 1.

### Regression by hand from sums (2018 Semester Test 2 Q4) (working mine; matches the printout)
Training hours and output, $n=10$: $\sum x=311$, $\sum y=535$, $\sum x^2=10213$, $\sum y^2=29649$, $\sum xy=17240$.

WORKING
$$S_{xx}=10213-\frac{311^2}{10}=540.9\qquad S_{xy}=17240-\frac{(311)(535)}{10}=601.5\qquad S_{yy}=29649-\frac{535^2}{10}=1026.5$$
$$b_1=\frac{601.5}{540.9}=1.112\qquad b_0=53.5-1.112(31.1)=18.92\qquad \hat{y}=18.92+1.112x$$
- Slope: each extra hour of training raises average output by about 1.11 units.
- Intercept: the average output with no training would be 18.92. This is an extrapolation, because $x=0$ is outside the data.
- $r=\dfrac{601.5}{\sqrt{540.9(1026.5)}}=0.81$: a strong positive linear relationship. $r^2=0.6516$ matches the printout's R Square.
- Residual at $x=40$: $\hat{y}=18.92+1.112(40)=63.40$. The two workers with 40 hours produced 60 and 63, so their residuals are $-3.40$ and $-0.40$.
- Test: $t=3.868$ and $F=14.96=t^2$, p-value $.0048<.05$. Reject $H_0:\beta_1=0$; output is linearly related to training hours.

### Regression from a printout, with a PI (STA1B10 2012 Semester Test 2 Q7) (memo; the PI is working mine)
Forest age and tree diameter, $n=9$. The printout gives $b_0=12.056$, $b_1=0.328$, $t=49.77$, $MSE=1.2018$, $SSR=2976.48$, Total $SS=2984.89$.

WORKING
- $\hat{y}=12.056+0.328x$. $H_0:\beta_1=0$ against $H_a:\beta_1\neq0$; $t=49.77$ with p-value $\approx0$. Reject $H_0$: the model is useful.
- $\hat{y}(83)=39.28$ cm.
- 95% PI at $x_0=83$. From the raw data, $\bar{x}=79.44$ and $S_{xx}=27672.22$:
$$39.28\pm2.365\sqrt{1.2018\left(1+\frac19+\frac{(83-79.44)^2}{27672.22}\right)}=39.28\pm2.73=(36.54,\ 42.01)$$
- $r^2=2976.48/2984.89=99.72\%$ of the variation in diameter is explained by age.
- $s=\sqrt{MSE}=1.096$ estimates $\sigma$.
- Slope: diameter increases by 0.328 cm on average per extra year of age.

Also from printouts (2016 Q7, memo):
- Identify both test statistics: $t=-5.62$ and $F=31.61$, with the same p-value .0002.
- $r=-\sqrt{0.7597}=-0.8716$; the sign comes from the negative slope.
- Predicting at $x=100$ is refused because it is outside the observed $x$ range (extrapolation).

### Reading the diagnostic plots (2016 Q6 and 2011 Q6.2 to 6.3) (memo)
- Residuals versus fits:
  - a random band of equal width means constant variance holds (2011)
  - a cyclical or curved pattern, or a funnel, means the assumption is violated or the wrong model was fitted (2016)
- Normal probability plot:
  - roughly straight means normality holds (2011)
  - a clear S-shape far from a straight line means normality is violated (2016)

Each plot checks its own assumption only.

---

## Common mistakes

Pulled from the S6 to S9 struggle logs and callouts, at the pattern level.

- Treating paired data as two independent samples. Same subjects means differences, a one-sample $t$ and $n-1$ df. This slipped in three sessions. (S7, S8, S9)
- Putting a mean where a total belongs. $SSTr$, $SST$, $S_{xx}$ and $S_{xy}$ use totals squared over the count inside them, with no bars. A negative sum of squares is an alarm to check which count sits under which total, not something to guess past. (S8, S9)
- Reversing $MSE$ and $MSTr$. $MSE$ is built around each group's own mean and cannot see differences between means. $MSTr$ inflates when the means differ. (S8)
- Wrong $Q$ subscripts. Use $Q_{\alpha,I,I(J-1)}$: the second subscript is the number of means $I$ (not $I-1$), the third is the error df (not the total df). (S8)
- Reading a Tukey line as "equal". Joined means are "not shown to differ", and the relation is not transitive: 4 and 3 joined, 3 and 2 joined, yet 4 and 2 can differ. (S8)
- Running Tukey after failing to reject in ANOVA. Stop there; there is nothing to locate. (S8)
- Treating Tukey's $\alpha$ as the per-pair error rate. It is the family (experimentwise) rate, so each individual interval is wider than a plain 95% one. (S8)
- In the $SST$ proof: confusing which piece is $SSE$ (it contains $x_{ij}$, no $J$) and which is $SSTr$ (only means, carries the $J$), and dropping dots. (S8)
- Mixing up the diagnostic plots. The normal plot checks normality only. Residuals versus fits checks equal variance (and a U shape points to the wrong model). (S9)
- Giving a PI with the wrong centre. The CI and PI at the same $x_0$ share the centre $\hat{y}$; the PI is just wider. (S9)
- Confusing $r$ and $r^2$. $r^2=SSR/\text{Total }SS$, not $SSE$ over anything. $r$ is the square root with the slope's sign. (S9)
- Stating the regression null as "the model is useful" (as slide 20 prints it). The null is slope $=0$. (S9)
- In the $F$ test, using $F_\alpha$ for a two-tailed test (use $F_{\alpha/2}$), or swapping the variances without swapping the df. (S7)
- Treating a count of 8 as close enough to 10 in the proportion condition. The lecturer applies it strictly. (S7)
- Using $n>30$ for the large-sample cutoff. It is 40 throughout. (S7, lecturer's reply)
- Reading "fail to reject" as "proved $H_0$". (S5, carried)

---

## Tips

- Dissect the question before choosing a formula:
  - What is compared: means, proportions, variances, more than two means, or a relationship?
  - Same subjects or different?
  - Sample sizes against 40?
  - Variance or SD given? Mock Q15 gives sample variances, not SDs, so do not square them again.
  - Which population is 1? Define it in step 1 and keep the order throughout.
- Translate the wording into $\Delta_0$ and the direction of $H_a$:
  - "more than 70 greater" gives $\mu_D=70$ against $\mu_D>70$
  - "exceeds by more than 5" gives $\mu_1-\mu_2=-5$ against $<-5$ when 2 is the larger
  - "beneficial" or "lowered" fixes the direction of the difference you defined
- Type I or Type II after a decision. Rejected $H_0$ means only a Type I error is possible; not rejected means only a Type II. Then describe the error in the story: "concluding fluoride helps when it does not". (2016 Q3.3, 2018 Q1.4)
- A CI confirms a test only when both use the same $\alpha$ and sidedness. When they disagree, check the levels first (2024 SA3 Q1c).
- Read a printout by role:
  - Coefficients give $b_0$ and $b_1$; the slope row's t Stat and P-value give the slope test.
  - Significance F is the p-value of $F$.
  - R Square is $r^2$; Multiple R is $\lvert r\rvert$, and the sign comes from the slope.
  - Standard Error is $\sqrt{MSE}$, the estimate of $\sigma$.
  - Lower 95% and Upper 95% on the slope row give the CI for $\beta_1$.
- A residual is observed minus fitted, $y-\hat{y}$, at a data point. A negative residual means the point lies below the line. (2022 Paper C Q10e)
- "What percentage cannot be explained" is $1-r^2$. (2022 Paper C Q10b, 2025 SA3 Q4f)
- Refuse to predict outside the observed $x$ range, and say why (extrapolation). For a prediction inside the range, comment on reliability from $r^2$. (2016 Q7.3, 2022 Paper C Q10d)
- The best estimate of the common $\sigma$ in ANOVA or regression is $\sqrt{MSE}$. (2011 Q5.4, 2012 Q7.6)
- ANOVA from totals: compute $x_{\cdot\cdot}^2/IJ$ once and reuse it in both $SST$ and $SSTr$, then get $SSE$ by subtraction. If $SSE$ is given instead (2023 Paper A Q6b), work backwards: $SSTr=SST-SSE$.
- Sanity checks:
  - Every SS is at least 0.
  - Df add up: $IJ-1=(I-1)+I(J-1)$ and $n-1=1+(n-2)$.
  - $F=t^2$ in regression.
  - The fitted line passes through $(\bar{x},\bar{y})$.

---

## Memo errors: do not copy

Each was checked by recomputing from the question data.

| Source | What it says | Correct |
|---|---|---|
| Solution 7 Q3 | "by significantly more than 500" | 5000, as in the hypotheses |
| STA1B10 2016 memo Q3.2 (twins, paired) | $s_d^2=5$; p-value $=0.0058$ | $s_d=5$ ($s_d^2=25$); $t=2.2$ on 3 df gives p-value $\approx0.058$ ($.05<p<.10$). The decision "do not reject" stands |
| 2016 memo Q8.2 and 2024 SA3 memo Q3b (banks) | Means labelled 5.6 $=\bar{x}_2$, 6.8 $=\bar{x}_3$, 7.6 $=\bar{x}_1$; "difference between treatments 1 and 2" | $\bar{x}_X=6.8$, $\bar{x}_Y=7.6$, $\bar{x}_Z=5.6$. The significant difference is between banks Y and Z (treatments 2 and 3) |
| STA1B10 2011 memo Q6.7 (doctors PI) | Sets the $(x_0-\bar{x})^2/S_{xx}$ term to 0 | $\bar{x}$ is not given in the printout, so the memo drops the term. Correctly the term is included, and the PI is slightly wider unless $x_0=\bar{x}$ |
| 2024 SA3 memo Q1 (bolts) | Treats the two-proportion procedures as valid | Machine B has $n\hat{p}_2=8<10$, so it fails the strict validity rule |
| 2022 Paper C Q4 | Summary table headed PEPSI 307.3, COKE 142.4 | The raw data put Coke at 307.3 (the 2018 paper has the labels the right way round) |
| 2023 Paper A Q3 | Gives $\bar{d}=4.96$, $s_d^2=8.24$ | The raw data give $\bar{d}=4.93$ and $s_d^2=8.50$. Use the given values in the exam, since that is what the memo will use |

---

## Do not forget

- Pick the procedure first: same subjects means paired; proportions mean $z$; variances mean $F$; more than two means means ANOVA then Tukey; a relationship means regression.
- Two means: both samples over 40 means $z$ with $s^2$; otherwise pooled $t$ on $m+n-2$ df, with normality and equal variances stated.
- Proportions: pool $\hat{p}$ for the test, do not pool for the CI, and check all four counts are at least 10.
- $F$ test: larger variance on top, df from the top group first, $F_{\alpha/2}$ for two-tailed.
- ANOVA: totals in the computing formulas, $F=MSTr/MSE$ on $(I-1, I(J-1))$, and both assumptions stated (normality and homoscedasticity).
- Tukey: $w=Q_{\alpha,I,I(J-1)}\sqrt{MSE/J}$, only after rejecting; joined means are not shown to differ.
- Regression: $b_1=S_{xy}/S_{xx}$, $b_0=\bar{y}-b_1\bar{x}$, $r^2=SSR/\text{Total }SS$, $t^2=F$, the null is slope 0. The PI is wider than the CI and shares its centre.
- Every application: formula, substitute, simplify, interpret, with the conclusion in context and naming $\alpha$.
- Proofs to rehearse: $SST=SSTr+SSE$, $E(MSE)=\sigma^2$, $E(S_p^2)=\sigma^2$, and $E$ and $V$ of $\hat{p}_1-\hat{p}_2$ and of $\bar{X}-\bar{Y}$ (see [[STA01B1_Proofs_ST2]]).

## See also
- [[STA01B1_Proofs_ST2]]
- [[STA01B1_Summary_ST1]]
- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]]
- [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances]]
- [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]]
- [[STA01B1_Notes_S9_Simple_Linear_Regression]]
- [[STA01B1_Notes_S5_Hypothesis_Testing]]
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]
