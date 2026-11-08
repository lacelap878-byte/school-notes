# STA01B1 Final: Proofs (S1 to S10)

Notation: $V(\cdot)$ for variance, $E(\cdot)$ for expectation, $\sigma^2=V(X)$, $q=1-p$. Every symbol written out, every dot and bar kept. Each proof ends with the line you can copy as the conclusion.

Facts used throughout:
- (F1) $V(X)=E(X^2)-[E(X)]^2$, so $E(X^2)=V(X)+[E(X)]^2$.
- (F2) $E(aX+bY)=aE(X)+bE(Y)$. For independent $X,Y$: $V(aX+bY)=a^2V(X)+b^2V(Y)$.
- (F3) For $X_1,\dots,X_n$ iid with mean $\mu$ and variance $\sigma^2$: $E(\bar X)=\mu$ and $V(\bar X)=\frac{\sigma^2}{n}$.

---

## P1. Mean squared error equals variance plus bias squared
$MSE(\hat\theta)=E[(\hat\theta-\theta)^2]$.
1. Add and subtract $E(\hat\theta)$: $\hat\theta-\theta=[\hat\theta-E(\hat\theta)]+[E(\hat\theta)-\theta]$.
2. Square: $(\hat\theta-\theta)^2=[\hat\theta-E(\hat\theta)]^2+2[\hat\theta-E(\hat\theta)][E(\hat\theta)-\theta]+[E(\hat\theta)-\theta]^2$.
3. Take $E$. The bracket $[E(\hat\theta)-\theta]$ is a constant, so the middle term is $2[E(\hat\theta)-\theta]\cdot E[\hat\theta-E(\hat\theta)]=2[E(\hat\theta)-\theta]\cdot0=0$.
4. $E\big[\hat\theta-E(\hat\theta)\big]^2=V(\hat\theta)$, and $[E(\hat\theta)-\theta]^2=\text{bias}^2$.

**Therefore $MSE(\hat\theta)=V(\hat\theta)+[\text{bias}(\hat\theta)]^2$.**

## P2. The expected value of S squared is sigma squared
$S^2=\frac{\sum(X_i-\bar X)^2}{n-1}$.
1. $\sum(X_i-\bar X)^2=\sum X_i^2-2\bar X\sum X_i+n\bar X^2=\sum X_i^2-2n\bar X^2+n\bar X^2=\sum X_i^2-n\bar X^2$.
2. $E(X_i^2)=\sigma^2+\mu^2$ (F1). $E(\bar X^2)=V(\bar X)+\mu^2=\frac{\sigma^2}{n}+\mu^2$.
3. $E\!\left[\sum X_i^2-n\bar X^2\right]=n(\sigma^2+\mu^2)-n\!\left(\frac{\sigma^2}{n}+\mu^2\right)=n\sigma^2+n\mu^2-\sigma^2-n\mu^2=(n-1)\sigma^2$.
4. Divide by $n-1$.

**Therefore $E(S^2)=\sigma^2$, so $S^2$ is unbiased for $\sigma^2$.**

## P3. Divisor n: the bias of the variance estimator
Here $\hat\sigma^2=\frac{\sum(X_i-\bar X)^2}{n}$.
1. From P2 step 3: $E\!\left[\sum(X_i-\bar X)^2\right]=(n-1)\sigma^2$.
2. $E(\hat\sigma^2)=\frac{(n-1)\sigma^2}{n}=\sigma^2-\frac{\sigma^2}{n}$.
3. $\text{bias}=E(\hat\sigma^2)-\sigma^2=\mathbf{-\frac{\sigma^2}{n}}$. It underestimates $\sigma^2$, and the bias shrinks as $n$ grows (asymptotically unbiased).

## P4. X bar squared minus S squared over n is unbiased for mu squared
1. $E(\bar X^2)=V(\bar X)+[E(\bar X)]^2=\frac{\sigma^2}{n}+\mu^2$.
2. $E\!\left(\frac{S^2}{n}\right)=\frac{E(S^2)}{n}=\frac{\sigma^2}{n}$ (P2).
3. $E\!\left(\bar X^2-\frac{S^2}{n}\right)=\frac{\sigma^2}{n}+\mu^2-\frac{\sigma^2}{n}=\mu^2$.

**Therefore $\bar X^2-\frac{S^2}{n}$ is unbiased for $\mu^2$.** ($\bar X^2$ alone has bias $\frac{\sigma^2}{n}$.)

## P5. Bias of p hat squared
Here $\hat p=\frac{X}{n}$ and $X\sim\text{Bin}(n,p)$.
1. $E(\hat p)=p$ and $V(\hat p)=\frac{pq}{n}$.
2. $E(\hat p^2)=V(\hat p)+[E(\hat p)]^2=\frac{pq}{n}+p^2$.
3. $\text{bias}=E(\hat p^2)-p^2=\mathbf{\frac{pq}{n}}$. $\hat p^2$ overestimates $p^2$.

## P6. Mean and variance of p hat one minus p hat two
Independent samples of size $m$ and $n$.
1. $E(\hat p_1)=p_1$ and $E(\hat p_2)=p_2$, so $E(\hat p_1-\hat p_2)=\mathbf{p_1-p_2}$ (unbiased).
2. $V(\hat p_1)=\frac{p_1q_1}{m}$ and $V(\hat p_2)=\frac{p_2q_2}{n}$.
3. The samples are independent, so $V(\hat p_1-\hat p_2)=V(\hat p_1)+(-1)^2V(\hat p_2)=\mathbf{\frac{p_1q_1}{m}+\frac{p_2q_2}{n}}$.

## P7. A linear combination of two observations
Here $\hat\theta_1=\frac{X_1+3X_2}{4}$, with $X_1,X_2$ independent, each with mean $\mu$ and variance $\sigma^2$.
1. $E(\hat\theta_1)=\frac{\mu+3\mu}{4}=\mu$: unbiased.
2. $V(\hat\theta_1)=\frac{1}{16}(\sigma^2+9\sigma^2)=\frac{10\sigma^2}{16}=\frac{5\sigma^2}{8}$.
3. Compare with $\bar X=\frac{X_1+X_2}{2}$: $V(\bar X)=\frac{\sigma^2}{2}=\frac{4\sigma^2}{8}<\frac{5\sigma^2}{8}$. Both are unbiased, so **choose the smaller variance ($\bar X$)**.

Rule: weights summing to $1$ keep it unbiased; the variance is $\sum(\text{weight}^2)\,\sigma^2$.

## P8. The pooled variance is unbiased for sigma squared
$S_p^2=\frac{(m-1)S_1^2+(n-1)S_2^2}{m+n-2}$, with both samples from populations with common variance $\sigma^2$.
1. $E(S_1^2)=E(S_2^2)=\sigma^2$ (P2).
2. $E(S_p^2)=\frac{(m-1)\sigma^2+(n-1)\sigma^2}{m+n-2}=\frac{(m+n-2)\sigma^2}{m+n-2}=\mathbf{\sigma^2}$.

## P9. Confidence interval for mu one minus mu two, variances known
Independent normal samples with known $\sigma_1^2$ and $\sigma_2^2$.
1. $\bar X_1\sim N\!\left(\mu_1,\frac{\sigma_1^2}{m}\right)$ and $\bar X_2\sim N\!\left(\mu_2,\frac{\sigma_2^2}{n}\right)$, independent.
2. $\bar X_1-\bar X_2\sim N\!\left(\mu_1-\mu_2,\ \frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}\right)$.
3. $$Z=\frac{(\bar X_1-\bar X_2)-(\mu_1-\mu_2)}{\sqrt{\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}}}\sim N(0,1)$$
4. $P(-z_{\alpha/2}\le Z\le z_{\alpha/2})=1-\alpha$.
5. Multiply through by the standard error, subtract $(\bar X_1-\bar X_2)$, then multiply by $-1$ (reversing the inequalities).

**$(\bar X_1-\bar X_2)\pm z_{\alpha/2}\sqrt{\frac{\sigma_1^2}{m}+\frac{\sigma_2^2}{n}}$ is a $100(1-\alpha)\%$ CI for $\mu_1-\mu_2$.**

(One-sample version: the same steps with $Z=\frac{\bar X-\mu}{\sigma/\sqrt n}$, giving $\bar X\pm z_{\alpha/2}\frac{\sigma}{\sqrt n}$. With $\sigma$ unknown, replace $\sigma$ by $S$ and $z$ by $t_{\alpha/2,n-1}$.)

## P10. SST equals SSTr plus SSE
$I$ groups, $J$ values each; $\bar x_{i\cdot}$ is the group mean and $\bar x_{\cdot\cdot}$ is the grand mean.

$$SST=\sum_i\sum_j(x_{ij}-\bar x_{\cdot\cdot})^2,\qquad SSTr=J\sum_i(\bar x_{i\cdot}-\bar x_{\cdot\cdot})^2,\qquad SSE=\sum_i\sum_j(x_{ij}-\bar x_{i\cdot})^2$$

1. Add and subtract $\bar x_{i\cdot}$: $x_{ij}-\bar x_{\cdot\cdot}=(x_{ij}-\bar x_{i\cdot})+(\bar x_{i\cdot}-\bar x_{\cdot\cdot})$.
2. Square and sum:
$$SST=\sum_i\sum_j(x_{ij}-\bar x_{i\cdot})^2+2\sum_i\sum_j(x_{ij}-\bar x_{i\cdot})(\bar x_{i\cdot}-\bar x_{\cdot\cdot})+\sum_i\sum_j(\bar x_{i\cdot}-\bar x_{\cdot\cdot})^2$$
3. The first term is $SSE$ (no $J$).
4. Last term: $(\bar x_{i\cdot}-\bar x_{\cdot\cdot})^2$ does not depend on $j$, so $\sum_i\sum_j=J\sum_i(\bar x_{i\cdot}-\bar x_{\cdot\cdot})^2=SSTr$ (it carries the $J$).
5. Middle term: for fixed $i$, $(\bar x_{i\cdot}-\bar x_{\cdot\cdot})$ is constant in $j$, so the term equals $2\sum_i(\bar x_{i\cdot}-\bar x_{\cdot\cdot})\sum_j(x_{ij}-\bar x_{i\cdot})$. Using $\sum_j x_{ij}=J\bar x_{i\cdot}$, we get $\sum_j(x_{ij}-\bar x_{i\cdot})=J\bar x_{i\cdot}-J\bar x_{i\cdot}=0$, so the middle term is $0$.

**Therefore $SST=SSTr+SSE$.**

Computing forms (totals, no bars):
$$SST=\sum\sum x_{ij}^2-\frac{x_{\cdot\cdot}^2}{IJ},\qquad SSTr=\frac{\sum x_{i\cdot}^2}{J}-\frac{x_{\cdot\cdot}^2}{IJ}$$

## P11. Expected count in a two-way table
1. Under $H_0$ (independence): $P(\text{row }i\text{ and column }j)=P(\text{row }i)\,P(\text{column }j)=p_{i\cdot}\,p_{\cdot j}$.
2. Expected count $=n\times p_{i\cdot}\,p_{\cdot j}$.
3. Estimate $p_{i\cdot}$ by $\frac{n_{i\cdot}}{n}$ and $p_{\cdot j}$ by $\frac{n_{\cdot j}}{n}$.
4. $E_{ij}=n\cdot\frac{n_{i\cdot}}{n}\cdot\frac{n_{\cdot j}}{n}=\mathbf{\frac{n_{i\cdot}\,n_{\cdot j}}{n}}$ (row total times column total, divided by the grand total).

## P12. The short form of the chi-square statistic
1. $\frac{(O-E)^2}{E}=\frac{O^2}{E}-2O+E$.
2. Sum over all cells: $\sum\frac{(O-E)^2}{E}=\sum\frac{O^2}{E}-2\sum O+\sum E$.
3. $\sum O=\sum E=n$, so $-2n+n=-n$.

**Therefore $\sum\frac{(O-E)^2}{E}=\sum\frac{O^2}{E}-n$.**

## P13. Sample size n from alpha and beta
Lower-tailed: $H_0:\mu=\mu_0$, true mean $\mu'<\mu_0$, $\sigma$ known. Rejection region: $\bar X\le c$.
1. $\alpha$: $P(\bar X\le c\mid\mu_0)=\alpha$, so $\frac{c-\mu_0}{\sigma/\sqrt n}=-z_\alpha$, that is $\mathbf{c=\mu_0-z_\alpha\frac{\sigma}{\sqrt n}}$.
2. $\beta$: $P(\bar X>c\mid\mu')=\beta$, so $\frac{c-\mu'}{\sigma/\sqrt n}=z_\beta$, that is $\mathbf{c=\mu'+z_\beta\frac{\sigma}{\sqrt n}}$.
3. Equate: $\mu_0-z_\alpha\frac{\sigma}{\sqrt n}=\mu'+z_\beta\frac{\sigma}{\sqrt n}$.
4. $\mu_0-\mu'=(z_\alpha+z_\beta)\frac{\sigma}{\sqrt n}$, so $\sqrt n=\frac{\sigma(z_\alpha+z_\beta)}{\mu_0-\mu'}$.

$$\mathbf{n=\left[\frac{\sigma(z_\alpha+z_\beta)}{\mu_0-\mu'}\right]^2,\ \text{rounded UP.}}$$

- Upper-tailed ($\mu'>\mu_0$): $c=\mu_0+z_\alpha\frac{\sigma}{\sqrt n}$ and $c=\mu'-z_\beta\frac{\sigma}{\sqrt n}$, giving $n=\left[\frac{\sigma(z_\alpha+z_\beta)}{\mu'-\mu_0}\right]^2$.
- Two-sided: replace $z_\alpha$ by $z_{\alpha/2}$ (use the boundary nearer $\mu'$).
- Proportion: $c=p_0-z_\alpha\sqrt{\frac{p_0q_0}{n}}=p'+z_\beta\sqrt{\frac{p'q'}{n}}$, so $n=\left[\frac{z_\alpha\sqrt{p_0q_0}+z_\beta\sqrt{p'q'}}{p'-p_0}\right]^2$.

## P14. Sample size for a confidence interval of half-width E
1. Error bound: $E=z_{\alpha/2}\frac{\sigma}{\sqrt n}$.
2. Solve: $\sqrt n=\frac{z_{\alpha/2}\sigma}{E}$, so $\mathbf{n=\left(\frac{z_{\alpha/2}\sigma}{E}\right)^2}$, rounded up.
3. Proportion: $E=z_{\alpha/2}\sqrt{\frac{\hat p\hat q}{n}}$, so $\mathbf{n=\frac{z_{\alpha/2}^2\,\hat p\hat q}{E^2}}$ ($\hat p=0.5$ when unknown, since $\hat p\hat q\le0.25$).

## P15. Building chi-square, t and F (Practical 2)
- **$\chi^2_\nu$:** if $Z_1,\dots,Z_\nu$ are independent $N(0,1)$, then $\sum Z_i^2\sim\chi^2_\nu$. Example: $\frac{(n-1)S^2}{\sigma^2}\sim\chi^2_{n-1}$.
- **$t_\nu$:** if $Z\sim N(0,1)$ and $X\sim\chi^2_\nu$ are independent, then $T=\frac{Z}{\sqrt{X/\nu}}\sim t_\nu$. Example: $Z=\frac{\bar X-\mu}{\sigma/\sqrt n}$ and $X=\frac{(n-1)S^2}{\sigma^2}$ with $\nu=n-1$, so $T=\frac{\bar X-\mu}{S/\sqrt n}$.
- **$F_{\nu_1,\nu_2}$:** if $X_1\sim\chi^2_{\nu_1}$ and $X_2\sim\chi^2_{\nu_2}$ are independent, then $F=\frac{X_1/\nu_1}{X_2/\nu_2}\sim F_{\nu_1,\nu_2}$. Example: ANOVA, $F=\frac{MSTr}{MSE}$.
- Independence of the pieces is a stated condition each time.

## Quick checks for a blank-page sit
- P1, P2 and P10 are the three most likely: write them from memory first.
- Mark-losers: missing dots ($x_{ij}$, $\bar x_{i\cdot}$, $\bar x_{\cdot\cdot}$), missing bars on means, the $J$ in $SSTr$, and a missing "$=0$" justification for the cross term.
