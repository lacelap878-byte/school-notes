---
module: CSC01B1
topic: Complexity Analysis
session: 11
tags: [definition, formula, worked-example, common-mistake, exam-flagged, struggle, added]
---

# CSC01B1 S11: Complexity Analysis

This note covers the 41 slide complexity analysis deck. The deck is not in a numbered lecture. The exam asks for it in Q3.5 (10 marks): count the steps in a short function and give the Big-O. Anything beyond the slides is marked (added). #exam-flagged

**Partial coverage, said plainly:** the counting method (slides 5 to 17) was taught and drilled. Sorting and searching (slides 22 to 41) were NOT taught; only their Big-O results are listed below. The Big-O definition formula slides (6 to 9) were not captured cleanly. Re-read them from the PDF.

## What it measures
Running time depends on the machine, so complexity analysis counts operations instead and ignores the machine (slide 5). #definition

## The three assumptions
Write these at the top of every Q3.5 answer. #exam-flagged
1. The operations counted are a fair measure of the time taken.
2. Each counted operation takes the same amount of time.
3. N is the size of the problem (name it: for example, `_end`, the number of elements).

The operations counted are things like `=`, `<`, `++`, `[]`, `==`, `return` and arithmetic and logical operators.

<span style="color:#e8590c">Open: the three assumptions are not memorised. In the session-end quiz the answer was a gut feeling. Also unsure why assumption 3 changes with the question: N is whatever the problem size is in THAT code.</span>

## The method (added)
T(N) = (operations outside the loop) + (passes) x (operations per pass).

- Nested loops multiply the pass counts.
- Sequential loops add.
- Drop constants and keep the highest power. The result is the Big-O.
- Count the WORST case.
- ⚠️ The outer loop's own overhead is ADDED once per outer pass, not multiplied by the inner loop.

<span style="color:#e8590c">Open: combining nested loops. In the drill a term was multiplied that should have been added.</span>

## Examples from the slides
- O(1): the time does not depend on N (slides 9 and 10).
- O(N): one loop over N (slides 11 and 12).
- O(N squared): nested loops, T(N) = N squared + N gives O(N squared). Highest power wins (slides 13 to 17). In the session the answer "n squared plus n, the big-o is n squared" was correct.
- Recursion is covered on slides 18 to 20 (not taught).

## Worked example (2025-C UJBuffer::search)
Operations: `=`, `<`, `++`, `[]`, `==`, `return`. N is `_end`.
- Outside the loop: 2.
- Per pass: 4.
- Worst case: N passes (the item is last or missing).
- T(N) = 4N + 2, so O(N).
Format for the exam: state the three assumptions, list the counted operations, show T(N), then give O(N). #worked-example

## Sorting and searching (slides 22 to 41), results only
```
algorithm        | worst case
-----------------|-----------
insertion sort   | O(n squared)
selection sort   | O(n squared)
bubble sort      | O(n squared)
merge sort       | O(n log n)
quick sort       | O(n log n)
linear search    | O(n)
binary search    | O(log n)
```
The papers 2021 to 2025 never name these in a question, so the table is low priority. Slide 24 is insertion sort (two nested loops), slide 28 derives selection sort at O(n squared), slide 33 merge sort at O(n log n), slide 41 binary search at O(log n).

## Lecture recap
- Count operations, not seconds.
- State the three assumptions.
- T(N) = outside + passes x per pass, worst case.
- Nested multiplies, sequential adds, keep the highest power.

## Do not forget
- ⚠️ Write the three assumptions every time.
- ⚠️ Name what N is.
- ⚠️ Worst case.
- Drop constants and lower terms last.
- Q3.5 is worth 10 marks. It is mostly counting.

## See also
- [[CSC01B1_Notes_S10_StacksAndQueues]]
- [[CSC01B1_Notes_S9_LinkedLists]]
