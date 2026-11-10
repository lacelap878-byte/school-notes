Supersedes S1 to S7. This is the only handoff file needed.

# STA01B1 Handoff S8 (Single-Factor ANOVA and Tukey's Procedure)

## 1. Objective (this session)
Generate CDG v8 notes for Lecture 9 (single-factor ANOVA, Devore and Berk Ch 10 / 11.1 to 11.2 as numbered on the slides) from Lecture 9.pdf: notation and assumptions, sums of squares, mean squares and the F test, the ANOVA table and computing formulas, the Breakfast Problem, Tukey's procedure (Examples 10.5 and 10.6), and the simultaneous confidence level behind Tukey's method. Add the lecturer's proof that SST = SSTr + SSE, which is not on the slides. Run the session-start revision quiz and the session-end check quiz. Then produce Memo.

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
S8 | Single-Factor ANOVA and Tukey's Procedure | STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md | ANOVA hypotheses, notation and dots, assumptions, SSTr/SSE/MSTr/MSE/F, ANOVA table, Breakfast Problem, proof that SST = SSTr + SSE, Tukey's HSD (Examples 10.5 and 10.6), simultaneous confidence level
```

## 4. Content summary
S1: compressed, unchanged in substance (sampling distributions, CLT, statistic vs parameter).
S2: compressed, unchanged in substance (point estimation, unbiasedness, MVUE, standard error).
S3: compressed, unchanged in substance (confidence intervals for a mean and a proportion, sample size planning, one-sided bounds).
S4: compressed, unchanged in substance (t interval, prediction interval, variance CI).
S5: compressed, unchanged in substance (hypotheses, Type I/II error, rejection regions, Case I/II Z tests).
S6: compressed, unchanged in substance (two-sample z and pooled t tests and CIs, Sp^2, why differences and not sums or quotients).
S7: compressed, unchanged in substance (paired t test and CI with the s_D = 11.96 correction, two-proportion z test and CI, F test for two variances, 30 vs 40 threshold table).

S8, in detail. Source: Lecture 9.pdf, slides 1 to 34 (slides 1 and 34 carry no content), read as images. Six parts, plus the proof, plus two quizzes.

Setup (slides 2 to 8): H0: mu1 = ... = muI against Ha: at least two differ. X_ij / x_ij double subscript. Sample mean xbar_i. = sum_j x_ij / J and grand mean xbar.. = sum_i sum_j x_ij / IJ, lowercase on the slides. Assumptions: each X_ij normal with E = mu_i and V = sigma^2 (homoscedasticity), rule of thumb that the largest sample SD is not much more than twice the smallest.

Sums of squares, mean squares, F (slides 9 to 13): SSTr = J sum_i (Xbar_i. - Xbar..)^2, SSE = sum_i sum_j (X_ij - Xbar_i.)^2 = (J-1)(S1^2 + ... + SI^2). MSTr = SSTr/(I-1), MSE = SSE/(I(J-1)), F = MSTr/MSE. ANOVA table with df I-1, I(J-1), IJ-1. Computing formulas use TOTALS with no bars: SST = sum sum x_ij^2 - x..^2/IJ, SSTr = sum x_i.^2/J - x..^2/IJ, SSE = SST - SSTr. The treatment definition on slide 13 has two forms: the double sum, and J times the single sum.

Breakfast Problem (slides 14 to 22): I = 3, J = 4, totals 37, 59, 53, grand total 149. SST = 122.9167, SSTr = 64.6667, SSE = 58.25, MSTr = 32.3333, MSE = 6.4722, F = 5.00 on 2 and 9 df, no decision stated on the slides. MSE is a pooled estimate of sigma^2 whether or not H0 holds (it is the average of the three group variances). MSTr inflates when the means differ. Three between/within pictures (no difference, partial, full).

Proof (not on the slides): SST = SSE + SSTr. The lecturer's proof, confirmed by the user as the one built in session. Eight moves: definition, add 0 as -xbar_i. + xbar_i., expand as a^2 + 2ab + b^2 keeping the middle term factored, name the ends (first piece = SSE with no J, last piece = SSTr because it has no j so the inner sum gives J), distribute the middle term over the first bracket, substitute the group-mean rule sum_j x_ij = J xbar_i. (first term) and J times a constant (second term), cancel the two identical terms with the summation left in place, done. The user reports the lecturer said a missed dot costs a mark and that the proof is likely worth 6 to 8 marks (a user report, not confirmed in writing).

Tukey (slides 23 to 33): used only after H0 is rejected. Pairwise CIs for mu_i - mu_j, I(I-1)/2 of them, controlling the simultaneous level. w = Q(alpha, I, I(J-1)) * sqrt(MSE/J), Tukey's HSD. Second subscript on Q is I and not I-1 as in F; third is the error df. Underline adjacent sorted means that differ by less than w; a joined pair means "not shown to differ", not "equal", and it is not transitive. Example 10.5 (oil filters): I = 5, J = 9, F = 37.84 against F(.05,4,40) = 2.61, Q(.05,5,40) = 4.04, w = .4, groups {5,3}, {2}, {4,1}; with xbar_2 = 14.15 the groups become {5,3} and {2,4,1}. Example 10.6 (rats and ethanol): I = 4, J = 5, SAS table F = 21.09, P = 0.0001, Q(.05,4,16) = 4.05, w = 17.47, means 32.76, 47.92, 61.54, 79.28; joined pairs 4-3 and 3-2 only; 1 vs 2 differs by 17.74, a tight call. Simultaneous level: .95^2 = .90, .95^3 = 86%, individual level for two independent intervals = 100 sqrt(.95)% = 97.5%. Tukey's intervals are not independent, so the .95^k arithmetic is only an illustration, but Q(.05) still controls the simultaneous level at 95% and Q(.01) at 99%. Alpha is the family (experimentwise) error rate.

Corrections issued against the hand-copied pages in session (the user should check the hand copy):
1. Computing formulas: x_i. and x.. are totals with no bars (Computational Formulae table and the Breakfast Problem working). 149 is the grand total.
2. Example 10.5: second subscript on Q is I and not I-1 as in F.
3. Example 10.5: delete the aside about xbar_2 = 14.15 bridging to 13.3. With 14.15, brand 2 joins the top group.
4. Breakfast Problem statement: "children" was invented. The slides give no scenario text.
5. The arrow into Example 10.6 said "unequal-looking data". The groups are balanced, J = 5 each.
6. Example 10.5: delete the added note saying the source writes k(I-1)/2. The slide says I(I-1)/2.
7. Simultaneous-level slide: three intervals all use xbar_1., not xbar_3.
8. Computational Formulae, treatment definition: add the double-sum form before the J times single-sum form.
9. Example 10.6: delete "and it is the one place a rounded MSE could matter". Rounding does not change the 1 vs 2 call.
10. Setup, sample mean and grand mean formulas: lowercase xbar on the slides (capital Xbar was used in the live page).
11. Em dashes appeared in several earlier live parts and are not allowed. The notes file has none.

Quizzes: session-start revision quiz (4 questions on S7): the user missed Q1 (paired design as a one-sample problem on differences). Session-end check quiz (8 questions): the user missed Q2, Q3, Q4, Q6, Q7 (screenshots supplied); Q1, Q5 and Q8 were not reported as missed and are treated as passed pending the user's confirmation. Q7 was reworded afterwards because its wording was unclear; the underlying gap is unconfirmed until retested with the actual expressions shown. Each miss was corrected on the spot and logged as open.

Sources beyond the slides this session: the lecturer's proof (as described and confirmed by the user). Everything else is from Lecture 9.pdf.

## 5. Last position
Part 6 of 6, "The Interpretation of alpha in Tukey's Procedure". All 34 slides covered. Proof added. Both quizzes run. Memo produced this message.

## 6. Parked items
1. Choosing n for a worded subgroup proportion claim ("proportion of X within Y" vs "proportion of X who are Y"). Not in Lecture 9. Still parked (S5 to S8).
2. Reading a P-value range off a printed t-table (fixed columns only). Lecture 9's F test is a straight rejection-region decision, Example 10.6 gives an exact SAS P-value, and Tukey uses the Q table, so the chance to introduce it passed again. Still parked (S5 to S8).

Open actions, waiting on the lecturer (email drafted, to be sent by the user; notes stay as written unless she says otherwise, then the user returns and the notes are changed):
1. Is the S5 Case II cutoff n > 30 intended, against n > 40 in the S3 and S6 large-sample procedures?
2. What large-sample condition applies to the two-proportion test and CI, and does the textbook rule of 10 successes and 10 failures carry over? Example 9.11 has n*q2hat = 8.
3. Is "m < 40 and/or n < 40" on the pooled t CI slide intentional, against "and" on the test slide?
4. Confirm the F shortcut uses F(alpha/2), and the alpha .10 illustration.
5. (new, low priority) Lecture 9 mixes Chapter 10 with Table 11.x and Example 11.x numbering, and captions the oil-filter ANOVA table as "Example 11.4" under a slide labelled Example 10.5. Is that intended?

## 7. Resume block
```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG
protocol file (v8) and this handoff memo together with the S8 struggle log.

Lecture 9 (single-factor ANOVA) is done as S8: hypotheses, notation with
the dots, assumptions, SSTr / SSE / MSTr / MSE / F, the ANOVA table and
the totals-not-means computing formulas, the Breakfast Problem, the
lecturer's proof that SST = SSTr + SSE, Tukey's procedure (Examples
10.5 and 10.6) and the simultaneous confidence level.

Run the session-start revision quiz first, drawn from the S8 struggle log
in this order: MSE vs MSTr when H0 is false; SSTr computing formula with
totals not means; the third subscript of Q (error df, not total df);
which piece of the SST expansion is SSE and which is SSTr and where the
J goes (show the actual expressions in the question); Tukey's joint level
vs individual level; and one check that a paired design is a one-sample
problem on the differences. Make the questions rigorous, not recognition
level, and address any miss on the spot.

Two items are parked because no lecture yet covers them: choosing n for
a worded subgroup proportion claim, and reading a P-value range off a
printed t-table. Check the next lecture against them.

Five questions for my lecturer are drafted and pending (the n > 30 vs
n > 40 cutoff, the large-sample condition for two proportions, "and" vs
"and/or" on the pooled t slides, the F shortcut with alpha .10, and the
Chapter 10 vs 11 numbering). If she confirms the notes as written, leave
them. If she says otherwise, I will tell you what to change.

Before delivering any part, check formulas, subscripts and dots against
the slide images.
```
