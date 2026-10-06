---
module: STA01B1
topic: ANOVA table routine for the test
tags: [formula, worked-example, common-mistake, exam-flagged, struggle]
---

# STA01B1: ANOVA table routine for the test

Not a session note. A one-page routine for building a single-factor ANOVA table quickly with a Casio fx-991ZA PLUS. It uses the computing formulas from the ANOVA lecture. The test information sheet asks for formula, then substitute, then simplify, then interpret, so every step below is written that way.

## 1. Set up (30 seconds)
- $H_0: \mu_1 = \mu_2 = \cdots = \mu_I$ and $H_a$: at least two means differ.
- Write $I$ (groups), $J$ (values per group) and $IJ$ (all values). For 3 groups of 5: $I = 3$, $J = 5$, $IJ = 15$.

## 2. Calculator, one group at a time (3 to 4 minutes)
The keys are for the fx-991ES PLUS family. Check them once with the example group below: you should see 65 and 855.
- `MODE`, `3`, `1` opens the one-column table.
- Type each value with `=` after it, then `AC`.
- `SHIFT`, `1`, `3`, `2`, `=` gives the group total.
- `SHIFT`, `1`, `3`, `1`, `=` gives the group's sum of squared values.
- Write both down straight away.
- For the next group, `SHIFT`, `1`, `2` reopens the table. Type over the old values (every group has the same $J$).

## 3. The three pieces (2 minutes)
- Grand total $x_{\cdot\cdot}$: add the group totals.
- Every value squared, added: $\displaystyle\sum_i\sum_j x_{ij}^2$ is the sum of the groups' sums of squares.
- Group totals piece: $\displaystyle\sum_i \frac{x_{i\cdot}^2}{J}$ is each group total squared, added, divided by $J$.
- Grand total piece: $\displaystyle\frac{x_{\cdot\cdot}^2}{IJ}$ is the grand total squared, divided by $IJ$. Box it. It is one number.

> [!warning] Order check, every time
> The grand total piece is the smallest, then the group totals piece, then the every-value piece. If they are not in that order, one of them is wrong. Fix it before building the table.

## 4. The three sums of squares (1 minute)
Write the formula, substitute, simplify.

$$SST = \sum_i\sum_j x_{ij}^2 - \frac{x_{\cdot\cdot}^2}{IJ}$$

$$SSTr = \sum_i \frac{x_{i\cdot}^2}{J} - \frac{x_{\cdot\cdot}^2}{IJ}$$

$$SSE = SST - SSTr$$

## 5. The table (2 minutes)
- df: treatments $I - 1$, error $I(J-1)$, total $IJ - 1$.
- $MSTr = SSTr/(I-1)$ and $MSE = SSE/[I(J-1)]$.
- $F = MSTr/MSE$.
- Check: the df add up, the sums of squares add up, and $F$ is positive.

## 6. Decision and interpretation (1 minute)
- Read $F_{\alpha,\,I-1,\,I(J-1)}$ from the table. If $F$ is larger, reject $H_0$.
- Say it in words for the context: at the stated level there is evidence that at least two group means differ.
- If $H_0$ is rejected, Tukey comes next: $w = Q_{\alpha,\,I,\,I(J-1)}\sqrt{MSE/J}$. The second subscript is $I$ and the third is the error df, not the total df.

## Slips to avoid #common-mistake #struggle
- Multiplying the grand total piece by $IJ$ again. The 15 copies are already inside $x_{\cdot\cdot}^2/IJ$, so doing it again gives a huge negative $SST$. The double sum belongs only on the first term.
- Using means where totals belong. In the computing formulas $x_{i\cdot}$ and $x_{\cdot\cdot}$ are totals, with no bars.
- Dividing by the wrong count: the group totals piece by $J$, the grand total piece by $IJ$.
- Reading a negative sum of squares as an answer. It is an alarm. Go back to the order check.

## Worked example (composite) #worked-example
Group 1: 12, 15, 11, 14, 13. Group 2: 18, 16, 20, 17, 19. Group 3: 14, 13, 16, 12, 15.

| Group | total | sum of squares |
|---|---|---|
| 1 | 65 | 855 |
| 2 | 90 | 1630 |
| 3 | 70 | 990 |

- $x_{\cdot\cdot} = 225$.
- Every value squared, added: $855 + 1630 + 990 = 3475$.
- Group totals piece: $(65^2 + 90^2 + 70^2)/5 = 3445$.
- Grand total piece: $225^2/15 = 3375$.
- Order check: $3375 < 3445 < 3475$.

$$SST = 3475 - 3375 = 100 \qquad SSTr = 3445 - 3375 = 70 \qquad SSE = 100 - 70 = 30$$

| Source | df | SS | MS | F |
|---|---|---|---|---|
| Treatments | 2 | 70 | 35 | 14 |
| Error | 12 | 30 | 2.5 | |
| Total | 14 | 100 | | |

$F_{.05,2,12} = 3.89$ and $14 > 3.89$, so reject $H_0$.

## Time budget
Set up 0.5 min, calculator 3 to 4 min, three pieces and check 2 min, sums of squares 1 min, table 2 min, decision 1 min. About 10 minutes, with 4 or 5 groups taking a minute or two more on data entry.

## See also
- [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]] for the full ANOVA notes and the lecturer's proof that $SST = SSTr + SSE$.
