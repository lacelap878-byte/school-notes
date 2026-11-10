Supersedes S1 to S6. This is the only handoff file needed.

# STA01B1 Handoff S7 (Paired Data, Two Proportions and Two Variances)

## 1. Objective (this session)
Generate CDG v6 notes for Lecture 8 (Devore and Berk Ch 9, sections 9.3 to 9.5: the paired t test and interval, inference on two population proportions, inference on two population variances) from Lecture 8.pdf. Read image-only slides from user-supplied screenshots, take the proportion test boxes from user-supplied textbook excerpts, resolve the proportion branch of the open distribution/test choice item, build the 30 versus 40 threshold table, and draft a clarification email to the lecturer. Then produce Memo.

## 2. Topic ledger
```
S1 | Statistics and Sampling Distributions                    | full | open struggle no
S2 | Point Estimation                                         | full | open struggle no
S3 | Statistical Intervals                                    | full | open struggle no
S4 | Intervals Based on a Normal Population                   | full | open struggle no
S5 | Hypothesis Testing                                       | full | open struggle yes
S6 | Inferences Based on Two Samples                          | full | open struggle yes
S7 | Paired Data, Two Proportions and Two Variances           | full | open struggle yes
```

## 3. Notes index
```
S1 | Statistics and Sampling Distributions | STA01B1_Notes_S1_Statistics_and_Sampling_Distributions.md | statistic vs parameter, sampling distribution of Xbar and To, CLT, how large is large
S2 | Point Estimation | STA01B1_Notes_S2_Point_Estimation.md | point estimators, unbiasedness, MVUE, standard error, p-hat as Xbar
S3 | Statistical Intervals | STA01B1_Notes_S3_Statistical_Intervals.md | CI for mean (known/large-sample unknown sigma), CI for proportion, sample size planning, one-sided bounds
S4 | Intervals Based on a Normal Population | STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population.md | t interval, prediction interval, CI for the variance
S5 | Hypothesis Testing | STA01B1_Notes_S5_Hypothesis_Testing.md | H0/Ha, Type I/II error, rejection regions, Case I/II Z tests for a mean
S6 | Inferences Based on Two Samples | STA01B1_Notes_S6_Inferences_Based_on_Two_Samples.md | distribution of Xbar-Ybar, z test known/large-sample variance for two means, large-sample CI, pooled t test and CI, Sp^2
S7 | Paired Data, Two Proportions and Two Variances | STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances.md | paired t test and CI, E and V of p1-hat minus p2-hat, two-proportion z test and CI, F test for two variances, 30 vs 40 threshold table
```

## 4. Content summary
S1: compressed, unchanged in substance (sampling distributions, CLT, statistic vs parameter).
S2: compressed, unchanged in substance (point estimation, unbiasedness, MVUE, standard error).
S3: compressed, unchanged in substance (confidence intervals for a mean and a proportion, sample size planning, one-sided bounds).
S4: compressed, unchanged in substance (t interval, prediction interval, variance CI).
S5: compressed, unchanged in substance (hypothesis tests, Type I/II error, Case I/II Z tests for a mean).
S6: compressed, unchanged in substance (distribution of Xbar-Ybar, two-sample z tests and CI, pooled t, first P-value and its doubling).

S7, this session, in detail: Built Lecture 8 live under CDG v6 across 7 parts. The part map was revised once before Part 1: the original split put the paired CI and its example across two parts, and after reading the image-only slides it became one part per topic (total unchanged at 7).
Part 1, paired t setup (slides 1 to 6): tyre wear example, the same data analysed as independent vs paired (t 0.574, P .582 vs t 12.829, P .0002), assumptions on the differences D_i, test statistic t = (dbar - Delta0)/(sD/sqrt n). Part 2, Example 9.9 (slides 7 to 9): arm elevation study, n = 16, dbar 6.75, sD 8.234, t = 3.28 vs t(.025,15) = 2.131, reject (alpha .05 assumed, not stated in source). Part 3, paired CI, Example 9.10 (slides 10 to 12): medical image retrieval, n = 13, worked as a composite (Tier 3, alpha .05 assumed) since the source gave data and a normality check but no working. Part 4, difference of two proportions (slides 13 to 15): X ~ Bin(m,p1), Y ~ Bin(n,p2) independent, E(p1hat - p2hat) = p1 - p2 and V = p1q1/m + p2q2/n, with an added derivation because the slide defers the proof to textbook page 492. Part 5, two-proportion z test, Example 9.11 (slides 16 to 19): pooled phat, z = (p1hat - p2hat)/sqrt(phat qhat (1/m + 1/n)), plea and sentencing data, z = -4.94, P-value bounded at .0004 using the last table row 3.49. Part 6, CI for p1 - p2, Example 9.13 (slides 20 to 22): unpooled, chemotherapy vs hybrid treatment, (-.247, .039) at 99%. Part 7, F test for two variances, Example 9.14 (slides 23 to 27): theorem F = (S1^2/sigma1^2)/(S2^2/sigma2^2) on (m-1, n-1) df, baked goods data, f = 8.37, worked in two versions (slide alpha .02 with F.01,5,7 = 7.46; lecture illustration alpha .10 with F.05,5,7 = 3.97 confirmed by the user against the textbook table), plus the larger-variance-on-top shortcut which slide 26 itself states.

Sources beyond the slides this session, all labelled in the notes: user-supplied textbook boxes for the one-sample and two-sample proportion tests (the source of the validity condition of 10 successes and 10 failures), and user-supplied screenshots for image-only slides 7, 8, 9, 12, 17, 18, 19, 21, 22, 25, 26.

Correction to Part 3 as first delivered in chat: the sample standard deviation of the 13 differences was given as 11.61. The correct value is 11.96 (sum of squared differences 7201, minus 267^2/13, divided by 12, giving a variance of 143.10). The corrected 95% interval is (13.31, 27.77), not (13.52, 27.56). This notes file carries the corrected numbers throughout; the version delivered live in chat for hand-copying still has the arithmetic slip and needs the same fix applied by hand.

Conceptual discussion, folded into the notes: why paired data removes shared between-subject noise and what it does not control; whether the t distribution is always used (it is not: the paired test is a one-sample problem on D_i, so the usual known-variance, sample size and normality conditions apply); what changes at 30 vs 40 (the arithmetic is the same, only the label, the table and the stated justification differ); why proportion procedures use Z and never t (the variance is built from p itself); the P-value bound at the table edge; the correction that the larger-variance-on-top shortcut is in the slides, not only the lecturer's method; how the lecturer marks (a wrong table value or wrong alpha with a correct setup costs one mark, unconfirmed with the lecturer).

Threshold finding: Lecture 5 (S5, Case II test, slide 9) says n > 30. Lecture 7 (S6, large-sample z test and CI, slides 3 and 4) says m > 40 and n > 40. The S3 large-sample CI says n > 40, with an added rationale in the vault (substituting S adds variability beyond the CLT). Nothing in the slides reconciles 30 with 40. The pooled t test slide says m < 40 and n < 40 while its CI slide says m < 40 and/or n < 40. Lecture 8 gives no cutoff for the two-proportion procedures ("Large samples" only), and the F test has none. The full threshold table is in the S7 notes file. Resolved afterwards by the lecturer: use 40 throughout (see section 6).

## 5. Last position
Lecture notes: complete, all 27 slides of Lecture 8 covered (title slide contributes nothing, slide 27 is a reference to Chapter 9 sections 9.3 to 9.5). Struggle log checked and updated. Memo produced this message.

## 6. Parked items
1. Choosing n for a worded subgroup proportion claim ("proportion of X within Y" vs "proportion of X who are Y"). Not in Lecture 8. Still parked (S5, S6, S7).
2. Reading a P-value range off a printed t-table (fixed columns only). Example 9.9 used a rejection region and no P-value, so the chance to introduce it passed again. Still parked.

Lecturer's reply received and applied to the S7 notes (all four questions closed):
1. Large-sample cutoff for a mean: use m > 40 (and n > 40) throughout. The S5 Case II n > 30 is superseded. The S5 notes file has been corrected to 40.
2. Two proportions: use the textbook rule (all of m*p1hat, m*q1hat, n*p2hat, n*q2hat at least 10), applied strictly. Example 9.11 has n*q2hat = 8 and fails it.
3. Pooled t: "m < 40 and/or n < 40" is intentional and is the rule. Her reply does not separately mention the test slide, which prints "and"; and/or is used for both.
4. F test: use the table correctly; the df and alpha asked for will be in the exam table. The alpha .10 illustration was a lecture-only workaround. The larger-variance-on-top shortcut was not contradicted.
Idea under consideration by the user, undecided: a standalone stats definitions file linked from session notes.

Resolved and closed this session (no longer parked): proportion tests always use Z, with the validity condition at 10, not 5 (the 5 was a placeholder in the S5 memo and its resume block, carried into the S6 memo, never a rule stated in any notes file).

## 7. Resume block
```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG
protocol file and this handoff memo. My notes on Lecture 8 (Devore and
Berk 9.3 to 9.5) are complete: the paired t test and CI (Examples 9.9 and
9.10, the latter worked as a composite), the mean and variance of
p1-hat minus p2-hat, the two-proportion z test (Example 9.11) and CI
(Example 9.13), and the F test for two variances (Example 9.14, in two
versions: the slide's alpha .02 and the lecture's alpha .10 illustration).
The notes file carries a 30 vs 40 threshold table.

Two items are parked because Lecture 8 doesn't cover them: choosing n for
a worded subgroup proportion claim, and reading a P-value range off a
printed t-table. Please check Lecture 9 (single-factor ANOVA) against them.

My lecturer has answered the four questions and the S7 notes now carry
her answers: use n > 40 throughout for a mean (the S5 n > 30 is
superseded), apply the two-proportion condition of 10 successes and 10
failures strictly (Example 9.11 fails it at n*q2-hat = 8), the pooled t
condition is "and/or", and use the exam F table correctly at the stated
alpha (the alpha .10 was a lecture-only workaround). My S5 notes file
has already been corrected to 40.

Lecture 9 is single-factor ANOVA, the natural next step after comparing
two variances and two means, and it uses an F statistic.
```
