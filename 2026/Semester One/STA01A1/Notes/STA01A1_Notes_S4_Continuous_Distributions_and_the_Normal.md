---
module: STA01A1
topic: Continuous Distributions and the Normal
session: S4
tags: [definition, formula, worked-example, common-mistake, added]
---

# STA01A1 Notes S4: Continuous Distributions and the Normal

Source: Lecture 9 (20 slides) and Lecture 10 (28 slides), slide numbers as printed; textbook Chapter 4 (sections 4.1 to 4.3). Short revision notes written from the slides, not from a teaching session.

Scope: SA2 (18 May 2026) covered pdfs, the uniform, the normal and normal percentiles. The final (13 June 2026) took pdfs, the normal (write its pdf for the question given) and normal percentiles. All integration in Chapter 4, and sections 4.4 to 4.6, were left out.

Checked: every probability below was recomputed in Python from $\Phi$, rounded to 4 decimals as in Table A.3, on 15 Nov 2026.

## From histograms to a density curve (source, Lecture 9 slides 2 to 5)

- A continuous rv has $P(X = c) = 0$ for every $c$ (defined in: [[STA01A1_Notes_S3_Discrete_Random_Variables#Random variables (source, Lecture 6 slides 2 to 6)|Random variables]]).
- Lake depth measured to the nearest metre, then centimetre, then finer: the probability histograms (total area 1) approach a smooth curve, also with area 1. The probability of a depth between $a$ and $b$ is the area under that curve between $a$ and $b$.

## The pdf (source, Lecture 9 slides 6 to 12)

> **Definition:** Let $X$ be a continuous rv. Then a probability distribution or probability density function (pdf) of $X$ is a function $f(x)$ such that for any two numbers $a$ and $b$ with $a \le b$, the probability that $X$ takes on a value in the interval $[a, b]$ is the area above this interval and under the graph of the density function. The graph of $f(x)$ is often referred to as the density curve.

For $f(x)$ to be a legitimate pdf, it must satisfy the following 2 conditions:
> 1. $f(x) \ge 0$ for all $x$
> 2. The area under the entire graph of $f(x)$ must equal 1

Because $P(X = c) = 0$, endpoints do not matter:

$$P(a \le X \le b) = P(a < X < b) = P(a \le X < b) = P(a < X \le b)$$

- A pmf puts "blobs" of probability at points; a pdf spreads it continuously along an interval.

> [!warning] A density is not a probability (added)
> $f(x)$ is a height, not a chance. Probability is area, so a single point always has probability 0.

## The uniform distribution (source, Lecture 9 slides 9 to 10)

> **Definition:** A continuous rv $X$ is said to have a uniform distribution on the interval $[A, B]$ if the pdf of $X$ is:

$$f(x; A, B) = \begin{cases} \dfrac{1}{B - A} & A \le x \le B \\[1ex] 0 & \text{otherwise} \end{cases}$$

Example (source, Lecture 9 slide 9, Example 4.4): $f(x) = \frac{1}{360}$ for $0 \le x < 360$, 0 otherwise. Check it is a pdf and find $P(90 \le X \le 180)$.
   $f(x) \ge 0$ and the area is a rectangle $360 \times \frac{1}{360} = 1$. $P(90 \le X \le 180) = 90 \times \frac{1}{360} = 0.25$.

## The cdf and percentiles (source, Lecture 9 slides 14 to 18)

- The cdf $F(x)$ is the area under the density curve to the left of $x$ (found by integrating the pdf from $-\infty$ to $x$; integration was not examined in 2026).

> **Proposition:** Let $X$ be a continuous rv with pdf $f(x)$ and cdf $F(x)$. Then for any number $a$, $P(X > a) = 1 - F(a)$, and for any two numbers $a$ and $b$ with $a < b$, $P(a \le X \le b) = F(b) - F(a)$

> **Proposition:** If $X$ is a continuous rv with pdf $f(x)$ and cdf $F(x)$, then at every $x$ at which the derivative $F'(x)$ exists, $F'(x) = f(x)$

> **Definition:** Let $p$ be a number between 0 and 1. The $(100p)$th percentile of the distribution of a continuous rv $X$, denoted by $\eta(p)$, is that value on the measurement axis such that $100p\%$ of the area under the graph of $f(x)$ lies to the left of $\eta(p)$ and $100(1 - p)\%$ lies to the right.

> **Definition:** The median of a continuous distribution, denoted by $\tilde{\mu}$, is the 50th percentile. That is, half the area under the density curve is to the left of $\tilde{\mu}$ and half is to the right of $\tilde{\mu}$.

## The normal distribution (source, Lecture 10 slides 2 to 8)

> **Definition:** Let $X$ be a continuous rv. $X$ is said to have a normal distribution with parameters $\mu$ and $\sigma$ if the pdf of $X$ is:

$$f(x; \mu, \sigma) = \frac{1}{\sigma\sqrt{2\pi}}\, e^{-\frac{1}{2}\left(\frac{x - \mu}{\sigma}\right)^2} \qquad \text{for } -\infty < x < \infty$$

$\mu$ is the mean, $\sigma$ the standard deviation, $e = 2.7183$ and $\pi = 3.1416$.

- Bell shaped and symmetric about the mean, which is also the median. A larger $\sigma$ gives a wider, flatter curve.
- Heights, measurement errors, test scores and many other populations fit a normal curve well. Sums and averages are often roughly normal even when single values are not (Central Limit Theorem, Chapter 6).

## The standard normal (source, Lecture 10 slides 9 to 17)

> **Definition:** The normal distribution with parameter values $\mu = 0$ and $\sigma = 1$ is called the standard normal distribution. A random variable that has a standard normal distribution is called a standard normal random variable and will be denoted by $Z$. The pdf of $Z$ is

$$f(z; 0, 1) = \frac{1}{\sqrt{2\pi}}\, e^{-\frac{z^2}{2}} \qquad \text{for } -\infty < z < \infty$$

> The cdf of $Z$ is $P(Z \le z)$, which we will denote by $\Phi(z)$.

- Table A.3 gives $\Phi(z)$, the area to the left of $z$. Example: $P(Z \le -2.85) = 0.0022$.

> $z_\alpha$ will denote the value on the measurement axis for which $\alpha$ of the area under the $z$ curve lies to the right of $z_\alpha$

- So $z_\alpha$ is the $100(1 - \alpha)$th percentile, and by symmetry the area left of $-z_\alpha$ is also $\alpha$. The $z_\alpha$ are called $z$ critical values. Example: $z_{.05} = 1.645$, the 95th percentile.

Example (source, Lecture 10 slide 13, Example 4.13)
Find (a) $P(Z \le 1.25)$, (b) $P(Z > 1.25)$, (c) $P(Z \le -1.25)$, (d) $P(-.38 \le Z \le 1.25)$.

WORKING
(a) $\Phi(1.25) = .8944$. (b) $1 - .8944 = .1056$. (c) $\Phi(-1.25) = .1056$, the same by symmetry. (d) $\Phi(1.25) - \Phi(-.38) = .8944 - .3520 = .5424$.

## Nonstandard normal distributions (source, Lecture 10 slides 18 to 23)

> **Proposition:** If $X$ has a normal distribution with mean $\mu$ and standard deviation $\sigma$, then

$$Z = \frac{X - \mu}{\sigma}$$

> has a standard normal distribution. Thus:

$$P(a \le X \le b) = P\left(\frac{a - \mu}{\sigma} \le Z \le \frac{b - \mu}{\sigma}\right) = \Phi\left(\frac{b - \mu}{\sigma}\right) - \Phi\left(\frac{a - \mu}{\sigma}\right)$$

$$P(X \le a) = \Phi\left(\frac{a - \mu}{\sigma}\right) \qquad P(X \ge b) = 1 - \Phi\left(\frac{b - \mu}{\sigma}\right)$$

$z$ is the standard score: how many standard deviations $x$ lies from the mean.

Empirical rule: if a population is (approximately) normal, roughly 68%, 95% and 99.7% of values are within 1, 2 and 3 SD of the mean. Exactly: $.6826$, $.9544$, $.9974$.

> **Proposition:**

$$(100p)^{\text{th}} \text{ percentile for normal}(\mu, \sigma) = \mu + \left[(100p)^{\text{th}} \text{ percentile for standard normal}\right] \times \sigma$$

Example (source, Lecture 10 slide 19, Example 4.16)
Reaction time $X$ is normal with $\mu = 1.25$ s and $\sigma = 0.46$ s. Write the pdf of $X$, then find $P(1.00 \le X \le 1.75)$.

WORKING
$f(x; 1.25, 0.46) = \dfrac{1}{0.46\sqrt{2\pi}}\, e^{-\frac{1}{2}\left(\frac{x - 1.25}{0.46}\right)^2}$ for $-\infty < x < \infty$.
$P\left(\frac{1.00 - 1.25}{.46} \le Z \le \frac{1.75 - 1.25}{.46}\right) = \Phi(1.09) - \Phi(-.54) = .8621 - .2946 = .5675$.

Example (source, Lecture 10 slide 23, Example 4.18)
A machine dispenses $X$ ml, normal with $\mu = 1893$ and $\sigma = 23.07$. What container size $c$ overflows only 0.5% of the time?

WORKING
$c$ is the 99.5th percentile. $\Phi(2.58) = .9951$ is the table value closest to .995, so $c = 1893 + 2.58(23.07) = 1952.5$ ml.

## Normal approximation to the binomial (source, Lecture 10 slides 24 to 27)

> **Proposition:** Let $X$ be a binomial rv based on $n$ trials with success probability $p$. Then if the binomial probability histogram is not too skewed, $X$ has approximately a normal distribution with $\mu = np$ and $\sigma = \sqrt{npq}$

$$P(X \le x) = B(x; n, p) \approx \Phi\left(\frac{x + 0.5 - np}{\sqrt{npq}}\right)$$

$q = 1 - p$. The $+0.5$ is the continuity correction. In practice the approximation is adequate provided both $np \ge 10$ and $nq \ge 10$.

Example (source, Lecture 10 slide 27, Example 4.20)
25% of drivers are uninsured; $X$ counts uninsured drivers in a sample of 50. Approximate $P(X \le 10)$ and $P(5 \le X \le 15)$.

WORKING
$np = 12.5 \ge 10$, $nq = 37.5 \ge 10$; $\sigma = \sqrt{50(.25)(.75)} = 3.06$.
$P(X \le 10) \approx \Phi\left(\frac{10.5 - 12.5}{3.06}\right) = \Phi(-.65) = .2578$.
$P(5 \le X \le 15) = B(15) - B(4) \approx \Phi\left(\frac{15.5 - 12.5}{3.06}\right) - \Phi\left(\frac{4.5 - 12.5}{3.06}\right) = .8365 - .0045 = .8320$.

> *I checked the exact binomial answers in Python: .2622 and .8348, so the approximation is close but not exact.*

## Do not forget

- Continuous: $P(X = c) = 0$, so $<$ and $\le$ give the same probability.
- Standardise first: $z = (x - \mu)/\sigma$, then read $\Phi(z)$, the area to the left.
- $z_\alpha$ has area $\alpha$ to its right, so it is the $100(1 - \alpha)$th percentile.
- Normal approximation: check $np \ge 10$ and $nq \ge 10$, and add 0.5 for $P(X \le x)$.

## See also

- [[STA01A1_Notes_S1_Describing_Data]]
- [[STA01A1_Notes_S2_Probability]]
- [[STA01A1_Notes_S3_Discrete_Random_Variables]]

---
*CDG v13 | written S4 | 2026-11-15*
