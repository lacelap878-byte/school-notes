# Handoff Memo: STA01B1 Chapter 7, Statistical Intervals

## 1. Objective
Generate structured study notes from the uploaded Chapter 7 lecture PDF (Statistical Intervals, Devore and Berk, sections 7.1 and 7.2) following the CDG protocol, then work through conceptual questions on sample size planning and confidence level notation.

## 2. Topics Covered (all new this session)
1. Basic properties of confidence intervals, point estimate limitations
2. Derivation of the CI for mu with known sigma
3. Definition and interpretation of a 95% CI for mu
4. Interpreting the confidence level, long run frequency interpretation
5. Other levels of confidence, general z_alpha/2 form, plus Example 7.3
6. Confidence level, precision, sample size tradeoffs, plus Example 7.4
7. Large sample CI for mu using s, plus validity conditions
8. Worked Examples 7.6 and 7.7
9. CI for a population proportion p
10. Worked Examples 7.8 and 7.9
11. One sided confidence intervals for mu and p, plus Example 7.10

## 3. Content Summary (facts only)
- A point estimate alone gives no information about precision, since sampling variability means it is virtually never exactly equal to the parameter. A confidence interval reports a plausible range instead.
- For a normal population with known sigma, the CI for mu is derived by standardizing X bar and algebraically isolating mu, giving the random interval $(\bar{X} - z_{\alpha/2}\sigma/\sqrt{n}, \bar{X} + z_{\alpha/2}\sigma/\sqrt{n})$.
- The confidence level (e.g. 95%) describes the long run success rate of the procedure across repeated sampling, not a probability statement about one already computed interval.
- Wider interval means higher confidence but less precision; the only way to increase confidence without increasing width is to increase n.
- When sigma is unknown, S replaces sigma in a large sample CI, valid for any population shape once n > 40 (a stricter threshold than the general CLT rule of thumb, due to the extra variability from estimating sigma with S).
- The range rule of thumb ($\sigma \approx \text{range}/4$) is used only for advance sample size planning when no value of s or sigma exists yet, based on the assumption that roughly 95% of a normal population's values lie within 2 standard deviations either side of the mean. This is a statement about the population's individual values, distinct from the Central Limit Theorem, which concerns the shape of the sampling distribution of X bar regardless of population shape.
- The CI for a proportion p uses $\hat{p}\hat{q}/n$ as the variance term, valid as a large sample approximation when $n\hat{p} > 10$ and $n\hat{q} > 10$.
- For sample size planning for p when no prior estimate exists, $\hat{p} = 0.5$ is used because $\hat{p}(1-\hat{p})$ is maximized at $p=0.5$, giving the most conservative (largest) required n, guaranteeing the target error regardless of the true proportion.
- One sided confidence bounds use $z_\alpha$ (not $z_{\alpha/2}$), since all the error is placed in a single tail. A one sided bound is tighter than the corresponding side of a two sided interval at the same confidence level.
- Question dissection skill established: identify what is being solved for, extract the error of estimation E (watch "within" vs "width," off by a factor of 2), convert confidence level to $z_{\alpha/2}$, and identify the spread estimate (given sigma or hat-p, range rule for sigma, or 0.5 for hat-p when no prior estimate exists and question says "irrespective of p").
- Worked and self corrected a practice sample size problem (poll, within 3 percentage points, 95% confidence, no prior p estimate): correctly identified E = 0.03 (after unit conversion from percentage points), $z_{\alpha/2}=1.96$, $\hat{p}=0.5$, and computed n = 1068.
- Clarified the distinction between $\alpha$ (both tails combined), $\alpha/2$ (one tail), and the cumulative table value at $z_{\alpha/2}$, which equals $1-\alpha/2$, not $1-\alpha$ and not $\alpha$.
- Noted that Example 7.9 in the source builds on the adjusted proportion CI formula from Example 7.8 (matching the referenced width of 0.257), not the traditional formula from the CI proposition, though the user's own course (per their lecturer) uses the traditional formula for STA01B1's own sample size calculations.

## 4. Last Position
Notes: complete, all 11 topics from Chapter 7 covered.
Conceptual discussion: resolved, ending on the alpha vs alpha/2 vs cumulative table value distinction, confirmed correct.

## 5. Parked Items
None.

## 6. Resume Block
```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG protocol
file (or I will re-upload it) and this handoff memo. My notes on Chapter 7,
Statistical Intervals (Devore and Berk, 7.1 and 7.2), are complete, all 11
topics covered: basic CI properties, derivation for known sigma, definition
and interpretation of a 95% CI, interpreting the confidence level, other
confidence levels (Example 7.3), confidence/precision/sample size tradeoffs
(Example 7.4), large sample CI for mu (Examples 7.6, 7.7), CI for a
proportion p, proportion worked examples (Examples 7.8, 7.9), and one sided
CIs for mu and p (Example 7.10).

I also worked through question dissection skills for sample size problems
(within vs width, finding E, z_alpha/2, and the spread estimate), the
distinction between the range rule of thumb and the CLT, why hat-p = 0.5 is
used for conservative sample size planning, and the alpha vs alpha/2 vs
cumulative table value distinction. All conceptual threads from this session
are resolved. Ready to continue with the next Chapter or topic.
```
