---
module: STA01A1
topic: Probability
session: S2
tags: [definition, formula, theorem, worked-example, common-mistake, added]
---

# STA01A1 Notes S2: Probability

Source: Lecture 3 (26 slides), Lecture 4 (11 slides) and Lecture 5 (23 slides), slide numbers as printed; the Counting rules sheet in the Lectures folder (3 pages, cited by page); textbook Chapter 2. Short revision notes written from the slides, not from a teaching session.

Scope: SA1 (23 March 2026) covered all of this. The final (13 June 2026) listed sample spaces and Venn diagrams, the three axioms, all proofs, the addition, multiplication, conditional, total probability and Bayes rules with tree diagrams, mutual exclusiveness and independence, and the product, permutation and combination rules.

Checked: every number below was recomputed in Python on 15 Nov 2026.

## Sample spaces and events (source, Lecture 3 slides 9 to 11)

An experiment is any action or process whose outcome is subject to uncertainty (toss a die, test a fuse).

> **Definition:** The sample space of an experiment, denoted by $S$, is the set of all possible outcomes of that experiment

> **Definition:** An event is any collection (subset) of outcomes contained in the sample space $S$. An event is said to be simple if it consists of exactly one outcome and compound if it consists of more than one outcome.

Example: list the sample space for tossing a coin twice, and for rolling two dice.
   $S = \{HH, HT, TH, TT\}$. Two dice: the 36 ordered pairs $(1,1), (1,2), \dots, (6,6)$.

## Set relations (source, Lecture 3 slides 12 to 15)

> **Definition:**
> 1. The union of two events $A$ and $B$, denoted by $A \cup B$ and read "$A$ or $B$," is the event consisting of all outcomes that are either in $A$ or in $B$ or in both events, that is, all outcomes in at least one of the events.
> 2. The intersection of two events $A$ and $B$, denoted by $A \cap B$ and read "$A$ and $B$," is the event consisting of all outcomes that are in both $A$ and $B$
> 3. The complement of an event $A$, denoted by $A'$ is the set of all outcomes in $S$ that are NOT contained in $A$.

> **Definition:** When $A$ and $B$ have no outcomes in common, they are said to be disjoint or mutually exclusive events. It is written as $A \cap B = \emptyset$

- On a Venn diagram, $S$ is the box and events are circles: $A \cap B$ is the overlap, $A'$ is everything in the box outside $A$, and disjoint events are circles that do not touch.

## Axioms of probability (source, Lecture 3 slides 16 to 17)

> Let $S$ denote the sample space of an experiment. The probability of an event $A$ in $S$, denoted by $P(A)$, is a number for which the following conditions hold:
> 1. $P(A) \ge 0$
> 2. $P(S) = 1$
> 3. For an infinite collection of mutually exclusive events $A_1, A_2, \ldots \subset S$ it follows that

$$P(A_1 \cup A_2 \cup \ldots) = \sum_{i=1}^{\infty} P(A_i)$$

## Propositions from the axioms (source, Lecture 3 slide 18)

> 1. $P(\emptyset) = 0$
> 2. For any event $A$, $P(A) = 1 - P(A')$
> 3. For any events $A$ and $B$,

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

Proofs (added; the slide marks 2 and 3 Prove!):
1. Take $A_1 = A_2 = \ldots = \emptyset$. They are mutually exclusive, so axiom 3 gives $P(\emptyset) = \sum P(\emptyset)$, which only holds if $P(\emptyset) = 0$.
2. $A$ and $A'$ are disjoint and $A \cup A' = S$. Axiom 3 (with the rest of the collection empty) and axiom 2 give $1 = P(S) = P(A) + P(A')$.
3. Split into disjoint pieces: $A \cup B = A \cup (B \cap A')$ and $B = (A \cap B) \cup (B \cap A')$. So $P(A \cup B) = P(A) + P(B \cap A')$ and $P(B \cap A') = P(B) - P(A \cap B)$. Substitute.

## Equally likely outcomes (source, Lecture 3 slides 19 to 23, Lecture 4 slide 2)

If the simple events of an experiment are equally likely:

$$P(A) = \frac{N(A)}{N} = \frac{\text{number of simple events in } A}{\text{total number of simple events}}$$

Example (source, Lecture 3 slide 23): a bowl holds one red, one blue and one green sweet; a child takes two. Find P(at least one red).
   Ordered outcomes RB, RG, BR, BG, GB, GR, each $1/6$. At least one red: RB, RG, BR, GR, so $4/6 = 2/3$.

## Counting rules (source, Lecture 4 slides 3 to 8)

> **Proposition (product rule):** If the first element or object of an ordered pair can be selected in $n_1$ ways, and for each of these $n_1$ ways the second element of the pair can be selected in $n_2$ ways, then the number of pairs is $n_1 n_2$.

- General product rule: $k$ choices made in turn, with $n_1, n_2, \dots, n_k$ options, give $n_1 n_2 \cdots n_k$ ordered collections. Two dice: $6 \times 6 = 36$.

> **Definition:** The number of ordered sequences of $k$ objects taken from a set of $n$ distinct objects is given by

$$P_{k,n} = \frac{n!}{(n-k)!} \quad \text{where } n! = n(n-1)(n-2)\cdots(2)(1) \text{ and } 0! = 1.$$

> **Definition:** The number of unordered combinations of size $k$ that can be formed from $n$ distinct objects is given by

$$\binom{n}{k} = \frac{n!}{k!\,(n-k)!}$$

- Order matters: permutation. Order does not matter: combination. A 3-digit lock code from 1, 2, 3, 4: $P_{3,4} = 24$. A 3-person subcommittee from 5: $\binom{5}{3} = 10$.

Example (source, Lecture 4 slides 9 to 10)
A box holds 4 red and 2 green sweets. A child takes 2 at random. Find P(exactly one red).

WORKING
Counting: $\binom{4}{1}\binom{2}{1} / \binom{6}{2} = (4 \times 2)/15 = 8/15$.
Tree: $(4/6)(2/5) + (2/6)(4/5) = 16/30 = 8/15$.

## More counting patterns (source, Counting rules sheet pages 1 to 3)

- Circular arrangements of $n$ objects: $(n-1)!$, since rotating the circle gives no new arrangement. 10 people at a round table: $9! = 362\,880$.
- Arranging $n$ items where some are identical: $\dfrac{n!}{n_1!\, n_2! \cdots}$. BANANA: $\dfrac{6!}{3!\,2!\,1!} = 60$.
- Items that must stay together: treat them as one block, then multiply by the arrangements inside the block. COMPUTER with O, U, E together: 6 units, so $6! \times 3! = 4320$.
- "At least" questions: add the separate cases. A 5-person committee from 6 men and 8 women with at least 3 women: $\binom{8}{3}\binom{6}{2} + \binom{8}{4}\binom{6}{1} + \binom{8}{5}\binom{6}{0} = 840 + 420 + 56 = 1316$ (the total is added; the sheet stops at the sum).
- (added) The sheet's committee example with Arjun always included gives $5 \times P(9,4) = 15\,120$, which treats the 5 seats as ordered. For an ordinary committee, where order does not matter, the count is $\binom{9}{4} = 126$.

## Conditional probability and the multiplication rule (source, Lecture 5 slides 2 to 3)

> **Definition:** The probability that $A$ occurs, given that event $B$ has occurred is called the conditional probability of $A$ given $B$ and is defined as

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)} \quad \text{if } P(B) \ne 0$$

> For any two events, $A$ and $B$, the probability that both $A$ and $B$ occur is

$$P(A \cap B) = P(A \mid B)\,P(B)$$

## Law of total probability (source, Lecture 5 slides 5 to 8)

> Let $S$ be a sample space and $A_1, A_2, \ldots, A_k$ events in $S$.
> - The events are said to be mutually exclusive if $A_i \cap A_j = \emptyset$ for all $i \ne j$
> - The events are said to be exhaustive if $A_1 \cup A_2 \cup \ldots \cup A_k = S$
> - If the events are mutually exclusive and exhaustive, they are said to form a partition of the sample space.

Let $A_1, \ldots, A_k$ be a partition of $S$. Then for any event $B$ in $S$:

$$P(B) = \sum_{i=1}^{k} P(A_i)\,P(B \mid A_i)$$

Proof (source, slide 8): $B = (B \cap A_1) \cup \ldots \cup (B \cap A_k)$, and these pieces are disjoint. Axiom 3 gives $P(B) = \sum P(B \cap A_i)$, and the multiplication rule turns each term into $P(A_i)\,P(B \mid A_i)$.

## Bayes' rule (source, Lecture 5 slides 9 to 11)

> Let $A_1, A_2, A_3, \ldots, A_k$ be mutually exclusive and exhaustive events with prior probabilities $P(A_1), P(A_2), \ldots, P(A_k)$. If an event $B$ occurs, the posterior probability of $A_j$, given that $B$ occurred is

$$P(A_j \mid B) = \frac{P(A_j \cap B)}{P(B)} = \frac{P(B \mid A_j)\,P(A_j)}{\sum_{i=1}^{k} P(B \mid A_i)\,P(A_i)} \quad \text{for } j = 1, 2, \ldots, k$$

The prior is the chance before $B$ is seen; the posterior is the updated chance after.

Example (source, Lecture 5 slides 19 to 20)
49% of a population are female. 8% of females and 12% of males are at high risk of a heart attack. One person is picked at random. Find P(high risk female), P(high risk), and P(male given high risk).

WORKING
$P(H \cap F) = P(F)\,P(H \mid F) = 0.49(0.08) = 0.0392$.
$P(H) = 0.51(0.12) + 0.49(0.08) = 0.0612 + 0.0392 = 0.1004$ (total probability).
$P(M \mid H) = 0.0612 / 0.1004 = 0.61$.

## Independence (source, Lecture 5 slides 13 to 21)

> Two events $A$ and $B$ are independent if and only if $P(A \mid B) = P(A)$ or $P(B \mid A) = P(B)$. Otherwise, they are dependent.

> The events $A$ and $B$ are independent if and only if (iff)

$$P(A \cap B) = P(A)\,P(B)$$

> Events $A_1 \ldots A_n$ are mutually independent if for every $k$ ($k = 2, 3, \ldots, n$) and every subset of indices $i_1 \ldots i_k$,

$$P(A_1 \cap A_2 \cap \ldots \cap A_k) = P(A_{i_1})\,P(A_{i_2}) \cdots P(A_{i_k})$$

(added) The left side on the slide should read $P(A_{i_1} \cap A_{i_2} \cap \ldots \cap A_{i_k})$, the same subset as the right side.

Example (source, Lecture 5 slide 18): 10% of people are high risk; 3 are picked independently. Find P(exactly one high risk).
   $P(HNN) + P(NHN) + P(NNH) = 3(0.1)(0.9)^2 = 0.243$.

> [!warning] Mutually exclusive is not independent (added)
> If $A$ and $B$ are disjoint with $P(A) > 0$ and $P(B) > 0$, then $P(A \cap B) = 0$ but $P(A)\,P(B) > 0$, so they are dependent. Disjoint means one rules the other out, which is the opposite of "no influence".

## Do not forget

- $P(A \mid B)$ needs $P(B) \ne 0$; the given event goes in the denominator.
- Bayes: the numerator is one branch of the tree; the denominator is the law of total probability.
- Disjoint events with positive probabilities are never independent.
- Order matters: permutation. Order does not matter: combination.

## See also

- [[STA01A1_Notes_S1_Describing_Data]]

---
*CDG v13 | written S2 | 2026-11-15*
