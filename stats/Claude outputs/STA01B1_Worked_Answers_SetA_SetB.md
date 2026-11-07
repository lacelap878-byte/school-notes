# STA01B1 worked answers: Set A and Set B (Q1 style practice)

Written Sat 7 Nov 2026 for Mdumiseni Sithomo. Compare your own pages against this, then redo the items marked REDO without looking. Each answer carries its reason, so you can rebuild it from understanding, not from memory of wording.

How checked: every number was recomputed (exact fractions, and an exact binomial sum for the bias in Set A Q4). Nothing here comes from outside the notes and the lecturer hints.

---

# SET A (40 marks, marked about 24/40 on Fri 6 Nov)

## A1. The CLT (5)
(a) For large $n$ (in this course $n>40$), the sampling distribution of $\bar X$ is approximately normal:
$$\bar X \approx N\!\left(\mu,\ \frac{\sigma^2}{n}\right)$$
Three marks: the **shape** (approximately normal), the mean $\mu$, the variance $\sigma^2/n$. You left out the shape three times. The word "approximately normal" is the shape.
(b) Intervals and tests need to know how far $\bar x$ can sit from $\mu$ by chance. That is the sampling distribution of $\bar X$. The CLT gives it as approximately normal for large $n$ whatever the shape of the population, so we can use $z$-based intervals and tests without knowing the population's shape. Two marks: need the sampling distribution, and the CLT supplies it whatever the population.

## A2. How the distributions are built (4)
- $\chi^2_\nu = Z_1^2+\cdots+Z_\nu^2$, a sum of $\nu$ squared independent standard normals.
- $t_\nu = \dfrac{Z}{\sqrt{\chi^2_\nu/\nu}}$, with $Z$ and $\chi^2_\nu$ independent.
- $F_{\nu_1,\nu_2} = \dfrac{\chi^2_{\nu_1}/\nu_1}{\chi^2_{\nu_2}/\nu_2}$, the two $\chi^2$ independent.
Why: $t$ is a normal divided by an estimate of its own spread (that is why it has heavier tails). $F$ is a ratio of two variance-like quantities (that is why ANOVA uses it).

## A3. Unbiased estimators (7)
(a) Unbiased means $E(\hat\theta)=\theta$: correct on average over repeated samples. For $\bar X$:
$$E(\bar X)=\frac1n\sum_{i=1}^n E(X_i)=\frac1n(n\mu)=\mu$$
(b) $\hat\theta=\dfrac{X_1+2X_2+3X_3}{6}$.
$$E(\hat\theta)=\frac{E(X_1)+2E(X_2)+3E(X_3)}{6}=\frac{\mu+2\mu+3\mu}{6}=\frac{6\mu}{6}=\mu$$
The weights $\frac16,\frac26,\frac36$ add to **1**. That is why it is unbiased (a weighted average of things each centred on $\mu$). You called the sum 6: it is $6/6=1$.
$$V(\hat\theta)=\frac{1+4+9}{36}\sigma^2=\frac{7\sigma^2}{18}>\frac{6\sigma^2}{18}=V(\bar X)$$
Both unbiased, so the smaller variance wins: $\bar X$ is better.
(c) $E(\bar X^2)=V(\bar X)+[E(\bar X)]^2=\dfrac{\sigma^2}{n}+\mu^2$, so the bias of $\bar X^2$ for $\mu^2$ is $\dfrac{\sigma^2}{n}$.

## A4. Bias of $\hat p(1-\hat p)$ (3)
Key fact: $E(Y^2)=V(Y)+[E(Y)]^2$. **Plus**, not minus (your slip). It follows from $V(Y)=E(Y^2)-[E(Y)]^2$.
$$E(\hat p^2)=V(\hat p)+[E(\hat p)]^2=\frac{pq}{n}+p^2$$
$$E\big(\hat p(1-\hat p)\big)=E(\hat p)-E(\hat p^2)=p-\frac{pq}{n}-p^2=pq-\frac{pq}{n}=\frac{pq(n-1)}{n}$$
$$\text{bias}=\frac{pq(n-1)}{n}-pq=-\frac{pq}{n}$$
Every line follows from the line above. The bias line is the last step (expected value minus the parameter), not a copy of the line before. (Check: for $n=10$, $p=0.3$ the exact value is $0.189$ against $pq=0.21$, a bias of $-0.021=-pq/n$.)

## A5. Deriving a confidence interval (6)
(a) $\bar X\sim N(\mu,\sigma^2/n)$, so
$$Z=\frac{\bar X-\mu}{\sigma/\sqrt n}\sim N(0,1)$$
$$P(-1.96<Z<1.96)=0.95$$
$$P\!\left(-1.96\frac{\sigma}{\sqrt n}<\bar X-\mu<1.96\frac{\sigma}{\sqrt n}\right)=0.95$$
Multiply by $-1$ (the inequalities flip), then add $\bar X$:
$$P\!\left(\bar X-1.96\frac{\sigma}{\sqrt n}<\mu<\bar X+1.96\frac{\sigma}{\sqrt n}\right)=0.95$$
Interval: $\bar x\pm1.96\,\sigma/\sqrt n$. Estimates replace unknowns at the end only.
(b) Replace $\sigma$ by $s$ and use $t$ with $n-1$ degrees of freedom. Why: estimating $\sigma$ adds uncertainty, so the standardised statistic has heavier tails than a normal.

## A6. Explain and describe (6)
(a) The sampling distribution of $\bar X$ is the distribution of the sample mean over all possible samples of size $n$: centred at $\mu$, standard error $\sigma/\sqrt n$. It describes the sample mean, not individual observations.
(b) Assume $H_0$ is true. Ask how unlikely data as extreme as ours would be under $H_0$ (test statistic, then $p$-value or rejection region). If very unlikely, reject $H_0$; if not, fail to reject. A test never proves: it gives evidence.
(c) ANOVA compares the variation between group means ($MSTr$) with the variation within groups ($MSE$). A large ratio $F$ means the means differ by more than chance within groups would produce.

## A7. Proof of $SST=SSTr+SSE$ (4)
Full line-by-line version: the section "Proof that SST = SSTr + SSE" in your S8 notes. Skeleton, with the reason for each move:
1. Start from the definition, $SST=\sum\sum(x_{ij}-\bar x_{\cdot\cdot})^2$ (grand **mean**, two dots, with a bar).
2. Add $0$ as $-\bar x_{i\cdot}+\bar x_{i\cdot}$ (to bring in the group mean both pieces need).
3. Expand $(a+b)^2=a^2+2ab+b^2$ with $a=x_{ij}-\bar x_{i\cdot}$, $b=\bar x_{i\cdot}-\bar x_{\cdot\cdot}$.
4. First piece has $x_{ij}$, so it is $SSE$. Last piece has only means (no $j$), so the inner sum gives $J$, and it is $SSTr=J\sum_i(\bar x_{i\cdot}-\bar x_{\cdot\cdot})^2$.
5. Middle term: distribute, then use $\sum_j x_{ij}=J\bar x_{i\cdot}$ on the term that still has $x_{ij}$.
6. The two middle terms are identical and subtracted, so they cancel (keep the 2 until then).
Marks are lost for a missing dot or symbol. REDO from memory tonight.

## A8. True or false (5)
(a) **False.** The interval is about $\mu$, not about where the data lie.
(b) **True.** $SE=\sigma/\sqrt n$; $\sqrt4=2$, so the standard error halves.
(c) **False.** Unbiased means correct on average over repeated samples, not in every sample.
(d) **False.** $SSE$ is the variation within groups. Between groups is $SSTr$.
(e) **False.** Failing to reject means the evidence was not strong enough, not that $H_0$ is true.

---

# SET B (40 marks, 21/40 on Sat 7 Nov)

## B1. $\hat p_1-\hat p_2$ (4)
$$E(\hat p_1-\hat p_2)=E(\hat p_1)-E(\hat p_2)=p_1-p_2$$
(each $\hat p$ is unbiased for its own $p$; expectation of a difference is the difference of expectations.)
$$V(\hat p_1-\hat p_2)=V(\hat p_1)+V(\hat p_2)=\frac{p_1q_1}{m}+\frac{p_2q_2}{n}$$
**Independence is used here:** for independent samples the covariance is $0$, so $V(A-B)=V(A)+V(B)$. Variances add even when the statistics are subtracted. Check your page: $q=1-p$ (not $p-1$), subscripts on $p$ and $q$, and sample 1 has size $m$, so $m$ goes under $p_1q_1$. REDO.

## B2. Type I and Type II (5)
$H_0$: at least 20% are satisfied.
(a) Type I: reject $H_0$ when it is true: conclude fewer than 20% are satisfied when at least 20% really are.
(b) Type II: fail to reject $H_0$ when it is false: do not conclude fewer than 20% are satisfied when fewer than 20% really are.
(c) $\beta$ **increases**. A smaller $\alpha$ shrinks the rejection region, so a false $H_0$ is harder to reject. (The reason was the mark you missed.)

## B3. $\hat\theta=\dfrac{2X_1+X_2+X_3}{4}$ (5)
(a)
$$E(\hat\theta)=\frac{2E(X_1)+E(X_2)+E(X_3)}{4}=\frac{2\mu+\mu+\mu}{4}=\frac{4\mu}{4}=\mu$$
The key move: **replace each $E(X_i)$ by $\mu$.** An expected value is a fixed number. You wrote $X_1/2+X_2/4+X_3/4$, which keeps the random variables and never reaches $\mu$. Weights $\frac24+\frac14+\frac14=1$, so it is unbiased.
(b) Constants come out squared, independent variances add:
$$V(\hat\theta)=\frac{4V(X_1)+V(X_2)+V(X_3)}{16}=\frac{6\sigma^2}{16}=\frac{3\sigma^2}{8}$$
(c) $V(\bar X)=\dfrac{\sigma^2}{3}=0.333\sigma^2<0.375\sigma^2=V(\hat\theta)$. Both are unbiased, so $\bar X$ is better: smaller variance. REDO (a) and (b).

## B4. $\hat\theta=\bar X+c$ (4)
(a) Bias is $E(\hat\theta)-\mu$, so $(\mu+c)-\mu=c$. You computed $E(\hat\theta)$ but did not subtract $\mu$.
(b) Adding a constant does not change the spread, so $V(\bar X+c)=V(\bar X)=\dfrac{\sigma^2}{n}$. (Your long route was correct; finish on $\sigma^2/n$, not "$V(\bar X)$".)
(c)
$$MSE=V+\text{bias}^2=\frac{\sigma^2}{n}+c^2$$
Variance is $\sigma^2/n$; $\sigma/\sqrt n$ is the standard error. REDO.

## B5. $\mu_1-\mu_2$ (6)
(a) Independent samples from normal populations, known variances:
$$\bar X-\bar Y\sim N\!\left(\mu_1-\mu_2,\ \frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}\right)$$
(mean of a difference is the difference of means; variances add.) There is no $D$ here: $\mu_D$ and $\sigma_D$ belong to **paired** data (one sample of differences). Two independent samples, two sizes $m$ and $n$, two variances.
$$Z=\frac{(\bar X-\bar Y)-(\mu_1-\mu_2)}{\sqrt{\sigma_1^2/m+\sigma_2^2/n}}\sim N(0,1),\qquad P(-1.96<Z<1.96)=0.95$$
Rearranging for $\mu_1-\mu_2$ (flip, then add):
$$(\bar x-\bar y)\pm1.96\sqrt{\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}}$$
Both bounds start from $\bar x-\bar y$ (a plus sign between them on the left bound was your slip).
(b) When the variances are unknown, the populations are normal and the variances are assumed equal: pool them into $S_p^2$ and use $t$ with $m+n-2$ degrees of freedom. REDO.

## B6. ANOVA and Tukey (5)
(a) Each separate $t$ test carries its own chance $\alpha$ of a false rejection. Run three and the overall chance of at least one false rejection is more than $\alpha$. Tukey controls the overall error rate at $\alpha$ for all comparisons together.
(b) 
$$W=Q_{\alpha,\,I,\,I(J-1)}\sqrt{\frac{MSE}{J}}$$
$Q$ from the studentised range table, $\alpha$ the overall level, $I$ the number of treatments, $I(J-1)$ the error degrees of freedom, $MSE$ from the ANOVA table, $J$ the observations per treatment.
(c) If two sample means differ by more than $W$, the two **population** means are judged significantly different.

## B7. Regression, $n=20$ (6)
**Scope note (7 Nov, from the user): regression is interpretation only. In the exam the printout gives $t$, the degrees of freedom and the $p$-value, so you read them and do not calculate them. The calculation below only shows where the printed number comes from.**
(a) $H_0:\beta_1=0$ versus $H_a:\beta_1\ne0$. Test statistic:
$$t=\frac{b_1}{SE(b_1)}=\frac{4.5}{1.2}=3.75,\qquad df=n-2=18$$
$|3.75|>2.101$, so reject $H_0$. At the 5% level there is sufficient evidence of a linear relationship between study hours and exam mark.
(b) $b_1$: each extra hour of study goes with an average increase of about 4.5 marks in exam mark. $R^2$: 81% of the variation in exam marks is explained by the linear relationship with study hours. ($R^2$ is the proportion of variation explained. "Strong positive relationship" describes $r$.) REDO.

## B8. True or false (5)
(a) **False.** $SE(\bar X)$ is the spread of the sample mean from sample to sample. Individual observations vary by $\sigma$.
(b) **True.** Higher confidence needs a larger critical value ($1.96$ against $1.645$), so a wider interval.
(c) **False.** Both unbiased, so the **smaller** variance is better.
(d) **True.** The CLT works whatever the population shape; $n=100>40$.
(e) **False.** A $p$-value of $0.03$ rejects at 5% but not at 1%.

---
*CDG v11 | written 2026-11-07*
