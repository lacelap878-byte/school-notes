Supersedes S1 to S8.

# STA01B1 Struggle Log S9 (Simple Linear Regression)

## 1. Open items (unresolved, oldest first)
```
choosing n for a worded subgroup proportion claim | first seen S5 | "proportion of X within Y" vs "proportion of X who are Y" changes which n to use; no lecture on file has posed this kind of question yet, and Lecture 10 (regression) has no proportions | 5
reading a P-value range off a printed t-table | first seen S5 | fixed columns only, not continuous like the Z table; Lecture 10 gave no chance to practise it (the t test on the slides has no worked numbers; the composite example used a rejection decision) | 5
source inconsistencies pending the lecturer | first seen S6 | the S6 to S8 cutoff questions are answered (see section 2). Still open: Lecture 10 slide 17 has a blank SSE formula; slides 19 and 20 have notation and wording problems (beta_0 for the hypothesised slope, H0 stated backwards); slides 28 and 29 use alpha and beta; Chapter 10 vs 11 vs 12 numbering. A gap in the source, not a recognition failure | 4
which diagnostic plot checks which assumption | first seen S9 | given a straight normal plot and a U-shaped residuals-versus-fits plot, picked "normality is violated, because the residual plot shows a pattern". The normal plot checks normality; residuals versus fits is the equal-variance check (and, added, a U shape points to the wrong model). A pattern in one plot says nothing about the other plot's assumption | 1
centre and width of a prediction interval given a confidence interval | first seen S9 | a complete guess. Picked (9.1, 14.9), wide enough but centred on 12.0, when the confidence interval (10.2, 12.8) has midpoint 11.5. Both intervals share the centre yhat, and the prediction interval is wider because of the extra 1 under the root. The user did not use the centre check | 1
```

Retention checks (answered correctly in S9, kept because the user says they may be forgotten; see section 5):
```
totals vs means in S_xx and SSTr | first seen S8 | answered correctly at the end of S9 (S_xx from x = 1, 2, 4, 5, 8) after a miss at the start (SSTr, a guess once the user's answer came out negative). The root cause the user gave: not knowing how to sum or find the totals | 2
paired design is a one-sample problem on the differences | first seen S7 | slipped at the start of S9 (picked the pooled two-sample t) and at the end of S9 was answered correctly (20 customers rating two products). It has now come up in three sessions in a row | 3
regression df, with more than one predictor | first seen S9 | answered correctly (2 and 17 for two predictors, n = 20) | 1
t squared = F and the sign of F | first seen S9 | answered correctly | 1
r squared vs r, and which sum of squares goes underneath | first seen S9 | answered correctly (SSR 45, SSE 15 gives 0.75 and 0.866) | 1
```

## 2. Resolved this session
```
MSE vs MSTr when H0 is false | resolved S9 | answered correctly in the revision quiz (add a constant to one group: SSE unchanged, SSTr changes). MSE is built from deviations around each group's own mean, so it cannot see the group means differ; MSTr can
SSTr computing formula: totals not means | resolved S9 | missed at the start (a guess after a negative result), then answered correctly at the end through the S_xx retest. A total squared over the count inside it; a sum of squares cannot be negative, so a negative value means the two terms were built differently
third subscript of Q (error df, not total df) | resolved S9 | answered correctly in the revision quiz: Q(.05, 4, 24) for I = 4, J = 7
SST proof: which piece is SSE and which is SSTr, and where the J goes | resolved S9 | answered correctly in the revision quiz with the actual expressions shown: the piece containing x_ij is SSE with no J; the piece with only means has no j, so the inner sum gives J
Tukey: joint level vs individual level | resolved S9 | answered correctly in the revision quiz: Q(.05) fixes the family level at 95%, so each interval is wider than a plain 95% interval
paired design as a one-sample problem (S8 provisional) | resolved S9 | see retention checks; closed on the end-of-session retest, kept on the watch list
source inconsistencies about cutoffs | resolved S9 | the lecturer's reply: n > 40 throughout, the strict 10-and-10 proportion rule, "and/or" on the pooled t condition, exam F table at the stated alpha. (The S8 files still showed these as pending; this log closes them.)
```
Carried from S7, resolved S7 and held across two later sessions with no recurrence, so now dropped: proportion branch (always Z), proportion validity at 10 not 5, P-value doubling, what changes between n > 30 and n > 40.

## 3. Notation and terminology still causing trouble
- Dots in ANOVA: x_ij (no dot), xbar_i. (one dot), xbar.. (two dots). The lecturer has said a missed dot in the proof costs a mark.
- Totals vs means: in the computing formulas x_i. and x.. are totals with no bars, and S_xx and S_xy use (sum x)^2 / n and (sum x)(sum y) / n, a total squared over the count inside it.
- Q(alpha, I, I(J-1)): second subscript I, third subscript the error df.
- In regression, df is counted per slope: regression df = number of slopes (1 here), error df = n - k - 1, Total df = n - 1.
- Fits vs residuals vs group means: a fit is the line's predicted value at an observed x_i (not a group mean); the residual is observed minus fit; the fits average to ybar.
- x0 is a chosen x value, not necessarily a data point. The confidence interval at x0 is for the average y (a point on the line of means); the prediction interval is for one new y.
- Slide 19 writes beta_0 for the hypothesised slope, not the intercept. Slide 20 states H0 as "model is useful", which is backwards. Slides 28 and 29 write the line of means with alpha and beta.
- SAS wording from S8: Model = Treatments, Error = Error, Corrected Total = Total.
- Underscored or joined means in Tukey = "not shown to differ", not "equal", and the relation is not transitive.

## 4. Patterns across sessions
```
distribution/test choice | seen in S5, S6, S7, S8, S9 | each lecture added one branch to "which formula and which distribution apply here". S5 the one-sample mean fork, S6 the two-sample mean fork, S7 the proportion fork (always Z) and the variance fork (always F), S8 the more-than-two-means fork (ANOVA F, then Tukey), S9 the regression fork (t on the slope, F on the model, which are the same test for one x). The paired design is the one that keeps recurring: it slipped in S7, S8 and S9
totals vs means in computing formulas | seen in S8, S9 | S8: bars on totals in the SSTr formula and the miss on SSTr; S9: the SSTr miss again at the start, with the root cause "not knowing how to sum or find the totals", then correct on S_xx. The user noticed the answer was negative, which was the right alarm, but guessed instead of checking which count sat under which total
source inconsistencies not reconciled by the slides | seen in S6, S7, S8, S9 | S6 one, S7 four, S8 several (Chapter 10 vs 11 numbering, an unexplained RSE label, k vs I), S9 more (blank SSE formula on slide 17, H0 stated backwards on slide 20, beta_0 reused for the hypothesised slope on slide 19, alpha and beta on slides 28 and 29, Chapter 10 to 12 numbering). A pattern in the source material, not a gap in the user's understanding; the fix is external (the lecturer's answer)
```

## 5. Retest first (ranked)
1. Which diagnostic plot checks which assumption (normal probability plot vs residuals versus fits). Show a pair of plots and ask what follows; include a funnel as well as a U shape.
2. Centre and width of a prediction interval given a confidence interval at the same x0. Give a different confidence interval, and make one distractor wide but off-centre.
3. Retention: totals vs means. A fresh S_xx or SSTr from totals, and ask for the sign check. Weight this one, since it has now slipped in two sessions.
4. Retention: paired design as a one-sample problem on differences (three sessions in a row). Use a new context that does not say "before and after".
5. Retention: regression df for a model with more than one predictor, and Total = regression + error.
6. Retention: t squared = F, F is never negative, and the numerator df is the regression df.
7. Retention: r squared vs r, and which sum of squares goes underneath.
8. Retention, one question at most each: MSE vs MSTr, Q subscripts, the SST proof pieces, Tukey's family error rate (all answered correctly in S9).
9. Parked: choosing n for a worded subgroup proportion claim, and reading a P-value range off a t-table (only if the next lecture supplies material).
