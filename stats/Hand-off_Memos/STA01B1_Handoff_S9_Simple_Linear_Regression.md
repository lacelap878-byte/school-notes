Supersedes S1 to S8. This is the only handoff file needed.

# STA01B1 Handoff S9 (Simple Linear Regression)

## 1. Objective (this session)
Generate CDG v8 notes for Lecture 10 (simple linear regression, Chapter 12 as numbered on the slides) from Lecture 10.pdf: scatter plots, the probabilistic model, least squares, the total sum of squares and its split, r and r squared, the ANOVA table for regression, the t and F tests for the slope, cautions, residual diagnostics, and the confidence and prediction intervals at x0. The copy-ready pages were kept short on purpose (three parts, about 4 to 5 notebook pages) because the notebook is nearly full, and the notes file was written at full depth. Run the session-start revision quiz and the session-end check quiz. Then produce Memo.

## 2. Topic ledger
```
S1 | Statistics and Sampling Distributions                    | full | open struggle no
S2 | Point Estimation                                         | full | open struggle no
S3 | Statistical Intervals                                    | full | open struggle no
S4 | Intervals Based on a Normal Population                   | full | open struggle no
S5 | Hypothesis Testing                                       | full | open struggle yes
S6 | Inferences Based on Two Samples                          | full | open struggle yes
S7 | Paired Data, Two Proportions and Two Variances           | full | open struggle yes
S8 | Single-Factor ANOVA and Tukey's Procedure                | full | open struggle yes
S9 | Simple Linear Regression                                 | full | open struggle yes
```

## 3. Notes index
```
S1 | Statistics and Sampling Distributions | STA01B1_Notes_S1_Statistics_and_Sampling_Distributions.md | statistic vs parameter, sampling distribution of Xbar and To, CLT, how large is large
S2 | Point Estimation | STA01B1_Notes_S2_Point_Estimation.md | point estimators, unbiasedness, MVUE, standard error, p-hat as Xbar
S3 | Statistical Intervals | STA01B1_Notes_S3_Statistical_Intervals.md | CI for mean (known/large-sample unknown sigma), CI for proportion, sample size planning, one-sided bounds
S4 | Intervals Based on a Normal Population | STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population.md | t interval, prediction interval, CI for the variance
S5 | Hypothesis Testing | STA01B1_Notes_S5_Hypothesis_Testing.md | H0/Ha, Type I/II error, rejection regions, Case I/II Z tests for a mean (Case II cutoff now n > 40 per the lecturer)
S6 | Inferences Based on Two Samples | STA01B1_Notes_S6_Inferences_Based_on_Two_Samples.md | distribution of Xbar-Ybar, z test known/large-sample variance for two means, large-sample CI, pooled t test and CI, Sp^2
S7 | Paired Data, Two Proportions and Two Variances | STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances.md | paired t test and CI, E and V of p1-hat minus p2-hat, two-proportion z test and CI, F test for two variances, 30 vs 40 threshold table
S8 | Single-Factor ANOVA and Tukey's Procedure | STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md | ANOVA hypotheses, notation and dots, assumptions, SSTr/SSE/MSTr/MSE/F, ANOVA table, Breakfast Problem, proof that SST = SSTr + SSE, Tukey's HSD (Examples 10.5 and 10.6), simultaneous confidence level
S9 | Simple Linear Regression | STA01B1_Notes_S9_Simple_Linear_Regression.md | probabilistic model and assumptions on epsilon, least squares (with derivation), fits and residuals, Total SS = SSR + SSE (with proof), r and r squared, regression ANOVA table, why regression df is 1, t and F tests (t squared = F), cautions, diagnostic plots, CI and PI at x0, one composite example carried from the line to the intervals
```

## 4. Content summary
S1: compressed, unchanged in substance (sampling distributions, CLT, statistic vs parameter).
S2: compressed, unchanged in substance (point estimation, unbiasedness, MVUE, standard error).
S3: compressed, unchanged in substance (confidence intervals for a mean and a proportion, sample size planning, one-sided bounds).
S4: compressed, unchanged in substance (t interval, prediction interval, variance CI).
S5: compressed, unchanged in substance (hypotheses, Type I/II error, rejection regions, Case I/II Z tests; Case II cutoff corrected to n > 40).
S6: compressed, unchanged in substance (two-sample z and pooled t tests and CIs, Sp^2, why differences and not sums or quotients).
S7: compressed, unchanged in substance (paired t test and CI with the s_D = 11.96 correction, two-proportion z test and CI with the strict 10-and-10 condition, F test for two variances, 30 vs 40 threshold table now settled at 40).
S8: compressed. Single-factor ANOVA: H0 all means equal, double-subscript notation and the dots, normality and equal variance, SSTr / SSE / MSTr / MSE / F, the ANOVA table and the totals-not-means computing formulas, the Breakfast Problem, the lecturer's proof that SST = SSTr + SSE (likely 6 to 8 marks, a missed dot costs a mark), Tukey's HSD with Q(alpha, I, I(J-1)) and Examples 10.5 and 10.6, and the family error rate behind Tukey.

S9, in detail. Source: Lecture 10.pdf, 31 slides numbered as printed (slide 1 title, slide 31 blank). Read as images, because the text layer lost Greek letters and formula layout. Three parts, plus the notes file, plus two quizzes.

Model (slides 2 to 11): regression predicts y from the x_i. Scatter plot reads form, strength and unusual observations. Deterministic y = b0 + b1 x versus probabilistic y = b0 + b1 x + epsilon, with line of means E(y) = b0 + b1 x and epsilon normal with mean 0 and common variance sigma^2.

Least squares (slides 12 and 13): minimise SSE = sum (y_i - b0 - b1 x_i)^2. b1 = Sxy/Sxx, b0 = ybar - b1 xbar, Sxy = sum xy - (sum x)(sum y)/n, Sxx = sum x^2 - (sum x)^2/n. The line passes through (xbar, ybar). Added in the notes: derivation from the two partial derivatives, giving sum e = 0 and sum x e = 0.

Strength and the split (slides 14 to 18): r = Sxy / sqrt(Sxx Syy), r^2 = Sxy^2/(Sxx Syy) = SSR/Total SS (slide marks the last one NB). Total SS = Syy = sum (y - ybar)^2 = sum y^2 - (sum y)^2/n. SSR = sum (yhat - ybar)^2. Total SS = SSR + SSE. ANOVA table: df 1, n-2, n-1, MSR = SSR/1, MSE = SSE/(n-2), F = MSR/MSE. Added: proof that Total SS = SSR + SSE (the cross term vanishes by the two conditions), SSR = b1^2 Sxx = b1 Sxy = Sxy^2/Sxx.

Tests and cautions (slides 19 to 22): t test of H0 slope = 0 with t = (b - beta_0)/sqrt(MSE/Sxx) as printed (beta_0 there is the hypothesised slope, so t = b1/sqrt(MSE/Sxx) on n-2 df). F = MSR/MSE, reject if F > F_alpha with 1 and n-2 df, equivalent to the t test with t^2 = F (added proof). Not rejecting slope = 0 does not mean unrelated (Type II error, nonlinear relationship). Cautions: wrong model, extrapolation, causality.

Diagnostics and intervals (slides 23 to 30): residual = y - yhat, normal with mean 0 and variance sigma^2 if assumptions hold. Normal probability plot of residuals (straight rising line for normality), residuals versus fits (random scatter around zero for equal variance). Estimate of average y or particular y at x0 is yhat = b0 + b1 x0. CI = yhat +/- t(alpha/2, n-2) sqrt(MSE(1/n + (x0 - xbar)^2/Sxx)); PI = yhat +/- t(alpha/2, n-2) sqrt(MSE(1 + 1/n + (x0 - xbar)^2/Sxx)). The only difference is the extra 1; both are centred on yhat; both narrowest at xbar.

Composite example (no source data on the slides): (1,2), (2,3), (3,5), (4,6). Sxx 5, Sxy 7, Syy 10, b1 1.4, b0 0.5, r^2 0.98, SSR 9.8, SSE 0.2, MSE 0.1, F 98, t 9.90 (t^2 = F), residuals 0.1, -0.3, 0.3, -0.1. At x0 = 3: CI (3.95, 5.45), PI (3.15, 6.25). Also x0 = 2.5 and x0 = 6 in the notes table.

Source problems found (all in the S9 notes under Where the source is inconsistent): slide 17 SSE formula blank; slide 19 uses beta_0 for the hypothesised slope; slide 20 states H0 as "model is useful" (backwards, should be slope 0); slides 28 and 29 use alpha and beta for the line of means; slide 14 uses Syy before slide 16 defines it; Chapter 10, 11, 12 numbering mixed; Examples 12.1, 12.2, 12.4 and 12.12 are named with no data.

Session discussion folded into the notes: why both t and F (same test for one x, t squared = F; they differ with several x's); why regression df is 1 (counting free numbers: Total 3, Error 2, Regression 1 for the example, so df = number of slopes, error df = n - k - 1); what the fits are (the line's predicted value at each x_i, not group means; they average ybar); what "at x0" means (the x you choose, with the sales and R50k illustration); what the slide pictures show (normal plot, residual plot, two lines on a hump, true line versus fitted line).

Quizzes. Session-start revision quiz (6 questions on the S8 items): the user missed Q2 (SSTr from totals, a guess after getting a negative value) and Q6 (paired design, picked the pooled two-sample t); Q1, Q3, Q4, Q5 correct. Session-end check quiz (7 questions): the user missed Q5 (which plot checks which assumption: picked "normality is violated" for a U-shaped residuals-versus-fits plot) and Q6 (centre and width of a prediction interval given a confidence interval, a complete guess, picked a wide interval centred in the wrong place); Q1 (S_xx from totals, passed), Q2 (df for two predictors), Q3 (t squared = F), Q4 (r squared and r), Q7 (paired design) correct and not guessed. The user said the correct ones could still be forgotten, so they are logged as retention checks ranked below the two real misses.

Notes: the page budget affects only the hand-copied parts. The notes.md stays full length or more expansive (user instruction this session).

## 5. Last position
Part 3 of 3, "Diagnostics, confidence and prediction intervals". All slides 2 to 30 covered. Both quizzes run. Memo produced this message.

## 6. Parked items
1. Choosing n for a worded subgroup proportion claim ("proportion of X within Y" vs "proportion of X who are Y"). Not in Lecture 10. Still parked (S5 to S9).
2. Reading a P-value range off a printed t-table (fixed columns only). Lecture 10's t test has no worked numbers on the slides and the composite example used a rejection decision, so the chance to introduce it passed again. Still parked (S5 to S9).

Resolved and closed by the lecturer (her written reply, recorded this session): use n > 40 throughout for a mean (S5 Case II slide's n > 30 is superseded; the S5 notes file was corrected); apply the two-proportion condition of 10 successes and 10 failures strictly (Example 9.11 fails it at n*q2hat = 8); the pooled t condition "m < 40 and/or n < 40" is intended; use the exam F table correctly at the stated alpha (the alpha .10 was a lecture-only workaround). The S8 handoff still listed these four as pending, because that file was written in a separate chat before the reply was carried over. They are closed here.

Open actions, waiting on the lecturer:
1. Slide 17 of Lecture 10: the formula under "Sum of squares for error" is blank. Probable omission. (The user said they will ping her.)
2. Optional, to raise at the same time: slide 20 states H0 as "model is useful" (should be slope 0); slide 19 uses beta_0 for the hypothesised slope; slides 28 and 29 write the line of means with alpha and beta.
3. Lecture numbering mixes Chapter 10, 11 and 12, and captions the oil-filter ANOVA table as Example 11.4 under a slide labelled Example 10.5. Is that intended? Low priority, carried from S8.

To-do on a vault file: the S8 notes file (STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md) still says, under "Where the source is inconsistent", that the earlier cutoff questions are "still waiting on the lecturer's answer". They have been answered (see above). That sentence needs updating. Send the S8 notes file next session, or ask for it, and the line will be fixed.

## 7. Resume block
```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG
protocol file (v8) and this handoff memo together with the S9 struggle log.

Lecture 10 (simple linear regression) is done as S9: the probabilistic
model and its assumptions, least squares, fits and residuals, Total SS =
SSR + SSE, r and r squared, the regression ANOVA table and why the
regression df is 1, the t and F tests for the slope (t squared = F),
cautions, the two residual diagnostic plots, and the confidence and
prediction intervals at x0. Lecture 11 is the last lecture of the module.

Run the session-start revision quiz first, drawn from the S9 struggle log
in this order: which diagnostic plot checks which assumption (normal plot
versus residuals versus fits); the centre and width of a prediction
interval given a confidence interval at the same x0; then a few retention
checks, one question each: S_xx or SSTr from totals with a sanity check
on the sign, regression and error df for a model with more than one
predictor, t squared = F and the sign of F, r squared versus r, and a
paired design as a one-sample problem on differences. Make the questions
rigorous, not recognition level, and address any miss on the spot.

Two items are parked because no lecture yet covers them: choosing n for a
worded subgroup proportion claim, and reading a P-value range off a
printed t-table. Check Lecture 11 against them.

Lecturer questions pending: the blank SSE formula on slide 17 of Lecture
10 (and, optionally, the slide 19 and 20 wording and the alpha and beta
notation on slides 28 and 29), and the Chapter 10 versus 11 versus 12
numbering. The earlier four cutoff questions are answered (n > 40, strict
10-and-10 rule, and/or, exam F table at the stated alpha). The S8 notes
file still has a line saying they are pending; I will send that file so
the line can be fixed.

Practical notes: my notebook is nearly full (roughly 6 pages left after
S9, an estimate), so the copy-ready parts for the last lecture must be
compact, likely review mode and few parts. The notes.md file stays full
length or more expansive. Before delivering any part, check formulas,
subscripts and dots against the slide images, because the PDF text layer
loses Greek letters and formula layout.
```
