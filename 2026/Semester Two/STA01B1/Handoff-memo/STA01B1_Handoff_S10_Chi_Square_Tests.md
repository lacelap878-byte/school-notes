Supersedes S1 to S9. This is the only handoff file needed.

# STA01B1 Handoff S10 (Chi-Square Tests)

## 1. Objective (this session)

Cover Lecture 11 (Chapter 14: goodness of fit and contingency tables) as S10 under CDG v11, with the final summative assessment on Monday 9 November 2026 at 08:30. The lecture was new to the student, who was told to self-study it, and the notebook has no pages left, so there were no copy-ready parts. The session ran as a slow question session: a die and a table first, then the formula, then goodness of fit, then two-way tables, with the student's own questions steering it. The session-start revision quiz (6 questions) and the session-end check quiz (6 questions) were both run and the screenshots read. Then Memo. The notes file is for reading and revision, not for copying, and carries two Obsidian graphs at the student's request.

## 2. Topic ledger

```
S1  | Statistics and Sampling Distributions                    | full | open struggle no
S2  | Point Estimation                                         | full | open struggle no
S3  | Statistical Intervals                                    | full | open struggle no
S4  | Intervals Based on a Normal Population                   | full | open struggle no
S5  | Hypothesis Testing                                       | full | open struggle yes
S6  | Inferences Based on Two Samples                          | full | open struggle yes
S7  | Paired Data, Two Proportions and Two Variances           | full | open struggle yes
S8  | Single-Factor ANOVA and Tukey's Procedure                | full, amended S10 | open struggle yes
S9  | Simple Linear Regression                                 | full | open struggle yes
S10 | Chi-Square Tests                                         | full | open struggle yes
```

## 3. Notes index

```
S1  | Statistics and Sampling Distributions | STA01B1_Notes_S1_Statistics_and_Sampling_Distributions.md | statistic vs parameter, sampling distribution of Xbar and To, CLT, how large is large
S2  | Point Estimation | STA01B1_Notes_S2_Point_Estimation.md | point estimators, unbiasedness, MVUE, standard error, p-hat as Xbar
S3  | Statistical Intervals | STA01B1_Notes_S3_Statistical_Intervals.md | CI for mean (known/large-sample unknown sigma), CI for proportion, sample size planning, one-sided bounds
S4  | Intervals Based on a Normal Population | STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population.md | t interval, prediction interval, CI for the variance
S5  | Hypothesis Testing | STA01B1_Notes_S5_Hypothesis_Testing.md | H0/Ha, Type I/II error, rejection regions, Case I/II Z tests for a mean (Case II cutoff now n > 40 per the lecturer)
S6  | Inferences Based on Two Samples | STA01B1_Notes_S6_Inferences_Based_on_Two_Samples.md | distribution of Xbar-Ybar, z test known/large-sample variance for two means, large-sample CI, pooled t test and CI, Sp^2
S7  | Paired Data, Two Proportions and Two Variances | STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances.md | paired t test and CI, E and V of p1-hat minus p2-hat, two-proportion z test and CI, F test for two variances, 30 vs 40 threshold table
S8  | Single-Factor ANOVA and Tukey's Procedure | STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md | ANOVA hypotheses, notation and dots, assumptions, SSTr/SSE/MSTr/MSE/F, ANOVA table, Breakfast Problem, proof that SST = SSTr + SSE, Tukey's HSD (Examples 10.5 and 10.6), simultaneous confidence level
S9  | Simple Linear Regression | STA01B1_Notes_S9_Simple_Linear_Regression.md | probabilistic model and assumptions on epsilon, least squares (with derivation), fits and residuals, Total SS = SSR + SSE (with proof), r and r squared, regression ANOVA table, why regression df is 1, t and F tests (t squared = F), cautions, diagnostic plots, CI and PI at x0, one composite example
S10 | Chi-Square Tests | STA01B1_Notes_S10_Chi_Square_Tests.md | multinomial experiments, expected counts, Pearson's chi-square, why the formula works (four links), goodness of fit with examples, degrees of freedom as unknowns minus equations, two-way tables (independence and homogeneity) with four worked examples, the assumptions, ANOVA versus chi-square, the answer routine, two Obsidian graphs
```

Also in the vault, not in the chain: Summaries (ST1, ST2), Proofs (ST1, ST2) and stats/extra (the ANOVA test routine). The final summary (Revise Final) is still to be built.

## 4. Content summary

S1: sampling distributions, CLT, statistic vs parameter.
S2: point estimation, unbiasedness, MVUE, standard error.
S3: confidence intervals for a mean and a proportion, sample size planning, one-sided bounds.
S4: t interval, prediction interval, variance CI.
S5: hypotheses, Type I/II error, rejection regions, Case I/II Z tests (cutoff n > 40).
S6: two-sample z and pooled t tests and CIs, Sp^2.
S7: paired t, two-proportion z with the strict 10-and-10 rule, F test for two variances.
S8: single-factor ANOVA, the proof SST = SSTr + SSE (a missed dot costs a mark), Tukey's procedure.
S9: simple linear regression: least squares, Total SS = SSR + SSE, r squared, the t and F tests (t squared = F), diagnostic plots, CI and PI at x0.

S10, in detail. Source: Lecture 11.pdf, 22 slides numbered as printed (slide 1 title, slide 22 closing reference to Chapter 14, sections 14.1 and 14.3), plus Tutorial 11 and Solution 11. Read as images where needed; slides 15 to 17 are textbook pictures with no text layer, and the expected counts and the statistic 19.18 were recomputed.

What the lecture says. Data as counts in categories, the multinomial experiment (five conditions) and the binomial as k = 2 (slides 2 to 4). The expected count E = n p_i0 from the claim in H0 (slide 5). Pearson's statistic, sum of (O - E)^2 / E, large values against H0, upper tail only (slides 6 and 7). Goodness of fit with df = k - 1 (slide 7) and the example of 40 employees on flexible working hours (slide 8: expected 10 each, chi-square 5.6, cut-off 6.251 at 10% with 3 df, fail to reject). The note that E should be at least 5 (slide 9). Contingency tables, independence and dependence, E_ij = n_i n_j / n, df = (I - 1)(J - 1) (slides 10 to 14). The furniture defects example by shift (slides 15 to 17: chi-square 19.18, df 6, cut-off 18.5476 at .005, reject). Comparing multinomial populations and the test of homogeneity with fixed totals (slides 18 and 19). The two assumptions and the two fixes for small expected counts (slides 20 and 21).

What was built in session from the student's questions (all in the notes file, marked added):
- A fair die as the first example (6, 14, 9, 11, 8, 12 gives chi-square 4.2, cut-off 11.07 with 5 df, do not reject). Why the gaps are squared and divided by E, and what a "score" is (the test statistic).
- Expected count vs expected value of one roll (3.5), and what an expected count is (chance times number of tries).
- Where the formula comes from, in four links: a count wobbles by about the square root of E, so (O - E) / sqrt(E) is a z-score, its square is one term of the formula, and a sum of squared z-scores is chi-square with k - 1 degrees of freedom. A correction was recorded: the exact variance of a count is np(1 - p), close to E only when p is small.
- A simulation of fair and loaded dice (rerun in script, 200 000 experiments: a fair die averages 5.0 with 4.8% above 11.07, a die loaded towards 6 averages about 11.0 with 41% above).
- Degrees of freedom as unknowns minus equations, with a table covering the die, a 2 by 3 table, the t test and regression. The student asked many times whether the last roll is "forced". Answered with the six-endings table, the first-throw check (the gaps sum to zero from the first throw on, so zero cannot mean forced), the sweets analogy, and the wording "new information", never "forced". The student said the first-throw check settled it and that they were getting it, but the df item stays open until they explain it back.
- The two-way table: expected counts by multiplying chances (independence), checked with the rule that an expected count cannot exceed its row or column total. Worked: 2023 Paper A question 7 (chi-square 0.1847, df 1, 3.841, do not reject), Tutorial 11 question 35 (6.454, df 2, 5.991, reject), question 44 (11.65 recomputed against the solution's 11.60) and question 3 (1.57 against 7.815, do not reject).
- Chi-square against ANOVA: what is recorded for each person (labels or a measurement). Real-world link: digit patterns (Benford's law) as an example of goodness of fit used to flag made-up numbers; mentioned in session as an illustration only, not examinable.

The student attended no Lecture 11 class and is self-studying from the slides, with videos that the lecturer supplied and the student intends to watch. No video has been confirmed at 60 percent or more, so none is embedded.

Quizzes. Session-start revision quiz (6 questions): all correct. Q1 (PI centre and width), Q2 (plot to assumption), Q3 (paired design), Q4 (SSTr from totals), Q5 (Q table column), Q6 (conclusion wording, multiple choice). On Q2 the student said they did not understand the residuals half of the question, so the item stays open with a picture added to the session. Session-end check quiz (6 questions): misses Q1 (picked ANOVA with df 2 and 297), Q2 (picked 35, the average of the two totals) and Q4 (picked "too many degrees of freedom"), and Q6 right but guessed. Q3 (df = 4 for 5 categories) and Q5 (conclusion wording) taken as correct, since no screenshot was sent. In-session slips in written answers: df = 39 for goodness of fit, a total of 4.6 for 5.6, 21.24 for 21.42, and the conclusion "at 10 percent confidence level, the alternate hypothesis is rejected".

Study approach: the student said that copying notes is the wrong use of time a week out and wants to work with questions and past papers. They asked for tables rather than paragraphs when explanations were not landing, and for everything to be in plain words. They also asked for Obsidian graphs in notes drafts where they help.

## 5. Last position

S10 as a question session (no parts). Covered: the multinomial setting, the statistic and its origin, goodness of fit, degrees of freedom, the two-way table with its independence and homogeneity versions, the assumptions, test choice, and the answer routine. One example (the 2023 Paper A question 7) and the faculty question were worked in full. Both quizzes run and the screenshots read. Memo produced this message. Not yet done: the final summary (Revise Final), timed past papers, the video watching, the account of how ST1, ST2 and the practical test went.

## 6. Parked items

1. Choosing n for a worded subgroup proportion claim ("proportion of X within Y" vs "proportion of X who are Y"). Not in any lecture. Still parked (S5 to S10).
2. Reading a P-value range off a printed t-table. The lecturer said for SA2 that P-values are calculated only for z tests; the final's rule is unknown. Do not drill it until she answers (an older summary file has a bracketing tip that should not be drilled). Still parked (S5 to S10).

Resolved this session: the stale line in the S8 notes ("still waiting on the lecturer's answer") has been corrected by an Amend S8 (see section 8). The S9 handoff listed it as a to-do.

Waiting on the lecturer, for the online meeting on Thursday 5 November and the consultation on Friday 6 November. Draft question list, to be sharpened:

About the final (Monday 9 November, 08:30):
1. Which textbook paragraphs and tutorials does the final cover?
2. Is it the same fill-in format as the summative assessments? How long is it and how many marks?
3. SA2 had no proofs. Will the final have proofs, and which?
4. On SA2 only z tests had P-values. Is that the same on the final, and what about chi-square (slide 16 and Solution 11 quote P-value ranges)?
5. Which tables come with the paper, and is there a formula sheet?

Topics we cannot place:
6. Which chi-square tests are examinable: goodness of fit, independence, homogeneity? (Evidence so far: the Mock Exam (Past Papers/Full Module), from an older pack, has a goodness of fit question on market shares and an independence interpretation question, and the 2022 work schedule limits Lecture 11 to textbook paragraphs 14.1 and 14.3.)
7. Is the test for one variance (the chi-square family in the learning guide) examinable, or only the interval?
8. Is covariance examinable (listed under regression in the learning guide)?
9. Do we need consistency and efficiency of estimators beyond unbiasedness and MVUE?
10. Are memos available for the 2022 Paper C and the 2023 Paper A (no memos in the folder)?
11. The one-sample t test, the one-proportion z test and P-values are Lecture 6 (textbook paragraphs 8.3 to 8.5), now Lectures/Lecture 06.pdf, a 2021 deck identical in numbering to this year's (Lectures 5 and 7 to 11 are byte for byte the same files). Both 2026 information sheets skip it (SA1: Lectures 1 to 5; SA2: Lectures 7 to 10). The student reports that week was postponed for a test and that the material was done; no Lecture 6 deck was in the student's 2026 folder, and the vault has no notes on it. Are they examinable on the final? The deck says t when n < 30, but the lecturer ruled n > 40; which applies?

Lecture 10 slides, open since S9:
12. Slide 17: the formula under "Sum of squares for error" is blank.
13. Slide 20 states H0 as "model is useful" (should it be slope equals 0?). Slide 19 uses beta_0 for the hypothesised slope. Slides 28 and 29 write the line of means with alpha and beta. Which notation on the paper?

Lecture 11 slides, new in S10:
14. Slide 14: row and column totals are written n_i and n_j with no dots (the ANOVA lecture used dots). Do we need dots?
15. The tables on slides 11 and 12 use r and c while the formulas use I and J. Which notation on the paper?
16. A 2 by 2 chi-square test is the same test as the two-proportion z test, but the validity rules differ (expected counts at least 5 vs 10 successes and 10 failures in every group). Which applies?
17. The slides carry a 2021 date stamp. Is this lecture current, and is the whole of Chapter 14 sections 14.1 to 14.3 in scope?
18. Solution 11 question 44 gives chi-square 11.60. A recomputation from the printed table gives 11.65. Which should be used?
19. Could the final ask us to prove that the expected count is n_i n_j / n (the lecturer's route: intersection, independence, p_ij, substitute)? May we use the computational formula chi-square = sum of O^2/E minus n? (Both proofs are in the S10 notes, under Proofs that may be asked.)
20. Gap noticed in the proof files: 2022 Paper C question 11 asks whether p-hat squared is unbiased for p squared. It is not in the ST1 or ST2 proofs. It is biased: E(p-hat squared) = p(1 - p)/n + p squared.

To do:
- The account of how ST1, ST2 and the practical test went, in the student's own words (what appeared, where they got stuck, what they would do differently). Asked for once in the S10 setup and not yet given. The final summary has a section built from it.
- Lecture 6 content (t test for a mean, one-proportion z test, P-values) is Lectures/Lecture 06.pdf. Tutorial 6 and its solution (in Tutorials) cover it too, and Practical 6 was on the SA2 practical. If the lecturer confirms it is examinable, run it as late material with `follows: S5` and a fresh number (S11), as a short question session. Not yet read in detail.
- Watch the lecturer's videos on chi-square (the student's plan). Links to Lecture 11 Parts 1 to 7 and a "must watch" note were found in Old Years/Classroom Pages 2022/Week 13.pdf (also listed in stats/extra/STA01B1_Extra_Folder_Findings.md); check them against your 2026 links. To embed any, the protocol needs the URL, title, channel, percent watched (at least 60) and start and end times.
- Timed past papers (closed book, marked against a worked memo made here): 2023 Paper A and 2022 Paper C. Both are full-module papers with no memo. Only the chi-square question differs in scope.
- The final summary: `Revise Final S1 to S10`, once the scope is confirmed by the lecturer on Thursday.
- A v12 proposal on how the protocol should run near tests and exams is in stats/extra/CDG_v12_Proposals.md. It needs moving to the Proposals folder at the vault root, which the session could not reach.

## 7. Resume block

```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG
protocol file (v11) and this handoff memo together with the S10 struggle
log.

My final is on Monday 9 November 2026 at 08:30. Lecture 11 (chi-square:
goodness of fit, independence and homogeneity, Chapter 14) is done as S10
and is the last lecture. The lecturer meets us online on Thursday 5
November and holds a consultation on Friday 6 November, so I need good
questions ready before then (draft list in the handoff, section 6).

My notebook is full. Do not write copy-ready parts. Work through
questions, past papers (2022 Paper C and 2023 Paper A, no memos, so mark
against your own worked answers) and drills. I want tables where an
explanation is not landing, plain words for every interpretation, and
Obsidian graphs (desmos-graph blocks) in notes drafts where they help. I
am tired after exams and need things one step at a time.

Start with the session-start revision quiz from the S10 struggle log, in
written form, not only multiple choice, since my slips show in written
work: (a) a goodness of fit question with a percentage claim (E from the
claim, df = k - 1, cut-off, conclusion sentence); (b) a two-way table
with totals given (one expected count with the "cannot exceed its row or
column total" check, df = (I - 1)(J - 1)); (c) a scenario with only
labels recorded and three groups, asking which test and why (chi-square
vs ANOVA); (d) a table with one expected count under 5 (can I use the
test, and what do I do). Then, in my own words, ask me to explain why
there are 5 degrees of freedom for 6 counts with a known total, without
the word "forced". Address any miss on the spot, then retest it later.

After that: the plot-to-assumption item (show a funnel and a U shape and
ask me to read each), copying slips under time, rounding before F, then
retention checks.

Tell me what I still owe you: how ST1, ST2 and the practical test went
(in my own words, for the final summary). Remind me that the final summary
(Revise Final) can only be built once the lecturer confirms the scope on
Thursday.
```

## 8. Protocol versions

```
file | written with (version, session) | amended with (version, session) or none
STA01B1_Handoff_Memo.md | CDG version not recorded | none
STA01B1_Handoff_S1_Statistical_Intervals.md | CDG version not recorded | none
STA01B1_Handoff_S2_Point_Estimation.md | CDG version not recorded | none
STA01B1_Handoff_S5_Hypothesis_Testing.md | v6, S5 | none
STA01B1_Handoff_S6_Inferences_Based_on_Two_Samples.md | CDG version not recorded | none
STA01B1_Handoff_S7_Paired_Data_Proportions_and_Variances.md | v8, S7 | none
STA01B1_Handoff_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md | v8, S8 | none
STA01B1_Handoff_S9_Simple_Linear_Regression.md | v8, S9 | none
STA01B1_Handoff_S10_Chi_Square_Tests.md | v11, S10 | none
STA01B1_StruggleLog_S1_Statistical_Intervals.md | CDG version not recorded | none
STA01B1_StruggleLog_S5_Hypothesis_Testing.md | v6, S5 | none
STA01B1_StruggleLog_S6_Inferences_Based_on_Two_Samples.md | CDG version not recorded | none
STA01B1_StruggleLog_S7_Paired_Data_Proportions_and_Variances.md | v8, S7 | none
STA01B1_StruggleLog_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md | v8, S8 | none
STA01B1_StruggleLog_S9_Simple_Linear_Regression.md | v8, S9 | none
STA01B1_StruggleLog_S10_Chi_Square_Tests.md | v11, S10 | none
STA01B1_Notes_S1_Statistics_and_Sampling_Distributions.md | CDG version not recorded | none
STA01B1_Notes_S2_Point_Estimation.md | CDG version not recorded | none
STA01B1_Notes_S3_Statistical_Intervals.md | CDG version not recorded | none
STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population.md | CDG version not recorded | none
STA01B1_Notes_S5_Hypothesis_Testing.md | v6, S5 | S7 (v8): n > 30 corrected to n > 40
STA01B1_Notes_S6_Inferences_Based_on_Two_Samples.md | CDG version not recorded | none
STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances.md | v8, S7 | none
STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure.md | v8, S8 | S10 (v11): stale "still waiting on the lecturer" line corrected
STA01B1_Notes_S9_Simple_Linear_Regression.md | v8, S9 | none
STA01B1_Notes_S10_Chi_Square_Tests.md | v11, S10 | none
```

Versions marked "not recorded" were never written into the files. The versions given for S5, S7, S8 and S9 come from the session summaries of those chats, not from footers in the files.

## 9. Friction log

Cumulative. The first entries come from earlier chats' summaries and are marked; S10 is recorded in full. Ten entries, so the fold-into-the-protocol proposal is not yet due, but the S10 events point to one (see the v12 proposal file).

```
S6 | Inferences Based on Two Samples | Claude stripped all LaTeX from a copy-ready part (reading "no Obsidian syntax" as "no LaTeX") | the student meant: no wikilinks or callouts on the page, but keep LaTeX for formulas | the student corrected it and the part was redrafted (from the S6 chat summary)
S6 | Inferences Based on Two Samples | Claude treated an instruction as a Go signal and produced the next part | the student meant only to give an instruction, not to continue | the student corrected it; Go is the only continue signal (from the S6 chat summary)
S9 | Simple Linear Regression | Claude assumed a tight page budget should shrink the notes.md file too | the student meant only the hand-copied parts are tight; the notes file stays full length | the student said so and it became a standing rule (from the S9 chat summary)
S10 | Chi-square, first contact | Claude put the whole lecture on one screen and assumed some grasp of the topic | the student met chi-square for the first time and the pace was too fast | restarted from one die example, one idea at a time
S10 | Zero total of the gaps | Claude said the gaps always add to zero, as the reason for squaring them | the student heard that each deviation should be zero, and then that the last roll is predetermined, so gambling would be pointless | the sweets table, the six-endings table, the first-throw check, and dropping the idea as unneeded for the exam
S10 | Expected count | Claude said "expected count" | the student thought of 3.5, the expected value of one roll | separated the expected value of a roll from the expected count of a face, and said chi-square treats faces as labels
S10 | Degrees of freedom | Claude explained df as "the last cell is forced" | the student heard that the last roll or cell has no freedom of choice, and that adding a throw would change which one is free | "unknowns minus equations" and "new information", never the word "forced"; the picture still needs retesting in the student's own words
S10 | Formatting | Claude explained in paragraphs | the student could not take in the words and asked for tables three times | tables with concrete numbers, one per idea, as the default for this student when an idea is not landing
S10 | A "check" | Claude called a rearranged formula a check ("same answer") | the student pointed out that nothing was changed mathematically, so agreement proves nothing | called it an equivalence, and used an independent route (a script) for real checks
S10 | Fatigue | Claude kept the pace of a normal session | the student was tired after a late exam and said so | slower steps, smaller asks, tables, and an offer to stop; files written in the background
```

---
*CDG v11 | written S10 | 2026-11-03*
