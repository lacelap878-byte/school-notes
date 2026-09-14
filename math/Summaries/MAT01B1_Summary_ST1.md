---
module: MAT01B1
test: ST1
tags: []
---

# ST1 Summary

## Material covered
- [[MAT01B1_Notes_S1_CalculusApplications]]
- [[MAT01B1_Proofs_ST1]]
- [[MAT01B1_Notes_S2_DerivativeIntegralReference]]
- [[MAT01B1_Notes_S3_IntegrationExamples]]

## Condensed concept pass

**Fermat's Theorem.** A local extremum with an existing derivative forces $f'(c)=0$. Converse false. (see: [[MAT01B1_Proofs_ST1#Fermat's Theorem]])

**Rolle's Theorem.** Same height at both endpoints forces a flat point somewhere strictly in between. (see: [[MAT01B1_Proofs_ST1#Rolle's Theorem]])

**Mean Value Theorem.** Instantaneous rate equals average rate somewhere in the interval, $f'(c)=\frac{f(b)-f(a)}{b-a}$. (see: [[MAT01B1_Proofs_ST1#Mean Value Theorem]])

**Theorem 5 / Corollary 7.** Zero derivative everywhere forces a constant function, equal derivatives force functions differing only by a constant, this is why antiderivatives carry $+C$. (see: [[MAT01B1_Proofs_ST1#Theorem 5 and Corollary 7]])

**Increasing/Decreasing Test.** Sign of $f'$ directly gives the direction the curve moves. (see: [[MAT01B1_Proofs_ST1#Increasing/Decreasing Test]])

**Curve sketching.** Critical points from $f'=0$, classify with a sign chart, concavity and inflection points from $f''$. (see: [[MAT01B1_Notes_S1_CalculusApplications#Curve sketching (added)]])

**Integration by Parts.** Reverse product rule, pick $u$ by LIATE. (see: [[MAT01B1_Notes_S2_DerivativeIntegralReference#Integration by Parts]])

**Trig substitution.** Matches a root of $a^2\pm b^2x^2$ to a sine, secant, or tangent substitution via a Pythagorean identity. (see: [[MAT01B1_Notes_S2_DerivativeIntegralReference#Trig substitutions]])

**Partial fractions.** Break a rational function back into the simple fractions that summed to make it, integrate each piece. (see: [[MAT01B1_Notes_S2_DerivativeIntegralReference#Partial fractions]])

**$\sin^n\cos^m$ and $\tan^n\sec^m$.** Strip one factor for the substitution's $du$, convert the rest with a Pythagorean identity. The $\tan^n\sec^m$, $n$ even $m$ odd case needs the secant reduction formula. (see: [[MAT01B1_Notes_S2_DerivativeIntegralReference#Products and quotients of trig functions]])

**Derivatives of inverse trig and inverse hyperbolic functions.** Both families come from implicit differentiation plus a Pythagorean or hyperbolic identity, the trig set picks up an absolute value from a domain sign split that the hyperbolic set never needs. (see: [[MAT01B1_Proofs_ST1#Derivatives of inverse trig functions (added, absent from the source entirely)|derivatives of inverse trig functions]], [[MAT01B1_Proofs_ST1#Derivatives of inverse hyperbolic functions (added, absent from the source entirely)|derivatives of inverse hyperbolic functions]])

**Improper integrals.** Type I (infinite interval) and Type II (asymptote in the interval) both defined as a limit. $p$-integral test and Comparison Test decide convergence when the antiderivative is hard or impossible. (see: [[MAT01B1_Notes_S1_CalculusApplications#Improper integrals (added)]])

## Worked example notebook
- $x^3-3x^2$ sign chart and concavity, (source: [[MAT01B1_Notes_S1_CalculusApplications#Curve sketching (added)]])
- $\int xe^x\,dx$, Integration by Parts via LIATE, (source: [[MAT01B1_Notes_S3_IntegrationExamples#Integration by Parts]])
- $\int \frac{dx}{\sqrt{9-x^2}}$, trig substitution, (source: [[MAT01B1_Notes_S3_IntegrationExamples#Trig Substitution]])
- $\int \frac{3x+5}{(x-1)(x+2)}\,dx$, partial fractions, distinct linear factors, (source: [[MAT01B1_Notes_S3_IntegrationExamples#Partial Fractions]])
- $\int \sin^3x\cos^2x\,dx$, $n$ odd case, (source: [[MAT01B1_Notes_S3_IntegrationExamples#$\sin^n x \cos^m x$]])
- $\int \tan^3x\sec^3x\,dx$, $\int \tan^2x\sec^4x\,dx$, $\int \tan^2x\sec^3x\,dx$, the three $\tan^n\sec^m$ cases, (source: [[MAT01B1_Notes_S3_IntegrationExamples#$\tan^n x \sec^m x$]])
- Strategy recognition: u-sub into IBP, trig identity vs trig substitution, partial fractions vs trig substitution, (source: [[MAT01B1_Notes_S3_IntegrationExamples#Miscellaneous: mixing and matching strategies]])
- $\int_1^{\infty}\frac{1}{x^2}\,dx$, Type I convergent, (source: [[MAT01B1_Notes_S1_CalculusApplications#Improper integrals (added)]])
- $\int_0^1\frac{1}{\sqrt{x}}\,dx$, Type II convergent, (source: [[MAT01B1_Notes_S1_CalculusApplications#Improper integrals (added)]])
- $\int_1^{\infty}\frac{1}{\sqrt{x^3+1}}\,dx$, Comparison Test, (source: [[MAT01B1_Notes_S1_CalculusApplications#Improper integrals (added)]])

## Common mistakes
None flagged yet for this range, nothing to list without inventing one. Flag anything that trips you up while working through the notes and it goes here.

## Tips
None on file yet for this range, same reason as above.
