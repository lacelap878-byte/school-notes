Supersedes S1 to S8.

# STA01B1 Struggle Log S9 (Simple Linear Regression)

## 1. Open items (unresolved, oldest first)
```
choosing n for a worded subgroup proportion claim | first seen S5 | "proportion of X within Y" vs "proportion of X who are Y" changes which n to use; no lecture on file has posed this kind of question yet, and Lecture 10 (regression) has no proportions | 5
reading a P-value range off a printed t-table | first seen S5 | fixed columns only, not continuous like the Z table; Lecture 10 gave no chance to practise it (the t test on the slides has no worked numbers; the composite example used a rejection decision) | 5
source inconsistencies pending the lecturer | first seen S6 | the S6 to S8 cutoff questions are answered (see section 2). Still open: Lecture 10 slide 17 has a blank SSE formula; slides 19 and 20 have notation and wording problems (beta_0 for the hypothesised slope, H0 stated backwards); slides 28 and 29 use alpha and beta; Chapter 10 vs 11 vs 12 numbering. A gap in the source, not a recognition failure | 4
which diagnostic plot checks which assumption | first seen S9 | given a straight normal plot and a U-shaped residuals-versus-fits plot, picked "normality is violated, because the residual plot shows a pattern". The normal plot checks normality; residuals versus fits is the equal-variance check (and, added, a U shape points to the wrong model). A pattern in one plot says nothing about the other plot's assumption | 1
centre and width of a prediction interval given a confidence interval | first seen S9 | a complete guess. Picked (9.1, 14.9), wide enough but centred on 12.0, when the confidence interval (10.2, 12.8) has midpoint 11.5. Both intervals share the centre yhat, and the prediction interval is wider because of the extra 1 under the root. The user did not use the centre check | 1
reading Q from the studentized range table (Table A.10): column = number of groups | first seen S9 | in the timed practice run (3 groups of 5, error df 12) the user read 3.08, the entry under the column headed 2 (two groups), instead of the column headed 3, so the ruler came out 2.83 instead of 3.47. The arithmetic after that was correct. The user's screenshot showed only the first column of the table, so the cause was never looking across to the column for I = 3. Same family as the Q subscript rule, but this time the slip was in the table lookup, not in writing the subscripts | 1
recalling formulas under time: SSTr computing formula, F degrees of freedom, Tukey's ruler | first seen S9 | three recall asks during one practice run: the SSTr computing formula, which df go with F (answer: I - 1 and I(J-1)), and Tukey's formula. Each was answered by being reminded, then used correctly. This is a memory problem, not an understanding problem, so the fix is a closed-book recall check, not more explanation | 1
rounding before the F ratio | first seen S9 | divided the rounded MSTr 98.065 by the rounded MSE 4.23 and got F = 23.18 instead of 23.17. The decision was unaffected (3.89 is far away), but the rule matters when F sits close to the critical value, and SSE is found by subtraction, which magnifies rounding error. Keep two or more decimals, or use Ans and the calculator memory, and round only F at the end | 1
```

Retention checks (answered correctly in S9, kept because the user says they may be forgotten; see section 5):
```
totals vs means in S_xx and SSTr | first seen S8 | answered correctly at the end of S9 (S_xx from x = 1, 2, 4, 5, 8) after a miss at the start (SSTr, a guess once the user's answer came out negative). The root cause the user gave: not knowing how to sum or find the totals. The later root cause (S9 ANOVA drill): the user applied the double sum (times IJ) to the correction term, so the 15 copies were counted twice and SST came out negative. Retested in the timed 3 by 5 practice run with a fresh data set and the three-piece order check: SSTr 196.13, SST 246.93, SSE 50.80, all correct with no negative value | 3
paired design is a one-sample problem on the differences | first seen S7 | slipped at the start of S9 (picked the pooled two-sample t) and at the end of S9 was answered correctly (20 customers rating two products). It has now come up in three sessions in a row | 3
regression df, with more than one predictor | first seen S9 | answered correctly (2 and 17 for two predictors, n = 20) | 1
t squared = F and the sign of F | first seen S9 | answered correctly | 1
r squared vs r, and which sum of squares goes underneath | first seen S9 | answered correctly (SSR 45, SSE 15 gives 0.75 and 0.866) | 1
full single-factor ANOVA table and decision from raw data | first seen S9 | practice run on 3 groups of 5 (plant growth): sums of squares correct, table correct (df 2, 12, 14), decision correct (F about 23.17 against 3.89, reject), Tukey conclusion correct once the right Q was used (group 2 higher than 1 and 3; 1 and 3 not shown to differ). Finished well inside the 10 minutes the user set. The 4 by 5 and 5 by 5 cases were not yet tried | 1
t vs F in ANOVA | first seen S9 | asked whether the t distribution could be used for the ANOVA. Answer: no, t squared = F only when the numerator df is 1 (regression with one x, or two groups). With 3 groups the numerator df is 2, so F alone is the overall test and Tukey (Q) is the follow-up | 1
```

## 2. Resolved this session
```
MSE vs MSTr when H0 is false | resolved S9 | answered correctly in the revision quiz (add a constant to one group: SSE unchanged, SSTr changes). MSE is built from deviations around each group's own mean, so it cannot see the group means differ; MSTr can
SSTr computing formula: totals not means | resolved S9 | missed at the start (a guess after a negative result), then answered correctly at the end through the S_xx retest. A total squared over the count inside it; a sum of squares cannot be negative, so a negative value means the two terms were built differently
third subscript of Q (error df, not total df) | resolved S9 | answered correctly in the revision quiz: Q(.05, 4, 24) for I = 4, J = 7
SST proof: which piece is SSE and which is SSTr, and where the J goes | resolved S9 | answered correctly in the revision quiz with the actual expressions shown: the piece containing x_ij is SSE with no J; the piece with only means has no j, so the inner sum gives J
Tukey: joint level vs individual level | resolved S9 | answered correctly in the revision quiz: Q(.05) fixes the family level at 95%, so each interval is wider than a plain 95% interval
paired design as a one-sample problem (S8 provisional) | resolved S9 | see retention checks; closed on the end-of-session retest, kept on the watch list
negative sum of squares in an ANOVA table | resolved S9 | root cause found: multiplying the correction term (grand total squared over IJ) by IJ again. A one-page routine (STA01B1_ANOVA_Test_Routine.md, now in stats/extra) uses the lecture's three pieces with an order check (grand total piece, then group totals piece, then every-value piece, smallest to largest). A fresh practice run came out correct with no negative value. Keep on the watch list as a retention check
source inconsistencies about cutoffs | resolved S9 | the lecturer's reply: n > 40 throughout, the strict 10-and-10 proportion rule, "and/or" on the pooled t condition, exam F table at the stated alpha. (The S8 files still showed these as pending; this log closes them.)
```
Carried from S7, resolved S7 and held across two later sessions with no recurrence, so now dropped: proportion branch (always Z), proportion validity at 10 not 5, P-value doubling, what changes between n > 30 and n > 40.

## 3. Notation and terminology still causing trouble
- Dots in ANOVA: x_ij (no dot), xbar_i. (one dot), xbar.. (two dots). The lecturer has said a missed dot in the proof costs a mark.
- Totals vs means: in the computing formulas x_i. and x.. are totals with no bars, and S_xx and S_xy use (sum x)^2 / n and (sum x)(sum y) / n, a total squared over the count inside it.
- Q(alpha, I, I(J-1)): second subscript I, third subscript the error df. In Table A.10 the column header is the number of groups I (2, 3, 4, ...), and the row is the error df. The entry 3.08 at df 12 is the 2-group column; the 3-group column at df 12 gives 3.77. Always read across to the column for the number of groups.
- F for single-factor ANOVA: numerator df I - 1 (treatments), denominator df I(J-1) (error). The total df IJ - 1 is only used to close the table.
- Tukey ruler: w = Q(alpha, I, I(J-1)) times sqrt(MSE / J), where MSE is over J, the values per group. Two means differ if their gap is bigger than w.
- Rounding rule for calculations: never round the three pieces to whole numbers; keep two or more decimals (or use Ans and the calculator memory) and round only F at the end. Write F as "23.17 > 3.89", with the context sentence for the interpretation (for example, "mean plant growth differs for at least two of the fertilisers").
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
table lookups and recall slips in timed calculation work | seen in S5, S9 | S5: reading a P-value range off a t-table (still parked). S9: the wrong Q column (the 2-group column instead of the 3-group column) and three formula-recall asks in one practice run. The method was fine each time; what failed was reading the right column or holding the formula in memory. Fix: a closed-book recall check and one rehearsal of the table lookup (row = error df, column = number of groups)
```

## 5. Retest first (ranked)
0. Calculation drills before the theory test: (a) Q table lookup for different I and error df, with the whole table visible and the right column named; (b) closed-book recall of the SSTr computing formula, F's two df, and Tukey's ruler; (c) one 4 by 5 ANOVA with a Tukey follow-up, timed; (d) a close-call F where rounding SSE could flip the decision.
1. Which diagnostic plot checks which assumption (normal probability plot vs residuals versus fits). Show a pair of plots and ask what follows; include a funnel as well as a U shape.
2. Centre and width of a prediction interval given a confidence interval at the same x0. Give a different confidence interval, and make one distractor wide but off-centre.
3. Retention: totals vs means. A fresh S_xx or SSTr from totals, and ask for the sign check. Weight this one, since it has now slipped in two sessions.
4. Retention: paired design as a one-sample problem on differences (three sessions in a row). Use a new context that does not say "before and after".
5. Retention: regression df for a model with more than one predictor, and Total = regression + error.
6. Retention: t squared = F, F is never negative, and the numerator df is the regression df.
7. Retention: r squared vs r, and which sum of squares goes underneath.
8. Retention, one question at most each: MSE vs MSTr, Q subscripts, the SST proof pieces, Tukey's family error rate (all answered correctly in S9).
9. Parked: choosing n for a worded subgroup proportion claim, and reading a P-value range off a t-table (only if the next lecture supplies material).
