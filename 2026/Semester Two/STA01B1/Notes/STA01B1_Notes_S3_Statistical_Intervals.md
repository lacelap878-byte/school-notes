---
module: STA01B1
topic: Statistical Intervals
session: S3
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Statistical Intervals (Devore & Berk, Ch 7.1 & 7.2)

A point estimate is a single number and, by itself, says nothing about how close it is likely to be to the true parameter. This chapter replaces the single number with a range that comes with a stated level of trust attached.

## Basic properties of confidence intervals

Because of sampling variability, the point estimate virtually never exactly equals the parameter, and the point estimate alone gives no way to judge how close it might be. The alternative is to calculate and report an entire interval of plausible values, an interval estimate or confidence interval (CI).

### Derivation, known $\sigma$, normal population
Since the population is normal, $\bar{X}$ is also normal (defined in: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]), so
$$\frac{\bar{X}-\mu}{\sigma/\sqrt{n}}$$
follows a standard normal distribution. Fixing the confidence coefficient at $1-\alpha = 0.95$ gives $P(-1.96 < Z < 1.96) = 0.95$. Substituting the standardized form and isolating $\mu$ algebraically:
$$P\left(-1.96 < \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} < 1.96\right) = 0.95$$
$$P\left(-1.96\frac{\sigma}{\sqrt{n}} < \bar{X}-\mu < 1.96\frac{\sigma}{\sqrt{n}}\right) = 0.95$$
$$P\left(\bar{X}-1.96\frac{\sigma}{\sqrt{n}} < \mu < \bar{X}+1.96\frac{\sigma}{\sqrt{n}}\right) = 0.95$$
giving the random interval
$$\left(\bar{X}-1.96\frac{\sigma}{\sqrt{n}}, \ \bar{X}+1.96\frac{\sigma}{\sqrt{n}}\right)$$

### Definition, 95% CI for $\mu$
$$\left(\bar{x}-1.96\frac{\sigma}{\sqrt{n}}, \ \bar{x}+1.96\frac{\sigma}{\sqrt{n}}\right)$$
Interpretation: one can be highly confident, at the 95% confidence level, that $\mu$ falls in this interval.

## Interpreting the confidence level

> [!warning] The confidence level is not a probability about one computed interval (common mistake)
> Once a sample is drawn and the interval is calculated, $\mu$ either is or is not in that specific interval, there is no probability left to talk about for that one interval. The 95% describes the long run success rate of the *procedure*: if you repeated the sampling and interval-building process many times, about 95% of the resulting intervals would contain $\mu$, and about 5% would miss it entirely by chance. "95% confident" is a statement about the method's track record, not about the one interval sitting in front of you.

## Other levels of confidence

Any desired confidence level is achieved by replacing 1.96 with the appropriate standard normal critical value $z_{\alpha/2}$, where the shaded tail area beyond $z_{\alpha/2}$ is $\alpha/2$ and $P(-z_{\alpha/2} \le Z \le z_{\alpha/2}) = 1-\alpha$.

### Definition, general form (exam-flagged)
A $100(1-\alpha)\%$ confidence interval for the mean $\mu$ of a normal population when $\sigma$ is known:
$$\left(\bar{x}-z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}, \ \bar{x}+z_{\alpha/2}\cdot\frac{\sigma}{\sqrt{n}}\right) \quad \text{or} \quad \left(\bar{x}-z_{\alpha/2}\cdot SE, \ \bar{x}+z_{\alpha/2}\cdot SE\right)$$
The quantity $z_{\alpha/2}\cdot SE$ is called the error of estimation.

> [!note] $\alpha$ vs $\alpha/2$ vs the table value (struggle)
> Three related but distinct numbers: $\alpha$ is the total error allowed, split across both tails combined (e.g. $\alpha = .10$ for 90% confidence). $\alpha/2$ is the area in *one* tail alone (e.g. .05). The cumulative area you actually look up in a standard normal table to find $z_{\alpha/2}$ is $1-\alpha/2$, not $1-\alpha$ and not $\alpha$ itself, since the table gives area to the left of a $z$ value, and $z_{\alpha/2}$ sits at the point with $\alpha/2$ area still remaining to its right.

**Example 7.3 (source, slide 14)**
Final exam scores normally distributed, believed $\sigma = 13$. Sample of 40 students, $\bar{x} = 70.7$. 90% confidence: $\alpha = .10$, so $z_{\alpha/2} = z_{.05} = 1.645$ (cumulative table area .9500).
$$70.7 \pm (1.645)\frac{13}{\sqrt{40}} = 70.7 \pm 3.4 = (67.3, 74.1)$$

## Confidence level, precision, sample size

A wider interval gives higher confidence but less precision; a narrower interval gives more precision but less confidence. A good CI is both narrow and has a large confidence coefficient, but these pull against each other for a fixed $n$. N.B the only way to increase confidence without increasing width is to increase the sample size.

**Example 7.4 (source, slide 16)**
Response time normal, $\sigma = 25$ millisec. Desired: 95% CI with width at most 10.
$$10 = 2\cdot(1.96)(25/\sqrt{n})$$
$$\sqrt{n} = 2\cdot(1.96)(25)/10 = 9.80 \implies n = (9.80)^2 = 96.04$$
Since $n$ must be an integer, a sample size of 97 is required.

## Large sample confidence intervals (unknown $\sigma$)

If $n$ is sufficiently large, the standardized variable
$$Z = \frac{\bar{X}-\mu}{S/\sqrt{n}}$$
has approximately a standard normal distribution, giving a large sample CI for $\mu$ with confidence level approximately $100(1-\alpha)\%$:
$$\left(\bar{x}-z_{\alpha/2}\cdot\frac{s}{\sqrt{n}}, \ \bar{x}+z_{\alpha/2}\cdot\frac{s}{\sqrt{n}}\right)$$
This is valid regardless of the population's shape. N.B generally $n > 40$ is needed, a stricter threshold than the CLT rule of thumb of $n \ge 30$ (see: [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]]), because substituting $S$ for the unknown $\sigma$ introduces additional variability on top of what the CLT already accounts for.

**Example 7.6 (source, slide 19)**
50 algebra placement scores, $\bar{x} = 19.82$, $s = 4.50$.
$$19.82 \pm 1.96\frac{4.50}{\sqrt{50}} = 19.82 \pm 1.25 = (18.6, 21.1)$$
That is, $18.6 < \mu < 21.1$ with confidence level approximately 95%.

**Example 7.7 (source, slide 20)**
Same algebra score context, sample size planning. No value of $s$ exists yet, so the investigator believes virtually all population values lie between 10 and 30. Using $(30-10)/4 = 5$ as a reasonable value for $s$, the sample size for a 95% CI of width 2 (i.e. within 1) is
$$n = [(1.96)(5)/1]^2 \approx 96$$

> [!note] Range rule of thumb vs the Central Limit Theorem (struggle)
> These answer different questions and must not be conflated. The range rule ($\sigma \approx \text{range}/4$) is a rough guess at the *population's* spread, used only for advance sample size planning when no $s$ or $\sigma$ estimate exists yet. It rests on the assumption that roughly 95% of a normal population's individual values fall within 2 standard deviations either side of the mean, so a 4-standard-deviation span covers most of the range. It is a statement about single observations. The CLT, by contrast, is a statement about the shape of the *sampling distribution* of $\bar{X}$ (approximately normal for large $n$, regardless of population shape). One estimates a spread before any calculation is possible, the other justifies the normal-based CI formula itself.

## Confidence interval for a population proportion

### Proposition (exam-flagged)
An approximate $100(1-\alpha)\%$ CI for a population proportion $p$:
$$\left(\hat{p}-z_{\alpha/2}\cdot\sqrt{\frac{\hat{p}\hat{q}}{n}}, \ \hat{p}+z_{\alpha/2}\cdot\sqrt{\frac{\hat{p}\hat{q}}{n}}\right)$$
Large sample validity condition: $n\hat{p} > 10$ and $n\hat{q} > 10$.

**Example 7.8 (source, slide 22)**
48 ignition trials, 16 resulted in ignition, $\hat{p} = 16/48 = .333$. An adjusted CI with confidence level approximately 95% (the formula the source text builds here) is
$$\frac{.333 + (1.96)^2/96 \pm 1.96\sqrt{(.333)(.667)/48 + (1.96)^2/9216}}{1+(1.96)^2/48} = \frac{.373 \pm .139}{1.08} = (.217, .474)$$
The traditional interval (the Proposition above) on the same data is
$$.333 \pm 1.96\sqrt{(.333)(.667)/48} = .333 \pm .133 = (.200, .466)$$
The two intervals would agree much more closely with a substantially larger sample size.

> [!note] Which formula this course uses (added)
> Example 7.9 below builds on the adjusted CI formula introduced in Example 7.8, not the traditional Proposition formula, and its width of .257 matches that adjusted interval. Per the lecturer, STA01B1's own sample size problems use the **traditional** formula, not this adjusted one. Recognise both if seen in the textbook, but default to the traditional formula for this course's calculations unless told otherwise.

**Example 7.9 (source, slide 23)**
Following on from 7.8's adjusted interval (width .257), the $n$ necessary for a width of .10 irrespective of the value of $p$:
$$n = \frac{2(1.96)^2(.25)-(1.96)^2(.01)\pm\sqrt{4(1.96)^4(.25)(.25-.01)+(.01)(1.96)^4}}{.01} = 380.3$$

> [!note] Why $\hat{p} = 0.5$ for sample size planning (struggle)
> When no prior estimate of $p$ exists, $\hat{p}(1-\hat{p})$ is used in the sample size formula, and this product is maximised exactly at $p = 0.5$ (it is a downward parabola in $p$, peaking at the midpoint). Plugging in $\hat{p}=0.5$ therefore produces the *largest possible* required $n$ for the target error, which is precisely what "irrespective of the value of $p$" calls for: whatever the true $p$ turns out to be, a sample size computed this way is guaranteed to be large enough, since no other value of $p$ could have demanded more.

**Worked example (composite): sample size for a poll**
A pollster wants an estimate accurate to within 3 percentage points at 95% confidence, with no prior estimate of $p$. $E = 0.03$ (already converted from "3 percentage points" to a proportion, watch this conversion), $z_{\alpha/2} = 1.96$, $\hat{p} = 0.5$ since no prior estimate is given and the bound must hold irrespective of $p$.
$$n = \frac{z_{\alpha/2}^2\,\hat{p}\hat{q}}{E^2} = \frac{(1.96)^2(.5)(.5)}{(.03)^2} = 1067.1 \implies n = 1068$$
COVERS: applies the question dissection skill below to the traditional-formula case.

> [!note] Question dissection skill for sample size problems (added)
> 1. Identify what is being solved for (usually $n$).
> 2. Extract the error of estimation $E$. Watch "within" (this value already is $E$) versus "width" (the stated width is $2E$, so divide by 2 first), a frequent off-by-a-factor-of-2 trap.
> 3. Convert the stated confidence level to $z_{\alpha/2}$.
> 4. Identify the spread estimate: a given $\sigma$ or $\hat{p}$ directly; the range rule of thumb when estimating $\sigma$ with no data yet; or $\hat{p} = 0.5$ when no prior proportion estimate exists and the problem asks for a bound irrespective of $p$.

## One sided confidence intervals

Placing all the error in a single tail uses $z_\alpha$, not $z_{\alpha/2}$, since only one tail carries the $\alpha$ area.

### Proposition, $\mu$
$$\text{Upper bound: } \mu < \bar{x}+z_\alpha\cdot\frac{s}{\sqrt{n}} \qquad \text{Lower bound: } \mu > \bar{x}-z_\alpha\cdot\frac{s}{\sqrt{n}}$$

### Proposition, $p$
$$\text{Upper bound: } p < \hat{p}+z_\alpha\cdot\sqrt{\frac{\hat{p}\hat{q}}{n}} \qquad \text{Lower bound: } p > \hat{p}-z_\alpha\cdot\sqrt{\frac{\hat{p}\hat{q}}{n}}$$

N.B a one sided bound is tighter than the corresponding side of a two sided interval at the same confidence level, because all of $\alpha$'s allowance sits in the one tail being bounded, instead of being split across two.

**Example 7.10 (source, slide 26)**
Algebra score data again, $\bar{x} = 19.82$, $s = 4.50$, $n = 50$. Lower confidence bound for $\mu$ at 95% confidence:
$$19.82 - (1.645)\cdot\frac{4.50}{\sqrt{50}} = 19.82 - 1.05 = 18.77$$
So, with 95% confidence, $\mu$ lies in $(18.77, \infty)$. This lower bound (18.77) sits above the lower bound of the two-sided interval from Example 7.6 (18.6), exactly the tightening described above.

## Do not forget

- A confidence interval is built around $\bar{x}$ or $\hat{p}$; the confidence level describes the long run success rate of the *method*, not a probability about one already-computed interval.
- $z_{\alpha/2}$ is read off the table at cumulative area $1-\alpha/2$, never at $1-\alpha$ or $\alpha$ directly.
- Large sample CI for $\mu$ with unknown $\sigma$ needs $n > 40$, stricter than the CLT's $n \ge 30$, because $S$ replacing $\sigma$ adds extra variability.
- Range rule of thumb estimates the population spread before data exists; it is not the CLT and answers a different question.
- $\hat{p} = 0.5$ for proportion sample size planning is the conservative, worst-case choice, not an assumption about the true $p$.
- "Within" gives $E$ directly; "width" is $2E$, divide first.
- One sided bounds use $z_\alpha$ and are tighter than the matching side of a two sided interval at the same confidence level.
- This course's own sample size calculations for $p$ use the traditional CI formula, not the adjusted formula from Example 7.8/7.9.

## See also
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] — sampling distribution of $\bar{X}$, and the CLT rule of thumb this chapter's $n>40$ threshold builds on.
- [[STA01B1_Notes_S2_Point_Estimation]] — standard error, the building block for every interval in this note.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] — the same $z_{\alpha/2}$ and $z_\alpha$ critical values reappear there as rejection-region boundaries rather than interval limits, and its large-sample Case II reuses the $S$-for-$\sigma$ substitution introduced here.
