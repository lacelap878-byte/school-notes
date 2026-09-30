---
module: STA01B1
topic: Single-Factor ANOVA and Tukey's Procedure
session: S8
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# STA01B1 Notes S8: Single-Factor ANOVA and Tukey's Procedure

Source: Lecture 9.pdf, slides 1 to 34 (slide 1 is the chapter title card and slide 34 is a closing reference to Chapter 10, sections 10.1 and 10.2, so neither carries content). One result, the proof that $SST = SSTr + SSE$, is not on the slides. It is the lecturer's proof as described by the student in session, and the algebra is written out here from that description.

Labels used: `(source, slide N)`, `(source: lecturer's proof, as described in session)`, `(added)` for anything beyond the source.

Note for anyone who copied the live session by hand: four things were wrong there and are right here. The computing formulas use totals with no bars. The second subscript on $Q$ is $I$, not $I-1$, and the third is the error df. The mean formulas on the notation slides are lowercase $\bar{x}$. The Breakfast Problem has no scenario text on its slides.

## Why ANOVA exists

Earlier sessions compared two means at a time. Single-factor ANOVA compares two or more populations with a single test, so there is no need to run a two-sample test for every pair. (added) Running every pair separately would also multiply the chances of a false alarm, which is the problem the last section of these notes deals with for the follow-up comparisons.

The test answers one question only: are the means all equal, or not? If it says they are not, a second tool (Tukey's procedure) says which ones differ.

## The hypotheses (source, slide 2) #definition

$$H_0: \mu_1 = \mu_2 = \cdots = \mu_I$$
$$H_a: \text{at least two of the } \mu_i\text{'s are different}$$

Here $\mu_i$ is the true mean of population $i$, and $I$ is the number of populations. $H_a$ does not say every mean differs, only that the common-mean claim in $H_0$ fails somewhere.

## Notation: the double subscript (source, slides 3 to 6) #definition

Each observation needs two labels, which population it came from and which observation within that population it is.

$$X_{ij} = \text{the random variable (rv) denoting the } j\text{th measurement from the } i\text{th population}$$
$$x_{ij} = \text{the observed value of } X_{ij} \text{ when the experiment is performed}$$

Example (source, slide 4): Table 11.1 (compression strength of four types of box, so $I = 4$ and $J = 6$ measurements each) has $x_{42}$ as the 2nd observation in the 4th row.

The mean of the $i$th sample, and the grand mean over everything:

$$\bar{x}_{i\cdot} = \frac{\sum_{j=1}^{J} x_{ij}}{J} \qquad i = 1, 2, \ldots, I$$
$$\bar{x}_{\cdot\cdot} = \frac{\sum_{i=1}^{I}\sum_{j=1}^{J} x_{ij}}{IJ}$$

$J$ is the number of observations per sample, $I$ the number of samples, so $IJ$ is the total number of observations. On the slides these means are lowercase $\bar{x}$; the sums of squares slide uses capital $\bar{X}$ for the random-variable versions.

> [!warning] The dots are marks
> The dot replaces the index that was summed or averaged away. $x_{ij}$ has no dot (a single observation). $\bar{x}_{i\cdot}$ has one dot (averaged over $j$). $\bar{x}_{\cdot\cdot}$ has two (averaged over both). The lecturer has said a missed dot costs a mark in the proof below. #struggle

## Assumptions (source, slides 7 and 8) #definition

There are two assumptions, and both carry weight. Each $X_{ij}$ is normally distributed, with

$$E(X_{ij}) = \mu_i$$
$$V(X_{ij}) = \sigma^2$$

- **Assumption 1, normality.** Every observation comes from a normal population.
- **Assumption 2, homoscedasticity (equal variances).** Look at the second line: $\sigma^2$ has no $i$ on it. Only the mean $\mu_i$ is allowed to depend on the population. The variance $\sigma^2$ is one shared number for all $I$ populations. The slide writes "(equal variances!)" in red with an exclamation mark and names it in a callout, so it is flagged as important, not a footnote.

> [!warning] Homoscedasticity is not a side note
> (added) $MSE$ is the average of the group variances, and it is the denominator of $F$. It only makes sense as one estimate of one $\sigma^2$ if every group really shares that $\sigma^2$. Tukey's $w$ also uses that same single $MSE$ for every pair, so Tukey relies on it as well. If one group is far more spread out than the rest, the pooled $MSE$ describes none of the groups well, and the $F$ test and Tukey's intervals cannot be trusted. State both assumptions whenever you use ANOVA. #struggle

Rough check, since $\sigma^2$ is never known exactly (source, slide 8): the equal-variance assumption is considered reasonable when the largest sample standard deviation is not much more than twice the smallest. In Table 11.1 the sample SDs run from 37.20 to 46.55, and $2 \times 37.20 = 74.4$, so the largest is comfortably inside the rule.

## The idea: variation between against variation within (source, slides 9, 19 to 22)

If $H_0$ is true, all $I$ samples come from populations with the same mean, so the sample means should be reasonably close. The test compares a measure of variation between the sample means with a measure of variation calculated within each sample.

The source shows this with three pictures of three hypothetical population curves, each with its between-group spread and within-group spreads drawn as bars:
- No real difference: the curves overlap heavily and the between spread is about the same size as the within spreads. Nothing pushes $F$ away from 1.
- Partial difference: two curves overlap and one sits apart. Some separation, but not for every pair.
- Full difference: all three curves sit apart and the between spread dwarfs every within spread. That picture gives a large $F$ and a rejection of $H_0$.

(The bars in the source pictures carry an "RSE" label that the slides do not explain, so it is left out here.)

## Sums of squares (source, slide 10) #formula

$$SSTr = J\sum_i \left(\bar{X}_{i\cdot} - \bar{X}_{\cdot\cdot}\right)^2$$
$$SSE = \sum_i\sum_j \left(X_{ij} - \bar{X}_{i\cdot}\right)^2 = (J-1)\left(S_1^2 + S_2^2 + \cdots + S_I^2\right)$$

$SSTr$ (treatment) measures how far the group means sit from the grand mean. $SSE$ (error) measures how far the observations sit from their own group's mean. $S_i^2$ is the sample variance of group $i$.

The second form of $SSE$ says it is just the group variances added and rescaled, the same pooling idea as the pooled two-sample variance, stretched from two groups to $I$ groups.

## Mean squares and the F statistic (source, slide 11) #formula

$$MSTr = \frac{SSTr}{I-1} \qquad MSE = \frac{SSE}{I(J-1)}$$
$$F = \frac{MSTr}{MSE}$$

Each mean square is a sum of squares divided by its degrees of freedom. A large $F$ means the between-group variation is large relative to the within-group variation, which is the signal that the means are not all equal.

## The ANOVA table (source, slides 12 and 13) #formula

| Source of Variation | df | Sum of Squares | Mean Square | $f$ |
|---|---|---|---|---|
| Treatments | $I-1$ | $SSTr$ | $MSTr = SSTr/(I-1)$ | $MSTr/MSE$ |
| Error | $I(J-1)$ | $SSE$ | $MSE = SSE/[I(J-1)]$ | |
| Total | $IJ-1$ | $SST$ | | |

Definitions and computing formulas (source, slide 13):

| Sum of Squares | df | Definition | Computing Formula |
|---|---|---|---|
| total $= SST$ | $IJ-1$ | $\sum_i\sum_j (x_{ij}-\bar{x}_{\cdot\cdot})^2$ | $\sum_i\sum_j x_{ij}^2 - x_{\cdot\cdot}^2/IJ$ |
| treatment $= SSTr$ | $I-1$ | $\sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = J\sum_i(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2$ | $\sum_i x_{i\cdot}^2/J - x_{\cdot\cdot}^2/IJ$ |
| error $= SSE$ | $I(J-1)$ | $\sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})^2$ | $SST - SSTr$ |

> [!warning] Totals in the computing formulas, means in the definitions
> In the computing column, $x_{i\cdot}$ is a treatment total and $x_{\cdot\cdot}$ is the grand total, with no bars. The definition column uses means, so it has bars. Putting a bar on $x_{\cdot\cdot}$ in the computing formula turns 149 into 12.42 and wrecks the answer. Quick sanity check: the two terms being subtracted, $\sum x_{i\cdot}^2/J$ and $x_{\cdot\cdot}^2/IJ$, should be about the same size (in the Breakfast Problem, 1914.75 and 1850.08). #common-mistake #struggle

The error row's computing formula is just $SST - SSTr$. That shortcut works because $SST = SSTr + SSE$ always holds, which is the identity proved below. The degrees of freedom split the same way: $IJ - 1 = (I-1) + I(J-1)$. (added)

## Worked example: the Breakfast Problem (source, slides 14 to 18) #worked-example

Three breakfast conditions ($I = 3$), four observations each ($J = 4$). The slides give the data and no scenario text; later slides only mention average attention spans as the measurement.

| No Breakfast | Light Breakfast | Full Breakfast |
|---|---|---|
| 8, 7, 9, 13 | 14, 16, 12, 17 | 10, 12, 16, 15 |
| $T_1 = 37$ | $T_2 = 59$ | $T_3 = 53$ |

Test $H_0: \mu_1 = \mu_2 = \mu_3$ against $H_a$: at least one mean is different.

Grand total $x_{\cdot\cdot} = 37 + 59 + 53 = 149$, and $IJ = 12$, so

$$\frac{x_{\cdot\cdot}^2}{IJ} = \frac{149^2}{12} = 1850.0833$$
$$SST = \sum_i\sum_j x_{ij}^2 - \frac{x_{\cdot\cdot}^2}{IJ} = (8^2 + 7^2 + \cdots + 15^2) - 1850.0833 = 122.9167$$
$$SSTr = \sum_i \frac{x_{i\cdot}^2}{J} - \frac{x_{\cdot\cdot}^2}{IJ} = \frac{37^2}{4} + \frac{59^2}{4} + \frac{53^2}{4} - 1850.0833 = 64.6667$$
$$SSE = SST - SSTr = 122.9167 - 64.6667 = 58.25$$

| Source | df | SS | MS | $F$ |
|---|---|---|---|---|
| Treatments | 2 | 64.6667 | 32.3333 | 5.00 |
| Error | 9 | 58.25 | 6.4722 | |
| Total | 11 | 122.9167 | | |

The source stops at the table and does not state a decision; a decision would compare $F = 5.00$ with the critical value for 2 and 9 df.

## Why F grows when H0 is false (source, slides 18 and 19, with added explanation) #struggle

Two facts carry the whole test.

- $MSE = SSE/(n-k)$ is a pooled estimate of the common $\sigma^2$, a weighted average of the sample variances, whether or not $H_0$ is true (source, slide 18). Here $n$ is the total number of observations and $k$ the number of populations, the same as $IJ$ and $I$.
- If $H_0$ is false and the population means differ, $MSTr$, which measures the variance in the sample means, is unusually large, so $F$ tends to be larger than usual (source, slide 19).

> [!warning] MSE does not feel the means, MSTr does
> $MSE$ is built from deviations around each group's own mean, so it cannot see whether the group means differ. $MSTr$ measures the spread of the group means themselves, so it can. The tempting wrong answer reverses them. #common-mistake #struggle

(added) Numbers from the Breakfast Problem make this concrete.
- The three group variances are $20.75/3 = 6.917$, $14.75/3 = 4.917$ and $22.75/3 = 7.583$. Their average is $58.25/9 = 6.4722$, which is exactly $MSE$. So $MSE$ really is the average of the group variances.
- Thought experiment: add 100 to every value in one group. That group's deviations from its own mean do not change, so $SSE$ and $MSE$ do not change. But its mean moves far from the others, so $MSTr$ explodes.
- $MSTr$ is $J$ times the variance of the sample means: $4 \times 8.0833 = 32.33$. If $H_0$ were true the sample means would wobble only by sampling noise, with variance about $\sigma^2/J$ each, and $J$ times that is about $\sigma^2$. That is why $F$ sits near 1 when $H_0$ is true (on average; it is not exactly 1 every time).

> *This is the same pooling move as the pooled variance from two-sample inference, just stretched from two groups to $I$ groups. It is the same idea reappearing, not a new one.*

## Proof that $SST = SSTr + SSE$ (source: lecturer's proof, as described in session) #theorem #exam-flagged

The lecturer showed this proof and has said it is important, likely worth 6 to 8 marks, with a mark lost for a missed dot (as reported in session, not confirmed in writing). The slides only use the identity and never prove it.

Know these first:

$$SSE = \sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})^2$$
$$SSTr = \sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = J\sum_i(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2$$
$$\sum_j x_{ij} = J\bar{x}_{i\cdot}$$

The third line is the group-mean rule, from $\bar{x}_{i\cdot} = \sum_j x_{ij}/J$. It is what gets substituted in step 6. The rule for constants: if $i$ or $j$ does not appear in an expression, it is constant with respect to that index.

**Step 1. Definition.**
$$SST = \sum_i\sum_j (x_{ij} - \bar{x}_{\cdot\cdot})^2$$

**Step 2. Add 0**, in the form $-\bar{x}_{i\cdot} + \bar{x}_{i\cdot}$, and regroup into two brackets. This brings in $\bar{x}_{i\cdot}$, which both $SSE$ and $SSTr$ need.
$$SST = \sum_i\sum_j \Big[(x_{ij} - \bar{x}_{i\cdot}) + (\bar{x}_{i\cdot} - \bar{x}_{\cdot\cdot})\Big]^2$$

**Step 3. Expand the square** as $a^2 + 2ab + b^2$, with $a = x_{ij} - \bar{x}_{i\cdot}$ and $b = \bar{x}_{i\cdot} - \bar{x}_{\cdot\cdot}$. Multiply out only as far as the three pieces and keep the middle term as two brackets with the 2 in front.
$$SST = \sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})^2 + 2\sum_i\sum_j (x_{ij}-\bar{x}_{i\cdot})(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot}) + \sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2$$

**Step 4. Substitute the two ends.**
- The first piece contains the observation $x_{ij}$ and matches the definition exactly, so it is $SSE$, with no $J$ in front.
- The last piece has no $j$ anywhere in it, so it is constant in $j$ and the inner sum gives $J$:
$$\sum_i\sum_j (\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = J\sum_i(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})^2 = SSTr$$

**Step 5. Middle term: distribute** the second bracket over the first, and let the sum act on each term. Keep the 2.
$$2\sum_i\sum_j x_{ij}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot}) \;-\; 2\sum_i\sum_j \bar{x}_{i\cdot}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$$

**Step 6. Substitute inside each term.**
- First term: $(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$ has no $j$, so it is constant. Use $\sum_j x_{ij} = J\bar{x}_{i\cdot}$.
- Second term: nothing has a $j$, so the sum over $j$ gives $J$.
$$2\sum_i J\bar{x}_{i\cdot}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot}) \;-\; 2\sum_i J\bar{x}_{i\cdot}(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$$

**Step 7. Cancel.** The two terms are identical and subtracted, so they cancel as they stand, with the summation left in place. The middle term is $0$.

**Step 8. Done.**
$$SST = SSE + SSTr$$

> [!warning] Where marks are lost
> Which piece is which: the first piece has $x_{ij}$ in it, so it is $SSE$ and has no $J$. The last piece has only means, so it is $SSTr$ and carries the $J$. Dots: $x_{ij}$ none, $\bar{x}_{i\cdot}$ one, $\bar{x}_{\cdot\cdot}$ two. The 2 stays on both middle terms until they cancel. Write both middle terms in the same order so the match is visible. Only the first middle term uses $\sum_j x_{ij} = J\bar{x}_{i\cdot}$, because it is the only one still containing $x_{ij}$. #struggle #exam-flagged

(added) The proof is pure algebra and needs no normality or equal-variance assumption. Those assumptions matter later, for the distribution of $F$. A shorter route pulls $(\bar{x}_{i\cdot}-\bar{x}_{\cdot\cdot})$ out of the inner sum first and uses $\sum_j (x_{ij}-\bar{x}_{i\cdot}) = 0$. It gives the same result, but the lecturer's version is the one above, so use that in an exam.

> *The eight moves, in short: write it, add 0, expand, name the two ends, distribute the middle, substitute with the group-mean rule, cancel, done. If the order slips in an exam, the anchor is that the ends become $SSE$ and $SSTr$ and the middle disappears.*

## Tukey's procedure: which means differ (source, slides 23 to 25) #definition

When the $F$ test is not significant, the analysis stops, because no differences among the means were identified. When $H_0$ is rejected, the natural next question is which means differ from one another. A method for that further analysis is called a multiple comparisons procedure.

The central idea (source, slide 24): calculate a confidence interval for each pairwise difference $\mu_i - \mu_j$ with $i < j$. For $I = 4$, the six required CIs are for $\mu_1 - \mu_2$ (but not also $\mu_2 - \mu_1$), $\mu_1 - \mu_3$, $\mu_1 - \mu_4$, $\mu_2 - \mu_3$, $\mu_2 - \mu_4$ and $\mu_3 - \mu_4$. If the interval for $\mu_i - \mu_j$ does not include 0, conclude that $\mu_i$ and $\mu_j$ differ significantly; if it does include 0, they are judged not significantly different. The procedures based on this idea differ in how the CIs are calculated. Tukey's is a popular method that controls the simultaneous confidence level for all $I(I-1)/2$ intervals at once.

Select $\alpha$, extract $Q_{\alpha,\,I,\,I(J-1)}$ from Appendix Table A.10, and calculate

$$w = Q_{\alpha,\,I,\,I(J-1)}\sqrt{\frac{MSE}{J}}$$

Then list the sample means in increasing order and underline every set of adjacent means that differ by less than $w$. Any pair of sample means not underscored by the same line corresponds to a pair of population means judged significantly different. The quantity $w$ is Tukey's honestly significant difference (HSD).

> [!warning] Read the subscripts of Q carefully
> Second subscript: $I$, the number of means being compared, and not $I - 1$ as in $F$ (source, slide 27). Third subscript: the error df $I(J-1)$, the degrees of freedom of the $MSE$ inside $w$, and not the total df $IJ - 1$. For $I = 5$, $J = 9$ that is $Q_{.05,5,40}$, not $Q_{.05,5,44}$. #common-mistake #struggle

## Example 10.5: oil filters (source, slides 26 to 28) #worked-example

Five brands of oil filter ($I = 5$) were compared on how much foreign material they capture, with $\mu_i$ the true average for brand $i$. Nine filters of each brand were used ($J = 9$), giving sample means $\bar{x}_1 = 14.5$, $\bar{x}_2 = 13.8$, $\bar{x}_3 = 13.3$, $\bar{x}_4 = 14.3$, $\bar{x}_5 = 13.1$.

| Source | df | SS | MS | $F$ |
|---|---|---|---|---|
| Treatments (brands) | 4 | 13.32 | 3.33 | 37.84 |
| Error | 40 | 3.53 | .088 | |
| Total | 44 | 16.85 | | |

Since $F_{.05,4,40} = 2.61$ and $37.84$ far exceeds it, $H_0$ is rejected decisively at level .05. Then $Q_{.05,5,40} = 4.04$ and

$$w = 4.04\sqrt{\frac{.088}{9}} = .4$$

Ordering the means and underscoring pairs that differ by less than .4:

```
x5     x3     x2     x4     x1
13.1   13.3   13.8   14.3   14.5
-------------         -------------
```

Reading it: 13.1 and 13.3 differ by .2, so they are joined. 13.8 minus 13.3 is .5, and 13.8 minus 13.1 is .7, both at least .4, so brand 2 cannot join them. 14.3 minus 13.8 is .5, so brand 2 cannot join the top pair either. 14.3 and 14.5 differ by .2 and are joined.

Brands 1 and 4 are not significantly different from one another, but are significantly higher than the other three brands. Brand 2 is significantly better than brands 3 and 5 but worse than brands 1 and 4. Brands 3 and 5 do not differ significantly.

The source's second configuration: if $\bar{x}_2 = 14.15$ instead of 13.8, with the same $w$, the picture changes. Then $14.5 - 14.15 = .35 < .4$, so brands 2, 4 and 1 share one line, and brands 5 and 3 share another:

```
x5     x3     x2      x4     x1
13.1   13.3   14.15   14.3   14.5
-------------  ---------------------
```

Brand 2 joins the top group, not the bottom one, since $14.15 - 13.3 = .85$ is far above $w$.

Note on labels: the ANOVA table is captioned "Table 11.3, ANOVA table for Example 11.4" in the source, while the slide's own label and text say Example 10.5. The lecture mixes Chapter 10 numbering with Table 11.x and Example 11.x numbering throughout (Table 11.1 on the notation slides too), which looks like two textbook editions being blended.

## Example 10.6: ethanol and REM sleep (source, slides 29 and 30) #worked-example

A biologist studied the effect of ethanol on sleep time. Twenty rats, matched for age and other characteristics, each received an oral injection of a particular ethanol concentration per kg of body weight, and rapid eye movement (REM) sleep time was recorded over 24 hours. Does the true average REM sleep time depend on the ethanol concentration?

| Treatment (ethanol) | REM Time | $x_{i\cdot}$ | $\bar{x}_{i\cdot}$ |
|---|---|---|---|
| 0 (control) | 88.6, 73.2, 91.4, 68.0, 75.2 | 396.4 | 79.28 |
| 1 g/kg | 63.0, 53.9, 69.2, 50.1, 71.5 | 307.7 | 61.54 |
| 2 g/kg | 44.9, 59.5, 40.2, 56.3, 38.7 | 239.6 | 47.92 |
| 4 g/kg | 31.0, 39.6, 45.3, 25.2, 22.7 | 163.8 | 32.76 |

SAS output (source, slide 30):

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 3 | 5882.35750 | 1960.78583 | 21.09 | 0.0001 |
| Error | 16 | 1487.40000 | 92.96250 | | |
| Corrected Total | 19 | 7369.75750 | | | |

(added) In SAS wording, Model is the Treatments row and Corrected Total is the Total row of the ANOVA table.

$P = 0.0001$, so $H_0$ is rejected. With $I = 4$ and 16 error df, $Q_{.05,4,16} = 4.05$ and

$$w = 4.05\sqrt{\frac{93.0}{5}} = 17.47$$

(The slide rounds $MSE$ to 93.0.) Ordering the means and underscoring:

```
x4      x3      x2      x1
32.76   47.92   61.54   79.28
-----------------
        -----------------
```

(added) The checks: $47.92 - 32.76 = 15.16$ and $61.54 - 47.92 = 13.62$ are both below 17.47, so those two neighbouring pairs are joined. $61.54 - 32.76 = 28.78$ is above, so treatments 4 and 2 are not joined. $79.28 - 61.54 = 17.74$ is just above 17.47, so treatment 1 stands alone.

> *The 1-versus-2 call is tight: 17.74 against 17.47, a margin of .27. Rounding does not rescue it either way, since using the unrounded $MSE = 92.9625$ gives $w \approx 17.46$ and treatment 1 still separates.*

## Reading the underscoring (source, slide 31)

The underscoring must be read with care. It seems to say treatments 2 and 3 do not differ, 3 and 4 do not differ, yet 2 and 4 differ. The suggested way of expressing this: although the evidence allows us to conclude that treatments 2 and 4 differ from one another, neither has been shown to be significantly different from 3. Treatment 1 has a significantly higher true average REM sleep time than any other treatment. It involves 0 ethanol, and there is a trend toward less sleep with more ethanol, although not all differences are significant.

(added) A joined pair means "not shown to differ", which is weaker than "equal". That relation is not transitive: 4-3 and 3-2 can both be unresolved while 4 and 2 are far enough apart to be significant. Two means are judged different only when no single line covers both.

## What alpha means in Tukey's procedure (source, slides 32 and 33) #definition

A 95% interval is only 95% reliable on its own. What matters when several intervals are computed is how often all of them capture their targets together, the simultaneous (joint) confidence level.

Take a 95% CI for a mean $\mu$ and, from an independent sample, a 95% CI for a proportion $p$. Each has probability .95 of capturing its parameter, and because the samples are independent, both do with probability

$$(.95)(.95) = (.95)^2 = .90$$

so the simultaneous level for the two is roughly 90%. With three CIs from independent samples it is $100(.95)^3\% \approx 86\%$. The more intervals there are, the lower the joint level drops.

To hold the simultaneous level at 95% for two independent samples, each interval must be run at $100\sqrt{.95}\,\% \approx 97.5\%$. The more intervals, the higher each individual level must be. (added) For $k$ independent intervals the individual level is $100(.95)^{1/k}\%$, the same step.

Tukey's intervals are different in one important way. They are not based on independent samples, because $MSE$ appears in every one and many intervals share the same sample mean (for example, when $I = 4$, three different intervals all use $\bar{x}_{1\cdot}$). So there is no straightforward probability argument for getting the simultaneous level from the individual levels, and the $(.95)^k$ arithmetic above is an illustration only. Even so, the simultaneous level is controlled: $Q_{.05}$ gives a simultaneous 95% level and $Q_{.01}$ gives 99%.

> [!warning] Alpha is the family error rate
> To get a 95% simultaneous level, each individual interval must be considerably wider than a plain 95% interval. Said another way, for a 5% experimentwise (family) error rate the individual (per-comparison) error rate must be considerably smaller than .05. The $\alpha$ in Tukey's procedure belongs to the whole set of comparisons, not to any single pair. MINITAB asks for the family error rate and reports the individual one. #common-mistake #struggle

> *This is why the sequence is ANOVA first and Tukey second, rather than a separate two-sample interval for every pair. Six pairwise intervals at 95% each would leave the joint coverage well below 95%, and the width of $w$ is what pays to bring it back up.*

## Where the source is inconsistent

- Chapter 10 versus 11 numbering, as noted under Example 10.5. Lecture and slide titles say Chapter 10; the tables and some example labels say 11.
- The "RSE" label on the between and within pictures is never explained.
- Slide 18 uses $k$ for the number of populations where the rest of the lecture uses $I$.
- The Breakfast Problem slides never state a scenario, a significance level or a decision.

These join the earlier cutoff questions (30 versus 40, "and" versus "and/or", no stated proportion or F cutoffs), which are still waiting on the lecturer's answer. They are gaps in the source, not gaps in understanding.

## Carried from earlier sessions #struggle

Paired data is a one-sample problem. At the start of this session, a revision question on the paired design was missed: two sets of measurements on the same people are 12 pairs, so the working data are the 12 differences $D_i$ and the procedure is one-sample with $n - 1$ df, not a two-sample pooled $t$. In the session-end check the same idea was retested and no miss was reported, so it is provisionally closed pending confirmation.

## Do not forget

- Hypotheses: $H_0: \mu_1 = \cdots = \mu_I$; $H_a$: at least two differ.
- Two assumptions, state both: normality, and equal variances (homoscedasticity), one common $\sigma^2$ for every group. Check the second with the rule that the largest sample SD is not much more than twice the smallest.
- Dots: $x_{ij}$ none, $\bar{x}_{i\cdot}$ one, $\bar{x}_{\cdot\cdot}$ two. A missed dot in the proof costs a mark.
- Computing formulas use totals with no bars; definitions use means with bars.
- $F = MSTr/MSE$ with $I-1$ and $I(J-1)$ df. $MSE$ ignores whether the means differ; $MSTr$ inflates when they do.
- $SSE = SST - SSTr$ works because $SST = SSTr + SSE$.
- Proof: add 0, expand, ends become $SSE$ (no $J$) and $SSTr$ (carries the $J$), distribute the middle, substitute $\sum_j x_{ij} = J\bar{x}_{i\cdot}$, cancel as it stands.
- Tukey: only after rejecting $H_0$. $w = Q_{\alpha,I,I(J-1)}\sqrt{MSE/J}$, second subscript $I$ not $I-1$, third the error df.
- Joined means are "not shown to differ", not "equal", and the relation is not transitive.
- $\alpha$ in Tukey is the family error rate; each individual interval is wider than a plain 95% one.

## See also

These links go to whole files, because the headings inside those files could not be opened and checked this session.

- [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances]] for the F test and F distribution used for two variances.
- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]] for the pooled variance $S_p^2$ that $MSE$ generalises.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] for rejection regions and the logic of testing.
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] for the normal-population intervals behind the assumptions.
- [[STA01B1_Notes_S3_Statistical_Intervals]] for confidence-level meaning and interpretation.
