# STA01B1 Final: Revise S1 to S10 (Mon 9 Nov, 08:30)

Read tonight, read again tomorrow morning. Built from your own ST1/ST2 summaries, proofs and S10 notes, re-scoped for the final. Dr H gives no formulas on the proofs and no formula for n. One- or two-sided is decided by the board on the day.

## 0. Your five slips (never again)
1. Standard error is σ/**√n**, not σ/n. Write E(X̄) = μ with the symbol, then the number.
2. Reject iff **p ≤ α** for every H_a. Only the side of the curve changes (upper tail: area to the right, lower: left, two-sided: double the smaller tail).
3. β is the area of the **TRUE-mean curve** on the side of c that is **NOT** the rejection region. α is the area of the H0 curve inside the rejection region.
4. Chi-square goodness of fit: **df = k − 1** (groups, never n − 1). Expected counts come from H0: E = n·p_i0.
5. After a non-rejection write: "not sufficient evidence that …" at the stated level, with context. Never "accept H0", never "the alternative is rejected", and a significance level is not a confidence level.

Also: the 15 copies of x̄ are already inside x²../IJ in ANOVA; a negative SS is an alarm.

## 1. Sampling distribution of X̄ (S1)
- E(X̄) = μ, V(X̄) = σ²/n, sd = σ/√n. Total T0: mean nμ, sd √n·σ.
- Normal population: X̄ is exactly normal. Otherwise CLT: X̄ approximately normal when n > 40 (Dr H's cut, the tutor says 30).
- Standardise: Z = (X̄ − μ)/(σ/√n). Probability of a range for X̄: use the sd of X̄, never of X.

## 2. Point estimation (S2)
- Bias = E(θ̂) − θ. Unbiased: bias 0. MSE = V(θ̂) + bias².
- Point estimate = a number from the data; point estimator = the random variable (the formula). A true/false trap.
- Compare two unbiased estimators: choose smaller variance.
- Useful: V(p̂) = pq/n, V(p̂1 − p̂2) = p1q1/m + p2q2/n, E = p1 − p2.

## 3. Proofs (skeletons, write every symbol, a mark per missing dot or bar)
- **MSE = V + bias²:** add and subtract E(θ̂), square, the cross term has E(θ̂ − E(θ̂)) = 0.
- **E(S²) = σ²:** Σ(Xi − X̄)² = ΣXi² − nX̄²; E(Xi²) = σ² + μ², E(X̄²) = σ²/n + μ²; get (n−1)σ². Divisor n gives bias −σ²/n.
- **X̄² − S²/n unbiased for μ²:** E(X̄²) = μ² + σ²/n, E(S²/n) = σ²/n.
- **p̂² bias:** E(p̂²) = p² + pq/n so bias = pq/n.
- **S_p² unbiased:** weights (m−1) and (n−1), each S² unbiased, weights sum to m+n−2.
- **CI for μ1 − μ2 (known σ):** X̄1 − X̄2 ~ N(μ1−μ2, σ1²/m + σ2²/n), standardise, P(−z ≤ Z ≤ z) = 1 − α, rearrange.
- **SST = SSTr + SSE:** add and subtract x̄_i., expand, cross term is Σ_i (x̄_i. − x̄..) Σ_j (x_ij − x̄_i.) = 0, the ends become SSE and SSTr (the one carrying the J). Dots: x_ij none, x̄_i. one, x̄.. two; grand mean has a bar, grand total does not.
- **Chi-square:** E_ij = n_i·n_j/n (independence gives p_i p_j, times n). χ² = ΣO²/E − n (expand the square, ΣO = ΣE = n).
- **Building distributions (Practical 2):** χ²_ν = ΣZ_i² (ν standard normals squared); t = Z/√(X/ν); F = (X1/ν1)/(X2/ν2). Independence of numerator and denominator is a condition.

## 4. Confidence intervals (S3, S4, S6, S7)
| Parameter | Interval | Notes |
|---|---|---|
| μ, σ known | x̄ ± z_{α/2} σ/√n | |
| μ, σ unknown | x̄ ± t_{α/2,n−1} s/√n | normal population |
| p | p̂ ± z_{α/2}√(p̂q̂/n) | |
| σ² | ((n−1)s²/χ²_{α/2,n−1}, (n−1)s²/χ²_{1−α/2,n−1}) | lower bound uses the upper chi-square |
| μ1 − μ2, σ known | (x̄1−x̄2) ± z_{α/2}√(σ1²/m+σ2²/n) | |
| μ1 − μ2, pooled t | (x̄1−x̄2) ± t_{α/2,m+n−2} s_p√(1/m+1/n) | s_p² = [(m−1)s1² + (n−1)s2²]/(m+n−2); equal variances assumed |
| paired μ_D | d̄ ± t_{α/2,n−1} s_d/√n | one sample of differences |
| p1 − p2 | (p̂1−p̂2) ± z_{α/2}√(p̂1q̂1/m + p̂2q̂2/n) | |
| prediction (one new value) | x̄ ± t s√(1 + 1/n) | wider than the CI |

- Sample size for width: n = (z_{α/2}σ/E)² for a mean; n = z²_{α/2} p̂q̂/E² for a proportion (p̂ = 0.5 if unknown). "Within" means E; "width" means 2E. Round up.
- df rule from Dr H: if the exact df is not in the table, use the closest listed value.

## 5. Type I, Type II, sample size (S5, the concept you cracked)
- α = P(reject H0 | H0 true) = area of the H0 curve in the rejection region.
- β = P(fail to reject | H0 false at the true value μ') = area of the μ' curve in the **complement** of the rejection region.
- c is a vertical line in the overlap of the two curves, between μ0 and μ' (halfway only if α = β). It is the x̄ whose p-value is exactly α.
- Direction decides the picture: H_a: μ < μ0 → rejection region left of c, β to the right. H_a: μ > μ0 → rejection right of c, β to the left. Two-sided: α/2 in each tail (z_{α/2}); β uses the true mean's curve and the nearer boundary.
- Given a rejection region (e.g. X̄ > 32, true mean 31): Type II = P(X̄ ≤ 32 | μ = 31).
- **Find n (derive it, no formula given).** Start at μ0 and walk toward μ' by z_α·se; start at μ' and walk toward μ0 by z_β·se. Both reach c, so equate and solve. Round n up.

| H_a | c from α | c from β | n |
|---|---|---|---|
| μ < μ0 | $\mu_0 - z_\alpha\frac{\sigma}{\sqrt n}$ | $\mu' + z_\beta\frac{\sigma}{\sqrt n}$ | $\left[\frac{\sigma(z_\alpha+z_\beta)}{\mu_0-\mu'}\right]^2$ |
| μ > μ0 | $\mu_0 + z_\alpha\frac{\sigma}{\sqrt n}$ | $\mu' - z_\beta\frac{\sigma}{\sqrt n}$ | $\left[\frac{\sigma(z_\alpha+z_\beta)}{\mu'-\mu_0}\right]^2$ |
| μ ≠ μ0 | use $z_{\alpha/2}$ and the boundary nearer μ' | | $\left[\frac{\sigma(z_{\alpha/2}+z_\beta)}{\lvert\mu'-\mu_0\rvert}\right]^2$ |

  Key: μ0 = H0 mean, μ' = the true mean asked about, se = σ/√n, c = cut-off in x̄ units, z_α and z_β = the z leaving α or β to its right (always positive). Proportion: same, with √(p0q0) beside z_α and √(p'q') beside z_β, over (p' − p0).
- Worked check (Set C B5): c = 47.5325, β(47) = 0.3594, n = 34.2 → 35.

## 6. Pooled t and paired t (S6, S7)
- Pooled t: H0 μ1 − μ2 = Δ0, df m+n−2, assumption equal variances (sample sds within a factor of 2) plus normality.
- Paired: two measurements on the same unit → take differences, one-sample t on d̄ with df n−1. Independent groups → pooled. State which, and why.

## 7. ANOVA and Tukey (S8)
- H0: μ1 = … = μ_I; H_a: at least two differ. Assumptions (say both): normal populations, equal variances (largest sd not more than 2× smallest).
- SST = Σx² − x²../IJ; SSTr = Σx_i.²/J − x²../IJ; SSE = SST − SSTr. Order check: grand piece < group piece < every-value piece.
- df: I−1, I(J−1), IJ−1. MSTr = SSTr/(I−1), MSE = SSE/(I(J−1)), F = MSTr/MSE; reject if F ≥ F_{α,I−1,I(J−1)}.
- Tukey only after rejecting: w = Q_{α,I,I(J−1)}√(MSE/J). Second subscript I, not I−1; third is the error df. Means differing by more than w differ; joined means are "not shown to differ", not "equal".

## 8. Regression: interpretation only (S9, Practical 10)
- Slope b1: "for each one-unit increase in x, y changes by b1 on average" (use variable names and units).
- R²: "R² % of the variation in y is explained by the linear relationship with x"; **not explained = 100% − R²**.
- t, df and p are on the printout; F = t² for the slope.
- Predict only inside the data range (outside is extrapolation).
- Residuals vs fitted: constant variance. Normal probability plot: normality.
- No hand-calculated coefficients, no scatter plots.

## 9. Chi-square (S10)
- Counts in categories only. Statistic χ² = Σ(O−E)²/E, upper tail, reject if χ² ≥ χ²_{α,df}.
- **Goodness of fit:** H0: p_i = p_i0; E_i = n·p_i0; df = k−1.
- **Independence:** H0: the two classifications are independent; E = row total × column total / n; df = (I−1)(J−1).
- Assumption: **every expected count ≥ 5** (the expected, not the observed, not the df). Fix: larger n or combine cells.
- Write: hypotheses → expected counts and the ≥ 5 check → statistic in a table → df and cut-off → decision → plain-words conclusion.
- Which test? A number measured on each person → t or ANOVA. Only labels → chi-square. Three groups alone do not make it ANOVA.
- Table A.7 prints 3.843 (df 1) and 5.992 (df 2) in the .05 column. Homogeneity is out.
- Example: 52, 38, 21, 9 against 40/30/20/10% of 120 → E = 48, 36, 24, 12, χ² = 1.57 < 7.815, df 3, do not reject.

## 10. Wording bank
- Slope: "On average, each additional [x unit] is associated with a change of [b1] [y unit]."
- R²: "[R²]% of the variation in [y] is explained by the linear relationship with [x]."
- Reject: "At the [α] level there is sufficient evidence that …"
- Fail to reject: "At the [α] level there is not sufficient evidence that …"
- CI meaning: "We are [95]% confident that the true [parameter] lies between a and b."
- ANOVA: "At least two population means differ"; Tukey: "[A] and [B] differ significantly."

## 11. Out of scope (do not spend time)
One-sample hypothesis tests (Lecture 6, Tutorial 6), chi-square homogeneity, hand-calculated regression coefficients, scatter plots.

## 12. Tomorrow morning, in this order (20 minutes)
1. Section 0, aloud.
2. Draw the two curves for a lower-tailed and an upper-tailed test, shade α and β, write both descriptions of c.
3. Write the SST = SSTr + SSE and E(S²) = σ² proofs from a blank page.
4. Tables A.3, A.5, A.7, A.9, A.10: find one value in each.
