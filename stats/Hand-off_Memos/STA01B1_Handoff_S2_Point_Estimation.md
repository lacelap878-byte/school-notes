# Handoff Memo: STA01B1 Point Estimation (Chapter 6)

## Core Objective of the Session
Generate structured study notes from the uploaded Point Estimation lecture PDF (Devore and Berk, Chapter 6) following the CDG protocol, then work through conceptual questions raised about the material, including a carried over thread on probability versus statistics and probability distribution versus sampling distribution.

## Notes Coverage Status
Full lecture notes are complete across two parts, covering the entire 22 slide deck.

**Part 1**
- Point estimate definition (page 248), point estimator notation using the hat symbol
- Examples 6.1, 6.2, 6.3 (proportion, several candidate estimators of mu, sample variance setup)
- General parameter notation theta
- Unbiased estimator definition (page 251), bias defined as E(theta hat) minus theta
- Proposition: p hat equals X over n is unbiased for p (page 252)
- Proposition: S squared with divisor n minus 1 is unbiased for sigma squared (page 253)
- Contrast: the divisor n version is a biased estimator of sigma squared
- Proposition: X bar is unbiased for mu, median and trimmed mean also unbiased under continuous symmetric distributions (page 254)

**Part 2**
- Minimum Variance Unbiased Estimation principle (page 256), relationship MSE equals variance plus bias squared
- MVU theorem: X bar is the MVUE for mu under a normal distribution
- Complications: best estimator depends on population shape, robust estimator concept (trimmed mean)
- Standard error definition (page 259) and estimated standard error
- Examples 6.9 (standard error of X bar, known versus estimated sigma) and 6.10 (standard error of p hat using pq over n, plus the upper bound 1 over 4n)

No sections remain uncovered from the source PDF.

## Conceptual Discussion Summary
- p hat identified as a special case of X bar, the sample mean of indicator (0 or 1) variables, unifying proportions and means under one concept
- theta clarified as the general placeholder symbol for an unknown parameter, theta hat as its estimator, not a function being evaluated
- Standard error notation sigma sub theta hat clarified as "the standard deviation of theta hat," not sigma treated as a function with theta as input
- Hat propagation rule established: a hat appears on a derived quantity specifically when an unknown parameter inside its formula has been replaced by an estimate
- Full derivation worked through for the bias of the divisor n variance estimator, using sigma hat squared equals (n minus 1 over n) times S squared and the known fact E(S squared) equals sigma squared, arriving at bias equals negative sigma squared over n
- Bias expression reading skill established: sign indicates direction of the systematic error (over or under estimate), and how the parameter n enters the expression indicates how the bias shrinks as sample size grows, all without needing to know the true parameter's numeric value
- Clarified that statistical bias is a mathematical gap between an estimator's average value and the true parameter, not a term about favoring particular groups
- Identified real contexts where biased estimators are still used, including maximum likelihood estimation, large sample settings where the bias becomes negligible, and some computational contexts
- Resolved the probability versus statistics distinction: probability reasons from a known model to outcomes, statistics reasons from observed outcomes back to an unknown model, and sampling distribution theory is a hybrid that temporarily uses probability tools (expectation, variance) to evaluate statistical tools (estimators)
- Established a mode switching rule: derivations and proofs are done in probability mode (parameter fixed but unknown, estimator treated as the random variable), while plugging in real data to compute a number is statistics mode (a single fixed reported value)
- Flagged and addressed two terminology traps: "accurate" conflates two separate technical properties, unbiasedness and precision or variance, into one casual word, and "prediction" wrongly implies a future event where point estimation instead concerns an already existing but unknown fixed parameter
- Worked through the full definitional chain: experiment, sample space, event, random variable, sample, probability distribution, and sampling distribution, clarifying that a probability distribution describes any single random variable while a sampling distribution describes a statistic built from a whole sample and remains a full distribution with its own mean and variance that narrows but does not collapse as n grows

## Last Position in Material
Lecture notes: complete (Part 1 and Part 2, full 22 slide deck covered).
Conceptual thread: probability versus statistics distinction and probability distribution versus sampling distribution distinction both addressed and considered resolved by the user. User intends to memorize the definitional chain and self test through repetition.

## Resume Instructions
To resume in a new chat, paste the following:

```
I'm resuming a CDG protocol session for STA01B1. Please read the CDG_STA.txt
protocol file (or I will re-upload it) and this handoff memo. My notes on
Point Estimation (Ch 6, Devore and Berk) are complete, full 22 slide deck.
I previously worked through the distinction between probability and statistics,
and between a probability distribution and a sampling distribution, and
considered this resolved. I want to self test on the definitional chain
(experiment, sample space, event, random variable, sample, probability
distribution, sampling distribution) and continue with the next topic in
the course.
```
