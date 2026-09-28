Supersedes S1 to S6.

# STA01B1 Struggle Log S7 (Paired Data, Two Proportions and Two Variances)

## 1. Open items (unresolved, oldest first)
```
choosing n for a worded subgroup proportion claim | first seen S5 | "proportion of X within Y" vs "proportion of X who are Y" changes which n to use; no lecture on file has posed this kind of question yet | 3
reading a P-value range off a printed t-table | first seen S5 | fixed columns only, not continuous like the Z table; Example 9.9 (S7) used a rejection-region decision only and had the chance to introduce this and did not | 3
source cutoff inconsistencies (30 vs 40, and vs and/or, no stated proportion or F cutoff) | first seen S7 | five separate slide-level inconsistencies collected into one threshold table this session (see S7 notes); genuinely unresolved until the lecturer answers the drafted email, not a recognition failure on the user's part | 1
```

## 2. Resolved this session
```
distribution/test choice, proportion branch | correction: Lecture 8 (S7) supplies both proportion procedures. Proportion tests and CIs use Z and never t, because the variance p(1-p)/n is built from p itself rather than a separately estimated nuisance parameter (Part 4). The test pools the two samples under H0: p1=p2 (Part 5); the CI does not pool, since it makes no such assumption (Part 6). This closes the last open branch of the item first raised in S5 and narrowed in S6.
proportion validity condition, 5 vs 10 | correction: the "5" was never a rule stated in a notes file, it was a placeholder written into the S5 handoff memo's parked-items list and carried into its resume block and then into the S6 memo. The user-supplied textbook boxes this session give the real condition: n*p0 >= 10 and n*(1-p0) >= 10 for one sample, and m*p1hat, m*q1hat, n*p2hat, n*q2hat all >= 10 for two samples. The S3 proof file and the Chapter 7 handoff already had this right at 10.
P-value doubling in a two-tailed test | reinforced, not newly resolved: recurred correctly in Example 9.11 (Part 5, 2P(Z>|z|)) and in the P-value bound at the table edge (Part 5), matching the rule established in S6 Example 9.4.
whether the t distribution is always used for a paired or two-sample test | correction: the paired test is a one-sample problem on the differences D_i, so the same known-variance, sample-size and normality conditions from every earlier session apply. t is not automatic; it depends on whether sigma_D is known, how large n is, and whether the differences are normal, the same three-way fork as every other mean procedure in this module.
what changes between the n>30 and n>40 versions of a large-sample procedure | correction: the arithmetic is identical either way (same test statistic, same substitution of S for sigma); only the label (Z vs a looser use of the same Z), the table read, and the stated justification differ. This was reached through several exchanges and ended with the user's own observation that the calculation doesn't change, which is correct and is now the standing explanation, not an add-on.
```

## 3. Notation or terminology still causing trouble
None new this session.

## 4. Patterns across sessions
```
distribution/test choice | seen in S5, S6, S7 | each new lecture added one branch to "which formula and which distribution apply here": S5 gave the one-sample mean fork, S6 the two-sample mean fork, S7 the proportion fork (always Z) and the variance fork (always F, under normality). The item that opened in S5 is now fully resolved for every case the course has presented; only the worded-subgroup-n variant (section 1 above) remains as a distinct, narrower open item.
source inconsistencies not reconciled by the slides | seen in S6 and S7 | S6 had one ("and" vs "and/or" on the pooled t slides), S7 collected four more (the 30 vs 40 cutoff, no stated proportion cutoff, Example 9.11 failing the textbook's own validity count, and the alpha used for Example 9.14). This is a pattern in the source material itself, not a gap in the user's understanding, and the fix is external (the lecturer's answer), not more study.
```

## 5. Retest first (ranked)
1. The proportion fork (always Z, pooled for the test, unpooled for the CI, 10-and-10 validity condition), since it is new material with an easy trap: reaching for a pooled estimate in the CI by habit from the test.
2. The larger-variance-on-top shortcut for the F test, specifically the degrees-of-freedom swap that must travel with the variance swap, and using F(alpha/2) rather than F(alpha) in the two-tailed case.
3. The paired t setup, specifically forming D_i first and reducing to a one-sample problem, since the temptation is to treat paired data as if it were the independent two-sample case from S6.
