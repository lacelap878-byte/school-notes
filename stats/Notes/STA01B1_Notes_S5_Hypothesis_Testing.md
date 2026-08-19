---
module: STA01B1
topic: Hypothesis Testing
session: S5
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Hypothesis Testing (Devore & Berk, Ch 8.1 & 8.2)

A confidence interval (see: [[STA01B1_Notes_S3_Statistical_Intervals]]) answers "what range of values is $\mu$ plausibly in." Hypothesis testing answers a different question: "does the sample evidence contradict a specific claimed value strongly enough to reject it."

## What is a statistical hypothesis

```
hy.poth.e.sis
noun
A proposed explanation made on the basis of limited evidence as a
starting point for further investigation.
```

```
A statistical hypothesis is a claim or assertion either about
- the value of a single parameter (population characteristic or
  characteristic of a probability distribution),
- about the values of several parameters,
- or about the form of an entire probability distribution.
```

In any hypothesis-testing problem there are two contradictory hypotheses under consideration, and the objective is to decide, based on sample information, which is correct. One claim is initially favoured and only rejected if sample evidence contradicts it and provides strong support for the alternative.

(aside) Court trial analogy: the judge must decide guilty or innocent. The person is assumed innocent to begin with, the state presents evidence trying to convince the judge to reject that assumption and conclude guilt. The presumption of innocence plays the role of $H_0$, guilt the role of $H_a$, evidence has to be strong enough to overturn the starting assumption, not merely suggest it.

### Definitions
```
The null hypothesis, denoted by H0, is the claim that is initially
assumed to be true.

The alternative hypothesis, denoted by Ha, is the assertion that is
contradictory to H0.
```
```
The null hypothesis will be rejected in favour of the alternative
hypothesis only if sample evidence suggests that H0 is false.
If the sample does not strongly contradict H0, we will continue to
believe in the probability of the null hypothesis.
The two possible conclusions from a hypothesis-testing analysis are
then:
- Reject H0, or
- Fail to reject H0
```

> [!warning] "Fail to reject" is not "prove true" (common mistake)
> The only two outcomes are reject $H_0$ or fail to reject $H_0$, there is no third option where $H_0$ is confirmed or proven. Failing to reject $H_0$ just means the sample didn't provide strong enough evidence against it, not that $H_0$ has been established as correct.

### Forms of the hypotheses
$$H_0: \theta = \theta_0$$
(assumed true until proven otherwise, $\theta_0$ is the null value, often representing "no difference, no improvement")
$$H_a: \theta \ne \theta_0 \quad \text{(two-tailed)} \qquad H_a: \theta < \theta_0 \quad \text{(lower-tailed)} \qquad H_a: \theta > \theta_0 \quad \text{(upper-tailed)}$$

## Test procedures

```
A test procedure is a rule, based on sample data, for deciding whether
to reject the null hypothesis.

1. A Test Statistic
   A function of the sample data on which the decision about Ho (to
   reject or not to reject!) is to be based.

2. A Rejection Region
   The set of all test statistic values for which Ho will be rejected.
```

## Errors in hypothesis testing

### Definitions (exam-flagged)
```
1. Type I error
   Rejecting the null hypothesis Ho when it is true.
   P(Type I) = alpha

2. Type II error
   Not rejecting the null hypothesis Ho when it is false.
   P(Type II) = beta
```
(aside, mnemonic quoted from the source slide) Proverbs 17:15: "He who justifies the wicked and he who condemns the righteous are both hateful to the Lord." Justifying the wicked (failing to convict someone guilty) parallels a Type II error; condemning the righteous (convicting someone innocent) parallels a Type I error.

**Example 8.4 (source, slide 11)**
A bumper design is known to sustain no visible damage 25% of the time in 10-mph crash tests. A modified bumper is proposed to increase this. Let $p$ = proportion of crashes with no damage. $H_0: p=.25$ (no improvement) versus $H_a: p>.25$. Experiment: $n=20$ independent crashes.

Test statistic: $X$ = number of crashes with no visible damage.
Rejection region: $R_8 = \{8,9,10,\ldots,19,20\}$, i.e. reject $H_0$ if $x \ge 8$.
This is called *upper-tailed* because it consists only of large values of the test statistic.

**Computing $\alpha$ for $R_8$**
When $H_0$ is true, $X \sim \text{Bin}(20, .25)$.
$$\alpha = P(\text{type I error}) = P(X \ge 8 \text{ when } X\sim\text{Bin}(20,.25)) = 1-B(7;20,.25) = 1-.898 = .102$$
When $H_0$ is actually true, roughly 10% of all experiments consisting of 20 crashes would result in $H_0$ being incorrectly rejected.

**Computing $\beta$, one value per alternative**
Unlike $\alpha$, there is not a single $\beta$, a different $\beta$ exists for each value of $p$ exceeding .25.
$$\beta(.3) = P(\text{type II error when } p=.3) = P(X\le 7 \text{ when } X\sim\text{Bin}(20,.3)) = B(7;20,.3) = .772$$

| $p$ | .3 | .4 | .5 | .6 | .7 | .8 |
|---|---|---|---|---|---|---|
| $\beta(p)$ | .772 | .416 | .132 | .021 | .001 | .000 |

N.B $\beta$ decreases as $p$ moves farther to the right of the null value .25. The greater the departure from $H_0$, the less likely such a departure will go undetected.

> [!note] The "worst case" boundary trick for a composite null (added)
> The test procedure above is still reasonable for the more realistic null hypothesis $p \le .25$. In that case there is no longer a single $\alpha$, but instead an $\alpha(p)$ for each $p \le .25$: $\alpha(.25), \alpha(.23), \alpha(.20), \alpha(.15)$, and so on. It can be verified that $\alpha(p) < \alpha(.25) = .102$ for any $p < .25$, that is, the largest value of $\alpha$ occurs exactly at the boundary value .25 between $H_0$ and $H_a$. Working with the boundary value is therefore the worst case, if $\alpha$ is small there, it will be as small or smaller for the rest of the more realistic composite null.

**Same experiment, a smaller rejection region $R_9$**
Now consider $R_9 = \{9,10,\ldots,20\}$, still with $X\sim\text{Bin}(20,p)$.
$$\alpha = P(H_0 \text{ rejected when } p=.25) = P(X\ge9 \text{ when } X\sim\text{Bin}(20,.25)) = 1-B(8;20,.25) = .041$$
The type I error probability has decreased. However, a price has been paid:
$$\beta(.3) = P(X\le8 \text{ when } X\sim\text{Bin}(20,.3)) = B(8;20,.3) = .887$$
$$\beta(.5) = B(8;20,.5) = .252$$
Both $\beta$'s are larger than the corresponding values for $R_8$ (.772 and .132).

> [!warning] $\alpha$ and $\beta$ trade off against each other (common mistake)
> $\alpha$ is computed by summing over test statistic values *inside* the rejection region, while $\beta$ is the probability the test statistic falls *outside* it (in the complement). Making the rejection region smaller must therefore decrease $\alpha$ while increasing $\beta$, for any fixed alternative value of the parameter. Neither error can be shrunk for free without also changing $n$.

**Example 8.5 (source, slides 15 to 18)**
Paint drying time is normally distributed with mean 75 min, $\sigma = 9$ min. A new additive is believed to keep drying times normal with $\sigma=9$ but is hoped to decrease the mean. Let $\mu$ = true average drying time with the additive. $H_0: \mu=75$ versus $H_a: \mu<75$. Only if $H_0$ can be rejected will the additive be declared successful.

Experimental data: $n=25$ specimens, $\bar{X}$ is normal with $\mu_{\bar{X}} = \mu$, $\sigma_{\bar{X}} = \sigma/\sqrt{n} = 9/\sqrt{25} = 1.8$. When $H_0$ is true, $\mu_{\bar{X}} = 75$, so an $\bar{x}$ value somewhat less than 75 would not strongly contradict $H_0$. A reasonable rejection region has the form $\bar{x} \le c$ (lower-tailed, small values of the test statistic). Take $c=70.8$.
$$\alpha = P(\bar{X}\le70.8 \text{ when } \bar{X}\sim N(75, 1.8^2)) = \Phi\left(\frac{70.8-75}{1.8}\right) = \Phi(-2.33) = .01$$
$$\beta(72) = P(\bar{X}>70.8 \text{ when } \bar{X}\sim N(72,1.8^2)) = 1-\Phi\left(\frac{70.8-72}{1.8}\right) = 1-\Phi(-.67) = 1-.2514=.7486$$
$$\beta(70) = 1-\Phi\left(\frac{70.8-70}{1.8}\right) = .3300 \qquad \beta(67) = .0174$$
For this test, only 1% of experiments will incorrectly reject $H_0$. But the chance of a type II error is very large when $\mu=72$ (a small departure from $H_0$), and quite small when $\mu=67$ (a substantial departure). $\alpha$ is computed using the distribution of the test statistic when $H_0$ is true; determination of $\beta$ requires knowing the test statistic's distribution when $H_0$ is false. As before, if the more realistic null hypothesis $\mu \ge 75$ is considered, the boundary value $\mu=75$ gives the largest of all the type I error probabilities.

**Changing the cutoff, same example**
The use of $c=70.8$ resulted in a very small $\alpha$ (.01) but rather large $\beta$'s. Try $c=72$ instead:
$$\alpha = P(\bar{X}\le72 \text{ when } \bar{X}\sim N(75,1.8^2)) = \Phi\left(\frac{72-75}{1.8}\right) = \Phi(-1.67) = .0475 \approx .05$$
$$\beta(72) = P(\bar{X}>72 \text{ when } \bar{X}\sim N(72,1.8^2)) = 1-\Phi(0) = .5$$
$$\beta(70) = 1-\Phi\left(\frac{72-70}{1.8}\right) = .1335 \qquad \beta(67) = 1-\Phi\left(\frac{72-67}{1.8}\right) = .0027$$
The larger rejection region (including more $\bar{x}$ values) decreases $\beta$ for each fixed $\mu$, but $\alpha$ has increased from .01 to about .05. If a type I error probability this large can be tolerated, the second region ($c=72$) is preferable to the first ($c=70.8$) because of the smaller $\beta$'s.

### Standardizing the test statistic

**Worked example (source, "An example")**
$\mu$ = true average nicotine content of brand B cigarettes. $H_0: \mu=1.5$ versus $H_a: \mu>1.5$, based on $n=32$, with $\sigma=.20$ assumed known and the population normal. $\bar{X}$ is normal with $\mu_{\bar{X}}=\mu$, $\sigma_{\bar{X}} = .20/\sqrt{32} = .0354$.

Rather than using $\bar{X}$ itself, standardize it assuming $H_0$ is true:
$$Z = \frac{\bar{X}-1.5}{\sigma/\sqrt{n}} = \frac{\bar{X}-1.5}{.0354}$$
$Z$ expresses the distance between $\bar{X}$ and its expected value under $H_0$, in standard deviations. For example, $z=3$ results from an $\bar{x}$ that is 3 standard deviations larger than expected were $H_0$ true.

Rejecting $H_0$ when $\bar{x}$ "considerably" exceeds 1.5 is equivalent to rejecting when $z$ "considerably" exceeds 0, so the rejection region takes the form $z \ge c$. To fix $\alpha=.05$: when $H_0$ is true, $Z$ has a standard normal distribution, so $c$ must capture upper-tail area .05, $c=z_{.05}=1.645$. Note $z\ge1.645$ is equivalent to $\bar{x}-1.5 \ge (.0354)(1.645)$, i.e. $\bar{x}\ge1.56$. Then $\beta$ is the probability that $\bar{X}<1.56$, computable for any $\mu>1.5$.

## Tests about a population mean

### Case I, normal population with known variance (exam-flagged)
Test statistic:
$$Z = \frac{\bar{X}-\mu_0}{\sigma/\sqrt{n}}$$
With $H_0: \mu = \mu_0$, the rejection region depends on the form of $H_a$:

| $H_a$ | Rejection region |
|---|---|
| $\mu > \mu_0$ (upper-tailed) | $z \ge z_\alpha$ |
| $\mu < \mu_0$ (lower-tailed) | $z \le -z_\alpha$ |
| $\mu \ne \mu_0$ (two-tailed) | $z \ge z_{\alpha/2}$ or $z \le -z_{\alpha/2}$ |

**Example 8.6 (source, slides "Tests about a Population Mean")**
A manufacturer of sprinkler systems claims the true average system-activation temperature is $130°$F. A sample of $n=9$ systems yields $\bar{x}=131.08°$F. Distribution of activation times is normal with $\sigma=1.5°$F. Does the data contradict the manufacturer's claim at significance level $\alpha=.01$?

1. Parameter of interest: $\mu$ = true average activation temperature.
2. Null hypothesis: $H_0: \mu = 130$ (null value $\mu_0=130$).
3. Alternative hypothesis: $H_a: \mu \ne 130$ (a departure from the claimed value in *either* direction is of concern).
4. Test statistic: $z = \dfrac{\bar{x}-\mu_0}{\sigma/\sqrt{n}} = \dfrac{\bar{x}-130}{1.5/\sqrt{n}}$
5. Rejection region: the form of $H_a$ implies a two-tailed test, rejection region $z\ge z_{.005}$ or $z\le -z_{.005}$. $z_{.005}=2.58$, so reject $H_0$ if $z\ge2.58$ or $z\le-2.58$.
6. Substituting $n=9$, $\bar{x}=131.08$: $z = \dfrac{131.08-130}{1.5/\sqrt{9}} = \dfrac{1.08}{.5} = 2.16$. The observed sample mean is a bit more than 2 standard deviations above what would have been expected were $H_0$ true.
7. $z=2.16$ does not fall in the rejection region ($-2.58<2.16<2.58$), so $H_0$ cannot be rejected at significance level .01. The data does not give strong support to the claim that the true average differs from the design value of 130.

### Case II, large sample tests ($n>30$) (exam-flagged)
When $\sigma$ is unknown, substitute the sample standard deviation $S$:
$$Z = \frac{\bar{X}-\mu_0}{S/\sqrt{n}}$$
Valid for $n>30$.

**Worked example, Example 8.8 (source, "An example" / "Tests about a Population Mean")**
A sample of bills for meals at a restaurant gave the tip as a percentage of the raw bill for each of 70 bills. Does it appear the population mean tip percentage exceeds the standard 15%?

1. $\mu$ = true average tip percentage.
2. $H_0: \mu = 15$
3. $H_a: \mu > 15$
4. $z = \dfrac{\bar{x}-15}{s/\sqrt{n}}$
5. Using a test with significance level .05, $H_0$ will be rejected if $z\ge1.645$ (an upper-tailed test).
6. With $n=70$, $\bar{x}=17.99$, $s=5.937$: $z = \dfrac{17.99-15}{5.937/\sqrt{70}} = \dfrac{2.99}{.7096} = 4.21$.
7. Since $4.21 \ge 1.645$, $H_0$ is rejected. There is evidence that the true average tip percentage exceeds 15%.

## Do not forget

- Two outcomes only: reject $H_0$, or fail to reject $H_0$. Failing to reject never means $H_0$ is proven true.
- $H_a$'s direction ($\ne$, $<$, $>$) fixes whether the test is two-tailed, lower-tailed, or upper-tailed, and which rejection region formula applies.
- $\alpha$ = P(Type I, reject a true $H_0$); $\beta$ = P(Type II, fail to reject a false $H_0$). $\beta$ is not a single number, it depends on which specific alternative parameter value is true.
- Shrinking the rejection region decreases $\alpha$ but increases $\beta$ for every fixed alternative, they trade off directly against each other.
- For a composite null ($\theta \le \theta_0$ or $\theta \ge \theta_0$), the boundary value $\theta_0$ gives the largest $\alpha$ among all values where $H_0$ holds, the worst case.
- Standardizing the test statistic to $Z$ expresses how many standard deviations $\bar{X}$ sits from the value $H_0$ claims, and lets the rejection region be written as a fixed critical value like $z_\alpha$ regardless of the specific numbers in the problem.
- Case I (known $\sigma$, any $n$, normal population) uses $Z=(\bar{X}-\mu_0)/(\sigma/\sqrt{n})$; Case II (unknown $\sigma$, $n>30$) substitutes $S$ for $\sigma$ in the same statistic.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — sampling distribution of $\bar{X}$ and its standard deviation $\sigma_{\bar{X}} = \sigma/\sqrt{n}$, used throughout this note's $\alpha$ and $\beta$ calculations.
- [[STA01B1_Notes_S3_Statistical_Intervals]] — the $z_{\alpha/2}$ and $z_\alpha$ critical value conventions carried over directly into rejection regions here.
