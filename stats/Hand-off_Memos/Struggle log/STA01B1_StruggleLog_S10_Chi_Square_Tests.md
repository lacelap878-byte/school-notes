Supersedes S1 to S9.

# STA01B1 Struggle Log S10 (Chi-Square Tests)

Evidence rule used below: every miss carries the exact wrong answer and the check that shows why it is wrong. For S10 the checks are hand calculations repeated by script (numpy and scipy), or the stated rule from the lecture. Where the verdict rests on the lecture's rule alone, the line says so.

## 1. Open items (unresolved, oldest first)
```
choosing n for a worded subgroup proportion claim | first seen S5 | "proportion of X within Y" vs "proportion of X who are Y" changes which n to use; no lecture on file has posed this kind of question. Lecture 11 (chi-square) has no sample-size planning, so the chance to meet it passed again | 6
reading a P-value range off a printed t-table | first seen S5 | fixed columns only, not continuous like the Z table. The lecturer said for Summative Assessment 2 that P-values are calculated only for z tests, so this may be out of scope for the final; Solution 11 and slide 16 do quote P-value ranges for chi-square tests, so the final's rule is unsettled. Do not drill it until the lecturer answers (an older summary file has an outdated bracketing tip) | 6
source inconsistencies pending the lecturer | first seen S6 | the S6 to S8 cutoff questions are answered (n > 40, strict 10-and-10, and/or, exam table at the stated alpha). Still open: Lecture 10 slide 17 has a blank SSE formula, slides 19 and 20 have notation and wording problems, slides 28 and 29 use alpha and beta, Chapter 10 vs 11 vs 12 numbering. New from Lecture 11: dots on n_i and n_j, r and c vs I and J, P-values for chi-square, the 5 vs 10 validity rule for a 2 by 2 table, a 2021 date stamp, and 11.60 vs 11.65 in Solution 11 question 44. A gap in the source, not a recognition failure | 5
which diagnostic plot checks which assumption | first seen S9 | S9 miss: given a straight normal plot and a U-shaped residuals-versus-fits plot, picked "normality is violated, because the residual plot shows a pattern". S10: answered correctly at the start (straight normal plot and a fan on residuals versus fits: "normality looks fine; the equal-variance assumption is doubtful"), but the student said they did not understand the second half of the question, the residuals. Explained with a picture: a residual is the vertical distance from a point to the line, the residuals-versus-fits plot is the same picture with the line laid flat, a band of even width is fine, a fan is unequal variance, a U shape is the wrong model. A correct answer without the reading behind it does not close the item | 2
df for goodness of fit is groups minus one, not people minus one | first seen S10 | in the flexible working hours example (40 employees, 4 groups) the student wrote "39 is the df". Evidence: df = k - 1 = 4 - 1 = 3, and the cut-off the student then read, chi-square .10 with 3 df = 6.251, was right. 39 is the n - 1 of the t test. A multiple choice question on the same rule (200 people, 5 categories, answer 4) was answered correctly, so the slip shows in written work | 1
conclusion wording after a failure to reject | first seen practical test prep, 13 Oct 2026 (outside the CDG chain; also "fail to reject the alternative" there); seen again S10 | exact wrong answer, written after the correct decision (chi-square 5.6 against 6.251, fail to reject H0): "at 10 percent confidence level, the alternate hypothesis is rejected". Evidence: 5.6 < 6.251 recomputed by script, so H0 is not rejected; a test never rejects the alternative; 10 percent is a significance level. A multiple choice version of the same wording, at the end of S10, was answered correctly (option "not sufficient evidence"), so the slip shows in the student's own written sentence. Right form: "At the 10% level there is not sufficient evidence that employees' feelings about the proposal differ" | 2
choosing chi-square or ANOVA | first seen S10 | quiz question (300 bank customers, 3 branches, satisfied or not): picked "ANOVA, with df = 2 and 297". Evidence: each customer has two labels and no measurement, so the data are counts in a 3 by 2 table, a chi-square test of independence with df = (3 - 1)(2 - 1) = 2. Three groups do not make a problem ANOVA | 1
expected count in a two-way table | first seen S10 | quiz question (row total 40, column total 30, n = 100): picked 35 (the average of the two totals). Evidence: 40 x 30 / 100 = 12; and 35 cannot be right because an expected count cannot exceed its column total of 30. In the worked faculty table the student then gave 21.24 for 34 x 63 / 100 where the value is 21.42 (digits swapped; recomputed by script). The student said they did not understand why the totals are multiplied; explained as independence meaning chances multiply, then times n | 1
the assumption is about expected counts | first seen S10 | quiz question (3 by 3 table, all observed counts at least 6, one expected count 3.2): picked "the test is invalid, because a 3 by 3 table has too many degrees of freedom". Evidence: the lecture's assumption (slides 20 and 21) is that every expected count is at least 5, so 3.2 breaks it; the degrees of freedom are 4 and play no part in the rule. The student said they did not understand this question at all | 1
expected counts come from the claim in H0 | first seen S10 | quiz question (200 clients, claim 40%, 30%, 20%, 10%, expected count for the 30% course): answered 60, correct, but the student said it was a guess. Evidence: 200 x 0.30 = 60. The trap is 50, the equal split, which holds only when H0 says all groups are equally likely. In the flexible working example the student also asked how we know everything is supposed to be 10 (answer: it is what H0 claims, not a fact we know) | 1
degrees of freedom and the "forced last count" picture | first seen S10 | not a wrong answer but a misreading that returned each time df was explained as "the last one is forced": the student heard that the last roll, or the last cell, has no freedom of choice, and asked whether that changes if a fourth throw is added. Cleared in session (see section 2). Still open because the student could not yet say, in their own words, why df is 5 for six counts, and said that the old picture comes back when they hear "forced" | 1
copying and adding slips in written calculations | first seen ST2 prep, 7 Oct 2026 (outside the CDG chain); seen in S10 | S10: chi-square total written as 4.6 where the contributions 3.6, 0, 1.6 and 0.4 add to 5.6 (the cell that was off by exactly 1.0 was not identified), and 21.24 for 21.42. Earlier: MSE written 0.056633 for 0.056333, and 4.46 for 4.26 from the F table. The method was right each time. Fix: glance back at each number after writing it, and check the total against a rough size | 3
```

Carried unchanged from S9 (not retested this session):
```
rounding before the F ratio | first seen S9 | divided the rounded MSTr 98.065 by the rounded MSE 4.23 and got F = 23.18 instead of 23.17. The decision was unaffected, but SSE is found by subtraction, which magnifies rounding error, and the rule matters when F sits near the critical value. Keep two or more decimals and round only F at the end | 2
recalling formulas under time | first seen S9 | the F degrees of freedom and Tukey's ruler were each recalled only after a reminder in a timed run. A memory problem, not an understanding one: the fix is a closed-book recall check, not more explanation | 2
```

Retention checks (answered correctly, kept because the student says correct answers can still be forgotten):
```
paired design is a one-sample problem on the differences | first seen S7 | answered correctly at the start of S10 in a new context (12 employees each using two typing apps, picked the paired t test on 12 differences, df 11). It has now come up in four sessions | 4
totals vs means in S_xx and SSTr | first seen S8 | answered correctly at the start of S10 (3 groups of 4, totals 20, 28, 36, SSTr = 32, with the order check 588 < 620) | 4
centre and width of a prediction interval given a confidence interval | first seen S9 | answered correctly at the start of S10 with new numbers (CI 40.6 to 47.0 has midpoint 43.8, so the PI 36.1 to 51.5); closed under retest, kept on the watch list | 2
reading Q from the studentized range table: column = number of groups | first seen S9 | answered correctly at the start of S10 (4 groups of 6: column 4, row 20); the question was multiple choice, so a real table lookup is still the better retest | 2
regression df with more than one predictor; t squared = F and the sign of F; r squared vs r; full ANOVA table and decision from raw data; t vs F in ANOVA | first seen S9 | answered correctly in S9, not retested in S10 | 1
```

## 2. Resolved this session
```
the sum of the gaps is zero, so the last roll must be determined | resolved S10 | the student asked whether the last throw has no freedom of choice, and tested it with "at throw 59 I can see which face is behind, so throw 60 must be that face". The fixes that worked: a table of the six possible 60th rolls (the total under and over matched in every row, so nothing was forced); the first-throw check (the gaps already sum to zero after one throw, and nobody would call a first throw forced); and the sweets analogy (60 sweets to 6 kids with a fair share of 10: whatever one kid has over, the others are missing). The student said the first-throw check settled it. The zero total never predicts the next face, and a fair die has no memory (gambler's fallacy)
"always adding zero means no new information, so df is zero" | resolved S10 | the zero belongs to the total of the gaps, which is always 0 and tells nothing; each gap varies and tells something. Six gaps tied by one relationship leave 5 independent pieces: df = 6 - 1 = 5, not 0
expected value of one roll (3.5) vs expected count per face | resolved S10 | the student expected 3.5 where the expected count was 1 (6 rolls). Chi-square never looks at face values: the faces are labels, and the expected count is how many times each label should come up (chance x number of trials)
what an expected count is | resolved S10 | "the expected count, like what?" Answered with coin and die: chance x number of tries is the target the claim in H0 aims at, not a prediction that the count lands on it
what the score is | resolved S10 | "what is a score?": the chi-square statistic, the single number from the formula, the same kind of thing as z or t
why it is called chi-squared | resolved S10 | chi is the Greek letter; the 2 is part of the name because the statistic is a sum of squared z-scores
how a formula can connect to reality (the "it feels like magic" worry) | resolved S10 | built from the CLT: a count wobbles by about the square root of E, so (O - E) / sqrt(E) is a z-score, squaring it gives one term of the formula, and a sum of squared z-scores is chi-square. A shop with 100 expected customers a day made it concrete (Friday 108 is 0.8 wobbles, Tuesday 135 is 3.5 wobbles). A simulation of fair and loaded dice showed the pile of scores. The student then said they understood
does knowing the total make me a cheater against my brother | resolved S10 | no: the total says nothing about the next roll; only knowing the die is loaded would give an edge, and a chi-square test could in time detect that
```

## 3. Notation and terminology still causing trouble
- "Expected count" is the number of times a category should occur in n trials, from the claim in H0. It is not the expected value of a measurement. In goodness of fit it is n times p; in a two-way table it is row total times column total over n.
- "Score" in session talk means the chi-square statistic, also called the test statistic.
- Degrees of freedom: for goodness of fit, categories minus 1 (never people minus 1); for a table, (I - 1)(J - 1). Avoid the word "forced" when explaining df; say "unknowns minus equations" or "new information".
- Over and under: for each category, the amount by which its observed count is over or under its expected count. The total over always equals the total under.
- 10 percent (or 5 percent) is the significance level, not a confidence level.
- Rows and columns: slides 11 and 12 use r and c, the formulas use I and J. I is the number of rows and J the number of columns.
- Dots in ANOVA: x_ij (no dot), xbar_i. (one dot), xbar.. (two dots); a missed dot in the proof costs a mark (lecturer). In the chi-square lecture row and column totals are n_i and n_j with no dots.
- Totals vs means in the computing formulas: x_i. and x.. are totals with no bars.
- Q(alpha, I, I(J - 1)): second subscript I, third subscript the error df. In the table the column is the number of groups and the row is the error df.
- F for single-factor ANOVA: numerator df I - 1, denominator df I(J - 1).
- In regression, df is counted per slope: regression df = number of slopes, error df = n - k - 1, Total df = n - 1.
- Fits vs residuals: a fit is the line's predicted value at an observed x; the residual is observed minus fit, the vertical distance from the point to the line.
- x0 is a chosen x value, not necessarily a data point. The confidence interval at x0 is for the average y; the prediction interval is for one new y.
- Underscored or joined means in Tukey mean "not shown to differ", not "equal".
- Rounding: never round the three ANOVA pieces to whole numbers; round only F at the end.

## 4. Patterns across sessions
```
distribution and test choice | seen in S5, S6, S7, S8, S9, S10 | each lecture added one more fork to "which formula and which distribution apply here". S10 added the counts fork: if each person is described only by labels, it is chi-square (goodness of fit for one variable, independence or homogeneity for two); if a measurement is recorded on each person, it is t or ANOVA. The slip came from the number of groups (three branches pointed to ANOVA). The paired design remains the one that keeps recurring: S7, S8, S9, ST2 prep
the n - 1 reflex for degrees of freedom | seen in S10 | after the t tests and ANOVA, df = n - 1 came back for goodness of fit (39 for 40 people and 4 groups). The counting rule, unknowns minus equations, gives 3. This is a habit from one family of tests applied to another, not a gap in understanding
conclusion wording after a decision | seen in practical test prep (13 Oct), ST2 prep (alpha wording, 7 Oct), S10 | the decision is correct and the sentence that follows claims too much or says it backwards. The multiple choice versions are answered correctly, so it is the student's own written sentence that slips. Fix: a fixed template ("At the _% level there is (not) sufficient evidence that ... in context") practised as a written answer
copying and arithmetic slips in written work | seen in ST2 prep (7 and 8 Oct), S10 | right method, wrong digit (0.056633 for 0.056333, 4.46 for 4.26, 21.24 for 21.42, a total of 4.6 for 5.6). A glance back after each step and a rough size check catch them. Only becomes a problem on a timed paper
totals vs means in computing formulas | seen in S8, S9, S10 (correct at the start of S10) | the totals piece divided by the count inside it; the order check catches a negative sum of squares
source inconsistencies not reconciled by the slides | seen in S6 to S10 | pattern in the source, not a gap in understanding; the fix is external (the lecturer's answer)
table lookups and recall slips in timed work | seen in S5, S9 | wrong Q column, three formula recalls in one practice run. S10 added no lookup practice: a chi-square table lookup (row = df, column = tail area) went right when asked
explanations that sound like forcing | seen in S10 | any explanation of df or of the zero total that said "the last one is determined" brought back the picture that the dice are forced. Phrasings that worked: tables with concrete counts, the sweets story, the first-throw check, and "unknowns minus equations"
```

## 5. Retest first (ranked)
0. Open the next session with a short mixed written drill in new contexts (written, not multiple choice, because the slips show in written work):
   - a goodness of fit question with a percentage claim, checking E from the claim, df = k - 1, the cut-off and the conclusion sentence;
   - a two-way table with the totals given, checking E for one cell with the "cannot exceed its row or column total" check, and df = (I - 1)(J - 1);
   - a scenario that names three groups and records only labels, asking which test (chi-square or ANOVA) and why;
   - a table with one expected count below 5, asking whether the test can be used and what to do.
1. Conclusion wording after a failure to reject, as a written sentence in a new context (open since 13 Oct).
2. Degrees of freedom explained back in the student's own words, for six counts with a known total, without the word "forced".
3. Which diagnostic plot checks which assumption: show a pair of plots including a funnel, and ask for the reading of each plot in the student's own words (the residuals-versus-fits plot was not understood).
4. Copying slips: a timed calculation, with a glance back after each step.
5. Rounding before the F ratio, with a close call near the critical value.
6. Retention, one question each: paired design as a one-sample problem (new context), totals vs means, centre and width of a prediction interval, the studentized range table lookup with the real table, regression df for more than one predictor.
7. Parked: choosing n for a worded subgroup proportion claim. The P-value range off a t-table only if the lecturer says P-values are examinable for t.

---
*CDG v11 | written S10 | 2026-11-03*
