Supersedes S1 to S5. This is the only handoff file needed.

# STA01B1 Handoff S6 (Inferences Based on Two Samples)

## 1. Objective (this session)
Generate CDG v6 notes for Lecture 7 (Devore and Berk Ch 9.1 to 9.2, Inferences Based on Two Samples) from Lecture_7.pdf, close a source gap on the pooled variance formula using a user-supplied section 9.2 excerpt, work Example 9.7 as a composite since the source gives no working, check the S5 struggle log and parked items against this lecture, then produce Memo.

## 2. Topic ledger
```
S1 | Statistics and Sampling Distributions            | full | open struggle no
S2 | Point Estimation                                 | full | open struggle no
S3 | Statistical Intervals                             | full | open struggle no
S4 | Intervals Based on a Normal Population             | full | open struggle no
S5 | Hypothesis Testing                                 | full | open struggle yes
S6 | Inferences Based on Two Samples                     | full | open struggle yes
```

## 3. Notes index
```
S1 | Statistics and Sampling Distributions | STA01B1_Notes_S1_Statistics_and_Sampling_Distributions.md | statistic vs parameter, sampling distribution of Xbar and To, CLT, how large is large
S2 | Point Estimation | STA01B1_Notes_S2_Point_Estimation.md | point estimators, unbiasedness, MVUE, standard error, p-hat as Xbar
S3 | Statistical Intervals | STA01B1_Notes_S3_Statistical_Intervals.md | CI for mean (known/large-sample unknown sigma), CI for proportion, sample size planning, one-sided bounds
S4 | Intervals Based on a Normal Population | STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population.md | t interval, prediction interval, CI for the variance
S5 | Hypothesis Testing | STA01B1_Notes_S5_Hypothesis_Testing.md | H0/Ha, Type I/II error, rejection regions, Case I/II Z tests for a mean
S6 | Inferences Based on Two Samples | STA01B1_Notes_S6_Inferences_Based_on_Two_Samples.md | distribution of Xbar-Ybar, z test known/large-sample variance for two means, large-sample CI, pooled t test and CI, Sp^2
```

## 4. Content summary
S1 to S4: compressed, unchanged in substance (sampling distributions and CLT; point estimation and MVUE; confidence intervals, large sample and proportion; t interval, prediction interval, variance CI).
S5: compressed, unchanged in substance (hypotheses and test procedure, Type I/II error, rejection region and the alpha/beta trade-off, standardising to Z, Case I/II Z tests for a mean, Examples 8.4 to 8.8).

S6, this session, in detail: Built Lecture 7 live under CDG v6 across 5 parts. Part 1 set up the shared assumptions and derived the mean and variance of Xbar-Ybar. Part 2 covered the z test for two means with known variances, Example 9.1 (GPA vs study hours). Part 3 covered the large sample z test substituting S1^2 and S2^2, Example 9.4 (control vs experimental teaching method), which also produced this course's first P-value and its two-tailed doubling. Part 4 covered the large sample CI for mu1-mu2, Example 9.5 (fall vs spring ACT scores), delivered in plain page format on the user's request (no wikilinks or callouts, LaTeX retained) since this was a hand-copy session. Part 5 covered the pooled two sample t test and CI. The source's own gap on the S_p^2 formula (referenced on slide 15 as "NB!!! Bottom of Page 377" but never given) was closed using a user-supplied excerpt of Devore and Berk section 9.2 (source: user-transcribed), which supplied S_p^2, its degrees of freedom m+n-2, and the textbook's own caution on preferring the two-sample t over the pooled t when normality or equal variances are in doubt. Example 9.7 (liner tensile strength, no fusion vs fused) had data and plots in the source but no worked solution, so it was worked as a composite (Tier 3, alpha=.05 assumed, not stated in source) covering both the test and the CI.

After Part 5, the S5 struggle log was checked against this lecture's material: the open Z vs t distribution-choice item is now half narrowed, the two-sample-means side is fully resolved by this lecture's three-way fork (Part 2/3/5), the proportion side remains open. Of the four S5 parked items, P-value doubling is resolved this session (Example 9.4); proportion tests with the n*p-hat>=10 condition, subgroup n selection, and t-table P-value reading all remain parked, none appear in Lecture 7's slides. The user also asked a conceptual question, answered in chat only, on why inference targets a difference of two means rather than a sum, product, or ratio, and how comparing more than two means generalises to ANOVA (Lecture_9.pdf). This is folded into the notes file as an (added) aside, not sourced from Lecture 7's slides.

## 5. Last position
Lecture notes: complete, all 21 slides of Lecture_7.pdf covered (title and closing reference slide contribute nothing).
Struggle log checked and folded in. Memo produced this message.

## 6. Parked items
1. Proportion hypothesis tests always using Z (never t), and the validity condition $n\hat{p}_0 \ge 5$ (or $\ge 10$ per the user-supplied 9.4 excerpt for the two-sample CI case). Not in Lecture 7's slides, no proportion test or CI appears in this source. Belongs to a later lecture.
2. Selecting $n$ for a worded subgroup proportion claim ("proportion of X within Y" vs "proportion of X who are Y"). Not in Lecture 7. Belongs to a later lecture.
3. Reading a P-value range off a printed t-table (fixed columns only, not continuous like the Z table). Example 9.7's working (this session, composite) used a rejection-region decision only, no P-value, so this lecture had the chance to introduce t-table P-value reading and did not. Still parked.

## 7. Resume block
```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG
protocol file and this handoff memo. My notes on Lecture 7, Inferences
Based on Two Samples (Devore and Berk 9.1, 9.2), are complete: the
distribution of Xbar-Ybar, the z test for two means with known
variances (Example 9.1), the large sample z test substituting S1^2/S2^2
(Example 9.4, first P-value in the course), the large sample CI for
mu1-mu2 (Example 9.5), and the pooled two sample t test and CI with
S_p^2 (Example 9.7, worked as a composite since the source gave no
solution).

Three items are parked because Lecture 7 doesn't cover them: proportion
tests always using Z with the n*p-hat validity condition, choosing n for
a worded subgroup proportion claim, and reading a P-value range off a
printed t-table. I believe a later lecture (possibly Lecture_8.pdf or a
lecture on proportions) covers some of these, unconfirmed. Please check
which once it's uploaded and resolve the parked items against it.

Lecture_9.pdf is confirmed to be single-factor ANOVA, the natural next
step after two-sample comparisons when there are more than two means to
compare.
```
