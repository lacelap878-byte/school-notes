---
module: CSC01B1
topic: Complexity Analysis
session: 11
tags: [definition, formula, worked-example, common-mistake, exam-flagged, struggle, added]
---

# CSC01B1 S11: Complexity Analysis

This note covers the 41 slide complexity analysis deck. The deck is not in a numbered lecture. The exam asks for it in Q3.5 (10 marks): count the steps in a short function and give the Big-O. Anything beyond the slides is marked (added). #exam-flagged

**Coverage, said plainly (Amended S11, 28 Oct):** the counting method (slides 5 to 17) was taught and drilled. Every other slide (6 to 9, 18 to 20 and 22 to 41) has now been read as an image and is written below as presented. Those sections were NOT taught in a session.

> N.B. The counting method (Q3.5) is the part that is examined. The Big-O definition, recursion and the sorting and searching slides are low frequency: sorts and searches are never named in the 2021 to 2025 question text, and the Q3.5 papers checked (2023-A, 2025-C) give a short piece of code to count. Do not spend much study time on those sections. Read them once.

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
- Recursion is covered on slides 18 to 20 (see "Recursion (slides 18 to 20)" below).

### Slide figures, as written (Amended S11)
- Example 1 (slide 10): T(N) = 1 + 1 + 1 + 1 + 1 + 3 + 4 = 12, so O(1). There is no iteration or recursion, so T(N) is the sum of the operations along the longest execution path.
- Example 2 (slides 11 and 12): operations counted are `= < && ! [] == ++`. Outside the loop: 2. Inside: guard (3) plus loop body (4), times the maximum number of loops (n). T(N) = 7N + 2, so O(N).
- Example 3 (slides 13 and 14): outside 3; innermost (header 3 plus body 1) times N; outer loop is the inner loop times N. The slide writes T(N) = 3 + N x (3N) = 3N squared + 3, so O(N squared).
- Example 3b (slides 15 to 17): the inner loop runs up to k, and k is at most N. Outside: 1 + 1 + 1 + 1 = 4. Innermost: (header 3 plus body 2) times k. The slide writes T(N) = 4 + 3N x (5N) = 25N squared + 4, so O(N squared).
- (added) Two slide arithmetic slips, harmless for the Big-O: in Example 3 a header of 3 plus a body of 1 is 4 per pass (the slide writes 3N), and in Example 3b 3N x 5N is 15N squared (the slide writes 25N squared). Use the method, not the slide's exact figures. The Example 3b code on slide 15 also has typos (`int k` declared twice, `j` never declared).

## Worked example (2025-C UJBuffer::search)
Operations: `=`, `<`, `++`, `[]`, `==`, `return`. N is `_end`.
- Outside the loop: 2.
- Per pass: 4.
- Worst case: N passes (the item is last or missing).
- T(N) = 4N + 2, so O(N).
Format for the exam: state the three assumptions, list the counted operations, show T(N), then give O(N). #worked-example

## Comparing algorithms and the Big-O definition (slides 6 to 8, Amended S11)

> N.B. Low frequency in past papers. Do not focus on this section.

- Benchmarking means running the algorithms and comparing their performance on a given problem (slide 6).
- Benchmarking misleads. Computer A sorts in 10s and computer B in 5s, but B is not necessarily the better algorithm: the computers may have different hardware, and some algorithms perform progressively worse as the problem size increases (slide 6).
- So compare the algorithms from first principles (slide 6).
- The execution time is normally governed by the input size N. It is written as a function T(N) (slide 7).
- The same N can perform better or worse on different inputs (an item near the start of a list versus one at the end). Programmers are pragmatic and look at the worst case, written O(f(x)) (slide 7).
- Look only at the term with the highest exponent (slide 7): O(1000 N^3 + 50000000 N^2 + 10 N + 5) gives O(N^3).
- Slide 8 shows the bound, assuming n > 0 (problem size is a positive integer):
  - |5n^4 + 2n^2 - 2n + 1| <= 5n^4 + 2n^2 - 2n + 1
  - |5n^4 + 2n^2 - 2n + 1| <= 5n^4 + 2n^4 - 2n^4 + n^4
  - |5n^4 + 2n^2 - 2n + 1| <= 6n^4
  - |5n^4 + 2n^2 - 2n + 1| <= 6|n^4|, so O(n^4).
- (added) Why it works: for n > 0 every lower power is at most n^4, so the whole expression is at most a constant (6) times n^4. That constant is why constants are dropped.

## Recursion (slides 18 to 20, Amended S11)

> N.B. Low frequency in past papers. The Q3.5 papers checked give iterative code. Do not focus on this section.

Slide 18 code:
```cpp
int power(int x, int n)
{
       if(n > 0)
               return (power(x, n - 1) * x);
       else
               return 1;
}
```
- Assume (slide 19): calling the recursive function is a fair measure of complexity, each operation takes the same time, N is the parameter n, and n >= 0 (valid for positive integers only).
- T(N) is a recursive function: T(N) = operations in the base case + operations in the recursive case (slide 19).
- Base case: 0, because no function calls are made (slide 20).
- Recursive case: T(1) = 1, T(2) = 1 + 1 = 2, T(3) = 1 + 1 + 1 = 3, so T(N) = N (slide 20).
- The algorithm is O(N) (slide 20).

## Sorting and searching (slides 22 to 41), results only

> N.B. Low frequency in past papers: sorts and searches are never named in the 2021 to 2025 question text. The table below is the part worth knowing. The slide detail after it is for reading once, not for drilling. (The heading says "results only"; it is kept unchanged because the Final summary links to it. The slide detail was added in Amend S11.)

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
The papers 2021 to 2025 never name these in a question, so the table is low priority.

### Sorting, slide 22
Sorting is arranging an array's elements in ascending or descending order. Sorting algorithms are classified by: 1. computational complexity (comparisons, swaps, overall); 2. memory usage (in place or not); 3. recursive versus iterative; 4. stability (is the order of equal entries before the sort preserved); 5. comparison criteria; 6. method employed (insertion, selection, exchange, merger).

### Insertion sort (slides 23 and 24)
- The array is divided into two parts: sorted (left) and unsorted (right). At the start only the sorted part is populated, with entry 0. Each entry met in the unsorted part is inserted into its correct place in the sorted part.
- Slide pseudocode: for k from 1 to N-1; x is arr[k]; for i from (k - 1) while the preceding elements are greater than x, shift arr[i] one position right; insert x at the correct location.
- Complexity: worst case O(n squared), best case (sorted) O(n), largely sorted O(n + d) where d is the number of inversions. It is an in-place, iterative, stable sort.
- Slide 24 code:
```cpp
void sort(int* arr, int arr_length)
{
  int temp;
  for(int k = 1; k < arr_length; k++)
  {
    temp = arr[k];
    int i;
    for(i = k - 1; (i >=0) && (arr[i] > temp); i--)
      arr[i + 1] = arr[i];
    arr[i + 1] = temp;
  }
}
```

### Selection sort (slides 25 to 28)
- Select the smallest entry and place it first, select the second smallest from the rest and place it second, and repeat for the remainder of the list. Performance is O(n squared) in all cases.
- Slide 25 pseudocode: for i from 0 to n-2: min is i; for j from i+1 to n-1: if A[j] < A[min] then min is j; swap A[i] and A[min]. The swap is temp = arr[j]; arr[j] = arr[k]; arr[k] = temp.
- Slide 26 code:
```cpp
int min_position(vector<int>& a, int from, int to)
/* PURPOSE: get the position of the smallest element in a vector range
RECEIVES: a - a vector
from, to - a range
RETURNS: the position of the smallest element in a[from]...a[to] */
{
        int min_pos = from;
        int i;
        for (i = from + 1; i <= to; i++)
           if (a[i] < a[min_pos])
              min_pos = i;
        return min_pos;
}
```
- Slide 27 code (the slide shows a round bracket instead of the opening brace, a typo):
```cpp
void swap(int& x, int& y)
/* PURPOSE: swap two integers
   RECEIVES: x, y - the integers to swap */
{  int temp = x;
   x = y;
   y = temp;
}
```
- Slide 28 analysis: assume the time is proportional to the number of accesses made to the array, and let l(n) be the number of accesses for size n.
  - l(n) = n+2+l(n-1)
  - l(n) = n+2+n-1+2+l(n-2)
  - l(n) = n+(n-1)+4+l(n-2)
  - l(n) = (the sum of i for i = 2 to n) + 2(n-1) + l(n-n+1)
  - l(n) = n(n+1)/2 - 1 + 2(n-1) + l(1)
  - l(n) = n(n+1)/2 - 1 + 2(n-1) + 0
  - l(n) = (1/2)n^2 + (1/2)n - 1 + 2n - 2
  - l(n) = (1/2)n^2 + (5/2)n - 3, so O(n^2).

### Merge sort (slides 29 to 33)
- Sorting one or two items is trivial. Split the array (vector) in two, sort each half with the same algorithm, merge the two sorted halves.
- Slides 29 to 31 code, `merge` (the three slides are one function):
```cpp
void merge(vector<int>& a, int from, int mid, int to)
/* PURPOSE: merge two adjacent ranges in a vector
 RECEIVES: a - the vector with the elements to merge
 from, mid - start and end of the first range
 to - end of the second range*/
{ int n = to - from + 1; /* size of the range to be merged */
/* merge both halves into a temporary vector b */
vector<int> b(n);
int i1 = from;
/* next element to consider in the first half */
int i2 = mid + 1;
 /* next element to consider in the second half */
int j = 0; /* next open position in b */
 /* as long as neither i1 nor i2 past the end, move the
   smaller element into b */
 while (i1 <= mid && i2 <= to) {
   if (a[i1] < a[i2]) {
         b[j] = a[i1];
         i1++;
       } else {
         b[j] = a[i2];
         i2++;
   }
    j++;
}
 /* note that only one of the two while loops below is executed  */
 /* copy any remaining entries of the first half */
 while (i1 <= mid)  {
        b[j] = a[i1];
        i1++;
        j++;
}
 /* copy any remaining entries of the second half */
 while (i2 <= to) {
       b[j] = a[i2];
       i2++;
       j++;
}
 /* copy back from the temporary vector */
 for (j = 0; j < n; j++)
     a[from + j] = b[j];
}
```
- Slide 32 code:
```cpp
void merge_sort(vector<int>& a, int from, int to)
/* PURPOSE: sort the elements in a range of a vector
RECEIVES: a - the vector with the elements to sort
from, to - start and end of the range */
{ if (from == to) return;
        int mid = (from + to) / 2;
        /* sort the first and the second half */
        merge_sort(a, from, mid);
        merge_sort(a, mid + 1, to);
        merge(a, from, mid, to);
}
```
- Slide 33 analysis: assume the time is proportional to the number of accesses, M(n) is the number of accesses for size n, and n = 2^m.
  - M(n) = M(n/2)+M(n/2)+3n+2n, which the slide simplifies to M(n) = 2M(n/2)+5n.
  - Repeated expansion: M(n) = 4M(n/4)+10n, then M(n) = 8M(n/8)+15n.
  - In general M(n) = 2^k M(n/2^k)+5nk. At k = m: M(n) = 2^m M(n/2^m)+5nm = nM(1)+5nm.
  - M(n) = n+5n log2 n, so O(n log n).

### Bubble sort (slide 34)
Adjacent entries are compared and swapped if necessary. This repeats until no more swaps can be made. Performance is O(n squared). Slide pseudocode:
```
procedure bubbleSort(A)
  do
    swapped <- false
    for each i in 0 to length(A) - 1 do
      if A[i] > A[i + 1] then
        swap(A[i], A[i + 1])
        swapped <- true
      end if
    end for
  while swapped
end procedure
```

### Quick sort (slide 35)
A recursive divide and conquer strategy. An arbitrary pivot value is selected. The list is reordered so that values greater than the pivot come after it and values less than the pivot come before it. The lesser and greater sub lists are sorted recursively. O(n log n). Slide pseudocode:
```
Quicksort(array)
  declare arrays less, equal & greater
    if array.length <= 1
        return array
    select a pivot value pivot from array
    foreach(x in array)
        if x < pivot then append x to less
        if x = pivot then append x to equal
        if x > pivot then append x to greater
    return quicksort(less) + equal + quicksort(greater)
```

### C++ built in sorting (slide 36)
The slide shows `#include <algorithm>`, a `compare` function `bool compare(int i, int j) { return (i<j); }`, and a vector filled with `push_back(1)`, `5`, `17` and `2`. `sort(v.begin(), v.end());` sorts it, with a comment on the slide that `sort(v.begin(), v.end(), compare);` also works. A loop then prints the elements; the console on the slide shows 1, 2, 5, 17.

### Linear search (slides 37 and 38)
Search for the item until it is found or the end of the list is reached. The worst case is when the nth element holds the item or the item is not present at all, so O(n). Slide 37 code:
```cpp
int linear_search(vector<int> v, int a)
/* PURPOSE: find an element in a vector
   RECEIVES: v - the vector with the elements to search
   a - the value to search for
   RETURNS: the index of the first match, or -1 if not found */
{
    int i;
    for (i = 0; i < v.size(); i++) {
      if (v[i] == a)
        return i;
    }
    return -1;
}
```

### Binary search (slides 39 to 41)
- Assume the array (vector) is sorted. Try the element in the middle. If it is the correct one, done. If the item sought is less than the item found, search the left half (same algorithm). If it is greater, search the right half (same algorithm).
- Slide 40 code:
```cpp
int binary_search(vector<int> v, int from, int to, int a)
/* PURPOSE: find an element in a sorted vector
RECEIVES: v - the sorted vector with the elements to search from,
to - the range to search
a - the value to search for
RETURNS: the index of the first match, or -1 if not found */
{ if (from > to)
      return -1;
   int mid = (from + to) / 2;
   int diff = v[mid] - a;
   if (diff == 0) /* v[mid] == a */
     return mid;
   else if (diff < 0) /* v[mid] < a */
     return binary_search(v, mid + 1, to, a);
   else
     return binary_search(v, from, mid - 1, a);
}
```
- Slide 41 analysis: assume the time is proportional to the number of accesses, B(n) is the number of accesses for size n, and n = 2^m. B(n) = B(n/2)+1 = B(n/4)+1+1 = B(n/4)+2, and so on to B(n) = B(n/2^k)+k. At k = m: B(n) = B(2^m/2^m)+m = 1+log2 n, so O(log n).

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

## Amendments
- 28 Oct (Amend S11): read slides 6 to 9, 18 to 20 and 22 to 41 as images and added them as presented (Big-O definition, recursion, every sort and search with the slide code and analysis). Corrected the partial-coverage paragraph. (added) Slide figures for Examples 1 to 3b, with two slide arithmetic slips flagged. Added N.B. lines: low frequency, do not focus too much on the Big-O definition, recursion and sorting and searching sections.
