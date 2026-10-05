---
module: STA01B1
topic: Proofs and Derivations
test: ST2
range: S6 to S9
tags: [theorem, formula, exam-flagged, struggle, added]
---

# STA01B1 Proofs (ST2, sessions S6 to S9)

Every derivation the Summative Assessment 2 theory test (Friday 9 October 2026) can ask for. That means two-sample inference, ANOVA and regression, plus the proof questions that past papers actually set on this material. Each heading names the result being proven.

Source labels:
- `(shown in source)`: the working appears on the lecture slides or in the session note.
- `(source: lecturer's proof)`: built in session S8 from the lecturer's method, as the student described it.
- `(source: past paper memo, ...)`: the derivation is printed in a departmental memo.
- `(added)`: a standard derivation of a result the source only states. It is marked so you can tell it apart from lecture material. Where a past paper asks for an added proof, that is noted too.

The last section lists results that are stated without proof at this level.

> [!note] About the links
> Many headings in the S7 to S9 notes carry an inline tag (for example `#theorem`), and I can't reliably anchor a link to those headings. Citations to them therefore link the whole file and name the heading in plain text. Untagged headings are anchored directly.

Standing notation: $X_1,\dots,X_m$ is a random sample with mean $\mu_1$ and variance $\sigma_1^2$, and $Y_1,\dots,Y_n$ is an independent random sample with mean $\mu_2$ and variance $\sigma_2^2$. In ANOVA there are $I$ groups with $J$ observations each. In regression there are $n$ pairs $(x_i, y_i)$.

---

## Part A. Two-sample inference (S6, S7)

## 1. Mean and variance of X̄ − Ȳ

Result: $E(\bar{X}-\bar{Y}) = \mu_1-\mu_2$ and $V(\bar{X}-\bar{Y}) = \dfrac{\sigma_1^2}{m}+\dfrac{\sigma_2^2}{n}$. #formula #theorem

(shown in source; see: [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Setup: assumptions and the distribution of X̄ − Ȳ|Setup: assumptions and the distribution of X̄ − Ȳ]])

Mean, by linearity of expectation (no independence needed):
$$E(\bar{X}-\bar{Y}) = E(\bar{X}) - E(\bar{Y}) = \mu_1 - \mu_2$$

Variance. For independent rvs, $V(aU+bW) = a^2V(U)+b^2V(W)$. Here $a=1$ and $b=-1$:
$$V(\bar{X}-\bar{Y}) = (1)^2V(\bar{X}) + (-1)^2V(\bar{Y}) = V(\bar{X})+V(\bar{Y}) = \frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}$$

using $V(\bar{X}) = \sigma_1^2/m$ and $V(\bar{Y}) = \sigma_2^2/n$ (proved in [[STA01B1_Proofs_ST1]], section 1).

$$\sigma_{\bar{X}-\bar{Y}} = \sqrt{\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}}$$

N.B the means subtract but the variances add, because $(-1)^2 = +1$. Independence of the two samples is what removes the covariance term.

-> Standardising $\bar{X}-\bar{Y}$ with this mean and standard deviation gives every $Z$ statistic for two means. The pooled $t$ uses the same structure with a common $\sigma^2$.

---

## 2. Building a confidence interval for μ1 − μ2 from the pivot

Result: $\bar{x}-\bar{y} \pm z_{\alpha/2}\sqrt{\dfrac{s_1^2}{m}+\dfrac{s_2^2}{n}}$ is a large-sample $100(1-\alpha)\%$ CI for $\mu_1-\mu_2$. #formula #added

(added; the interval is stated in [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Large Sample Confidence Interval for μ1 − μ2|Large Sample Confidence Interval for μ1 − μ2]]. The same steps apply to every interval in this module.)

For $m>40$ and $n>40$ the pivot
$$Z = \frac{\bar{X}-\bar{Y}-(\mu_1-\mu_2)}{\sqrt{\dfrac{S_1^2}{m}+\dfrac{S_2^2}{n}}}$$
is approximately standard normal. Write $SE = \sqrt{S_1^2/m + S_2^2/n}$. Then
$$P\left(-z_{\alpha/2} < \frac{\bar{X}-\bar{Y}-(\mu_1-\mu_2)}{SE} < z_{\alpha/2}\right) \approx 1-\alpha$$

Multiply through by $SE$ (positive, so the inequalities keep their direction):
$$P\left(-z_{\alpha/2}SE < \bar{X}-\bar{Y}-(\mu_1-\mu_2) < z_{\alpha/2}SE\right) \approx 1-\alpha$$

Subtract $\bar{X}-\bar{Y}$, then multiply by $-1$ (which reverses both inequalities):
$$P\left(\bar{X}-\bar{Y}-z_{\alpha/2}SE < \mu_1-\mu_2 < \bar{X}-\bar{Y}+z_{\alpha/2}SE\right) \approx 1-\alpha$$

Substituting the observed values gives the interval.

One-sided bounds. Put all of $\alpha$ in one tail. $P(Z < z_\alpha) = 1-\alpha$ rearranges to the lower bound $\mu_1-\mu_2 > \bar{x}-\bar{y}-z_\alpha SE$. $P(Z > -z_\alpha) = 1-\alpha$ gives the upper bound $\mu_1-\mu_2 < \bar{x}-\bar{y}+z_\alpha SE$.

The same argument, with a different pivot, produces every other interval in this module:
- Pooled $t$: pivot $\dfrac{\bar{X}-\bar{Y}-(\mu_1-\mu_2)}{\sqrt{S_p^2(1/m+1/n)}} \sim t_{m+n-2}$, critical value $t_{\alpha/2,m+n-2}$.
- Paired: pivot $\dfrac{\bar{D}-\mu_D}{S_D/\sqrt{n}} \sim t_{n-1}$.
- Two proportions: pivot $\dfrac{\hat{p}_1-\hat{p}_2-(p_1-p_2)}{\sqrt{\hat{p}_1\hat{q}_1/m+\hat{p}_2\hat{q}_2/n}} \approx N(0,1)$.

---

## 3. Test and interval agree (two-sided)

Result: a two-sided level $\alpha$ test of $H_0: \mu_1-\mu_2 = \Delta_0$ fails to reject exactly when $\Delta_0$ lies inside the $100(1-\alpha)\%$ CI. #theorem #added

(added; past papers use this in the form "use the interval to confirm your test conclusion", for example STA1B10 2011 Semester Test 2 Q1.2 and STA01B1 2024 Summative Assessment 3 Q1c.)

$$\text{Do not reject } H_0 \iff -z_{\alpha/2} < \frac{\bar{x}-\bar{y}-\Delta_0}{SE} < z_{\alpha/2} \iff \bar{x}-\bar{y}-z_{\alpha/2}SE < \Delta_0 < \bar{x}-\bar{y}+z_{\alpha/2}SE$$

The last statement says that $\Delta_0$ is inside the CI.

N.B this only holds when the CI level matches the test ($100(1-\alpha)\%$ with the same $\alpha$) and both are two-sided, or both one-sided in the same direction. The 2024 Summative Assessment 3 memo (Q1c) shows a 90% CI and a 5% test disagreeing for exactly this reason.

---

## 4. The pooled variance is an unbiased estimator of σ²

Result: if $\sigma_1^2 = \sigma_2^2 = \sigma^2$, then $S_p^2 = \dfrac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}$ satisfies $E(S_p^2) = \sigma^2$. #theorem #exam-flagged

(source: past paper memo, STA1B10 2012 Semester Test 2 Q6, 3 marks. The memo writes $n_1, n_2$, which are $m, n$ in the lecture notation. The formula is in [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples#Where the pooled variance comes from (source: user-transcribed, Devore and Berk section 9.2)|Where the pooled variance comes from]].)

Uses $E(S_1^2) = E(S_2^2) = \sigma^2$ (sample variance unbiased, [[STA01B1_Proofs_ST1]] section 4) and equal variances.

$$E(S_p^2) = E\left[\frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}\right]$$
$$= \frac{(n_1-1)E(S_1^2)+(n_2-1)E(S_2^2)}{n_1+n_2-2}$$
$$= \frac{(n_1-1)\sigma^2+(n_2-1)\sigma^2}{n_1+n_2-2}$$
$$= \sigma^2\left(\frac{n_1-1+n_2-1}{n_1+n_2-2}\right)$$
$$= \sigma^2$$

N.B the equal-variance assumption is used in the third line. Without it the two terms would be $\sigma_1^2$ and $\sigma_2^2$ and could not be factored out.

-> The same argument, extended from 2 groups to $k$ groups, proves that $MSE$ is unbiased (section 9).

---

## 5. Mean and variance of p̂1 − p̂2

Result: for independent $X \sim \text{Bin}(m,p_1)$ and $Y \sim \text{Bin}(n,p_2)$, with $\hat{p}_1 = X/m$ and $\hat{p}_2 = Y/n$,
$$E(\hat{p}_1-\hat{p}_2) = p_1-p_2 \qquad V(\hat{p}_1-\hat{p}_2) = \frac{p_1q_1}{m}+\frac{p_2q_2}{n}$$
#theorem #exam-flagged

(added in session; the slide defers the proof to the textbook. See: [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances#Difference of Two Proportions, Mean and Variance of p̂1 − p̂2|Difference of Two Proportions, Mean and Variance of p̂1 − p̂2]]. Past paper: STA01B1 2023 Paper A Q4, (a) 3 marks "Use rules of expected value to show ... unbiased ... Show ALL possible steps", (b) 4 marks "Determine $V(\hat{p}_1-\hat{p}_2)$".)

Binomial facts used: $E(X) = mp_1$, $V(X) = mp_1q_1$, $E(Y) = np_2$, $V(Y) = np_2q_2$, with $q = 1-p$.

(a) Unbiased:
$$E(\hat{p}_1-\hat{p}_2) = E\left(\frac{X}{m}-\frac{Y}{n}\right)$$
$$= \frac{1}{m}E(X)-\frac{1}{n}E(Y)$$
$$= \frac{1}{m}(mp_1)-\frac{1}{n}(np_2)$$
$$= p_1-p_2$$

so $\hat{p}_1-\hat{p}_2$ is an unbiased estimator of $p_1-p_2$.

(b) Variance, using independence of $X$ and $Y$:
$$V(\hat{p}_1-\hat{p}_2) = V\left(\frac{X}{m}-\frac{Y}{n}\right)$$
$$= \left(\frac{1}{m}\right)^2V(X)+\left(-\frac{1}{n}\right)^2V(Y)$$
$$= \frac{mp_1q_1}{m^2}+\frac{np_2q_2}{n^2}$$
$$= \frac{p_1q_1}{m}+\frac{p_2q_2}{n}$$

N.B constants come out of a variance squared, so the minus sign disappears. This is section 1 with $\sigma^2$ replaced by $pq$, because $\hat{p}$ is $\bar{X}$ of 0/1 indicators.

-> Under $H_0: p_1 = p_2 = p$ the variance becomes $pq(1/m+1/n)$. Estimating the common $p$ by $\hat{p} = (X+Y)/(m+n)$ gives the test statistic's denominator. The CI does not assume $p_1 = p_2$, so it keeps the separate $\hat{p}_1\hat{q}_1/m + \hat{p}_2\hat{q}_2/n$.

---

## 6. Where the F statistic comes from

Result: for independent random samples from normal populations, $F = \dfrac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2} \sim F_{m-1,\,n-1}$, and under $H_0: \sigma_1^2 = \sigma_2^2$ this reduces to $f = s_1^2/s_2^2$. #theorem

(The theorem is stated in source, Lecture 8 slide 23; see [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances#The F Distribution and the Test for Two Population Variances, Example 9.14|The F Distribution and the Test for Two Population Variances, Example 9.14]]. The link to chi-squared below is added.)

Definition (added; STA01B1 2023 Paper A Q1b asks which distribution this ratio follows): if $X_1 \sim \chi^2_{\nu_1}$ and $X_2 \sim \chi^2_{\nu_2}$ are independent, then
$$\frac{X_1/\nu_1}{X_2/\nu_2} \sim F_{\nu_1,\nu_2}$$

From a normal sample, $\dfrac{(m-1)S_1^2}{\sigma_1^2} \sim \chi^2_{m-1}$ and $\dfrac{(n-1)S_2^2}{\sigma_2^2} \sim \chi^2_{n-1}$ (the variance pivot from S4). Divide each by its df:
$$\frac{\dfrac{(m-1)S_1^2}{\sigma_1^2}\Big/(m-1)}{\dfrac{(n-1)S_2^2}{\sigma_2^2}\Big/(n-1)} = \frac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2} \sim F_{m-1,\,n-1}$$

Under $H_0$, $\sigma_1^2 = \sigma_2^2$ cancels, leaving $f = s_1^2/s_2^2$ with no unknown parameter.

N.B the normality of both populations is built into the chi-squared step. That is why the F test is so sensitive to non-normality.

---

## 7. The reciprocal rule for lower F critical values

Result: $F_{1-\alpha,\,\nu_1,\,\nu_2} = \dfrac{1}{F_{\alpha,\,\nu_2,\,\nu_1}}$. #formula #added

(added; the rule is stated in the S7 note and used in Solution 8 Q60d. $F_{\alpha}$ means the value with area $\alpha$ to its right.)

From the definition in section 6, if $F \sim F_{\nu_1,\nu_2}$ then $1/F = \dfrac{X_2/\nu_2}{X_1/\nu_1} \sim F_{\nu_2,\nu_1}$, so the df swap.

By the definition of the critical value, $P(F \le F_{1-\alpha,\nu_1,\nu_2}) = \alpha$. Taking reciprocals reverses the inequality:
$$P\left(\frac{1}{F} \ge \frac{1}{F_{1-\alpha,\nu_1,\nu_2}}\right) = \alpha$$

$1/F$ has the $F_{\nu_2,\nu_1}$ distribution, and the value with area $\alpha$ to its right is $F_{\alpha,\nu_2,\nu_1}$. Therefore
$$\frac{1}{F_{1-\alpha,\nu_1,\nu_2}} = F_{\alpha,\nu_2,\nu_1}$$

-> This is also why the "larger variance on top" shortcut works. Flipping the ratio flips the df, and a lower-tail rejection becomes an upper-tail one.

---

## Part B. Single-factor ANOVA (S8)

## 8. SST = SSTr + SSE

Result: $\displaystyle\sum_i\sum_j(x_{ij}-\bar{x}_{\cdot\cdot})^2 = \sum_i\sum_j(x_{ij}-\bar{x}_{i\cdot})^2 + J\sum_i(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2$ #theorem #exam-flagged #struggle

(source: lecturer's proof, reproduced exactly as in [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]], heading "Proof that SST = SSTr + SSE". The lecturer flagged it as likely worth 6 to 8 marks, with a mark lost for each missed dot.)

Know these first:
$$SSE = \sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})^2$$
$$SSTr = \sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = J\sum_i(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2$$
$$\sum_j x_{ij} = J\bar{x}_{i\cdot}$$

The third line is the group-mean rule, from $\bar{x}_{i\cdot} = \sum_j x_{ij}/J$. Rule for constants: if $i$ or $j$ does not appear in an expression, the expression is constant with respect to that index.

Step 1. Definition.
$$SST = \sum_i\sum_j (x_{ij} - \bar{x}_{\cdot\cdot})^2$$

Step 2. Add 0 in the form $-\bar{x}_{i\cdot} + \bar{x}_{i\cdot}$ and regroup into two brackets.
$$SST = \sum_i\sum_j \Big[(x_{ij} - \bar{x}_{i\cdot}) + (\bar{x}_{i\cdot} - \bar{x}_{\cdot\cdot})\Big]^2$$

Step 3. Expand as $a^2 + 2ab + b^2$, with $a = x_{ij} - \bar{x}_{i\cdot}$ and $b = \bar{x}_{i\cdot} - \bar{x}_{\cdot\cdot}$. Keep the middle term as two brackets with the 2 in front.
$$SST = \sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})^2 + 2\sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot}) + \sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2$$

Step 4. Substitute the two ends.
- The first piece contains $x_{ij}$ and matches the definition exactly, so it is $SSE$, with no $J$.
- The last piece has no $j$, so the inner sum gives $J$:
$$\sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = J\sum_i(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = SSTr$$

Step 5. Middle term: distribute the second bracket over the first and let the sum act on each term. Keep the 2.
$$2\sum_i\sum_j x_{ij}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot}) \;-\; 2\sum_i\sum_j \bar{x}_{i\cdot}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$$

Step 6. Substitute inside each term.
- First term: $(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$ has no $j$, so it is constant. Use $\sum_j x_{ij} = J\bar{x}_{i\cdot}$.
- Second term: nothing has a $j$, so the sum over $j$ gives $J$.
$$2\sum_i J\bar{x}_{i\cdot}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot}) \;-\; 2\sum_i J\bar{x}_{i\cdot}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$$

Step 7. Cancel. The two terms are identical and subtracted, so they cancel as they stand, with the summation left in place. The middle term is $0$.

Step 8. Done.
$$SST = SSE + SSTr$$

> [!warning] Where marks are lost
> The piece with $x_{ij}$ in it is $SSE$ and has no $J$. The piece with only means is $SSTr$ and carries the $J$. Dots: $x_{ij}$ has none, $\bar{x}_{i\cdot}$ has one, $\bar{x}_{\cdot\cdot}$ has two. The 2 stays on both middle terms until they cancel. Only the first middle term uses $\sum_j x_{ij} = J\bar{x}_{i\cdot}$, because it is the only one that still contains $x_{ij}$. #struggle

(added) The proof is pure algebra and needs no normality or equal-variance assumption. Those assumptions matter only for the distribution of $F$.

> *The eight moves, in short: write it, add 0, expand, name the two ends, distribute the middle, substitute with the group-mean rule, cancel, done.*

---

## 9. SSE in terms of the sample variances, and MSE is unbiased for σ²

Result: $SSE = (J-1)(S_1^2+\cdots+S_I^2)$, and under homoscedasticity $E(MSE) = \sigma^2$. #theorem #exam-flagged

(The first identity is stated in source, Lecture 9 slide 10. The unbiasedness proof is added. Past paper: STA01B1 2022 Paper C Q5, 5 marks: "Determine whether $MSE = \dfrac{SSE}{n-k} = \dfrac{(n_1-1)s_1^2+(n_2-1)s_2^2+\cdots+(n_k-1)s_k^2}{n-k}$ ... is an unbiased estimator of $\sigma^2$ or not. Keep in mind that one of the assumptions ... is the assumption of equal variances (homoscedasticity)." No memo was supplied, so the working below is mine. It follows the same steps as the memo proof in section 4.)

Part 1, the identity. Group $i$'s sample variance is $S_i^2 = \dfrac{\sum_j (X_{ij}-\bar{X}_{i\cdot})^2}{J-1}$, so $\sum_j (X_{ij}-\bar{X}_{i\cdot})^2 = (J-1)S_i^2$. Sum over $i$:
$$SSE = \sum_i\sum_j (X_{ij}-\bar{X}_{i\cdot})^2 = \sum_i (J-1)S_i^2 = (J-1)\left(S_1^2+S_2^2+\cdots+S_I^2\right)$$

With unequal group sizes $n_i$ the same step gives $SSE = \sum_i (n_i-1)S_i^2$. The error df is then $\sum_i(n_i-1) = n-k$, with $n = \sum n_i$ the total number of observations and $k$ the number of groups. With equal sizes, $n-k = IJ-I = I(J-1)$.

Part 2, unbiasedness. Homoscedasticity says every group has the same $\sigma^2$. Since each $S_i^2$ is unbiased for its own population variance, $E(S_i^2) = \sigma^2$ for every $i$.
$$E(MSE) = E\left[\frac{(n_1-1)S_1^2+(n_2-1)S_2^2+\cdots+(n_k-1)S_k^2}{n-k}\right]$$
$$= \frac{(n_1-1)E(S_1^2)+(n_2-1)E(S_2^2)+\cdots+(n_k-1)E(S_k^2)}{n-k}$$
$$= \frac{(n_1-1)\sigma^2+(n_2-1)\sigma^2+\cdots+(n_k-1)\sigma^2}{n-k}$$
$$= \sigma^2\,\frac{(n_1+n_2+\cdots+n_k)-k}{n-k}$$
$$= \sigma^2\,\frac{n-k}{n-k} = \sigma^2$$

So $MSE$ is an unbiased estimator of $\sigma^2$. This holds whether or not $H_0$ is true, because nothing in the proof uses the group means.

N.B homoscedasticity is used in the third line. Without it the terms would be $\sigma_1^2,\dots,\sigma_k^2$, and $E(MSE)$ would be a weighted average of different variances, not one $\sigma^2$. Say so explicitly, because the question points at it.

-> This is the formal reason "MSE does not feel the means". It also explains why $\hat{\sigma} = \sqrt{MSE}$ is the estimate of the common standard deviation in past papers (2011 Q5.4, 2016 Q7.5).

---

## 10. The ANOVA computing formulas

Result: $SST = \sum_i\sum_j x_{ij}^2 - \dfrac{x_{\cdot\cdot}^2}{IJ}$ and $SSTr = \dfrac{\sum_i x_{i\cdot}^2}{J} - \dfrac{x_{\cdot\cdot}^2}{IJ}$, with $x_{i\cdot}$ and $x_{\cdot\cdot}$ totals (no bars). #formula #added #struggle

(added; the formulas are stated in source, Lecture 9 slide 13.)

Totals and means are linked by $x_{i\cdot} = J\bar{x}_{i\cdot}$ and $x_{\cdot\cdot} = IJ\bar{x}_{\cdot\cdot}$.

SST. Expand the square. $\bar{x}_{\cdot\cdot}$ is constant, and $\sum_i\sum_j x_{ij} = x_{\cdot\cdot} = IJ\bar{x}_{\cdot\cdot}$:
$$SST = \sum_i\sum_j x_{ij}^2 - 2\bar{x}_{\cdot\cdot}\sum_i\sum_j x_{ij} + IJ\bar{x}_{\cdot\cdot}^2$$
$$= \sum_i\sum_j x_{ij}^2 - 2IJ\bar{x}_{\cdot\cdot}^2 + IJ\bar{x}_{\cdot\cdot}^2 = \sum_i\sum_j x_{ij}^2 - IJ\bar{x}_{\cdot\cdot}^2$$
$$= \sum_i\sum_j x_{ij}^2 - IJ\left(\frac{x_{\cdot\cdot}}{IJ}\right)^2 = \sum_i\sum_j x_{ij}^2 - \frac{x_{\cdot\cdot}^2}{IJ}$$

SSTr. Expand the square, using $\sum_i \bar{x}_{i\cdot} = I\bar{x}_{\cdot\cdot}$ (equal group sizes):
$$SSTr = J\sum_i \bar{x}_{i\cdot}^2 - 2J\bar{x}_{\cdot\cdot}\sum_i\bar{x}_{i\cdot} + IJ\bar{x}_{\cdot\cdot}^2 = J\sum_i \bar{x}_{i\cdot}^2 - IJ\bar{x}_{\cdot\cdot}^2$$

Then $J\bar{x}_{i\cdot}^2 = J\left(\dfrac{x_{i\cdot}}{J}\right)^2 = \dfrac{x_{i\cdot}^2}{J}$ and $IJ\bar{x}_{\cdot\cdot}^2 = \dfrac{x_{\cdot\cdot}^2}{IJ}$, so
$$SSTr = \frac{\sum_i x_{i\cdot}^2}{J} - \frac{x_{\cdot\cdot}^2}{IJ}$$

N.B every term is a total squared over the number of observations in that total: $x_{i\cdot}^2$ over $J$, $x_{\cdot\cdot}^2$ over $IJ$. A sum of squares can never be negative. A negative answer means a count went under the wrong total.

---

## 11. The simultaneous confidence level (why Tukey's intervals are wider)

Result: for $k$ independent 95% intervals, the joint level is $100(.95)^k\%$, and holding the joint level at 95% needs individual levels of $100(.95)^{1/k}\%$. #formula

(shown in source, Lecture 9 slides 32 and 33; see [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]], heading "What alpha means in Tukey's procedure". The $k$ form is added.)

Two independent intervals, each capturing its parameter with probability .95:
$$P(\text{both capture}) = (.95)(.95) = (.95)^2 = .9025 \approx .90$$

Three: $(.95)^3 \approx .857$, about 86%. To make two intervals jointly 95%, each must satisfy $c^2 = .95$, so $c = \sqrt{.95} \approx .975$. In general $c = (.95)^{1/k}$.

N.B Tukey's intervals are not independent ($MSE$ is in every one, and sample means are shared), so this arithmetic only illustrates the idea. The fact to quote is that $Q_{.05}$ gives a simultaneous level of 95%. The $\alpha$ is the family (experimentwise) error rate, and each individual interval is wider than a plain 95% interval.

---

## Part C. Simple linear regression (S9)

## 12. The computing forms of Sxx and Sxy

Result: $S_{xx} = \sum(x_i-\bar{x})^2 = \sum x_i^2 - \dfrac{(\sum x_i)^2}{n}$ and $S_{xy} = \sum(x_i-\bar{x})(y_i-\bar{y}) = \sum x_iy_i - \dfrac{(\sum x_i)(\sum y_i)}{n}$. #formula #added

(added; the computing forms are stated in source, Lecture 10 slide 13.)

$$\sum(x_i-\bar{x})^2 = \sum x_i^2 - 2\bar{x}\sum x_i + n\bar{x}^2 = \sum x_i^2 - 2n\bar{x}^2 + n\bar{x}^2 = \sum x_i^2 - n\bar{x}^2 = \sum x_i^2 - \frac{(\sum x_i)^2}{n}$$

$$\sum(x_i-\bar{x})(y_i-\bar{y}) = \sum x_iy_i - \bar{y}\sum x_i - \bar{x}\sum y_i + n\bar{x}\bar{y} = \sum x_iy_i - n\bar{x}\bar{y} = \sum x_iy_i - \frac{(\sum x_i)(\sum y_i)}{n}$$

Two useful by-products: $\sum(x_i-\bar{x}) = 0$, and therefore $\sum x_i(y_i-\bar{y}) = S_{xy}$ and $\sum x_i(x_i-\bar{x}) = S_{xx}$. Each holds because the extra piece is $\bar{x}\sum(y_i-\bar{y}) = 0$ or $\bar{x}\sum(x_i-\bar{x}) = 0$.

---

## 13. The least squares estimators

Result: minimising $SSE = \sum(y_i-b_0-b_1x_i)^2$ gives $b_1 = \dfrac{S_{xy}}{S_{xx}}$ and $b_0 = \bar{y}-b_1\bar{x}$. #theorem #exam-flagged

(added in session; see [[STA01B1_Notes_S9_Simple_Linear_Regression]], heading "Where the estimators come from". The estimators themselves are stated in source, Lecture 10 slide 13. Past papers ask you to "calculate the equation of the line of best fit, showing all formulae and steps", for example STA01B1 2025 SA3 Q4b, but none on file asks for this derivation.)

Set both partial derivatives to zero.

With respect to $b_0$:
$$\frac{\partial SSE}{\partial b_0} = -2\sum(y_i-b_0-b_1x_i) = 0$$
$$\Rightarrow \sum y_i - nb_0 - b_1\sum x_i = 0 \Rightarrow b_0 = \bar{y}-b_1\bar{x}$$

This condition also says $\sum e_i = 0$, where $e_i = y_i - \hat{y}_i$ is the residual.

With respect to $b_1$:
$$\frac{\partial SSE}{\partial b_1} = -2\sum x_i(y_i-b_0-b_1x_i) = 0 \Rightarrow \sum x_ie_i = 0$$

Substitute $b_0 = \bar{y}-b_1\bar{x}$:
$$\sum x_i\left(y_i-\bar{y}+b_1\bar{x}-b_1x_i\right) = 0$$
$$\sum x_i(y_i-\bar{y}) = b_1\sum x_i(x_i-\bar{x})$$

By section 12 the left side is $S_{xy}$ and the sum on the right is $S_{xx}$:
$$S_{xy} = b_1S_{xx} \Rightarrow b_1 = \frac{S_{xy}}{S_{xx}}$$

Consequence: at $x = \bar{x}$, $\hat{y} = b_0 + b_1\bar{x} = \bar{y}$, so the fitted line always passes through $(\bar{x},\bar{y})$.

N.B keep the two conditions $\sum e_i = 0$ and $\sum x_ie_i = 0$. They make the cross term vanish in section 14, and they explain why the error df is $n-2$.

---

## 14. Total SS = SSR + SSE

Result: $\sum(y_i-\bar{y})^2 = \sum(\hat{y}_i-\bar{y})^2 + \sum(y_i-\hat{y}_i)^2$ #theorem

(added in session; see [[STA01B1_Notes_S9_Simple_Linear_Regression]], heading "Why the total splits". The identity is stated in source, Lecture 10 slide 15.)

Add 0 in the form $-\hat{y}_i+\hat{y}_i$:
$$y_i-\bar{y} = (y_i-\hat{y}_i) + (\hat{y}_i-\bar{y}) = e_i + (\hat{y}_i-\bar{y})$$

Square and sum:
$$\text{Total }SS = \sum e_i^2 + 2\sum e_i(\hat{y}_i-\bar{y}) + \sum(\hat{y}_i-\bar{y})^2 = SSE + 2\sum e_i(\hat{y}_i-\bar{y}) + SSR$$

Cross term, with $\hat{y}_i = b_0 + b_1x_i$:
$$\sum e_i(\hat{y}_i-\bar{y}) = \sum e_i(b_0+b_1x_i-\bar{y}) = (b_0-\bar{y})\sum e_i + b_1\sum x_ie_i = 0 + 0$$

by the two least squares conditions from section 13. Therefore $\text{Total }SS = SSR + SSE$.

> *This has the same shape as the ANOVA proof (expand a square, and the middle term vanishes), but the middle term is killed differently: here by the least squares conditions, there by the group-mean rule. Do not mix the two in an exam. The ANOVA one is the proof the lecturer flagged.*

---

## 15. Shortcuts for SSR, and r² = SSR / Total SS

Result: $SSR = b_1^2S_{xx} = b_1S_{xy} = \dfrac{S_{xy}^2}{S_{xx}}$ and $r^2 = \dfrac{S_{xy}^2}{S_{xx}S_{yy}} = \dfrac{SSR}{\text{Total }SS}$. #formula #added

(added in session; see [[STA01B1_Notes_S9_Simple_Linear_Regression]], headings "Two shortcuts for SSR" and "Strength of the relationship". The source marks $r^2 = SSR/\text{Total }SS$ "NB!!".)

Since $b_0 = \bar{y}-b_1\bar{x}$:
$$\hat{y}_i-\bar{y} = b_0+b_1x_i-\bar{y} = b_1(x_i-\bar{x})$$

So
$$SSR = \sum b_1^2(x_i-\bar{x})^2 = b_1^2S_{xx} = \left(\frac{S_{xy}}{S_{xx}}\right)^2S_{xx} = \frac{S_{xy}^2}{S_{xx}} = b_1S_{xy}$$

Then, with $\text{Total }SS = S_{yy}$:
$$r^2 = \frac{S_{xy}^2}{S_{xx}S_{yy}} = \frac{S_{xy}^2/S_{xx}}{S_{yy}} = \frac{SSR}{\text{Total }SS}$$

N.B $r = S_{xy}/\sqrt{S_{xx}S_{yy}}$ takes the sign of $S_{xy}$, which is the sign of $b_1$. When you take $r = \pm\sqrt{r^2}$ from a printout, use the sign of the slope.

---

## 16. t² = F for the slope

Result: the $t$ statistic for $H_0: \beta_1 = 0$ and the regression $F$ satisfy $t^2 = F$. #theorem

(added in session; see [[STA01B1_Notes_S9_Simple_Linear_Regression]], heading "Why t² = F". The equivalence is stated in source, Lecture 10 slide 20. Past papers ask you to "identify the two test statistics in the printout", for example 2016 Q7.1 and 2018 Q4.3.)

$$t^2 = \left(\frac{b_1}{\sqrt{MSE/S_{xx}}}\right)^2 = \frac{b_1^2S_{xx}}{MSE} = \frac{SSR}{MSE} = \frac{SSR/1}{MSE} = \frac{MSR}{MSE} = F$$

using $SSR = b_1^2S_{xx}$ from section 15 and regression df $= 1$.

Check on a printout (STA1B10 2016 Semester Test 2 Q7): $t = -5.6224$ and $(-5.6224)^2 = 31.61 = F$. Both report the same p-value, 0.0002.

---

## 17. Results stated without proof at this level

These are used in the test, but no derivation was shown in any lecture, memo or session. Quote them, don't derive them.

- The pooled two-sample $t$: under normality and equal variances, $\dfrac{\bar{X}-\bar{Y}-(\mu_1-\mu_2)}{\sqrt{S_p^2(1/m+1/n)}} \sim t_{m+n-2}$. (Stated in S6, from user-transcribed section 9.2.)
- The paired $t$: $\dfrac{\bar{D}-\mu_D}{S_D/\sqrt{n}} \sim t_{n-1}$ when the differences are normal. (Stated in S7.)
- The large-sample normal approximations for $\bar{X}-\bar{Y}$ with $S$ substituted, and for $\hat{p}_1-\hat{p}_2$. (Stated in S6 and S7. They rest on the CLT, which is stated without proof in S1.)
- In ANOVA, under $H_0$ and the two assumptions, $F = MSTr/MSE \sim F_{I-1,\,I(J-1)}$. (Stated in S8. The behaviour of $MSTr$ under $H_a$ is described there, not proved.)
- Tukey's studentized range critical value $Q_{\alpha,I,I(J-1)}$ and its simultaneous coverage. (Stated in S8, Lecture 9 slides 25 and 33.)
- In regression, $t = b_1/\sqrt{MSE/S_{xx}} \sim t_{n-2}$ under $H_0: \beta_1 = 0$, and the CI and PI formulas at $x_0$. (Stated in S9, Lecture 10 slides 19, 27 to 30.) The explanation of why the PI carries the extra $1$ is in S9 under "Why the prediction interval is wider, and why both flare".

## Do not forget

- Means subtract, variances add: $V(\bar{X}-\bar{Y}) = \sigma_1^2/m + \sigma_2^2/n$, and the same holds for $\hat{p}_1-\hat{p}_2$ with $pq$.
- Unbiasedness proofs for $S_p^2$ and $MSE$ are the same three moves: take $E$ inside, use $E(S_i^2) = \sigma^2$ (homoscedasticity), factor out $\sigma^2$. Name the equal-variance assumption where you use it.
- $SST = SSTr + SSE$: add 0, expand, name the ends (the $SSE$ piece has no $J$, the $SSTr$ piece carries the $J$), distribute the middle, substitute $\sum_j x_{ij} = J\bar{x}_{i\cdot}$, cancel. Watch every dot.
- The least squares conditions $\sum e_i = 0$ and $\sum x_ie_i = 0$ drive $b_0$, $b_1$, the regression split and the $n-2$ df.
- $t^2 = F$ through $SSR = b_1^2S_{xx}$.
- The test and the CI agree only at matching $\alpha$ and matching sidedness.

## See also
- [[STA01B1_Summary_ST2]]
- [[STA01B1_Proofs_ST1]]
- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]]
- [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances]]
- [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]]
- [[STA01B1_Notes_S9_Simple_Linear_Regression]]
