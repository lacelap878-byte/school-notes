---
module: MAT01A1
topic: Logic and Proof Techniques
session: S2
tags: [definition, theorem, worked-example, common-mistake, added]
---

# MAT01A1 Notes S2: Logic and Proof Techniques

Source: the PDF notes "Logic and proof techniques" (sections 1.1, 1.2, 2.1, 2.2) and their Moodle slides (Propositional logic Parts 1 and 2, Predicate logic, Methods of proof, Mathematical induction), weeks 3 to 5. The slides set examples without answers, so the proofs in the examples are mine. Short revision notes, not from a teaching session.

Scope: the whole module was examined in the final (12 June 2026).

Checked: the truth-table claims were checked by brute force in Python on 15 Nov 2026; the proofs were checked by hand.

## Propositions and connectives (source: section 1.1, Part 1 slides)

> **Definition:** A proposition is a sentence that is true or false but not both.

- "5 is less than 3" is a proposition (false). "x is even", "He is shy", questions and requests are not.

> **Definition:** Propositions which cannot be broken up into smaller parts, are called primitive, or atomic, propositions.
> **Definition:** Compound propositions are formed from primitive propositions using logical connectives.

| Connective | Symbol | True precisely when |
|---|---|---|
| not (negation) | $\neg p$ | $p$ is false |
| and (conjunction) | $p \land q$ | both are true |
| or (disjunction) | $p \lor q$ | at least one is true (inclusive or) |
| if then (implication) | $p \to q$ | $p$ is false or $q$ is true (or both) |
| if and only if (biconditional) | $p \leftrightarrow q$ | both have the same truth value |

- In $p \to q$, $p$ is the antecedent (hypothesis) and $q$ the consequent (conclusion). It is false only when $p$ is true and $q$ is false, so a false antecedent makes it true whatever $q$ is. A promise "if you pass, you get R1000" is only broken if you pass and get nothing.
- Ways to say $p \to q$: if $p$, then $q$; $p$ implies $q$; $p$ only if $q$; $q$ if $p$; $q$ whenever $p$.
- Priority order: $\neg$, then $\land$ and $\lor$, then $\to$, then $\leftrightarrow$. Connectives of equal priority get brackets from left to right.

Example (source, Part 1 slides): find the truth value of "2 plus 2 equals 5 if, and only if, 3 is less than 5 whenever 2 is not less than 3".
   $p$ = 2 plus 2 equals 5, $q$ = 3 is less than 5, $r$ = 2 is less than 3. $(p \leftrightarrow ((\neg r) \to q)) = (F \leftrightarrow (F \to T)) = (F \leftrightarrow T) = F$.

## Truth tables, tautologies and contradictions (source: section 1.1, Part 2 slides)

- $n$ variables give $2^n$ rows. The rightmost variable alternates T, F; each variable further left doubles the block length; the leftmost is $2^{n-1}$ T's then $2^{n-1}$ F's.

> **Definition:** A tautology is a formula that obtains a truth value true for any assignment of truth values to the variables, i.e. it is a formula that is always true. Tautologies are also called logically valid formulas.
> **Definition:** A contradiction is a formula that obtains a truth value false for any assignment of truth values, i.e. it is a formula that is always false.

> **Definition:** Propositional formulas $A$ and $B$ are logically equivalent if for every assignment of truth values to the variables in them they obtain identical truth values, i.e., they have 'the same truth table'.

- We write $A \equiv B$. $A \equiv B$ if, and only if, $A \leftrightarrow B$ is a tautology.
- Example: $p \to (q \to p)$ is a tautology; $p \to (q \to r) \equiv (p \land q) \to r$; but $(p \lor q) \land r \not\equiv p \lor (q \land r)$ (they differ when $p = T$, $r = F$).

## Known equivalences (source: section 1.1, Part 2 slides)

$t$ is a tautology and $f$ a contradiction.

| Law | Equivalences |
|---|---|
| Commutative | $A \land B \equiv B \land A$, $\ A \lor B \equiv B \lor A$ |
| Associative | $(A \land B) \land C \equiv A \land (B \land C)$, $\ (A \lor B) \lor C \equiv A \lor (B \lor C)$ |
| Distributive | $A \land (B \lor C) \equiv (A \land B) \lor (A \land C)$, $\ A \lor (B \land C) \equiv (A \lor B) \land (A \lor C)$ |
| Identity | $A \land t \equiv A$, $\ A \lor f \equiv A$ |
| Negation | $A \lor \neg A \equiv t$, $\ A \land \neg A \equiv f$ |
| Double negative | $\neg(\neg A) \equiv A$ |
| Idempotent | $A \land A \equiv A$, $\ A \lor A \equiv A$ |
| Universal bound | $A \lor t \equiv t$, $\ A \land f \equiv f$ |
| De Morgan | $\neg(A \land B) \equiv \neg A \lor \neg B$, $\ \neg(A \lor B) \equiv \neg A \land \neg B$ |
| Absorption | $A \lor (A \land B) \equiv A$, $\ A \land (A \lor B) \equiv A$ |

$$A \leftrightarrow B \equiv (A \to B) \land (B \to A) \qquad A \to B \equiv \neg A \lor B$$

$$\neg(A \to B) \equiv A \land \neg B \qquad \neg(A \leftrightarrow B) \equiv (A \land \neg B) \lor (B \land \neg A)$$

## Contrapositive, converse and inverse (source: section 1.1, Part 2 slides)

For the implication $A \to B$:
- contrapositive $\neg B \to \neg A$, and $A \to B \equiv \neg B \to \neg A$
- converse $B \to A$, not equivalent to $A \to B$
- inverse $\neg A \to \neg B$, not equivalent to $A \to B$, but equivalent to the converse

(added) One slide writes the inverse as $\neg A \to \neg A$; it should be $\neg A \to \neg B$.

Example (source, Part 2 slides): "If $\pi$ is a real number, then $\pi$ is an integer" is false, but its converse "If $\pi$ is an integer, then $\pi$ is a real number" is true (false antecedent).

## Necessary and sufficient conditions (source: section 1.1, Part 2 slides)

> If $A$ and $B$ are propositional formulas, then
> - "$A$ is a sufficient condition for $B$" means $A \to B$,
> - "$A$ is a necessary condition for $B$" means $B \to A$, or, equivalently, $\neg A \to \neg B$.

- Sufficient: $A$ alone guarantees $B$. Necessary: $B$ only if $A$.
- "Divisible by 3 is necessary for divisible by 9" means: if a number is divisible by 9, then it is divisible by 3.

## Basic number theory (source: section 1.2, Predicate logic slides)

- $\mathbb{Z}^+ = \{1, 2, 3, \ldots\}$, $\mathbb{Z}^- = \{\ldots, -2, -1\}$, $\mathbb{N} = \{0, 1, 2, \ldots\}$, $\mathbb{Q} = \{q \mid q = \frac{a}{b}$ where $a, b \in \mathbb{Z}$ and $b \ne 0\}$, and $\mathbb{N} \subset \mathbb{Z} \subset \mathbb{Q} \subset \mathbb{R}$, all strict. $C \subset D$ (proper subset) means $C \subseteq D$ but $D \not\subseteq C$.

> Let $m$ and $n$ be integers with $m \ne 0$. We say $m$ divides $n$ or $m$ is a divisor of $n$ and write $m \mid n$ if there exists an integer $k$ such that $n = m \cdot k$.

> Let $p > 1$ be an integer. If the only positive divisors of $p$ are 1 and $p$, then we call $p$ a prime number.

- An integer $m$ is even if and only if $m = 2k$ for some $k \in \mathbb{Z}$; odd if and only if $m = 2k + 1$ for some $k \in \mathbb{Z}$.
- $1 \mid n$ and $n \mid n$ for every integer $n$; $m \mid 0$ for every $m \ne 0$; 1 is not prime.

## Predicates and quantifiers (source: section 1.2, Predicate logic slides)

> Given a domain, a predicate is a property that objects from the domain can have, or a relationship between objects from the domain.

- The domain (of discourse) is the set of values a variable can take. $Q(x)$ is "x is even"; $R(x, y)$ is "x is a divisor of y".
- $\forall$ (for all) is the universal quantifier; $\exists$ (there exists at least one) is the existential quantifier.
- $(\forall x \in D)(Q(x))$ is true if $Q(x)$ is true for every $x$ in $D$, and false if one counterexample exists.
- $(\exists x \in D)(Q(x))$ is true if at least one $x$ in $D$ makes $Q(x)$ true, and false if $Q(x)$ is false for every $x$ in $D$.
- Narrowing the domain: $(\forall x \in U)(P(x) \to Q(x))$ is the same as $(\forall x \in D)(Q(x))$, and $(\exists x \in U)(P(x) \land Q(x))$ is the same as $(\exists x \in D)(Q(x))$, where $D$ is the set of $x$ that make $P(x)$ true. "For all" pairs with $\to$; "there exists" pairs with $\land$.

Negations:

$$\neg(\forall x \in D)(Q(x)) \equiv (\exists x \in D)(\neg Q(x)) \qquad \neg(\exists x \in D)(Q(x)) \equiv (\forall x \in D)(\neg Q(x))$$

$$\neg(\forall x \in D)(P(x) \to Q(x)) \equiv (\exists x \in D)(P(x) \land \neg Q(x))$$

Example (source, Predicate logic slides): is $(\forall x \in \mathbb{Z})(|x| = 5 \to |x + 1| = 6)$ true?
   False: $x = -5$ gives $|-5| = 5$ but $|-4| = 4$.

## Methods of proof (source: section 2.1, Methods of proof slides)

- Direct proof: assume the hypothesis $A$ is true and show the conclusion $B$ is true.
- Proof by cases: assume the hypothesis, split into cases that exhaust all possibilities, and show each case gives the conclusion.
- Proof by contradiction: assume $\neg B$, derive something clearly false, so $\neg B$ is false and $B$ is true.
- Proof by contraposition: prove $\neg B \to \neg A$ instead, since $A \to B \equiv \neg B \to \neg A$.
- Disproof by counterexample: one actual value (not variables) that makes a "for all" claim false. You can disprove by example, but you cannot prove by example.

Example (direct, source: slides): if $a \mid b$ and $b \mid c$ for $a, b, c \in \mathbb{Z}$, then $a \mid c$.
   $b = ak$ and $c = bl$ for integers $k, l$. So $c = a(kl)$ with $kl \in \mathbb{Z}$, hence $a \mid c$.

Example (cases, source: slides): if $3 \nmid n$, then $n^2 = 3k + 1$ for some $k \in \mathbb{Z}$.
   Case $n = 3m + 1$: $n^2 = 3(3m^2 + 2m) + 1$. Case $n = 3m + 2$: $n^2 = 3(3m^2 + 4m + 1) + 1$. Both have the form $3k + 1$.

Example (contradiction, source: slides): prove $\sqrt{2} + \sqrt{6} < \sqrt{15}$.
   Suppose $\sqrt{2} + \sqrt{6} \ge \sqrt{15}$. Squaring (both sides positive): $8 + 2\sqrt{12} \ge 15$, so $2\sqrt{12} \ge 7$ and $48 \ge 49$, which is false.

Example (contraposition, source: slides): if $7x + 9$ is even, then $x$ is odd.
   Contrapositive: if $x$ is even, then $7x + 9$ is odd. $x = 2k$ gives $7x + 9 = 14k + 8 + 1 = 2(7k + 4) + 1$, which is odd.

Example (counterexample, source: slides): show $\tan^2\theta - 1 = \sec^2\theta$ is not an identity.
   $\theta = 0$: left side $0 - 1 = -1$, right side $1$.

## Mathematical induction (source: section 2.2, Induction slides)

> **Mathematical Induction:** Let $S$ be a set of natural numbers and let $a$ be a natural number. If the following are true
> 1. $a \in S$
> 2. $k \in S \Rightarrow k + 1 \in S$
>
> then $S$ contains every natural number greater than or equal to $a$.

- Steps: base case ($a$), then assume the statement for $k$ (the induction hypothesis) and prove it for $k + 1$. If the induction hypothesis was not used, the proof is wrong.

Example (source: slides): show $4^n - 1$ is divisible by 3 for every natural number $n \ge 0$.
   Base: $4^0 - 1 = 0 = 3 \cdot 0$. Hypothesis: $4^k - 1 = 3m$. Then $4^{k+1} - 1 = 4 \cdot 4^k - 1 = 4(3m + 1) - 1 = 3(4m + 1)$.

## Do not forget

- $p \to q$ is false only for T then F; a false antecedent makes it true.
- Negating: swap $\forall$ and $\exists$ and negate inside; $\neg(A \to B) \equiv A \land \neg B$.
- "A is necessary for B" means $B \to A$, not $A \to B$.
- Induction must use the induction hypothesis.

## See also

- [[MAT01A1_Notes_S1_Sigma_Inequalities_Trig_and_Complex_Numbers]]

---
*CDG v13 | written S2 | 2026-11-15*
