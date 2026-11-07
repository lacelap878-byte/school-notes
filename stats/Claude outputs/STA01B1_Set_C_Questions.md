# STA01B1 Set C: Monday prep (81 marks)

Section A is Question 1 style (theory and proofs). Section B is calculations. Do them as two sittings if you want. Suggested time: about 45 minutes each. Write every line as you would for Dr H, then send photos.

---

## SECTION A: Theory and proofs (41 marks)

**A1. (3)** State the Central Limit Theorem for $\bar X$ (shape, mean, variance and the condition on $n$ in this course). In one sentence, say why confidence intervals and tests for $\mu$ depend on it.

**A2. (4)** $X_1, X_2$ is a random sample from a population with mean $\mu$ and variance $\sigma^2$. Consider
$$\hat\theta_1=\frac{X_1+3X_2}{4}$$
(a) Show that $\hat\theta_1$ is an unbiased estimator of $\mu$. (2)
(b) Find $V(\hat\theta_1)$. (1)
(c) Compare $\hat\theta_1$ with $\bar X$ from the same two observations. Which is better, and why? (1)

**A3. (4)** Show that $S^2=\dfrac{1}{n-1}\sum_{i=1}^n (X_i-\bar X)^2$ is an unbiased estimator of $\sigma^2$. Show all steps.

**A4. (3)** Using A3, show that $\bar X^2-\dfrac{S^2}{n}$ is an unbiased estimator of $\mu^2$.

**A5. (2)** $X\sim \text{Bin}(n,p)$ and $\hat p=X/n$. Is $\hat p^2$ an unbiased estimator of $p^2$? If not, find its bias.

**A6. (4)** $X\sim\text{Bin}(m,p_1)$ and $Y\sim\text{Bin}(n,p_2)$ are independent, $\hat p_1=X/m$, $\hat p_2=Y/n$.
(a) Use the rules of expected value to show that $\hat p_1-\hat p_2$ is unbiased for $p_1-p_2$. Show all steps. (2)
(b) Determine $V(\hat p_1-\hat p_2)$. Say where independence is used. (2)

**A7. (3)** Two independent samples of sizes $m$ and $n$ come from populations with equal variance $\sigma^2$. Show that
$$S_p^2=\frac{(m-1)S_1^2+(n-1)S_2^2}{m+n-2}$$
is an unbiased estimator of $\sigma^2$. State the line where the equal-variance assumption is used.

**A8. (3)** Prove that $MSE(\hat\theta)=V(\hat\theta)+[\text{bias}(\hat\theta)]^2$.

**A9. (4)** Independent random samples of sizes $m$ and $n$ come from normal populations with known variances $\sigma_1^2$ and $\sigma_2^2$. Starting from the sampling distribution of $\bar X-\bar Y$, derive a $100(1-\alpha)\%$ confidence interval for $\mu_1-\mu_2$.

**A10. (4)** In single-factor ANOVA with $I$ treatments and $J$ observations per treatment, prove that $SST=SSTr+SSE$. Every dot and bar counts.

**A11. (2)** Show how the $t_\nu$ and the $F_{\nu_1,\nu_2}$ distributions are built from standard normal and chi-square variables. State the independence each one needs.

**A12. (5)** True or false? Give a reason for each.
(a) In a regression printout, the coefficient $b_1=4.82$ is the population slope $\beta_1$.
(b) If $H_0$ is not rejected at the 5% level, the data have shown that $H_0$ is true.
(c) In the $z$ test of $H_0: p_1=p_2$, the standard error uses the pooled $\hat p$ because $H_0$ says the two proportions are equal.
(d) A plot of the residuals against the fitted values is used to check whether the errors are normally distributed.
(e) A printed $p$-value of 0.000 means the probability that $H_0$ is true is zero.

---

## SECTION B: Calculations (40 marks)

**B1. (5)** Bolt lengths are normally distributed with mean 80 mm and standard deviation 0.6 mm. A random sample of 36 bolts is taken.
(a) Give $E(\bar X)$, $V(\bar X)$ and $\sigma_{\bar X}$, with units. (2)
(b) Calculate $P(79.8\le\bar X\le 80.2)$. (1)
(c) Suppose the shape of the population were unknown. Could (b) still be calculated with $n=36$? Explain. (1)
(d) The 36 bolts are laid end to end. Give the mean and standard deviation of the total length $T_0$. (1)

**B2. (4)** Two suppliers' cable strengths are compared. Supplier A: $m=10$, $\bar x=20.4$, $s_1^2=4$. Supplier B: $n=14$, $\bar y=18.1$, $s_2^2=6$. Assume normal populations with equal variances.
Calculate a 95% confidence interval for $\mu_1-\mu_2$ and explain it in plain words.

**B3. (6)** A regression of monthly electricity cost $y$ (rand) on floor area $x$ (m²) for 15 houses, with floor areas from 60 to 220 m², gives:

```
Predictor    Coef     SE Coef   T      P
Constant     310.5    85.2      3.64   0.003
Area         4.82     0.61      7.90   0.000

R-Sq = 82.8%
```

(a) State the hypotheses for testing whether there is a linear relationship. Give the decision at the 5% level and a plain conclusion. (2)
(b) Interpret the slope. (1)
(c) Interpret $R^2$. (1)
(d) Predict the monthly cost for a 150 m² house. (1)
(e) Can the model be used to predict the cost for a 300 m² house? Explain. (1)

**B4. (4)**
(a) $\sigma=8$. How large must $n$ be so that a 95% confidence interval for $\mu$ has a width of at most 3? (2)
(b) How large must $n$ be to estimate a proportion to within 0.04 with 90% confidence, if no estimate of $p$ is available? (2)

**B5. (8)** Fill weights are normal with $\sigma=6$ g. Test $H_0:\mu=50$ against $H_a:\mu<50$ with $n=16$ at $\alpha=0.05$.
(a) Give the rejection region in terms of $\bar x$. (2)
(b) Calculate $\beta(47)$. (3)
(c) What sample size gives $\beta(47)=0.10$ while keeping $\alpha=0.05$? (2)
(d) Explain in plain words what $\beta(47)$ means for the factory. (1)

**B6. (3)** Test $H_0:p=0.4$ against $H_a:p>0.4$ with $n=150$ at $\alpha=0.05$. Calculate the probability of a Type II error when the true proportion is $p=0.5$.

**B7. (6)** Four teaching methods ($I=4$) are each used on $J=6$ students. The sample means are $20.1,\ 24.3,\ 26.0,\ 31.2$ and $MSE=12.6$.
(a) Give the degrees of freedom for treatments, error and total. (1)
(b) Calculate $SSTr$ and $F$, and decide at the 5% level. (2)
(c) Calculate Tukey's $w$ at the 5% level. (2)
(d) Underline the means that are not significantly different, and say which pairs differ. (1)

**B8. (4)** A supplier claims three grades of product sell in the ratio 3 : 2 : 1. In a sample of 120 sales the counts are 66, 34 and 20. Test the claim at the 5% level. Give the hypotheses, test statistic, critical value, decision and plain conclusion.
