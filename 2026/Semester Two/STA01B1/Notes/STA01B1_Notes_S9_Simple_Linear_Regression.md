---
module: STA01B1
topic: Simple Linear Regression
session: S9
tags: [definition, formula, theorem, worked-example, common-mistake, exam-flagged, struggle, added]
---

# STA01B1 Notes S9: Simple Linear Regression

Source: Lecture 10.pdf, 31 slides numbered as printed on the deck (slide 1 is the title card and slide 31 is blank, so content runs from slide 2 to slide 30). The lecture is headed Chapter 12 and refers back to Chapter 10 (ANOVA) and Chapter 11 (diagnostics).

Labels used: `(source, slide N)`, `(composite)` for a worked example built here, `(added)` for anything beyond the slides.

> [!note] No source examples
> Examples 12.1, 12.2, 12.4 and 12.12 are named on the slides but their data and working are not shown. Every worked example in these notes is therefore a composite, built on one small data set that is carried from the line through to the intervals (see: Worked example, start to finish).

## Why regression (source, slides 2 to 4)

Chapter 10 used ANOVA to ask whether treatment means differ. Regression asks a different question: a response $y$ is affected by one or more independent variables $x_i$, and the aim is to use what the $x_i$ tell us to predict $y$.

Slide example: let $y$ be monthly sales revenue for a company. It might depend on $x_1$ = advertising expenditure, $x_2$ = time of year, $x_3$ = state of the economy, $x_4$ = size of inventory. We want to predict $y$ from $x_1, x_2, x_3, x_4$.

Three questions drive the chapter:
- Which of the independent variables are useful, and which are not?
- How can we build a prediction equation to predict $y$?
- How good is that prediction?

The lecture starts with the simplest case, a response $y$ that depends on a single independent variable $x$. Everything below is that case.

## The scatter plot (source, slides 5 to 7)

Pairs of numbers $(x, y)$ drawn as points on a two-dimensional graph form a scatter plot. The point $(2, 5)$ means $x = 2$, $y = 5$.

Three things to read off it:
- Form: a straight line sloping up or down, a curve, or no pattern at all.
- Strength: how tightly the points follow the pattern, strong or weak.
- Unusual observations: clusters or outliers.

Slide 7 shows four pictures: positive linear and strong, negative linear and weak, curvilinear (a hump), and no relationship. Two numerical measures then describe a linear relationship: one for its form (the equation of the line) and one for its strength and direction (the correlation, see: Strength of the relationship).

## Two models for the whole population (source, slides 8 to 11) #definition

For a sample of $n$ pairs we can simply fit the equation of a line. To describe the relationship for the whole population there are two models.

Deterministic model, every point exactly on the line:

$$y = \beta_0 + \beta_1 x$$

Probabilistic model, the line plus a random error:

$$y = \beta_0 + \beta_1 x + \varepsilon$$

Bivariate measurements almost never fall exactly on a straight line, so the course uses the probabilistic model. Its pieces:
- $\beta_0$ is the population intercept and $\beta_1$ the population slope. Both are unknown and are estimated from the sample.
- $E(y) = \beta_0 + \beta_1 x$ is the line of means. It gives the average value of $y$ for any fixed value of $x$.
- $\varepsilon$ is the random error. The population of measurements is generated as $y$ deviates from the line of means by $\varepsilon$.

(added) Reading the parameters: $\beta_1$ is the change in the average $y$ for a one unit increase in $x$. $\beta_0$ is the average $y$ at $x = 0$, which can be meaningless if $x = 0$ is far outside the data.

### The assumptions on the error (source, slide 10)

$\varepsilon$ has a normal distribution with mean 0 and common variance $\sigma^2$.

Said about $y$ itself (added): at each fixed $x$, $y$ is normal with mean $\beta_0 + \beta_1 x$ and variance $\sigma^2$. The slide 11 picture shows exactly this, three bell curves standing on the line at $x_1, x_2, x_3$, all with the same spread. These are the same normal, equal-variance assumptions as in ANOVA, now placed on $\varepsilon$. Every test and interval below relies on them, and the residual plots in the diagnostics section are how you check them.

## The method of least squares (source, slides 12 and 13) #definition #formula

The best-fitting line is calculated from $n$ pairs $(x_i, y_i)$. The estimates $b_0$ and $b_1$ are chosen so that the vertical distances of the points from the line are as small as possible.

$$\hat{y} = b_0 + b_1 x$$

$$SSE = \Sigma\left(y_i - b_0 - b_1 x_i\right)^2$$

$b_0$ and $b_1$ are the values that minimise $SSE$. Each term is one point's vertical miss from the line. The misses are squared so that points above and below the line do not cancel, and so that large misses count for more (added).

The least squares estimators (source, slide 13):

$$b_1 = \frac{S_{xy}}{S_{xx}} \qquad b_0 = \bar{y} - b_1\bar{x}$$

$$S_{xy} = \Sigma x_i y_i - \frac{(\Sigma x_i)(\Sigma y_i)}{n}$$

$$S_{xx} = \Sigma x_i^2 - \frac{(\Sigma x_i)^2}{n}$$

Find $b_1$ first, since $b_0$ uses it. The line always passes through $(\bar{x}, \bar{y})$, which follows from the formula for $b_0$.

> [!warning] Totals, not means, in S_xx and S_xy #struggle #common-mistake
> $\Sigma x_i^2$ means square each value and then add. $(\Sigma x_i)^2$ means add first and then square the total. In the second term the total is divided by $n$, the number of values inside that total. This is the same shape as the ANOVA computing formulas, a total squared over the count in it. Two sanity checks: $S_{xx}$ is a sum of squares and can never be negative, and the two terms being subtracted should be of similar size. A negative answer almost always means the two terms were built differently, for example one divided by $n$ and the other not.

### Where the estimators come from (added) #theorem

Set the two partial derivatives of $SSE$ to zero.

$$\frac{\partial SSE}{\partial b_0} = -2\Sigma(y_i - b_0 - b_1x_i) = 0 \;\Rightarrow\; \Sigma e_i = 0 \;\Rightarrow\; b_0 = \bar{y} - b_1\bar{x}$$

Here $e_i = y_i - \hat{y}_i$ is the residual of point $i$. The derivative with respect to $b_1$ gives

$$\frac{\partial SSE}{\partial b_1} = -2\Sigma x_i(y_i - b_0 - b_1x_i) = 0 \;\Rightarrow\; \Sigma x_i e_i = 0$$

Substituting $b_0 = \bar{y} - b_1\bar{x}$ into this gives $\Sigma x_i(y_i - \bar{y}) = b_1\Sigma x_i(x_i - \bar{x})$. The left side is $S_{xy}$ and the sum on the right is $S_{xx}$, so $S_{xy} = b_1S_{xx}$, which is $b_1 = S_{xy}/S_{xx}$.

The two conditions found on the way, $\Sigma e_i = 0$ and $\Sigma x_ie_i = 0$, are used twice later: to prove that the total sum of squares splits, and to count the degrees of freedom.

## Fits and residuals (source, slides 12, 17, 24, with added explanation) #definition

A fit is the value the line predicts at an observed $x_i$:

$$\hat{y}_i = b_0 + b_1x_i$$

It is not a group mean. It is the point on the fitted line directly above or below the observed point, and it estimates the average $y$ at that $x$. The residual is what is left over:

$$\text{Residual} = y_i - \hat{y}_i$$

The residual error is the leftover variation in each data point after the variation explained by the regression model has been removed (source, slide 24). If all assumptions have been met, the residuals should be normal with mean 0 and variance $\sigma^2$.

(added) Two facts follow from the derivation above. The residuals add to 0, so the fits average to $\bar{y}$. And $\Sigma x_ie_i = 0$. In the residuals-versus-fits plot, the horizontal axis is just these fitted values.

## Total variation and its two parts (source, slides 15 to 17) #formula

The total variation in the responses is measured by the total sum of squares:

$$\text{Total } SS = S_{yy} = \Sigma(y_i - \bar{y})^2 = \Sigma y_i^2 - \frac{(\Sigma y_i)^2}{n}$$

It is divided into two parts:
- $SSR$ (sum of squares for regression): the variation explained by using $x$ in the model.
- $SSE$ (sum of squares for error): the leftover variation not explained by $x$.

$$SSR = \Sigma(\hat{y}_i - \bar{y})^2$$

> [!warning] Slide 17 is missing a formula
> Slide 17 lists "Sum of squares for error" and then leaves the space blank. The formula is the one from the method of least squares, $SSE = \Sigma(y_i - \hat{y}_i)^2$, because $b_0 + b_1x_i$ is just $\hat{y}_i$. Slide 15 states that Total $SS = SSR + SSE$, so equivalently $SSE = \text{Total } SS - SSR$. This has been put to the lecturer as a probable omission.

### Why the total splits (added) #theorem

Write $y_i - \bar{y} = (y_i - \hat{y}_i) + (\hat{y}_i - \bar{y})$, square, and add over all points:

$$\text{Total } SS = SSE + SSR + 2\Sigma e_i(\hat{y}_i - \bar{y})$$

The cross term vanishes. Using $\hat{y}_i = b_0 + b_1x_i$,

$$\Sigma e_i(\hat{y}_i - \bar{y}) = (b_0 - \bar{y})\Sigma e_i + b_1\Sigma x_ie_i = 0 + 0$$

by the two conditions from the derivation of the estimators. So $\text{Total } SS = SSR + SSE$.

> *The shape is the same as the ANOVA proof that $SST = SSTr + SSE$: expand a square, and a middle term cancels. The cancelling is done differently here, using the two least squares conditions instead of the group-mean rule, so do not mix the two proofs up. The ANOVA one is the proof the lecturer flagged as likely worth marks. I have no sign that this regression one is examined, so I have kept it as an (added) explanation, not as a memorise-this proof.*

### Two shortcuts for SSR (added) #formula

Because $b_0 = \bar{y} - b_1\bar{x}$, each fit minus the mean is $\hat{y}_i - \bar{y} = b_1(x_i - \bar{x})$. Squaring and adding,

$$SSR = b_1^2S_{xx} = b_1S_{xy} = \frac{S_{xy}^2}{S_{xx}}$$

This lets you get $SSR$ by hand without computing any fits.

## Strength of the relationship (source, slides 14 and 15) #formula #exam-flagged

$$r = \frac{S_{xy}}{\sqrt{S_{xx}S_{yy}}} \quad \text{(correlation coefficient)}$$

$$r^2 = \frac{S_{xy}^2}{S_{xx}S_{yy}} \quad \text{(coefficient of determination)}$$

Since Total $SS = SSR + SSE$, $r^2$ measures:
- the proportion of the total variation in the responses that can be explained by using the independent variable $x$ in the model, and
- the percent reduction in the total variation from using the regression equation rather than just the sample mean $\bar{y}$ to estimate $y$.

$$r^2 = \frac{SSR}{\text{Total } SS}$$

The slide marks this last formula NB!!. It agrees with the first one: $\dfrac{S_{xy}^2}{S_{xx}S_{yy}} = \dfrac{S_{xy}^2/S_{xx}}{S_{yy}} = \dfrac{SSR}{\text{Total } SS}$ (added).

(added) $r$ takes the sign of $S_{xy}$, which is the sign of the slope $b_1$, so it also gives direction. $r^2$ has no sign and lies between 0 and 1. A high $r^2$ does not show that a straight line is the right model, which is what the residual plots are for.

> [!warning] r versus r-squared, and which sum of squares #struggle #common-mistake
> With $SSR = 45$ and $SSE = 15$, Total $SS = 60$ and $r^2 = 45/60 = 0.75$, not $15/60$ (that is the unexplained share) and not $45/15$ (not a proportion). Then $r = \sqrt{0.75} = 0.866$ with the slope's sign. Two slips to avoid: dividing by $SSE$, and reporting $r^2$ when the question asks for $r$.

## The ANOVA table and the degrees of freedom (source, slide 18) #formula

| Source | df | SS | MS | F |
|---|---|---|---|---|
| Regression | 1 | $SSR$ | $SSR/(1)$ | $MSR/MSE$ |
| Error | $n-2$ | $SSE$ | $SSE/(n-2)$ | |
| Total | $n-1$ | Total $SS$ | | |

$MSR = SSR/(1)$ and $MSE = SSE/(n-2)$. Total df $= n - 1$, regression df $= 1$, error df $= n - 1 - 1 = n - 2$.

### Why the regression df is 1 (explanation from session, added) #struggle

A sum of squares is built from a list of numbers, and its df is how many of those numbers are free to choose before the rest are forced. Count them for the example data, where $y_i - \bar{y}$ is $-2, -1, 1, 2$, the residuals are $0.1, -0.3, 0.3, -0.1$, and the fits minus $\bar{y}$ are $-2.1, -0.7, 0.7, 2.1$.

- Total SS, 4 numbers $y_i - \bar{y}$: they must add to 0, so pick three and the fourth is forced. Free: $3 = n - 1$.
- SSE, 4 residuals: they satisfy two conditions, $\Sigma e_i = 0$ and $\Sigma x_ie_i = 0$ (check: $1(0.1) + 2(-0.3) + 3(0.3) + 4(-0.1) = 0$). Two conditions on four numbers leave 2 free: $n - 2$.
- SSR, 4 numbers $\hat{y}_i - \bar{y}$: each equals $b_1(x_i - \bar{x})$, here $1.4 \times (-1.5), 1.4 \times (-0.5), 1.4 \times 0.5, 1.4 \times 1.5$. The $x$ values are fixed, so choosing $b_1$ fixes all four. Free: $1$.

$$\underbrace{3}_{\text{Total}} = \underbrace{1}_{\text{Regression}} + \underbrace{2}_{\text{Error}}$$

The rule is regression df = the number of slopes, not the number of dimensions or variables. The intercept is forced once the slope is known, since the line must pass through $(\bar{x}, \bar{y})$, and its cost is already paid in Total df $= n - 1$ (subtracting $\bar{y}$ uses one df). The error df $n - 2$ pays for both estimated parameters, $b_0$ and $b_1$.

With $k$ predictors the pattern is regression df $= k$ and error df $= n - k - 1$. For two predictors and $n = 20$: regression 2, error 17, Total 19 $= 2 + 17$. It is only 1 here because there is one slope. Compare ANOVA, where treatments had $I - 1$ df.

## Testing the usefulness of the model (source, slides 19 to 21) #formula #exam-flagged

### The t test for the slope (slide 19)

You can test the usefulness of $x$ in predicting $y$ with a $t$ test. As printed on the slide:

$$H_0: \beta = 0 \quad \text{versus} \quad H_a: \beta \neq 0$$

$$t = \frac{b - \beta_0}{\sqrt{\dfrac{MSE}{S_{xx}}}}$$

(added) Here $b$ is the slope estimate $b_1$, and the $\beta_0$ on this slide is the hypothesised slope, 0, not the intercept (see: Where the source is inconsistent). So under $H_0$,

$$t = \frac{b_1}{\sqrt{MSE/S_{xx}}}$$

on $n - 2$ df. The denominator is the standard error of $b_1$. It shrinks when $S_{xx}$ is large, which makes sense: the more spread out the $x$ values, the better the slope is pinned down.

### The F test for the model (slide 20)

If the model is useful, $MSR$ will be large compared with the unexplained variation $MSE$. As printed on the slide, to test $H_0$: model is useful in predicting $y$,

$$F = \frac{MSR}{MSE}$$

Reject $H_0$ if $F > F_{\alpha}$ with 1 and $n - 2$ df. The slide notes this test is exactly equivalent to the $t$ test, with $t^2 = F$.

> [!warning] Slide 20 states the null the wrong way round #common-mistake
> "$H_0$: model is useful in predicting $y$" is backwards. The null is that the model is not useful, which is the same as slope 0. A large $F$ rejects that null and so supports usefulness. Write it as slope 0 in an exam.

### Why $t^2 = F$ (added) #theorem

$$t^2 = \frac{b_1^2}{MSE/S_{xx}} = \frac{b_1^2S_{xx}}{MSE} = \frac{SSR}{MSE} = \frac{MSR}{MSE} = F$$

using $SSR = b_1^2S_{xx}$ and $MSR = SSR/1$. So the two tests are one test seen two ways. $F$ is a ratio of mean squares and can never be negative, and squaring $t$ removes its sign, so a two-sided $t$ test and the $F$ test always give the same decision.

### Why the course gives both (explanation from session, added)

With a single $x$ they are the same test. The $t$ version is about one parameter, so it can also be one-sided or test a slope other than 0. The $F$ version asks whether the model as a whole explains more than it leaves unexplained. With several $x$'s the model has several slopes: one $F$ test still asks whether any of it helps, while each slope has its own $t$ test, and now they differ. The $t$ distribution also appears in the intervals, because $MSE$ estimates $\sigma^2$ on $n - 2$ df.

### Reading a non-significant slope (slide 21)

Failing to reject $H_0$: slope $= 0$ does not necessarily mean $y$ and $x$ are unrelated.
- A Type II error means falsely declaring that the slope is 0 and that $x$ and $y$ are unrelated.
- $y$ and $x$ may be perfectly related in a nonlinear way, and a straight line cannot see that.

## Some cautions (source, slide 22)

- You may have fitted the wrong model.
- Extrapolation: predicting values of $y$ outside the range of the fitted data.
- Causality: do not conclude that $x$ causes $y$. There may be an unknown variable at work.

The slide 22 picture, as I read the small figure, fits two straight lines to one hump-shaped pattern over different stretches of $x$ (points marked $a$ to $f$ on the axis). The lines have different slopes, so a line fitted on one stretch misleads you on another. That is the wrong-model and the extrapolation caution in one picture (added).

## Diagnostic tools (source, slides 23 to 26)

The same tools used in Chapter 11 check the normality assumption and the equal variance assumption:
1. A normal probability plot of the residuals.
2. A plot of residuals versus fit, or residuals versus variables.

Normal probability plot: if the normality assumption is valid, the plot should resemble a straight line sloping upward to the right. If not, you will often see the pattern fail in the tails of the graph.

Residuals versus fits: if the equal variance assumption is valid, the plot should appear as a random scatter around the zero centre line. If not, you will see a pattern in the residuals.

(added) Two common patterns: a funnel (spread growing or shrinking along the fits) means the variance is not constant, and a U or hump shape means a straight line is the wrong model.

> [!warning] Each plot checks a different assumption #struggle #common-mistake
> The normal probability plot checks normality only. Residuals versus fits is the equal-variance check, and it should look like a shapeless cloud around zero. A straight normal plot with a U-shaped residuals-versus-fits plot is not "everything is fine", and it is not "normality is violated". It means the residual pattern puts an assumption in doubt (equal variance, or the straight line itself) even though normality looks fine. A pattern in one plot says nothing about the other plot's assumption. To keep them apart, ask what each plot compares: the normal plot compares the residuals with a bell curve, while the fits plot asks whether the spread is the same everywhere along the line.

## Estimation and prediction at a chosen $x_0$ (source, slides 27 to 30)

Once the line is shown to be useful and the diagnostic plots show no violated assumption, the line can do two jobs for a given value $x = x_0$:
- estimate the average value of $y$ at $x_0$, which is a point on the line of means, or
- predict a particular value of $y$ at $x_0$, which is one new observation.

The best (unbiased) estimate of either is the same number:

$$\hat{y} = b_0 + b_1x_0$$

What $x_0$ means (explanation from session, added): a regression line has a different average $y$ at every $x$, so you must say where you are asking. $x_0$ is the $x$ value you choose, and it need not be one of your data points. Using the slide 3 example with $x$ as advertising spend and $x_0 = $ R50k, the confidence interval answers "what is the average monthly revenue across all months with R50k of advertising?" while the prediction interval answers "what will next month's revenue be if I spend R50k?".

Particular values of $y$ are harder to predict, requiring a wider range of values in the prediction interval (slide 29).

Confidence interval, for the average value of $y$:

$$\hat{y} \pm t_{\alpha/2,\,n-2}\,SE(\hat{y}) = \hat{y} \pm t_{\alpha/2,\,n-2}\sqrt{MSE\left(\frac{1}{n} + \frac{(x_0 - \bar{x})^2}{S_{xx}}\right)}$$

Prediction interval, for a particular value of $y$:

$$\hat{y} \pm t_{\alpha/2,\,n-2}\,SE(y - \hat{y}) = \hat{y} \pm t_{\alpha/2,\,n-2}\sqrt{MSE\left(1 + \frac{1}{n} + \frac{(x_0 - \bar{x})^2}{S_{xx}}\right)}$$

with $S_{xx} = \Sigma x_i^2 - (\Sigma x_i)^2/n$ as before.

> [!warning] The extra 1, and the centre #struggle #common-mistake
> The only difference between the two formulas is the extra 1 under the root. It makes the prediction interval always wider than the confidence interval at the same $x_0$. Both are centred on the same $\hat{y}$, so the midpoint of a confidence interval is $\hat{y}$ and the prediction interval at the same $x_0$ must have that same midpoint. Given a confidence interval $(10.2, 12.8)$, the midpoint is $11.5$ and the half-width is $1.3$. A valid prediction interval is centred on $11.5$ with a half-width above $1.3$, such as $(9.1, 13.9)$. $(10.9, 12.1)$ is too narrow, $(10.2, 12.8)$ is the same width, and $(9.1, 14.9)$ is wide enough but centred on $12.0$.

### Why the prediction interval is wider, and why both flare (added)

The prediction interval has two sources of error. One is not knowing exactly where the true line is, which is the $\frac{1}{n} + \frac{(x_0 - \bar{x})^2}{S_{xx}}$ part and which the confidence interval also has. The other is the natural scatter of a single $y$ around the line, which is the extra $1 \times MSE$. Slide 28 shows this as the true line of means, a bell curve of $y$ values standing on it at $x_0$, and one particular value off the line. Slide 29 shows the fitted line sitting slightly off the true line, so the estimation error and the scatter add.

The term $(x_0 - \bar{x})^2$ makes both intervals narrowest at $x_0 = \bar{x}$ and wider the further $x_0$ is from $\bar{x}$. The fitted line pivots around $(\bar{x}, \bar{y})$, so it is steadiest there and wobblier at the ends. That is also why extrapolation is risky.

(added) At $x_0 = \bar{x}$ the prediction interval is $\bar{y} \pm t\sqrt{MSE(1 + 1/n)}$. It has the same form as the one-sample prediction interval for a single future observation from a normal population, $\bar{x} \pm t\,s\sqrt{1 + 1/n}$, with $MSE$ in place of $s^2$ and $n - 2$ df in place of $n - 1$.

## Worked example, start to finish (composite) #worked-example

Data $(x, y)$: $(1, 2)$, $(2, 3)$, $(3, 5)$, $(4, 6)$, so $n = 4$. This is deliberately tiny so every number can be checked by hand. With $n = 4$ the tests and intervals are only for illustration.

Sums: $\Sigma x_i = 10$, $\Sigma y_i = 16$, $\Sigma x_i^2 = 30$, $\Sigma y_i^2 = 74$, $\Sigma x_iy_i = 47$, $\bar{x} = 2.5$, $\bar{y} = 4$.

$$S_{xx} = 30 - \frac{10^2}{4} = 5 \qquad S_{xy} = 47 - \frac{(10)(16)}{4} = 7 \qquad S_{yy} = 74 - \frac{16^2}{4} = 10$$

$$b_1 = \frac{7}{5} = 1.4 \qquad b_0 = 4 - 1.4(2.5) = 0.5 \qquad \hat{y} = 0.5 + 1.4x$$

Fits and residuals:

| $x_i$ | $y_i$ | fit $\hat{y}_i$ | residual $e_i$ |
|---|---|---|---|
| 1 | 2 | 1.9 | 0.1 |
| 2 | 3 | 3.3 | -0.3 |
| 3 | 5 | 4.7 | 0.3 |
| 4 | 6 | 6.1 | -0.1 |

The residuals add to 0 and the fits average to 4. $SSE = 0.01 + 0.09 + 0.09 + 0.01 = 0.2$.

Strength: $r^2 = \dfrac{7^2}{5 \times 10} = 0.98$ and $r = +0.99$ (positive because $b_1 > 0$). $SSR = r^2 \times \text{Total } SS = 9.8$. Check with the shortcut: $b_1S_{xy} = 1.4 \times 7 = 9.8$, and $SSR + SSE = 9.8 + 0.2 = 10 = \text{Total } SS$.

| Source | df | SS | MS | F |
|---|---|---|---|---|
| Regression | 1 | 9.8 | 9.8 | 98 |
| Error | 2 | 0.2 | 0.1 | |
| Total | 3 | 10 | | |

Test of $H_0$: slope $= 0$: $t = \dfrac{1.4}{\sqrt{0.1/5}} = 9.90$ on 2 df, and $t^2 = 98 = F$. The table values are $t_{.025,2} = 4.303$ and $F_{.05;1,2} = 18.51$, so at the 5% level both tests reject $H_0$.

Intervals at three values of $x_0$, each with $t_{.025,2} = 4.303$ and $MSE = 0.1$:

| $x_0$ | $\hat{y}$ | $(x_0 - \bar{x})^2/S_{xx}$ | 95% CI for average $y$ | 95% PI for one $y$ |
|---|---|---|---|---|
| 2.5 (the mean) | 4.0 | 0 | $4.0 \pm 0.68$ = (3.32, 4.68) | $4.0 \pm 1.52$ = (2.48, 5.52) |
| 3 | 4.7 | 0.05 | $4.7 \pm 0.75$ = (3.95, 5.45) | $4.7 \pm 1.55$ = (3.15, 6.25) |
| 6 (outside the data) | 8.9 | 2.45 | $8.9 \pm 2.24$ = (6.66, 11.14) | $8.9 \pm 2.62$ = (6.28, 11.52) |

Worked line for $x_0 = 3$: CI half-width $= 4.303\sqrt{0.1(0.25 + 0.05)} = 0.75$ and PI half-width $= 4.303\sqrt{0.1(1 + 0.25 + 0.05)} = 1.55$.

Reading the table: at every $x_0$ the prediction interval is wider than the confidence interval and shares its centre. Both are narrowest at $\bar{x}$, and by $x_0 = 6$ (extrapolation, since the data stop at 4) both have widened a lot.

> *The four residuals square and add to 0.2, which is the $SSE$ in the ANOVA table, so $SSE$ really is the sum of squared residuals. I like this example because every identity in the lecture shows up in numbers you can verify by hand: $SSR = b_1S_{xy}$, $t^2 = F$, and $r^2 = SSR/\text{Total } SS$ all land exactly.*

## Where the source is inconsistent

- Slide 17 leaves the formula for $SSE$ blank (see: Total variation and its two parts).
- Slide 19 writes the hypothesised slope as $\beta_0$, which clashes with $\beta_0$ as the intercept on slides 9 to 11 (see: The t test for the slope).
- Slide 20 states the null hypothesis as "model is useful" (see: The F test for the model).
- Slides 28 and 29 draw the line of means with intercept $\alpha$ and slope $\beta$, while the other slides use $\beta_0$ and $\beta_1$.
- Slide 14 uses $S_{yy}$ before slide 16 defines it.
- Chapter numbering mixes Chapters 10, 11 and 12, which also happened in the ANOVA lecture and looks like two textbook editions being blended.
- Examples 12.1, 12.2, 12.4 and 12.12 are named without data.

These are gaps in the source, not gaps in understanding. Slide 17 is being put to the lecturer.

## Carried from earlier sessions #struggle

> [!note] Paired data is a one-sample problem
> Same subjects measured twice (before and after, or one customer rating two products) means the two sets are not independent. Take each pair's difference and run a one-sample $t$ on the $n$ differences with $n - 1$ df. A pooled two-sample $t$, a single-factor ANOVA with $I = 2$, and $n$ rather than $n - 1$ df are all wrong. This has slipped in S7, S8 and S9 and was answered correctly at the end of S9, so it is closed for now but stays on the watch list. The test is whether the two sets share the same subjects, not how many columns the data has.

> [!note] A negative sum of squares is an alarm, not an answer
> Every sum of squares is a sum of squared terms and cannot go below 0. If $SSTr$, $SSE$, $S_{xx}$ or $S_{yy}$ comes out negative, a count has gone under the wrong total: the usual causes are dividing a term by too large a count, leaving a term undivided (such as $(\Sigma x_i)^2$ with no $/n$), or putting a mean where a total belongs. Go back and check which count sits under which total before guessing.

## Do not forget

- Model: $y = \beta_0 + \beta_1x + \varepsilon$, with $\varepsilon$ normal, mean 0, common variance $\sigma^2$. The line of means is $E(y) = \beta_0 + \beta_1x$.
- $b_1 = S_{xy}/S_{xx}$ first, then $b_0 = \bar{y} - b_1\bar{x}$. The line passes through $(\bar{x}, \bar{y})$.
- $S_{xx}$ and $S_{xy}$: a total squared (or two totals multiplied) over $n$. Never negative for $S_{xx}$ and $S_{yy}$.
- Total $SS = SSR + SSE$, with df $n - 1 = 1 + (n - 2)$. Regression df is the number of slopes.
- $r^2 = SSR/\text{Total } SS$. $r$ is its root with the sign of the slope.
- $t = b_1/\sqrt{MSE/S_{xx}}$ on $n - 2$ df. $F = MSR/MSE$ on 1 and $n - 2$ df. $t^2 = F$. The null is slope 0.
- Non-significant slope does not mean unrelated: it could be nonlinear, or a Type II error.
- Normal plot checks normality. Residuals versus fits checks equal variance, and should be a shapeless cloud.
- Confidence interval: average $y$ at $x_0$. Prediction interval: one new $y$ at $x_0$. Same centre $\hat{y}$, and the prediction interval is wider because of the extra 1.
- Both intervals are narrowest at $\bar{x}$ and flare outwards. Do not extrapolate, and do not conclude causation.
- Paired data is one sample of differences with $n - 1$ df.

## See also

These links go to whole files, by design, and because the headings inside those files could not be opened and checked in this session. The in-body references above are plain text for the same reason.

- [[STA01B1_Notes_S8_Single_Factor_ANOVA_and_Tukey_Procedure]] for the ANOVA partition $SST = SSTr + SSE$, the F test, and the totals-versus-means computing formulas that $S_{xx}$ mirrors.
- [[STA01B1_Notes_S7_Paired_Data_Proportions_and_Variances]] for paired data as a one-sample problem and for the F distribution.
- [[STA01B1_Notes_S6_Inferences_Based_on_Two_Samples]] for the two-sample procedures that paired data is not.
- [[STA01B1_Notes_S5_Hypothesis_Testing]] for the logic of rejection regions and Type I and II errors.
- [[STA01B1_Notes_S4_Intervals_Based_on_a_Normal_Population]] for the t interval and the prediction interval for a single future observation.
