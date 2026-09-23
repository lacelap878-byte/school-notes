---
module: STA01B1
topic: Intervals Based on a Normal Population
session: S4
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Intervals Based on a Normal Population (Devore & Berk, Ch 7.3 & 7.4)

The large-sample CI for $\mu$ (see: [[STA01B1_Notes_S3_Statistical_Intervals]]) is valid whatever the population's shape, but only because the CLT is doing the work, and the CLT needs $n$ large. When $n$ is small, that justification disappears. The way forward is to assume a specific population shape instead, and normal is the shape most often reasonable.

## Assumption (p.295)
```
The population of interest is normal, so that X1, . . . , Xn constitutes
a random sample from a normal distribution with both mu and sigma
unknown.
```

## The $t$ distribution

### Theorem (p.295)
When $\bar{X}$ is the mean of a random sample of size $n$ from a normal distribution with mean $\mu$, the rv
$$T = \frac{\bar{X}-\mu}{S/\sqrt{n}}$$
has the $t$ distribution with $n-1$ degrees of freedom.

N.B this looks identical to the large-sample $Z$ statistic from the previous session (see: [[STA01B1_Notes_S3_Statistical_Intervals]]), the difference is that $T$'s distribution is exact for any $n$ under normality, while treating that same ratio as approximately standard normal was only valid for large $n$.

### Properties of $t$ distributions
```
1. Bell-shaped and centered at 0
2. More spread out than the standard normal curve
3. As n increases, the spread of the corresponding curve decreases
4. As n increases, the sequence of t curves approaches the standard
   normal curve
```
N.B property 2 is the whole reason a separate distribution is needed here: replacing the known $\sigma$ with the estimated $S$ adds extra uncertainty, and the $t$ distribution's wider tails are what account for that, exactly the same reasoning that pushed the large-sample rule of thumb from $n\ge 30$ to $n>40$ in the previous session.

## One-sample $t$ confidence interval

### Proposition (p.297) (exam-flagged)
Let $\bar{x}$ and $s$ be the sample mean and sample standard deviation from a random sample from a normal population with mean $\mu$. Then a $100(1-\alpha)\%$ confidence interval for $\mu$ is:
$$\left(\bar{x}-t_{\alpha/2,\,n-1}\cdot\frac{s}{\sqrt{n}}, \ \bar{x}+t_{\alpha/2,\,n-1}\cdot\frac{s}{\sqrt{n}}\right)$$
Assumption: normality of the underlying distribution.

**Example 7.11 (source, slides 7 to 9)**
Alcohol percentages for a sample of 16 beers (light beers excluded). A normal probability plot is sufficiently straight for the percentage to be assumed approximately normal. $\bar{x} = 5.34$, $s = .8483$, $n = 16$, so $df = 15$. A 95% two-sided interval requires $t_{.025,15} = 2.131$.
$$\bar{x} \pm t_{.025,15}\cdot\frac{s}{\sqrt{n}} = 5.34 \pm 2.131\cdot\frac{.8483}{\sqrt{16}} = 5.34 \pm .45 = (4.89, 5.79)$$
A 95% lower bound would use $-1.753$ in place of $\pm 2.131$.

(aside) The source notes this interval is consistent with the standard claim that wine and beer are roughly equivalent in alcohol content: a 5-ounce glass of 13% wine has .65 oz of alcohol, and a 12-ounce beer in this interval's range has .64 oz.

## A prediction interval

A prediction interval addresses a different question from a confidence interval: predicting a single future observation, rather than estimating the population mean.

### Proposition (p.300) (exam-flagged)
A prediction interval (PI) for a single observation to be selected from a normal population distribution is
$$\left(\bar{x}-t_{\alpha/2,\,n-1}\cdot s\sqrt{1+\frac{1}{n}}, \ \bar{x}+t_{\alpha/2,\,n-1}\cdot s\sqrt{1+\frac{1}{n}}\right)$$
The prediction level is $100(1-\alpha)\%$.

**Example 7.12 (source, slide 12)**
Fat content (%) of $n=10$ hot dogs: 25.2, 21.3, 22.8, 17.0, 29.8, 21.0, 25.5, 16.0, 20.9, 19.5. Assuming a normal population, a 95% CI for the mean fat content:
$$\bar{x} \pm t_{.025,9}\cdot\frac{s}{\sqrt{n}} = 21.90 \pm 2.262\cdot\frac{4.134}{\sqrt{10}} = 21.90 \pm 2.96 = (18.94, 24.86)$$
A point prediction for a single hot dog's fat content, analogous to a point estimate, is just $\bar{x} = 21.90$, but this gives no information about reliability or precision on its own.

**Example 7.13 (source, slide 14)**
With $n=10$, $\bar{x}=21.90$, $s=4.134$, $t_{.025,9}=2.262$, a 95% PI for the fat content of a single hot dog:
$$21.90 \pm (2.262)(4.134)\sqrt{1+\frac{1}{10}} = 21.90 \pm 9.81 = (12.09, 31.71)$$

> [!warning] A prediction interval is not a confidence interval (common mistake)
> A CI estimates where the population mean $\mu$ sits; a PI predicts where one new individual observation will fall. The PI is always wider, since it must account for both the uncertainty in estimating $\mu$ and the individual variability of a single observation around that mean, the $\sqrt{1+1/n}$ term versus the CI's $1/\sqrt{n}$ makes this explicit. In this example the PI's width is more than three times the CI's width on identical data.

## Confidence interval for the variance

### Theorem (p.304)
Let $X_1, X_2, \ldots, X_n$ be a random sample from a normal distribution $N(\mu, \sigma^2)$. Then
$$\frac{(n-1)S^2}{\sigma^2}$$
follows a chi-squared probability distribution with $n-1$ degrees of freedom.

### Proposition (exam-flagged)
A $100(1-\alpha)\%$ confidence interval for the variance $\sigma^2$ of a normal population:
$$\left(\frac{(n-1)s^2}{\chi^2_{\alpha/2,\,n-1}}, \ \frac{(n-1)s^2}{\chi^2_{1-\alpha/2,\,n-1}}\right)$$
A confidence interval for $\sigma$ has lower and upper limits that are the square roots of the corresponding limits in the interval for $\sigma^2$. Assumption: normality of the underlying distribution.

> [!note] Which chi-squared value goes where (added)
> The chi-squared distribution is not symmetric, so unlike the $z$ and $t$ intervals, the two critical values here are not the same number with opposite sign, $\chi^2_{\alpha/2,n-1}$ (the larger critical value, cutting off area $\alpha/2$ in the *upper* tail) divides into the CI's *lower* endpoint, while $\chi^2_{1-\alpha/2,n-1}$ (the smaller critical value, cutting off area $\alpha/2$ in the *lower* tail) divides into the *upper* endpoint. The example below shows this: 27.488 (the larger table value) produces the smaller endpoint .393, and 6.262 (the smaller table value) produces the larger endpoint 1.724.

**Example 7.15 (source, slides 17 to 18)**
Recall the beer alcohol percentage data from Example 7.11, where the normal plot was acceptably straight and $s = .8483$. The estimated variance is $s^2 = .8483^2 = .7196$. With $df = n-1 = 15$, a 95% CI requires $\chi^2_{.025,15} = 27.488$ and $\chi^2_{.975,15} = 6.262$. The interval for $\sigma^2$ is
$$\left(\frac{15(.7196)}{27.488}, \ \frac{15(.7196)}{6.262}\right) = (.393, 1.724)$$
Taking the square root of each endpoint gives $(.627, 1.313)$ as the 95% confidence interval for $\sigma$.

N.B with lower and upper limits differing by more than a factor of two, this interval is quite wide. Precise estimates of variability require large samples.

## Do not forget

- Small $n$ rules out the CLT justification, the $t$ interval instead assumes the population itself is normal.
- $T = (\bar{X}-\mu)/(S/\sqrt{n})$ has $t_{n-1}$ exactly under normality, for any $n$, not just approximately for large $n$.
- $t$ distributions are wider than $z$ for small $n$, precisely because $S$ replacing $\sigma$ adds uncertainty; they converge to $z$ as $n$ grows.
- A CI estimates $\mu$; a PI predicts one future observation, and is always wider than the matching CI, watch the $\sqrt{1+1/n}$ versus $1/\sqrt{n}$ difference.
- The chi-squared CI for $\sigma^2$ is asymmetric: the larger critical value ($\chi^2_{\alpha/2,n-1}$) gives the lower endpoint, the smaller critical value ($\chi^2_{1-\alpha/2,n-1}$) gives the upper endpoint.
- CI for $\sigma$ itself = square roots of the $\sigma^2$ interval's endpoints, not a separately derived formula.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — CLT and its rule of thumb, the large-sample justification this chapter's small-sample case can't rely on.
- [[STA01B1_Notes_S2_Point_Estimation]] — standard error, the building block for both the $t$ interval and the prediction interval here.
- [[STA01B1_Notes_S3_Statistical_Intervals]] — large-sample CI for $\mu$ using $z_{\alpha/2}$, the direct predecessor this note's $t_{\alpha/2,n-1}$ replaces for small $n$.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] — hypothesis testing stays with $Z$ for both its known-$\sigma$ and large-sample cases; the $t$ distribution introduced here is the natural next step for a small-sample unknown-$\sigma$ test, not yet covered.
