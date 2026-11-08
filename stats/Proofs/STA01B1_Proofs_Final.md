# STA01B1 Final: Proofs (S1 to S10)

Notation: V(·) for variance, E(·) for expectation, σ² = V(X), q = 1 − p. Every symbol written out, every dot and bar kept. Each proof ends with the line you can copy as the conclusion.

Facts used throughout:
- (F1) V(X) = E(X²) − [E(X)]², so E(X²) = V(X) + [E(X)]².
- (F2) E(aX + bY) = aE(X) + bE(Y). For independent X, Y: V(aX + bY) = a²V(X) + b²V(Y).
- (F3) For X1, …, Xn iid with mean μ, variance σ²: E(X̄) = μ, V(X̄) = σ²/n.

---

## P1. MSE = V(θ̂) + bias²
MSE(θ̂) = E[(θ̂ − θ)²].
1. Add and subtract E(θ̂): θ̂ − θ = [θ̂ − E(θ̂)] + [E(θ̂) − θ].
2. Square: (θ̂ − θ)² = [θ̂ − E(θ̂)]² + 2[θ̂ − E(θ̂)][E(θ̂) − θ] + [E(θ̂) − θ]².
3. Take E. The bracket [E(θ̂) − θ] is a constant, so the middle term is 2[E(θ̂) − θ]·E[θ̂ − E(θ̂)] = 2[E(θ̂) − θ]·0 = 0.
4. E[θ̂ − E(θ̂)]² = V(θ̂), and [E(θ̂) − θ]² = bias².

**Therefore MSE(θ̂) = V(θ̂) + [bias(θ̂)]².**

## P2. E(S²) = σ²   (S² = Σ(Xi − X̄)²/(n−1))
1. Σ(Xi − X̄)² = ΣXi² − 2X̄ΣXi + nX̄² = ΣXi² − 2nX̄² + nX̄² = ΣXi² − nX̄².
2. E(Xi²) = σ² + μ² (F1). E(X̄²) = V(X̄) + μ² = σ²/n + μ².
3. E[ΣXi² − nX̄²] = n(σ² + μ²) − n(σ²/n + μ²) = nσ² + nμ² − σ² − nμ² = (n − 1)σ².
4. Divide by n − 1.

**Therefore E(S²) = σ², so S² is unbiased for σ².**

## P3. Divisor n: bias of σ̂² = Σ(Xi − X̄)²/n
1. From P2 step 3: E[Σ(Xi − X̄)²] = (n − 1)σ².
2. E(σ̂²) = (n − 1)σ²/n = σ² − σ²/n.
3. bias = E(σ̂²) − σ² = **−σ²/n**. It underestimates σ², the bias shrinks as n grows (asymptotically unbiased).

## P4. X̄² − S²/n is unbiased for μ²
1. E(X̄²) = V(X̄) + [E(X̄)]² = σ²/n + μ².
2. E(S²/n) = E(S²)/n = σ²/n (P2).
3. E(X̄² − S²/n) = σ²/n + μ² − σ²/n = μ².

**Therefore X̄² − S²/n is unbiased for μ².** (X̄² alone has bias σ²/n.)

## P5. Bias of p̂²   (p̂ = X/n, X ~ Bin(n, p))
1. E(p̂) = p and V(p̂) = pq/n.
2. E(p̂²) = V(p̂) + [E(p̂)]² = pq/n + p².
3. bias = E(p̂²) − p² = **pq/n**. p̂² overestimates p².

## P6. E and V of p̂1 − p̂2   (independent samples of size m and n)
1. E(p̂1) = p1, E(p̂2) = p2, so E(p̂1 − p̂2) = **p1 − p2** (unbiased).
2. V(p̂1) = p1q1/m, V(p̂2) = p2q2/n.
3. Independent, so V(p̂1 − p̂2) = V(p̂1) + (−1)²V(p̂2) = **p1q1/m + p2q2/n**.

## P7. A linear combination: θ̂1 = (X1 + 3X2)/4
Given X1, X2 independent with mean μ, variance σ².
1. E(θ̂1) = (μ + 3μ)/4 = μ: unbiased.
2. V(θ̂1) = (1/16)(σ² + 9σ²) = 10σ²/16 = 5σ²/8.
3. Compare with X̄ = (X1 + X2)/2: V(X̄) = σ²/2 = 4σ²/8 < 5σ²/8. Both unbiased, so **choose the smaller variance (X̄)**.

Rule: weights summing to 1 keep it unbiased; variance is Σ(weight²)σ².

## P8. Pooled variance S_p² is unbiased for σ²
S_p² = [(m−1)S1² + (n−1)S2²]/(m + n − 2), both samples from populations with common σ².
1. E(S1²) = E(S2²) = σ² (P2).
2. E(S_p²) = [(m−1)σ² + (n−1)σ²]/(m + n − 2) = (m + n − 2)σ²/(m + n − 2) = **σ²**.

## P9. Confidence interval for μ1 − μ2 (σ1², σ2² known, independent normal samples)
1. X̄1 ~ N(μ1, σ1²/m), X̄2 ~ N(μ2, σ2²/n), independent.
2. X̄1 − X̄2 ~ N(μ1 − μ2, σ1²/m + σ2²/n).
3. Z = [(X̄1 − X̄2) − (μ1 − μ2)] / √(σ1²/m + σ2²/n) ~ N(0, 1).
4. P(−z_{α/2} ≤ Z ≤ z_{α/2}) = 1 − α.
5. Multiply through by the standard error, subtract (X̄1 − X̄2), multiply by −1 (reversing the inequalities).

**(X̄1 − X̄2) ± z_{α/2}√(σ1²/m + σ2²/n) is a 100(1 − α)% CI for μ1 − μ2.**

(One-sample version: same steps with Z = (X̄ − μ)/(σ/√n), giving X̄ ± z_{α/2}σ/√n. With σ unknown, replace σ by S and z by t_{α/2,n−1}.)

## P10. SST = SSTr + SSE   (I groups, J values each; x̄_i. group mean, x̄.. grand mean)
SST = ΣiΣj(x_ij − x̄..)², SSTr = JΣi(x̄_i. − x̄..)², SSE = ΣiΣj(x_ij − x̄_i.)².
1. Add and subtract x̄_i.: x_ij − x̄.. = (x_ij − x̄_i.) + (x̄_i. − x̄..).
2. Square and sum: SST = ΣiΣj(x_ij − x̄_i.)² + 2ΣiΣj(x_ij − x̄_i.)(x̄_i. − x̄..) + ΣiΣj(x̄_i. − x̄..)².
3. First term is SSE (no J).
4. Last term: (x̄_i. − x̄..)² does not depend on j, so ΣiΣj = JΣi(x̄_i. − x̄..)² = SSTr (carries the J).
5. Middle term: for fixed i, (x̄_i. − x̄..) is constant in j, so it equals 2Σi(x̄_i. − x̄..)Σj(x_ij − x̄_i.). Using Σj x_ij = J x̄_i., Σj(x_ij − x̄_i.) = J x̄_i. − J x̄_i. = 0, so the middle term is 0.

**Therefore SST = SSTr + SSE.**

Computing forms: SST = ΣΣx_ij² − x²../(IJ); SSTr = Σx_i.²/J − x²../(IJ) (totals, no bars).

## P11. Expected count in a two-way table: E_ij = n_i· n_·j / n
1. Under H0 (independence): P(row i and column j) = P(row i)P(column j) = p_i· p_·j.
2. Expected count = n × p_i· p_·j.
3. Estimate p_i· by n_i·/n and p_·j by n_·j/n.
4. E_ij = n (n_i·/n)(n_·j/n) = **n_i· n_·j / n** (row total × column total ÷ grand total).

## P12. χ² = Σ O²/E − n
1. (O − E)²/E = O²/E − 2O + E.
2. Sum over all cells: Σ(O − E)²/E = ΣO²/E − 2ΣO + ΣE.
3. ΣO = ΣE = n, so −2n + n = −n.

**Therefore Σ(O − E)²/E = ΣO²/E − n.**

## P13. Sample size n from α and β (lower-tailed, H0: μ = μ0, true μ' < μ0, σ known)
Rejection region: X̄ ≤ c.
1. α: P(X̄ ≤ c | μ0) = α, so (c − μ0)/(σ/√n) = −z_α, i.e. **c = μ0 − z_α σ/√n**.
2. β: P(X̄ > c | μ') = β, so (c − μ')/(σ/√n) = z_β, i.e. **c = μ' + z_β σ/√n**.
3. Equate: μ0 − z_α σ/√n = μ' + z_β σ/√n.
4. (μ0 − μ') = (z_α + z_β)σ/√n, so √n = σ(z_α + z_β)/(μ0 − μ').

**n = [σ(z_α + z_β)/(μ0 − μ')]², rounded UP.**

- Upper-tailed (μ' > μ0): c = μ0 + z_α σ/√n and c = μ' − z_β σ/√n, giving n = [σ(z_α + z_β)/(μ' − μ0)]².
- Two-sided: replace z_α by z_{α/2} (use the boundary nearer to μ').
- Proportion: c = p0 − z_α√(p0q0/n) = p' + z_β√(p'q'/n), so n = [(z_α√(p0q0) + z_β√(p'q'))/(p' − p0)]².

## P14. Sample size for a CI of half-width E
1. Error bound: E = z_{α/2}σ/√n.
2. Solve: √n = z_{α/2}σ/E, so **n = (z_{α/2}σ/E)²**, rounded up.
3. Proportion: E = z_{α/2}√(p̂q̂/n), so **n = z²_{α/2} p̂q̂/E²** (p̂ = 0.5 when unknown, since p̂q̂ ≤ 0.25).

## P15. Building χ², t and F (Practical 2)
- **χ²_ν**: if Z1, …, Zν are independent N(0,1), then ΣZi² ~ χ²_ν. Example: (n−1)S²/σ² ~ χ²_{n−1}.
- **t_ν**: if Z ~ N(0,1) and X ~ χ²_ν are independent, then T = Z/√(X/ν) ~ t_ν. Example: Z = (X̄ − μ)/(σ/√n), X = (n−1)S²/σ², ν = n − 1, so T = (X̄ − μ)/(S/√n).
- **F_{ν1,ν2}**: if X1 ~ χ²_{ν1} and X2 ~ χ²_{ν2} are independent, then F = (X1/ν1)/(X2/ν2) ~ F_{ν1,ν2}. Example: ANOVA, F = MSTr/MSE.
- Independence of the pieces is a stated condition each time.

## Quick checks for a blank-page sit
- P1, P2, P10 are the three most likely: write them from memory first.
- Mark-losers: missing dots (x_ij, x̄_i., x̄..), missing bars on means, the J in SSTr, a missing "= 0" justification for the cross term.
