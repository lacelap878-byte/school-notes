---
module: STA01B1
topic: Chi-Square Tests
session: S10
tags: [definition, formula, worked-example, common-mistake, exam-flagged, struggle, added]
---

# STA01B1 Notes S10: Chi-Square Tests

Source: Lecture 11.pdf, 22 slides numbered as printed (slide 1 is the title card, Chapter 14, and slide 22 is a closing reference to Chapter 14, sections 14.1 and 14.3, so content runs from slide 2 to slide 21). Extra examples come from Tutorial 11 and Solution 11. The deck carries the date stamp 9/27/2021 on every page, so it is an older deck (see: Where the source is inconsistent).

Labels used: `(source, slide N)`, `(source: Solution 11)`, `(composite)` for an example built here, `(added)` for anything beyond the slides.

How this session ran: the lecture was new to the student, who had no notebook pages left, so there were no copy-ready parts. The session was a slow question session, one idea at a time, with the explanations below built from the student's own questions. This file is for reading and revision, not for copying.

Colour key used here: <span style="color:#2f9e44">green</span> is the right version, <span style="color:#e03131">red</span> is the wrong version, <span style="color:#f08c00">orange</span> is an open struggle item.

## Why a new kind of test (source, slides 2 to 4)

Everything before this lecture used a measurement on each person (a mark, a weight, a growth in cm) and tested a mean. Chi-square is for data that are only labels: people sorted by ethnic origin, cars by colour, defects by type. What we then have is a count in each category.

The source calls such an experiment a multinomial experiment (slide 3). Its five conditions, as on the slide:

1. The experiment consists of $n$ identical trials.
2. Each trial results in one of $k$ categories.
3. The probability that the outcome falls into a particular category $i$ on a single trial is $p_i$ and remains constant from trial to trial. The sum of all $k$ probabilities is $p_1 + p_2 + \dots + p_k = 1$.
4. The trials are independent.
5. We are interested in the number of outcomes in each category, $N_1, N_2, \dots, N_k$, with $N_1 + N_2 + \dots + N_k = n$.

A binomial experiment is the special case $k = 2$ (slide 4): the two categories are success and failure, with chances $p$ and $q$ and counts $x$ and $n - x$. Until now we made inferences about one $p$. Here we make inferences about all of $p_1, p_2, \dots, p_k$ at once.

## The expected count (source, slide 5, with added explanation)

The test starts from a claim about the chances, the null hypothesis:

$$H_0: p_1 = p_{10},\ p_2 = p_{20},\ \dots,\ p_k = p_{k0}$$

$p_i$ is the true chance of category $i$ and $p_{i0}$ is the value the claim gives it.

If the claim is true, the number of times category $i$ should turn up in $n$ trials is its expected count:

$$E_i = n\,p_{i0}$$

$n$ is the number of trials and $p_{i0}$ is the chance of category $i$ under $H_0$.

The expected count always comes from the claim in $H_0$, never from the data. It is a target, not a prediction that the count will land on it. A fair die rolled 60 times has $E_i = 60 \cdot \tfrac{1}{6} = 10$ for each face, and a count of 8 or 12 is perfectly ordinary.

What the claim in $H_0$ says decides the expected counts. Two examples:

| Claim in $H_0$ | Chances | $E$ for $n = 40$ or $n = 120$ |
|---|---|---|
| Four opinions equally likely ($n = 40$) | $\tfrac{1}{4}$ each | 10 each |
| A tutoring centre expects 40%, 30%, 20% and 10% ($n = 120$, Tutorial 11) | .40, .30, .20, .10 | 48, 36, 24, 12 |

> [!note] The expected count is not the expected value of one roll
> The expected value of the number on a single fair die roll is 3.5. That is a different quantity. Chi-square never looks at the face values or their average. The faces are only labels, like "very favourable" or "engineering", and the expected count is how many times each label should come up in $n$ trials.

## Pearson's chi-square statistic (source, slides 6 and 7)

The statistic that measures how far the observed counts $O_i$ are from the expected counts $E_i$:

$$\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$$

$O_i$ is the observed count in category $i$, $E_i$ is its expected count, and the sum runs over every category (or every cell, in a table).

When $H_0$ is true the differences $O - E$ are small. When $H_0$ is false some are large. So we look for large values of the statistic, based on the chi-square distribution with the right degrees of freedom (slide 6). The rejection region is always the upper tail: reject $H_0$ if $\chi^2 \ge \chi^2_{\alpha,\,df}$.

Reading it plainly: the score is a total of how far the real counts are from the targets. A small score means the counts are close to what the claim predicts. A large score is what makes the claim look doubtful.

Why each part is there (added):
- The gaps $O - E$ cannot be added as they are, because both lists add up to $n$ and the gaps always cancel to zero. Squaring makes every miss count as a positive amount.
- Dividing by $E$ makes each miss relative to its size. A miss of 4 matters when 10 were expected, and almost not at all when 1000 were.

Worked example (composite). A die is rolled 60 times and gives 6, 14, 9, 11, 8, 12 for faces 1 to 6. With $E = 10$ for every face:

| Face | $O$ | $E$ | $O - E$ | $(O-E)^2$ | $(O-E)^2/E$ |
|---|---|---|---|---|---|
| 1 | 6 | 10 | $-4$ | 16 | 1.6 |
| 2 | 14 | 10 | $4$ | 16 | 1.6 |
| 3 | 9 | 10 | $-1$ | 1 | 0.1 |
| 4 | 11 | 10 | $1$ | 1 | 0.1 |
| 5 | 8 | 10 | $-2$ | 4 | 0.4 |
| 6 | 12 | 10 | $2$ | 4 | 0.4 |

$$\chi^2 = 4.2$$

Checked by script (scipy): 4.2.

The "score" the student asked about is simply this number. In an exam it is called the test statistic, the same kind of thing as $z$ in the $z$ tests and $t$ in the $t$ tests.

## Where the formula comes from (added)

The student asked how this formula connects to reality and not just to arithmetic. The chain has four links.

Link 1: a count wobbles by about $\sqrt{E}$. One face's count is a binomial count, so by the CLT it is roughly normal around $E_i$ when $E_i$ is large enough (this is where the rule $E_i \ge 5$ comes from). Its typical wobble is about $\sqrt{E_i}$. For $E = 10$ that is about 3.2.

Link 2: the count has a z-score.

$$Z_i = \frac{O_i - E_i}{\sqrt{E_i}}$$

$Z_i$ says how many typical wobbles category $i$ is from its target. For face 1 of the die above, $Z = \dfrac{6 - 10}{\sqrt{10}} \approx -1.26$.

Link 3: squaring the z-score gives exactly the formula's term.

$$Z_i^2 = \frac{(O_i - E_i)^2}{E_i}$$

For face 1, $(-1.26)^2 \approx 1.6$, matching the table. So dividing by $E$ is not arbitrary: it is the square of the typical wobble.

Link 4: a sum of squared z-scores is a chi-square variable (met in [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population#Confidence interval for the variance|Confidence interval for the variance]]).

$$\chi^2 = \sum_{i=1}^{k} Z_i^2 \quad \text{with} \quad df = k - 1$$

$k$ is the number of categories. The degrees of freedom are $k - 1$ and not $k$ because the counts are tied together by the total $n$ (see: Degrees of freedom as unknowns minus equations).

The "wobble" step relies on the CLT from [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions#The Central Limit Theorem (exam-flagged)|The Central Limit Theorem]]. This is why the approximation is only good when the expected counts are large enough.

> *I said at one point that $E_i$ is the variance of a count. Exactly, the variance is $np_{i0}(1 - p_{i0})$, which is close to $E_i$ only when $p_{i0}$ is small. The shortfall is absorbed by the $k - 1$ degrees of freedom. The exam works with $\chi^2 = \sum \frac{(O-E)^2}{E}$ and $df = k - 1$ as given, so the exact variance is not needed.*

## What the score looks like for a fair and a loaded die (added)

To see the cut-off arise, the session ran an interactive demo of 5000 simulated experiments of 60 rolls each, scoring every experiment against the claim "the die is fair". The numbers shown on the student's screen were not reported back, so the figures below come from a rerun of the same experiment in script (200 000 experiments):

- With a fair die the scores bunch to the left, with an average of 5.0. The mean of a chi-square variable equals its degrees of freedom, and here $df = 5$.
- 4.8% of fair-die experiments scored above 11.07, close to the 5% that the table value for $df = 5$ promises.
- With a die loaded so that 6 comes up twice as often (the other faces equally likely), the whole pile slides to the right: the average becomes about 11.0 and 41% of experiments cross 11.07.

The chi-square curve for $df = 5$, with the 5% rejection region shaded and the die's score of 4.2 marked (graph untested in the student's vault; tell me if the block does not render):

```desmos-graph
left=0; right=22; bottom=-0.02; top=0.18;
---
y=\frac{x^{1.5}e^{-x/2}}{2^{2.5}\left(1.5\right)!}\left\{x>0\right\}
0\le y\le\frac{x^{1.5}e^{-x/2}}{2^{2.5}\left(1.5\right)!}\left\{11.07\le x\le22\right\}
x=4.2
x=11.07
```

Reading the graph: the area under the whole curve is 1. The shaded area to the right of 11.07 is 5%. A fair die lands there only about 1 time in 20. The score 4.2 sits well to the left of the shaded region, so it gives no reason to doubt the die.

Upper-tail areas checked by script (numerical integration and scipy): $df = 5$ beyond 11.07 is 0.05, $df = 3$ beyond 6.251 is 0.10, $df = 2$ beyond 5.991 is 0.05, $df = 1$ beyond 3.841 is 0.05, $df = 6$ beyond 18.5476 is 0.005.

## Degrees of freedom as unknowns minus equations

#struggle

(explanation from session, added) Degrees of freedom count how many numbers in a table can still vary independently once something has been fixed:

$$df = \text{(number of unknowns)} - \text{(number of independent equations linking them)}$$

The idea is plain algebra. The statistics comes in because the unknowns are random, and the number of free random pieces decides the shape of the distribution of the score, so it decides which row of the table to use.

| Situation | Unknowns | Equations linking them | $df$ |
|---|---|---|---|
| Die, 6 counts with total 60 | 6 | 1 (the counts add to 60) | 5 |
| 2 by 3 table with all totals known | 6 | 4 independent (2 row totals and 3 column totals, one of the five is redundant) | 2 |
| Sample deviations from the mean, $n$ values | $n$ | 1 (they add to 0) | $n - 1$ |
| Regression residuals, $n$ values | $n$ | 2 (they add to 0 and $x$ times them adds to 0) | $n - 2$ |

For a table with $I$ rows and $J$ columns, $IJ$ cells and $I + J - 1$ independent totals give:

$$df = IJ - (I + J - 1) = (I - 1)(J - 1)$$

$I$ is the number of rows and $J$ the number of columns. Checked by example: the 2 by 3 table with row totals 30 and 20 and column totals 10, 15 and 25 lets exactly two cells be chosen freely (4 and 9), and the other four follow (17, 6, 6, 8).

For goodness of fit the degrees of freedom count the categories, not the people: $df = k - 1$ whether $n$ is 40 or 40 000. The $t$ test habit $df = n - 1$ does not apply here.

<span style="color:#f08c00">Open: the "forced last count" picture. The student understood the algebra but kept hearing that the last roll or last cell is "forced", and this misreading came back each time df was explained that way. It was cleared in session, and the argument that did it is recorded below. It is kept open until the student explains df back in their own words in the next session.</span>

What was cleared, in order:
- The rolls are always free. No roll is ever predetermined. What is tied together is the finished summary table, because the counts must add to $n$.
- The tie holds at every stage, even after the first throw (the targets are recalculated from the number of throws so far). So it cannot be a sign that something is forced. A first roll is not forced either.
- After 59 rolls, whichever face the 60th roll shows, "total over equals total under" holds. A table with all six possible 60th rolls showed it. The zero total never predicts the next face.
- Which cell is called the last one is arbitrary: any five of the six could be the free ones.
- Knowing the total gives no betting advantage over an opponent. A fair die has no memory, and believing a face is "due" is the gambler's fallacy.
- The better wording is "new information": six counts hold 5 counts' worth of what happened plus 1 count's worth of bookkeeping. Nothing is forced; the sixth number is redundant once you know the total.

> [!note] Over and under
> Total under is the sum of all "under by" amounts and total over is the sum of all "over by" amounts, measured from each fair share. They are always equal, for the same reason that 60 sweets shared among 6 kids with a fair share of 10 each leave the over-share kids with exactly what the under-share kids are missing.

The degrees of freedom of the chi-square curve change its shape. The curves for $df = 2, 3, 5$ and $9$ (graph untested in the student's vault):

```desmos-graph
left=0; right=25; bottom=-0.02; top=0.52;
---
y=0.5e^{-x/2}\left\{x>0\right\}
y=\frac{x^{0.5}e^{-x/2}}{2^{1.5}\left(0.5\right)!}\left\{x>0\right\}
y=\frac{x^{1.5}e^{-x/2}}{2^{2.5}\left(1.5\right)!}\left\{x>0\right\}
y=\frac{x^{3.5}e^{-x/2}}{2^{4.5}\left(3.5\right)!}\left\{x>0\right\}
```

The curve with $df = 2$ starts highest and falls away. With larger $df$ the hump moves right and flattens, and its average equals $df$. This is why the cut-off grows with $df$ (5.99 for $df = 2$ and 11.07 for $df = 5$, both at 5%), and why using the wrong $df$ gives the wrong cut-off.

## The goodness of fit test (source, slides 7 to 9)

One categorical variable is measured, and exact numerical values are specified for each of the $p_i$ (slide 7). The textbook reference is Example 14.1, page 623.

- $H_0: p_1 = p_{10}, \dots, p_k = p_{k0}$ and $H_a$: at least one $p_i$ differs from the value in $H_0$.
- Expected cell counts $E_i = n\,p_{i0}$.
- Degrees of freedom $df = k - 1$.
- Test statistic $\chi^2 = \sum \dfrac{(O_i - E_i)^2}{E_i}$.
- Reject $H_0$ if $\chi^2 \ge \chi^2_{\alpha,\,k-1}$.

A note from the slides (slide 9): the chi-square test statistic has only an approximate chi-square distribution, and for the approximation to be accurate statisticians recommend $E_i \ge 5$ for all cells.

Example (source, slide 8; working added). 40 employees were asked how favourable they are to a proposal introducing flexible working hours. Test at the 10% level whether there is a difference in favourability.

| Very favourable | Somewhat favourable | Undecided | Very unfavourable |
|---|---|---|---|
| 16 | 10 | 6 | 8 |

Working:
- $n = 16 + 10 + 6 + 8 = 40$. The claim is that the four opinions are equally likely, so $p_{i0} = \tfrac{1}{4}$ and $E = 40 \cdot \tfrac{1}{4} = 10$ for each. All are at least 5.
- Contributions: 3.6, 0, 1.6, 0.4.

$$\chi^2 = 5.6 \qquad df = 4 - 1 = 3 \qquad \chi^2_{.10,3} = 6.251$$

- $5.6 < 6.251$, so we do not reject $H_0$.

Conclusion in plain words:

> At the 10% level there is not sufficient evidence that employees' feelings about the flexible working hours proposal differ. The counts are close enough to an even split that ordinary luck could explain them.

Checked by script (numpy and scipy): contributions 3.6, 0, 1.6, 0.4, total 5.6, cut-off 6.251.

Example (source: Solution 11, Tutorial 11 question 3). A tutoring centre expects 40%, 30%, 20% and 10% of clients to come from business, engineering, social science and agriculture statistics. A random sample of 120 clients gives 52, 38, 21 and 9. Test at 5% whether the expectations are wrong.

- $E = 120 \times (.40, .30, .20, .10) = 48, 36, 24, 12$, all at least 5.

$$\chi^2 = \frac{(52-48)^2}{48} + \frac{(38-36)^2}{36} + \frac{(21-24)^2}{24} + \frac{(9-12)^2}{12} = 1.57$$

- $df = 3$ and $\chi^2_{.05,3} = 7.815$. Since $1.57 < 7.815$ we do not reject $H_0$. There is no significant evidence that the department's expectations are incorrect. Checked by script: 1.57.

<span style="color:#f08c00">Open: expected counts from the claim in $H_0$. A question asking for the expected count of the 30% course (200 clients, claim 40%, 30%, 20%, 10%) was answered correctly as 60 but was a guess. The trap is 50, the equal split, which applies only when $H_0$ says all groups are equally likely.</span>

<span style="color:#f08c00">Open: degrees of freedom for goodness of fit. In the flexible working hours example the student wrote $df = 39$, which is $n - 1$ from the $t$ test. Right: $df = k - 1 = 3$, counting the groups and not the people.</span>

## Two-way tables and the test of independence (source, slides 10 to 17)

Two qualitative variables are measured on each unit, giving bivariate data (slide 10). Examples on the slide: gender and colour blindness, age and opinion, professorial rank and type of university. The counts are summarised in a contingency table with $I$ rows and $J$ columns, so $IJ$ cells (slide 11). The question is whether one method of classification is contingent on, or dependent on, the other. Does the distribution of the measurements across the categories of variable 1 depend on which category of variable 2 is being observed? If not, the variables are independent (slide 12).

- $H_0$: the classifications are independent. $H_a$: the classifications are dependent.
- Observed cell counts $O_{ij}$ for row $i$ and column $j$. Expected cell counts $E_{ij} = n p_{ij}$.
- If $H_0$ is true, $p_{ij} = p_i p_j = P(\text{row } i) \times P(\text{column } j)$ (slide 13).

Estimate $p_i$ and $p_j$ by $\dfrac{n_i}{n}$ and $\dfrac{n_j}{n}$ (slide 14):

$$\hat{E}_{ij} = n\left(\frac{n_i}{n}\right)\left(\frac{n_j}{n}\right) = \frac{n_i\,n_j}{n}$$

$n_i$ is the total of row $i$, $n_j$ is the total of column $j$ and $n$ is the grand total.

$$\chi^2 = \sum \frac{(O_{ij} - \hat{E}_{ij})^2}{\hat{E}_{ij}} \qquad df = (I - 1)(J - 1)$$

The statistic has an approximate chi-square distribution with these degrees of freedom (slide 14).

Why multiplying: independence is exactly what lets you multiply chances, like two coin flips giving $\tfrac{1}{2} \times \tfrac{1}{2} = \tfrac{1}{4}$ for two heads. Rebuilt step by step for the cell "rural, government" in the table below, with 114 rural men, 172 government workers and 250 men in all (added):

| Step | What it says | Number |
|---|---|---|
| 1 | Chance a man is rural | $\tfrac{114}{250} = 0.456$ |
| 2 | Chance a man works in government | $\tfrac{172}{250} = 0.688$ |
| 3 | If independent, chance of both: multiply | $0.456 \times 0.688 = 0.3137$ |
| 4 | Turn the chance into a number of men: multiply by $n$ | $250 \times 0.3137 = 78.4$ |

There are two multiplications for two reasons: the first turns "independent" into a chance for the cell, and the second turns the chance into a count, as in $E = n \times p$. They simplify to the row total times the column total over $n$. A useful check on any expected count: a cell is part of its row and its column, so $E$ can never exceed either total.

<span style="color:#f08c00">Open: expected count in a two-way table. In a quiz question (row total 40, column total 30, $n = 100$) the student answered 35, which is the average of the two totals, and the right answer is $40 \times 30 / 100 = 12$. A quick check that catches it: 35 is larger than the column total of 30, which no expected count can be. In the session the same step also produced 21.24 for $34 \times 63 / 100$ where the right value is 21.42, a swapped pair of digits.</span>

Example (source, slides 15 to 17). A total of $n = 309$ furniture defects were recorded and classified into four types, A, B, C or D, and by the production shift (1, 2 or 3) in which the piece was made. Do the data present sufficient evidence that the type of defect varies with the shift? (Textbook Example 14.14, page 645.)

| Type | Shift 1 | Shift 2 | Shift 3 | Total |
|---|---|---|---|---|
| A | 15 | 26 | 33 | 74 |
| B | 21 | 31 | 17 | 69 |
| C | 45 | 34 | 49 | 128 |
| D | 13 | 5 | 20 | 38 |
| Total | 94 | 96 | 119 | 309 |

Expected counts, from the slide (slide 16), matching an independent recomputation:

| Type | Shift 1 | Shift 2 | Shift 3 |
|---|---|---|---|
| A | 22.51 | 22.99 | 28.50 |
| B | 20.99 | 21.44 | 26.57 |
| C | 38.94 | 39.77 | 49.29 |
| D | 11.56 | 11.81 | 14.63 |

$$\chi^2 = \frac{(15 - 22.51)^2}{22.51} + \frac{(26 - 22.99)^2}{22.99} + \dots + \frac{(20 - 14.63)^2}{14.63} = 19.18$$

- $df = (r - 1)(c - 1) = (4 - 1)(3 - 1) = 6$ and $\chi^2_{.005} = 18.5476$. The statistic is greater, so the P-value is less than .005, the result is highly significant, and we reject $H_0$. There is sufficient evidence that the proportions of defect types vary from shift to shift (slide 16).
- Checked by script: expected counts as on the slide, $\chi^2 = 19.18$.

Slide 17 then compares the three columns as conditional proportions (each column sums to 1). In plain words: for each shift it shows what share of its defects were each type. Shifts 1 and 2 have the defect types in the same general order (C, B, A, D from most to least), though in different proportions. Shift 3 shows a different pattern: C again, then A, D and B. This is how you see where the dependence is, once the test has said that there is some.

Example (composite from a past paper: 2023 Paper A, question 7, which has no memo). 250 men are classified by place of birth and place of work. Test at 5% whether the two are independent.

| | Government | Private sector | Row total |
|---|---|---|---|
| Rural area | 80 | 34 | 114 |
| City | 92 | 44 | 136 |
| Column total | 172 | 78 | 250 |

Expected counts: rural and government 78.432, rural and private 35.568, city and government 93.568, city and private 42.432. All are at least 5.

$$\chi^2 = 0.0313 + 0.0691 + 0.0263 + 0.0579 = 0.1847$$

$df = (2 - 1)(2 - 1) = 1$ and $\chi^2_{.05,1} = 3.841$. Since $0.185 < 3.841$ we do not reject $H_0$.

> At the 5% level there is not sufficient evidence that where a man works depends on where he was born.

Checked by script: expected counts and $\chi^2 = 0.1847$.

Example (source: Solution 11, Tutorial 11 question 35). 100 faculty members are classified by rank and gender. Test at 5% for a relationship.

| | Male | Female | Row total |
|---|---|---|---|
| Professor | 25 | 9 | 34 |
| Associate professor | 20 | 8 | 28 |
| Assistant professor | 18 | 20 | 38 |
| Column total | 63 | 37 | 100 |

Expected counts: professor 21.42 and 12.58, associate 17.64 and 10.36, assistant 23.94 and 14.06.

$$\chi^2 = 6.454 \qquad df = (3-1)(2-1) = 2 \qquad \chi^2_{.05,2} = 5.991$$

$6.454 \ge 5.991$, so we reject $H_0$.

> At the 5% level there is sufficient evidence that a faculty member's rank is related to their gender. Women make up a bigger share of the assistant professors than of the professors.

Checked by script: 6.454. Part d of the tutorial question asks about implications for the future. The solution's reading is that the gender imbalance is less pronounced in the lower ranks, which suggests more women are being hired now than before, so in 10 to 15 years the imbalance among full professors should shrink if those staff stay.

Example (source: Solution 11, Tutorial 11 question 44). A table of 485 people by age group (five groups) and whether they "want" something or not (Want 127, 118, 77, 61, 41 against Don't 23, 23, 5, 2, 8). The solution gets $\chi^2 = 11.60 \ge \chi^2_{.05,4} = 9.488$, so independence is rejected at 5% but not at 1% (.01 < P-value < .025). A recomputation from the unrounded expected counts gives 11.65 and a P-value of about 0.020, which gives the same decisions (see: Where the source is inconsistent).

## The test of homogeneity (source, slides 18 and 19)

> [!note] Not examined, per lecturer (as reported), 2026-11-07
> Dr Hildebrand (Moodle, 7 Nov): the test of homogeneity is not in this year's textbook and not in her papers, so leave it out. She adds that it works exactly like the test of independence; the only difference is that the sample sizes for the categories of one variable were fixed in the design. Kept as reference only, do not drill.

Sometimes researchers design the experiment so that the number of units falling in one set of categories is fixed in advance. Example on the slides: an experimenter selects 900 patients who have been treated for flu prevention, 300 from each of three types: no vaccine, one shot, two shots. The column totals are fixed in advance.

| | No vaccine | One shot | Two shots | Row total |
|---|---|---|---|---|
| Flu | | | | $r_1$ |
| No flu | | | | $r_2$ |
| Total | 300 | 300 | 300 | $n = 900$ |

Each column whose total is fixed in advance is actually a single multinomial experiment, so this is a set of three binomial populations (no vaccine, one shot and two shots). The question becomes: is the probability of getting the flu independent of the type of flu prevention used? (Textbook Example 14.13, page 641.) The chi-square test of independence with $(r-1)(c-1)$ degrees of freedom is equivalent to a test of the equality of the $c$ (or $r$) multinomial populations. This is called the test of homogeneity.

In plain words (added): in a test of independence one sample is classified two ways, and the question is whether the two labels are linked. In a test of homogeneity separate samples are taken from separate groups, with their sizes fixed, and the question is whether the groups have the same proportions. The expected counts, the statistic and the degrees of freedom are calculated the same way for both. The slides give no numbers for this example.

## The assumptions (source, slides 20 and 21)

Assumptions for Pearson's chi-square, as on the slides:

1. The cell counts $O_1, O_2, \dots, O_k$ must satisfy the conditions of a multinomial experiment, or a set of multinomial experiments created by fixing either the row or the column totals.
2. The expected cell counts $E_1, E_2, \dots, E_k$ should equal or exceed five.

If one or more expected cell counts is less than five, the slides give two options:
1. Choose a larger sample size $n$: the larger the sample, the closer the chi-square distribution approximates the distribution of the test statistic.
2. It may be possible to combine one or more of the cells with small expected cell counts, thereby satisfying the assumption.

<span style="color:#f08c00">Open: the assumption is about the expected counts. In a quiz question (a 3 by 3 table with all observed counts at least 6 and one expected count of 3.2) the student answered that the test is invalid "because a 3 by 3 table has too many degrees of freedom". Right: the assumption fails because one expected count is below 5, however large the observed counts are. Degrees of freedom play no part in this rule; they only pick the row of the table.</span>

Why the rule exists: the chi-square curve is an approximation, in the same way that the CLT needs a large $n$. It works only when each expected count is large enough, which is why 10 rolls of a die (expected count 1.67 per face) are too few for this test.

## Choosing between ANOVA and chi-square (added)

Both compare groups, but they work on different data. The question to ask is what is recorded for each person:

| | ANOVA | Chi-square, two-way table |
|---|---|---|
| Data in the table | Measurements, such as plant growth in cm | Counts, such as how many people fall in each box |
| Groups | One grouping, like 3 fertilisers | Two classifications, like place of birth and place of work |
| What it compares | The mean measurement of each group | Whether the counts spread the same way across the boxes |
| $H_0$ | All group means are equal | The two classifications are independent |
| Statistic | $F = MSTr/MSE$ | $\chi^2 = \sum (O-E)^2/E$ |

A number measured on each person points to $t$ or ANOVA (see: [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure#Why ANOVA exists|Why ANOVA exists]]). Only labels point to chi-square. Three groups on their own do not make a problem ANOVA.

<span style="color:#f08c00">Open: choosing the test. In a quiz question 300 bank customers were each asked which of 3 branches they use and whether they are satisfied. The student chose "ANOVA, with df = 2 and 297". Right: each customer has two labels and no measurement, so the data are counts in a 3 by 2 table and the test is the chi-square test of independence with $df = (3-1)(2-1) = 2$.</span>

## How to write the answer (added)

The routine for any chi-square question, in the order the paper wants it:

1. Hypotheses: $H_0$ and $H_a$ in words, with $p_i$ or "independent" and "dependent".
2. Expected counts, with the check that every one is at least 5.
3. Test statistic $\chi^2 = \sum \frac{(O-E)^2}{E}$, shown in a table for goodness of fit or for two-way tables.
4. Degrees of freedom and the cut-off $\chi^2_{\alpha,\,df}$ from the table.
5. Decision: reject $H_0$ if $\chi^2 \ge$ cut-off, else do not reject.
6. Conclusion in plain words, with the level and the context.

The conclusion is the step that slipped. A test only ever rejects $H_0$ or fails to; it never rejects the alternative and never proves $H_0$.

- <span style="color:#2f9e44">Right:</span> "At the 10% level there is not sufficient evidence that employees' feelings about the proposal differ."
- <span style="color:#e03131">Wrong:</span> "At the 10 percent confidence level, the alternate hypothesis is rejected." This says it backwards, and 10% is a significance level, not a confidence level.
- <span style="color:#e03131">Wrong:</span> "The four opinions are equally likely" or "we accept $H_0$". Failing to reject shows only that the data were not strong enough to back $H_a$.

<span style="color:#f08c00">Open: conclusion wording after a non-rejection. The same slip appeared in the practical test preparation. A multiple choice question on this was answered correctly at the start of the session, but in a fresh written answer (chi-square 5.6 against a cut-off of 6.251) the student wrote "at 10 percent confidence level, the alternate hypothesis is rejected". The decision was right: 5.6 is below 6.251, so we do not reject $H_0$.</span>

## Proofs that may be asked (added)

#theorem #formula #exam-flagged

The student expects curveballs: the lecturer sets proofs that are not on the slides (in the past papers, proofs of unbiasedness and variance keep appearing). Two results from this lecture are written out here as proofs.

### Proof that the expected count is n_i n_j over n

The proof follows the order the lecturer used in class (as described by the student): start from the intersection of the two classifications, declare independence from the assumption, get $p_{ij}$, then substitute back into the expected value.

Setup. A unit falls in row $i$ (event $A_i$) and column $j$ (event $B_j$). Let $p_{ij} = P(A_i \cap B_j)$, $p_i = P(A_i)$ and $p_j = P(B_j)$. The count $O_{ij}$ in cell $(i, j)$ is the number of the $n$ units that land in that cell.

Step 1. Start from the intersection: the chance that a unit lands in cell $(i, j)$ is

$$p_{ij} = P(A_i \cap B_j)$$

Step 2. Under $H_0$ the classifications are independent, so the probability of the intersection is the product:

$$p_{ij} = P(A_i)\,P(B_j) = p_i\,p_j$$

Step 3. Each of the $n$ units lands in the cell with chance $p_{ij}$, independently, so $O_{ij}$ is binomial with parameters $n$ and $p_{ij}$ and its expected value is

$$E(O_{ij}) = n\,p_{ij}$$

Step 4. Substitute $p_{ij}$ from step 2:

$$E(O_{ij}) = n\,p_i\,p_j$$

Step 5. The chances $p_i$ and $p_j$ are unknown, so estimate them by the sample proportions (row total over $n$, column total over $n$):

$$\hat{p}_i = \frac{n_i}{n} \qquad \hat{p}_j = \frac{n_j}{n}$$

Step 6. Substitute the estimates:

$$\hat{E}_{ij} = n\left(\frac{n_i}{n}\right)\left(\frac{n_j}{n}\right) = \frac{n_i\,n_j}{n}$$

$n_i$ is the total of row $i$, $n_j$ is the total of column $j$ and $n$ is the grand total. The hat on $E$ is there because it is an estimate. The step that earns the mark is the independence step (step 2). This matches slides 13 and 14.

### Proof of the computational formula for chi-square

Not in the lecture. Expand the square and use $\sum O = \sum E = n$ (both lists add up to the grand total):

$$\sum \frac{(O - E)^2}{E} = \sum \frac{O^2 - 2OE + E^2}{E} = \sum \frac{O^2}{E} - 2\sum O + \sum E = \sum \frac{O^2}{E} - 2n + n$$

$$\chi^2 = \sum \frac{O^2}{E} - n$$

$O$ is an observed count, $E$ an expected count and $n$ the grand total. For a two-way table, put $E_{ij} = \dfrac{n_i n_j}{n}$ into it:

$$\chi^2 = n\left(\sum \frac{O_{ij}^2}{n_i\,n_j} - 1\right)$$

Checked by script on four examples (the die, 2023 question 7, the faculty table and the furniture table): the long form and both short forms agree (4.2, 0.1847, 6.454 and 19.18).

> [!warning] Use with care
> The SA2 information sheet asked for formulae as given in the lecture notes. In an answer, write the lecture's formula $\sum \frac{(O-E)^2}{E}$ unless the lecturer allows the shortcut. The shortcut ends in a subtraction, so a rounded sum can shift the answer; keep 3 or 4 decimals and round only at the end.

## Where the source is inconsistent

- The tables on slides 11 and 12 label the rows $r$ and the columns $c$, while the text of slide 11 and the formulas from slide 14 use $I$ rows and $J$ columns. The degrees of freedom appear as $(I-1)(J-1)$ on slide 14 and as $(r-1)(c-1)$ on slides 16 and 19. They are the same thing.
- Slide 14 writes the row and column totals as $n_i$ and $n_j$ with no dots, where the ANOVA lecture used dots for totals. Does this lecture want dots?
- The slide footer date is 9/27/2021. The deck may predate this year's course, so what is in it may have changed.
- P-values versus critical values: slide 16 and Solution 11 give P-value ranges for chi-square tests (P < .005, and .01 < P < .025). The lecturer said for Summative Assessment 2 that P-values are calculated only for $z$ tests. Whether that holds for chi-square on the final is not settled.
- The validity thresholds differ between look-alike tests (added observation, not a claim of an error). The two-proportion $z$ test uses the strict rule of at least 10 successes and 10 failures in every group, while a chi-square test on a 2 by 2 table asks only for expected counts of at least 5. A 2 by 2 chi-square test and the two-proportion $z$ test are the same test.
- Solution 11, question 44, gives $\chi^2 = 11.60$. A recomputation from the printed table gives 11.65 (P-value about 0.020). The solution probably rounded the expected counts to one decimal place. The decisions are the same.
- The learning guide lists "testing hypotheses about one population variance" under the chi-square family and Chapter 14 under hypothesis testing. Lecture 11 does not cover the one-variance test. Whether it is examinable is not known.

These are gaps in the source, not gaps in understanding.

## Do not forget

- Chi-square is for counts in categories. A number measured on each person means $t$ or ANOVA instead.
- $\chi^2 = \sum \frac{(O-E)^2}{E}$ and only a large value counts against $H_0$ (upper tail).
- Expected counts come from the claim in $H_0$: $E = n\,p_{i0}$ for goodness of fit, and $E = \dfrac{\text{row total} \times \text{column total}}{n}$ for a table.
- $df = k - 1$ for goodness of fit (groups, never $n - 1$) and $df = (I-1)(J-1)$ for a table.
- Every expected count must be at least 5. It is the expected counts that are checked, not the observed counts and not $df$.
- Failing to reject: "not sufficient evidence that ..." with the level and the context. Never "the alternative is rejected", never "accept $H_0$".
- Keep expected counts as decimals. Check any expected count against its row and column totals: it cannot exceed either.
- The sum of the gaps $O - E$ is always zero and says nothing about the next roll. A fair die has no memory.
- Possible proofs: $E_{ij} = n_i n_j / n$ (start from the intersection, independence gives $p_i p_j$, times $n$, then estimate) and $\chi^2 = \sum O^2/E - n$ (expand the square, use $\sum O = \sum E = n$).

## See also

- [[STA01B1_Notes_S9_Simple_Linear_Regression]] for the same idea of degrees of freedom (the section on why the regression df is 1 has a tag in its heading, which breaks heading links, so this link is to the whole file) and for $n - 2$ error degrees of freedom.
- [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]] for ANOVA, the other test that compares groups.
- [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances]] for the two-proportion $z$ test, which is equivalent to a 2 by 2 chi-square test.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] for rejection regions, Type I and Type II error, and the logic of testing.
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] for the chi-square distribution as it first appears.
- [[STA01B1_Notes_S1_Statistics_and_Sampling_Distributions]] for the CLT.

## Amendments

- 2026-11-07: added a scope marker to The test of homogeneity (not examined, per lecturer as reported). No content removed.
- S10, later the same day: added the section Proofs that may be asked (the proof of the expected count, in the order the lecturer used it, and the proof of the computational formula for chi-square), and one line in Do not forget. Added at the student's request after they pointed out that the lecturer likes to set proofs that are not on the slides.

---
*CDG v11 | written S10 | amended S10 (v11), 2026-11-07 (v11) | 2026-11-07*
