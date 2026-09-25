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
Every test in this note is the single-parameter case, written $\theta$.

In any hypothesis-testing problem there are two contradictory hypotheses under consideration, and the objective is to decide, based on sample information, which is correct. One claim is initially favoured and only rejected if sample evidence contradicts it and provides strong support for the alternative.

(aside) Court trial analogy: the judge must decide guilty or innocent. The person is assumed innocent to begin with, the state presents evidence trying to convince the judge to reject that assumption and conclude guilt. The presumption of innocence plays the role of $H_0$, guilt the role of $H_a$. The analogy stops at how the decision is made: a judge weighs evidence by judgment, a test decides by a fixed rule (see: Test procedures).

### Null and alternative hypothesis
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

> [!warning] "Fail to reject" is not "prove true" (common mistake) #common-mistake
> The only two outcomes are reject $H_0$ or fail to reject $H_0$. Failing to reject $H_0$ just means the sample didn't provide strong enough evidence against it, not that $H_0$ has been established as correct.

### Forms of the hypotheses
$$H_0: \theta = \theta_0$$
(assumed true until proven otherwise, $\theta_0$ is the null value, often "no difference, no improvement")
$$H_a: \theta \ne \theta_0 \ \text{(two-tailed)} \qquad H_a: \theta < \theta_0 \ \text{(lower-tailed)} \qquad H_a: \theta > \theta_0 \ \text{(upper-tailed)}$$
N.B The direction in $H_a$ names the test: not-equal is two-tailed, less-than is lower-tailed, greater-than is upper-tailed.

Example (composite): a bottler claims true mean fill volume is 500 ml. $H_0: \mu = 500$ throughout. If the concern is fills too small: $H_a: \mu < 500$, lower-tailed. Too large: $H_a: \mu > 500$, upper-tailed. Either direction: $H_a: \mu \ne 500$, two-tailed.

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
The test statistic squeezes the sample into one number; the rejection region is the set of values of that number that trigger rejection, not a set of raw data values.

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
(aside, quoted from source) Proverbs 17:15: "He who justifies the wicked and he who condemns the righteous are both hateful to the Lord." Condemning the righteous (convicting an innocent person) matches a Type I error, justifying the wicked (freeing a guilty person) matches a Type II error.

> [!tip] Reading Type I vs Type II off a decision already made (struggle) #struggle
> A stated conclusion is a binary reject/fail-to-reject decision, and only one error type is even possible given which side of that decision you're on. If $H_0$ was rejected, the only risk exposure is Type I (rejecting a true $H_0$), Type II cannot have happened, since Type II requires failing to reject. If $H_0$ was not rejected, the only risk exposure is Type II. Smoke alarm analogy: the alarm sounding with no fire is a Type I error (a true "no fire" $H_0$ wrongly rejected); a fire with the alarm staying silent is a Type II error (a false "no fire" $H_0$ wrongly not rejected). Definitions alone are easy to mix up, tying each error to a physical scenario like this one is what makes the direction stick.

### Example 8.4 (bumper design)
A bumper design sustains no visible damage 25% of the time in 10-mph crash tests. A modified design is proposed to raise that rate. Let $p$ = proportion of crashes with the new design that show no damage.
$$H_0: p = .25 \ \text{(no improvement)} \qquad H_a: p > .25$$
Experiment: $n=20$ independent crashes. Test statistic: $X$ = number of crashes with no visible damage. Rejection region $R_8 = \{8,9,\ldots,20\}$, reject $H_0$ if $x \ge 8$. Called upper-tailed because it consists only of large values of the test statistic.

When $H_0$ is true, $X \sim \text{Bin}(20,.25)$.
$$\alpha = P(X \ge 8 \text{ when } X\sim\text{Bin}(20,.25)) = 1-B(7;20,.25) = 1-.898 = .102$$
Roughly 10% of all experiments of this kind would incorrectly reject $H_0$ when it is true.

Unlike $\alpha$, there is not a single $\beta$, a different $\beta$ exists for each $p > .25$.
$$\beta(.3) = P(X\le7 \text{ when } X\sim\text{Bin}(20,.3)) = B(7;20,.3) = .772$$

| $p$ | .3 | .4 | .5 | .6 | .7 | .8 |
|---|---|---|---|---|---|---|
| $\beta(p)$ | .772 | .416 | .132 | .021 | .001 | .000 |

N.B $\beta$ decreases as $p$ moves farther from the null value .25. The greater the departure from $H_0$, the less likely it goes undetected.

> [!note] The "worst case" boundary trick for a composite null (added) #added
> The test above is still reasonable for the more realistic $H_0: p \le .25$. There is then an $\alpha(p)$ for each $p\le.25$ instead of one $\alpha$, and $\alpha(p) < \alpha(.25)=.102$ for every $p<.25$. The largest $\alpha$ occurs exactly at the boundary value between $H_0$ and $H_a$. Checking $\alpha$ only at the boundary is enough, if it is small there it is as small or smaller everywhere else $H_0$ holds.

### Example 8.4, smaller rejection region $R_9$
Same experiment, $R_9=\{9,\ldots,20\}$, reject if $x\ge9$.
$$\alpha = P(X\ge9 \text{ when } X\sim\text{Bin}(20,.25)) = 1-B(8;20,.25) = .041$$
$\alpha$ decreased from .102 to .041. Price paid:
$$\beta(.3) = B(8;20,.3) = .887 \qquad \beta(.5) = B(8;20,.5) = .252$$
Both larger than the $R_8$ values (.772, .132).

> [!warning] $\alpha$ and $\beta$ trade off against each other (common mistake) #common-mistake
> $\alpha$ sums test statistic values inside the rejection region, $\beta$ is the probability the test statistic falls outside it. Shrinking the rejection region must decrease $\alpha$ while increasing $\beta$, for any fixed alternative, for a fixed $n$. Neither can shrink for free.

### Example 8.5 (paint drying time)
Paint drying time is normal, mean 75 min, $\sigma=9$ min. A new additive is believed to keep drying times normal with $\sigma=9$, hoped to decrease the mean. Only strong evidence should adopt it.
$$H_0: \mu=75 \qquad H_a: \mu<75$$
$n=25$ specimens, $\bar{X}\sim N(\mu, \sigma_{\bar{X}}^2)$, $\sigma_{\bar{X}}=9/\sqrt{25}=1.8$. A reasonable rejection region has the form $\bar{x}\le c$, lower-tailed. Take $c=70.8$.
$$\alpha = \Phi\left(\frac{70.8-75}{1.8}\right) = \Phi(-2.33) = .01$$
$$\beta(72) = 1-\Phi\left(\frac{70.8-72}{1.8}\right) = 1-\Phi(-.67) = .7486$$
$$\beta(70) = 1-\Phi\left(\frac{70.8-70}{1.8}\right) = .3300 \qquad \beta(67) = .0174$$
Only 1% of experiments incorrectly reject $H_0$, but the chance of a Type II error is very large near the null ($\mu=72$) and small far from it ($\mu=67$).

### Example 8.5, changing the cutoff
$c=70.8$ gave small $\alpha$ but large $\beta$'s. Try $c=72$:
$$\alpha = \Phi\left(\frac{72-75}{1.8}\right) = \Phi(-1.67) = .0475 \approx .05$$
$$\beta(72) = 1-\Phi(0) = .5 \qquad \beta(70) = .1335 \qquad \beta(67) = .0027$$
The larger rejection region decreases $\beta$ for each fixed $\mu$, but $\alpha$ rose from .01 to about .05. If a Type I error this large is tolerable, $c=72$ is preferable to $c=70.8$ for the smaller $\beta$'s.

> [!note] Why raising alpha can only flip a decision one way (added) #added
> A larger $\alpha$ enlarges the rejection region, it can only newly capture a test statistic value that was previously outside it, never expel one already inside. So raising $\alpha$ can only ever move a decision from fail-to-reject toward reject, never the reverse. If a computed $z$ already falls in the rejection region at a small $\alpha$, it stays there at every larger $\alpha$; it cannot un-reject.

## Standardizing the test statistic

### Standardizing example (nicotine content)
$\mu$ = true average nicotine content of brand B cigarettes. $H_0: \mu=1.5$ versus $H_a: \mu>1.5$, $n=32$, normal population, $\sigma=.20$ known. $\bar{X}\sim N(\mu, \sigma_{\bar{X}}^2)$, $\sigma_{\bar{X}}=.20/\sqrt{32}=.0354$.

Rather than use $\bar{X}$ itself, standardize assuming $H_0$ true:
$$Z = \frac{\bar{X}-1.5}{.0354}$$
$Z$ is the distance between $\bar{X}$ and its expected value under $H_0$, in standard deviations.

N.B Standardising turns a problem-specific cutoff on $\bar{x}$ into a fixed, reusable cutoff on $z$, the same $z$ value regardless of $\mu_0$, $\sigma$, or $n$.

Rejecting when $\bar{x}$ "considerably" exceeds 1.5 is equivalent to rejecting when $z$ "considerably" exceeds 0, rejection region $z\ge c$. Let $\alpha=.05$.
$$\alpha = P(Z\ge c \text{ when } Z\sim N(0,1)) \implies c=z_{.05}=1.645$$
$z\ge1.645 \iff \bar{x}-1.5\ge(.0354)(1.645) \iff \bar{x}\ge1.56$. $\beta$ is then $P(\bar{X}<1.56)$, computable for any $\mu>1.5$.

> [!tip] Fixed calculation order for a hypothesis test (struggle) #struggle
> A common failure mode is losing track partway through, not from missing a formula but from having no fixed sequence to plug numbers into. Use the seven step order Examples 8.6 and 8.8 below both follow: (1) name the parameter, (2) state $H_0$, (3) state $H_a$, (4) write the test statistic formula, (5) fix the rejection region from $H_a$'s form and the chosen $\alpha$, (6) substitute the sample numbers and compute, (7) compare to the rejection region and conclude in words. Doing this in the same order every time, rather than jumping to the arithmetic first, is what the worked examples below model.

## Tests about a population mean

### Case I: known variance (exam-flagged) #exam-flagged
Normal population, $\sigma$ known, any $n$. Test statistic:
$$Z = \frac{\bar{X}-\mu_0}{\sigma/\sqrt{n}}$$

| $H_a$ | Rejection region |
|---|---|
| $\mu>\mu_0$ (upper-tailed) | $z\ge z_\alpha$ |
| $\mu<\mu_0$ (lower-tailed) | $z\le -z_\alpha$ |
| $\mu\ne\mu_0$ (two-tailed) | $z\ge z_{\alpha/2}$ or $z\le -z_{\alpha/2}$ |

N.B the two-tailed region splits $\alpha$ into two tails of $\alpha/2$ each (defined in: $\alpha$ vs $\alpha/2$ vs the table value, [[STA01B1_Notes_S3_Statistical_Intervals]]), the same $z_{\alpha/2}$ notation used there for confidence intervals, here marking a rejection boundary instead of an interval's error of estimation.

### Example 8.6 (sprinkler activation temperature)
A sprinkler manufacturer claims true average activation temperature is $130°$F. $n=9$ systems, $\bar{x}=131.08°$F, normal population, $\sigma=1.5°$F, $\alpha=.01$.
1. Parameter: $\mu$ = true average activation temperature.
2. $H_0: \mu=130$
3. $H_a: \mu\ne130$ (departure in either direction is of concern)
4. $z = \dfrac{\bar{x}-130}{1.5/\sqrt{n}}$
5. Two-tailed (defined in: Case I: known variance), reject if $z\ge z_{.005}$ or $z\le-z_{.005}$; $z_{.005}=2.58$.
6. $z = \dfrac{131.08-130}{1.5/\sqrt{9}} = \dfrac{1.08}{.5} = 2.16$
7. $2.16$ does not fall in the rejection region ($-2.58<2.16<2.58$), $H_0$ cannot be rejected at $\alpha=.01$. The data does not strongly support a departure from 130.

### Case II: large sample tests (exam-flagged) #exam-flagged
When $\sigma$ is unknown and $n>30$, substitute $S$:
$$Z = \frac{\bar{X}-\mu_0}{S/\sqrt{n}}$$
N.B the three rejection regions from [[#Case I: known variance (exam-flagged)]] apply unchanged, only the denominator changes, $\sigma$ becomes $S$, and $n>30$ is required for the approximation, paralleling the $n>40$ threshold for large-sample confidence intervals (see: [[STA01B1_Notes_S3_Statistical_Intervals]]), where substituting $S$ for $\sigma$ was likewise stricter than the plain CLT rule of thumb.

### Example 8.8 (restaurant tip percentage)
70 restaurant bills, tip as a percentage of the raw bill. Does the population mean tip percentage exceed the standard 15%?
1. $\mu$ = true average tip percentage.
2. $H_0: \mu=15$
3. $H_a: \mu>15$
4. $z = \dfrac{\bar{x}-15}{s/\sqrt{n}}$
5. $\alpha=.05$, upper-tailed (defined in: [[#Case I: known variance (exam-flagged)]]), reject if $z\ge1.645$.
6. $n=70$, $\bar{x}=17.99$, $s=5.937$: $z=\dfrac{17.99-15}{5.937/\sqrt{70}}=\dfrac{2.99}{.7096}=4.21$
7. $4.21\ge1.645$, $H_0$ is rejected. Evidence the true average tip percentage exceeds 15%.

## Which case, and which tail

**Case I/Case II, from this lecture's source only**

| Condition | Test statistic | Distribution | Case |
|---|---|---|---|
| Population normal, $\sigma$ known, any $n$ | $Z=\dfrac{\bar{X}-\mu_0}{\sigma/\sqrt{n}}$ | standard normal, exact | [[#Case I: known variance (exam-flagged)]] |
| $\sigma$ unknown, $n>30$ | $Z=\dfrac{\bar{X}-\mu_0}{S/\sqrt{n}}$ | standard normal, approximate | [[#Case II: large sample tests (exam-flagged)]] |
| $\sigma$ unknown, $n\le30$ | not shown in this lecture's source | not shown in this lecture's source | not covered here |

N.B both cases here use $Z$, never $t$. The switch is not $t$ versus $Z$, it is which standard error formula applies, driven by whether $\sigma$ is known, the same fork already established for confidence intervals (see: [[STA01B1_Notes_S3_Statistical_Intervals]]). A small-sample unknown-$\sigma$ test would need $t$ (see: [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] for the $t$ distribution itself), but that test does not appear in this lecture.

**Wording to hypothesis form, from this lecture's own examples**

| Wording in the problem | $H_a$ form | Tail | Rejection region | Seen in |
|---|---|---|---|---|
| "no improvement," claimed exact value | $H_0:\theta=\theta_0$ | (baseline) | — | [[#Example 8.4 (bumper design)]], [[#Example 8.6 (sprinkler activation temperature)]] |
| "increase," "exceeds," "greater than" | $H_a:\theta>\theta_0$ | upper | $z\ge z_\alpha$ | [[#Example 8.4 (bumper design)]], [[#Standardizing example (nicotine content)]], [[#Example 8.8 (restaurant tip percentage)]] |
| "decrease," "hoped to lower," "less than" | $H_a:\theta<\theta_0$ | lower | $z\le-z_\alpha$ | [[#Example 8.5 (paint drying time)]] |
| "differs from," concern either direction | $H_a:\theta\ne\theta_0$ | two | $z\ge z_{\alpha/2}$ or $z\le-z_{\alpha/2}$ | [[#Example 8.6 (sprinkler activation temperature)]] |

N.B this lecture never produces a p-value, every decision is cutoff versus computed $z$. A p-value column belongs to whichever later lecture introduces it.

## Do not forget
- Two outcomes only: reject $H_0$, or fail to reject $H_0$. Never "prove $H_0$ true."
- $H_a$'s direction fixes the test: $\ne$ two-tailed, $<$ lower-tailed, $>$ upper-tailed.
- $\alpha$ = P(Type I, reject a true $H_0$); $\beta$ = P(Type II, fail to reject a false $H_0$), not a single number, it depends on the specific alternative.
- Given a stated decision alone, only one error type is even possible, reject exposes Type I only, fail to reject exposes Type II only.
- Shrinking the rejection region decreases $\alpha$ but increases $\beta$ for every fixed alternative. Raising $\alpha$ can only flip fail-to-reject into reject, never the reverse.
- For a composite null, the boundary value gives the largest $\alpha$, the worst case.
- Standardising to $Z$ turns a problem-specific cutoff into a fixed, reusable critical value.
- Case I (known $\sigma$, any $n$) uses $\sigma/\sqrt{n}$; Case II (unknown $\sigma$, $n>30$) substitutes $S$. Both use $Z$, this lecture has no small-sample unknown-$\sigma$ test.
- Follow the same seven step order every time: parameter, $H_0$, $H_a$, test statistic, rejection region, substitute, conclude.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — sampling distribution of $\bar{X}$ and $\sigma_{\bar{X}}=\sigma/\sqrt{n}$, used throughout this note's $\alpha$ and $\beta$ calculations.
- [[STA01B1_Notes_S3_Statistical_Intervals]] — the $z_{\alpha/2}$ and $z_\alpha$ critical value conventions and the $S$-for-$\sigma$ large-sample substitution, both carried over directly into this note.
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] — the $t$ distribution, not used in this lecture but the natural next step for a small-sample unknown-$\sigma$ test.
- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]] — extends the Case I/II fork and the seven step procedure from one sample to two, and adds the pooled $t$ test for small samples.
