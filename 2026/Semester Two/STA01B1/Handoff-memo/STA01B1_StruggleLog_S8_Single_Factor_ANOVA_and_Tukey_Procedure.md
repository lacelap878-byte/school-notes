Supersedes S1 to S7.

# STA01B1 Struggle Log S8 (Single-Factor ANOVA and Tukey's Procedure)

## 1. Open items (unresolved, oldest first)
```
choosing n for a worded subgroup proportion claim | first seen S5 | "proportion of X within Y" vs "proportion of X who are Y" changes which n to use; no lecture on file has posed this kind of question yet, and Lecture 9 (ANOVA) has no proportions | 4
reading a P-value range off a printed t-table | first seen S5 | fixed columns only, not continuous like the Z table; Lecture 9 again gave no chance to practise it (F test by rejection region, exact SAS P-value in Example 10.6, Q table for Tukey) | 4
source inconsistencies (30 vs 40 cutoff, and vs and/or, no stated proportion or F cutoff, and in S8 the Chapter 10 vs Table/Example 11.x numbering and an unexplained "RSE" label) | first seen S6 | genuinely unresolved until the lecturer answers the drafted email; a gap in the source, not a recognition failure | 3
paired design is a one-sample problem on the differences | first seen S7 (resolved S7), recurred S8 | in the S8 revision quiz picked a two-sample t "because there are two sets of measurements" instead of one-sample t on the 12 differences D_i with 11 df. The retest in the check quiz was not reported as missed, so this is provisional: confirm with the user | 2
MSE vs MSTr when H0 is false | first seen S8 | picked "MSTr still estimates sigma^2 and MSE is deflated", the reverse of the truth. MSE is built from deviations around each group's own mean so it does not see the group means differ; MSTr is J times the variance of the sample means and inflates. The user said they did not know this at all | 1
SSTr computing formula: totals not means | first seen S8 | picked the version with a bar on the grand total (the grand mean) instead of x.. the grand total. The same slip appeared in the live notes, so it is partly a delivery error | 1
third subscript of Q | first seen S8 | used the total df IJ - 1 = 44 instead of the error df I(J-1) = 40. The second subscript (I, not I-1) was right | 1
Tukey: joint level vs individual level | first seen S8 | picked "Tukey controls each interval at 95% separately, so the joint level is lower", which describes plain separate intervals, the problem Tukey fixes. Tukey fixes the family level and widens each interval | 1
proof: which piece of the expansion is SSE and which is SSTr, and where the J goes | first seen S8 | picked "the J belongs in SSE". The question showed the pieces only as "first square" and "last square", the user said it did not make sense, so the gap is unconfirmed until retested with the actual expressions shown | 1
```

## 2. Resolved this session
```
none fully closed this session. Every S8 item above stays open until answered correctly under retest; a correction on the spot is not evidence of understanding.
paired design (see section 1) | provisional: the check-quiz retest was not reported as missed. Closes on the user's confirmation.
```

Carried from S7, resolved S7 (drop if no recurrence by the end of S9):
```
distribution/test choice, proportion branch | resolved S7 | proportion tests and CIs use Z and never t because the variance p(1-p)/n is built from p itself; the test pools under H0, the CI does not
proportion validity condition, 5 vs 10 | resolved S7 | the real condition is 10 successes and 10 failures; the "5" was a placeholder in old memos
P-value doubling in a two-tailed test | resolved S6, reinforced S7 | 2P(Z > |z|)
what changes between n > 30 and n > 40 | resolved S7 | the arithmetic is identical; only the label, the table read and the stated justification differ
```
distribution/test choice for means (one-sample, two-sample, paired) | resolved S7 | see the paired-design open item above, which shows it can still slip.

## 3. Notation and terminology still causing trouble
- Dots: x_ij (no dot, one observation), xbar_i. (one dot, averaged over j), xbar.. (two dots, averaged over both). The lecturer has said a missed dot in the proof costs a mark.
- Totals vs means: in the computing formulas x_i. and x.. are totals with no bars; in the definitions xbar_i. and xbar.. are means with bars. Lowercase xbar on the notation slides; capital Xbar on the sums of squares slide for the random-variable versions.
- Q(alpha, I, I(J-1)): second subscript I (not I-1 as in F), third subscript the error df (not the total df).
- SAS wording: Model = Treatments, Error = Error, Corrected Total = Total.
- k and I both mean the number of populations (slide 18 uses k, the rest of the lecture uses I).
- Underscored / joined means = "not shown to differ", not "equal"; the relation is not transitive.
- Simultaneous, joint, family and experimentwise error rate all mean the same thing; individual and per-comparison also mean the same thing as each other.

## 4. Patterns across sessions
```
distribution/test choice | seen in S5, S6, S7, S8 | each new lecture added one branch to "which formula and which distribution apply here". S5 the one-sample mean fork, S6 the two-sample mean fork, S7 the proportion fork (always Z) and the variance fork (always F, under normality), S8 the more-than-two-means fork (ANOVA F, then Tukey once H0 is rejected). The paired-design recurrence in S8 shows the two-sample vs one-sample question can still slip.
source inconsistencies not reconciled by the slides | seen in S6, S7, S8 | S6 one ("and" vs "and/or"), S7 four (30 vs 40, no proportion cutoff, Example 9.11 failing the textbook's own count, the alpha for Example 9.14), S8 more (Chapter 10 vs Table/Example 11.x numbering, the oil-filter table captioned Example 11.4 under Example 10.5, an unexplained RSE label, k vs I). This is a pattern in the source material, not a gap in the user's understanding, and the fix is external (the lecturer's answer).
formulas delivered with a symbol or number slip, caught after delivery | seen in S7, S8 | S7 had one arithmetic slip (s_D 11.61 for 11.96). S8 had many: bars on totals, the Q subscript wording, a wrong aside about 14.15, an invented scenario, a misread k(I-1)/2, xbar_3. for xbar_1., a dropped double-sum form, capital vs lowercase xbar, a rounding claim, em dashes. This is a delivery-side pattern. The user's hand copy may carry these errors; the corrections are listed in the S8 handoff memo. Future parts should be checked against the slide images before delivery.
```

## 5. Retest first (ranked)
1. MSE vs MSTr when H0 is false (user said they knew nothing about it; give a numeric or thought-experiment question, for example adding a constant to one group).
2. SSTr computing formula with totals not means (a sanity-check question on the size of the two subtracted terms).
3. Third subscript of Q (error df vs total df) with a fresh I and J.
4. Proof: which piece of the expansion is SSE and which is SSTr, and where the J goes. Show the actual expressions, not "first square" and "last square". Also test the dots and the substitution in the middle term.
5. Tukey: joint (family) level vs individual level.
6. Paired design is a one-sample problem on the differences (confirm the S8 check-quiz result first; if it was answered correctly, this closes).
7. Parked: choosing n for a worded subgroup proportion claim, and reading a P-value range off a t-table (only if the next lecture supplies material).
