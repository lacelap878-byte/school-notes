---
module: STA01A1
topic: Describing Data
session: S1
tags: [definition, formula, worked-example, added]
---

# STA01A1 Notes S1: Describing Data

Source: Lecture 1 (27 slides) and Lecture 2 (33 slides), slide numbers as printed; textbook Chapter 1. These are short revision notes written from the slides, not from a teaching session.

Scope: SA1 (23 March 2026) covered all of this. The final (13 June 2026) took only the definitions of the mean and the variance from Chapter 1.

Checked: every number below was recomputed in Python on 15 Nov 2026.

## Population, sample and variables (source, Lecture 1 slides 3 to 4, Lecture 2 slide 2)

> - A **population** is a set of all measurements of interest
> - A **sample** is a subset of a population that is obtained through some process (sampling), for the purposes of investigating the properties of the underlying population.
> - A **parameter** is a numerical descriptive measure calculated for a population
> - A **statistic** is a numerical descriptive measure calculated for a sample
> - A **variable** is any attribute or characteristic (such as age, weight, length, etc.) of an object being investigated and that is considered to be capable of varying from one object to another in the population
> - The object or individual on which a variable is measured, is an **experimental unit** (case)

- Data: Latin for "those that are given", the actual values observed.
- Descriptive statistics: collecting, organising, presenting and analysing data. Inferential statistics: drawing conclusions about a population from a sample.
- Probability reasons from the population to a sample. Statistical inference reasons from a sample back to the population.

## Probability sampling methods (source, Lecture 1 slides 9 to 14)

Members are chosen from the target population purely by chance.

| Method | How it works | Use it when |
|---|---|---|
| Simple random | each possible sample of size $n$ has an equal probability of being selected | no special structure |
| Stratified | split into homogeneous strata, take a simple random sample from each in proportion to its size | the population is heterogeneous |
| Cluster | take a simple random sample of clusters, then random samples of units inside each chosen cluster | the population is large and spread out, with natural clusters that are alike |
| Systematic | pick the first unit at random from a sampling frame, then every $k$th unit after it | a list or database exists |

Example (source, Lecture 1 slide 14): a systematic sample of $n = 500$ from $N = 15\,000$.
   $k = N/n = 30$. Start at a random unit from 1 to 30 (the slide uses 2), then take units 32, 62, and so on.

## Types of variable (source, Lecture 1 slides 15 to 17)

> - A **categorical** variable divides the cases into groups, placing each case into exactly one of two or more categories
> - A **quantitative** variable measures or records a numerical quantity for each case.

- Quantitative data is either counted (traffic offences, cars at a tollgate) or measured (weight, reaction time).

## Frequency tables and histograms (source, Lecture 1 slides 19 to 26)

- Relative frequency $=$ frequency $/\, n$. Example: 6 blue sweets out of 25 gives $6/25 = 0.24$.
- Building a histogram for measurement data:
  1. Divide the range into 5 to 20 subintervals of equal length.
  2. Approximate width $=$ range $/$ number of subintervals.
  3. Round the width up to a convenient value.
  4. Left inclusion: each class holds its left endpoint but not its right, so $[20 ; 30)$ holds 20 but not 30.
  5. Tabulate the classes with frequencies and relative frequencies.
- Shapes: symmetric, bimodal (two peaks), skewed left (long left tail), skewed right (long right tail).

Example (source, Lecture 1 slides 21 to 26)
Ages of 50 UJ lecturers run from 26 to 70. Build a 6-class frequency table, describe the shape, and find the proportion younger than 40.

WORKING
Range $= 70 - 26 = 44$, width $= 44/6 = 7.33$, rounded up to 10, start at 20.

| Age | $[20;30)$ | $[30;40)$ | $[40;50)$ | $[50;60)$ | $[60;70)$ | $[70;80)$ |
|---|---|---|---|---|---|---|
| Frequency | 2 | 16 | 15 | 12 | 4 | 1 |

Skewed right, no outliers. Younger than 40: $(2 + 16)/50 = 0.36$.

## Mean (source, Lecture 2 slides 4 to 5)

> **Definition:** The sample mean of observations $x_1, x_2, x_3, \dots, x_n$ is given by:

$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n}$$

$x_i$ is the $i$th observation and $n$ is the sample size. The population mean is $\mu$.

- Advantage: uses all the data values. Disadvantages: only valid for numeric variables, distorted by outliers.

## Median (source, Lecture 2 slides 7 to 10)

> **Definition:** The middle value when the observations are ordered from smallest to largest, denoted by $\tilde{x}$. The median of observations $x_1, x_2, \dots, x_n$ is given by

$$\tilde{x} = \begin{cases} \left(\dfrac{n+1}{2}\right)^{\text{th}} \text{ ordered value} & \text{when } n \text{ is odd} \\[2ex] \dfrac{\left(\frac{n}{2}\right)^{\text{th}} + \left(\frac{n}{2}+1\right)^{\text{th}} \text{ ordered values}}{2} & \text{when } n \text{ is even} \end{cases}$$

- Advantage: not influenced by outliers. Disadvantage: only appropriate for numeric data.
- If the distribution is skewed, mean $\ne$ median, and you must decide which one is of interest.
- When each is best used (added, from the advantages above): the mean for roughly symmetric data without outliers; the median for skewed data or data with outliers. A right skew pulls the mean above the median (lecturers' ages: mean 44.9, median 43).

Example (source, Lecture 2 slide 9)
Find the mean and median heart rate (beats per minute) of each group. 19-year-olds: 108, 68, 80, 83, 72. 55-year-olds: 86, 86, 92, 100, 112, 116, 136, 140.

WORKING
19-year-olds: $\bar{x} = 411/5 = 82.2$; ordered 68, 72, **80**, 83, 108, so $\tilde{x} = 80$.
55-year-olds: $\bar{x} = 868/8 = 108.5$; $n$ even, so $\tilde{x} = (100 + 112)/2 = 106$.

## Quartiles, order statistics and the trimmed mean (source, Lecture 2 slides 11 to 16)

- Quartiles split the ordered data into four equal parts; the second quartile is the median. The 99th percentile separates the highest 1% from the bottom 99%.

> Consider a data set consisting of $n$ distinct observations $x_1, x_2, \dots, x_n$. Let $x_{(1)}, x_{(2)}, \dots, x_{(n)}$ denote the data set in ascending order, i.e. $x_{(1)} < x_{(2)} < \dots < x_{(n)}$. We refer to $x_{(1)}, x_{(2)}, \dots, x_{(n)}$ as the **order statistics** of the data set.

The trimmed mean leaves out the first $k$ and the last $(n - l)$ order statistics:

$$\bar{x}_{[k,l]} = \frac{1}{l-k}\sum_{j=k+1}^{l} x_{(j)} \qquad 1 \le k < l \le n$$

$x_{(j)}$ is the $j$th smallest value; $l - k$ is the number of values kept.

- It is robust (not unduly affected by outliers). Judges' scores in diving drop the extremes in the same way.

Example (composite, data from slide 14): trim 10, 18, 15, 13, 16 with $k = 1$, $l = 4$.
   Ordered 10, 13, 15, 16, 18, so $\bar{x}_{[1,4]} = (13 + 15 + 16)/3 = 14.67$.

## Range, IQR and variance (source, Lecture 2 slides 18 to 24)

- Range: $R = x_{(n)} - x_{(1)}$, adequate for small data sets.
- Interquartile range: $IQR = Q_3 - Q_1$, where $Q_3$ is the median of the upper half and $Q_1$ the median of the lower half.

Population variance:

$$\sigma^2 = \frac{\sum_{i=1}^{N}(x_i - \mu)^2}{N}$$

$N$ is the population size and $\mu$ the population mean.

Sample variance:

$$s^2 = \frac{\sum_{i=1}^{n}(x_i - \bar{x})^2}{n-1} = \frac{S_{xx}}{n-1}$$

Computing formula:

$$s^2 = \frac{\sum_{i=1}^{n} x_i^2 - \frac{\left(\sum_{i=1}^{n} x_i\right)^2}{n}}{n-1}$$

$S_{xx}$ is the sum of squared deviations from $\bar{x}$. Standard deviation: $s = \sqrt{s^2}$.

- Reading it: a larger $s$ means the values sit further from the mean, on average. $s$ is in the data's units; $s^2$ is in squared units.
- For bell-shaped data, about 68.3%, 95.5% and 99.7% of values lie within 1, 2 and 3 standard deviations of the mean (slide 24).

Example (composite, 19-year-old heart rates from slide 9)
Find $s^2$ and $s$ for 108, 68, 80, 83, 72.

WORKING
$\sum x_i = 411$, $\sum x_i^2 = 34\,761$, $S_{xx} = 34\,761 - 411^2/5 = 976.8$.
$s^2 = 976.8/4 = 244.2$, $s = 15.63$ beats per minute.

> **Proposition:** Let $x_1, x_2, \dots, x_n$ be a sample and $c$ be a constant
> 1. If $y_1 = x_1 + c,\ y_2 = x_2 + c, \dots, y_n = x_n + c$ then $s_y^2 = s_x^2$
> 2. If $y_1 = cx_1,\ y_2 = cx_2, \dots, y_n = cx_n$ then $s_y^2 = c^2 s_x^2$

Proof idea (added; the slide marks this PROOF!):
1. $\bar{y} = \bar{x} + c$, so $y_i - \bar{y} = x_i - \bar{x}$ and the squared deviations are unchanged.
2. $\bar{y} = c\bar{x}$, so $y_i - \bar{y} = c(x_i - \bar{x})$ and every squared deviation gains a factor $c^2$.

## Boxplots and outliers (source, Lecture 2 slides 25 to 31)

> **Definition:**
> - The lower fourth is the median of the smallest half
> - The upper fourth is the median of the largest half
> - The fourth spread $f_s$ is given by $f_s = \text{upper fourth} - \text{lower fourth}$

- Five-number summary: Min, lower fourth, median, upper fourth, Max.
- (added) When $n$ is odd, the usual textbook convention puts the median in both halves. The slides do not say, so check Chapter 1 before relying on it.

> **Definition:** Any observation farther than $1.5f_s$ from the closest fourth is an outlier. An outlier is extreme if it is more than $3f_s$ from the nearest fourth, and it is mild otherwise.

Reading a boxplot:
- median in the centre of the box, whiskers of equal length: symmetric
- median left of centre, long right whisker: skewed right
- median right of centre, long left whisker: skewed left
- Comparative boxplots put one boxplot per group, on the same variable, side by side to compare centre, spread and shape.

Example (composite, 55-year-old heart rates from slide 9)
Give the five-number summary of 86, 86, 92, 100, 112, 116, 136, 140 and check for outliers.

WORKING
Lower half 86, 86, 92, 100, so lower fourth $= 89$. Upper half 112, 116, 136, 140, so upper fourth $= 126$.
$f_s = 126 - 89 = 37$, $1.5f_s = 55.5$. Outliers would lie below $89 - 55.5 = 33.5$ or above $126 + 55.5 = 181.5$: none.
Five-number summary: 86, 89, 106, 126, 140.

## Do not forget

- Sample variance divides by $n - 1$; population variance divides by $N$.
- Outliers and skew pull the mean; the median and the trimmed mean resist them.
- Outlier: more than $1.5f_s$ beyond the nearest fourth; extreme beyond $3f_s$.
- Histogram classes use left inclusion: $[20 ; 30)$ holds 20, not 30.

---
*CDG v13 | written S1 | 2026-11-15*
