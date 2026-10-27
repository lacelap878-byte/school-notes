---
module: CSC01B1
topic: Final Summary (S1 to S11)
test_label: Final
tags: [summary]
---

# CSC01B1 Final Summary (Sessions 1 to 11)

Built for the exam on Monday 2 November 2026 (2 hours, 100 marks, written), not for first learning. If something here does not click, follow the link back to the full session note. Earlier test summaries are linked, not copied: [[CSC01B1_Summary_ST1]] and [[CSC01B1_Summary_ST2]].

Scope: the whole module, S1 to S11. `cs` PROFILE has no proof content, so no Proofs file accompanies this one.

Reliability: where this file and an older log disagree, the S9 to S11 session (27 October 2026) is the most recent record. Sessions S9, S10 and S11 are only partly covered (see Material covered, After ST2).

## Contents

Click a link to jump to it.

- [[#CSC01B1 Final Summary (Sessions 1 to 11)]] title, scope and how reliable the sources are
- [[#Definitions]] every term the file uses, with a labelled list anatomy
  - [[#Linked list terms]] node, head, current, nullptr, template, slide names against exam names
  - [[#Stack and queue terms]] LIFO, FIFO, push, top, pop, addQueue, deleteQueue, tail pointer
  - [[#Complexity terms]] Big-O, N, T(N), pass, worst case, the three assumptions
  - [[#Class and object terms]] composition against aggregation, delegation, overloading against overriding
  - [[#File and DLL terms]] record, header, seekg and seekp, padding, DLL, implicit and explicit linking
  - [[#Exception terms]] throw, try, catch, what(), stack unwinding
- [[#Material covered]] which notes belong to which test, and what S9 to S11 left out
  - [[#Before ST1 (S1 to S4)]] S1 to S4 notes
  - [[#Between ST1 and ST2 (S5 to S8)]] S5 to S8 notes
  - [[#After ST2 (S9 to S11)]] S9 to S11 notes, taught and not taught
- [[#Condensed concept pass]] one short entry per major result, linked
  - [[#Sessions 1 to 4]] pointers back to the ST1 summary and notes
  - [[#Sessions 5 to 8]] pointers back to the ST2 summary, plus templates and DLLs
  - [[#Linked lists]] node, head, loop stops, insert, delete
  - [[#Stacks and queues]] LIFO, FIFO and the linked versions
  - [[#Complexity analysis]] counting steps, nested loops, results table
- [[#Worked example notebook]] list code and a Big-O count, with earlier examples linked
  - [[#Counting nodes in a list]] the traversal skeleton
  - [[#Inserting after a value]] stop ON the node, link order
  - [[#Deleting a specific node]] stop BEFORE the node, the first node case
  - [[#Deleting the whole list]] temp, move, delete, then head is nullptr
  - [[#Counting steps for a search]] T(N) = 4N + 2 for 2025 C
- [[#What the tests showed]] the user's own account of ST1 and ST2 and where the marks stand
  - [[#Semester test 1 (ST1)]] the mark and the UML time loss, in the user's words
  - [[#Semester test 2 (ST2)]] the 49% cap, the remark and the query, in the user's words
  - [[#Where the marks stand]] the assessment rules and the exam mark needed
  - [[#Patterns across the tests]] what the user has and has not reported
- [[#Common mistakes]] grouped by pattern, open items in orange
  - [[#Writing from a blank page]] recognition against production, signatures, the counting skeleton
  - [[#Mixing look-alike patterns]] stop ON against stop BEFORE, member against friend, stack against queue
  - [[#Treating two independent things as one]] seekg and seekp, assignment and pointers, templates
  - [[#Pointers and list mechanics]] empty list, head, copying addresses
  - [[#Small copying slips]] names, missing lines, class name prefixes
  - [[#Jargon]] DLL words, padding, file stream traps
  - [[#Complexity]] assumptions, nested loops, unpractised operations
- [[#Decision aids]] question map, loop stops, operation table, stack or queue, Big-O steps, DLL linking
  - [[#Which question is this]] the paper map with marks and where to look
  - [[#Which loop test stops where]] the table for every list loop
  - [[#Linked list operations at a glance]] special cases and core lines
  - [[#Insert before and search]] the two list tasks never practised
  - [[#Stack or queue]] side by side table
  - [[#Counting steps and giving the Big-O]] the five steps and the results table
  - [[#Two class exception hierarchy]] base and derived exception code for Q2.2
  - [[#Implicit or explicit linking]] DLL client choice
- [[#Exam procedure]] timing, the UML cap, a check before moving on
- [[#Tips]] terminology traps and where to spend time

## Definitions

Words this file uses, one plain line each. Operator and signature words (signature, parameter, argument, operand, member operator, nonmember operator, the three places `const` can sit, `*this`, temporary) are defined once in [[CSC01B1_Summary_ST2#Definitions]] and are not repeated here.

### Linked list terms

Anatomy of a list. Each label points at a visible thing.

```
 head              node 1              node 2              node 3
 [address] ---->  [ data | next ] --> [ data | next ] --> [ data | next ] --> nullptr
 outside the      the item   the      the item   the      the item   next of the
 nodes            stored     address  stored     address  stored     last node
                            of the                of the              is nullptr
                            next node             next node
```

```cpp
template <typename T>
struct Node { T data; Node<T> *next; };

Node<string> *head = nullptr;
```

- **Node**: one box in the list. It holds an item (`data`) and the address of the next box (`next`).
- **head**: a pointer variable that holds the address of the first node. It lives outside the nodes. Lose it and the whole list is lost.
- **current**: a second pointer, copied from `head`, used to walk the list. Never walk with `head` itself.
- **nullptr**: the address that points at nothing. An empty list is `head = nullptr`. A pointer that was never given a value is garbage, not empty. The slides write `NULL` and the exam writes `nullptr`; treat them as the same.
- **Traverse**: visit every node from the first to the last by following `next`.
- **Slide names versus exam names**: the slides use `nodeType`, `info`, `link`, `NULL`; the exam uses `Node<T>`, `data`, `next`, `nullptr`. Same thing.
- **Template**: code with a type left blank (`T` or `Type`) that is filled in when it is used. `Node<string>` is a node whose `data` is a `string`. `template <class Type>` covers exactly the one declaration beneath it.

### Stack and queue terms

- **Stack**: items go in and come out at one end only, the top. Last in, first out: **LIFO**.
- **Queue**: items go in at the rear and come out at the front. First in, first out: **FIFO**.
- **push, top, pop**: add at the top; read the top without removing it; remove the top.
- **addQueue, deleteQueue**: the lecture's names for adding at the rear and removing from the front. Other books say enqueue and dequeue.
- **Tail pointer**: a second pointer to the last node, so adding at the rear needs no walk.

### Complexity terms

- **Big-O**: the highest power of N left after counting the steps and dropping constants. It says how the work grows with the problem size.
- **N**: the problem size. It is whatever grows in the code you are given, for example `_end`, the number of elements.
- **T(N)**: the number of counted operations for a problem of size N.
- **Pass**: one run of a loop body.
- **Worst case**: the input that makes the code do the most work. Complexity questions count this one.
- **The three assumptions**: the operations counted are a fair measure of time; each takes the same time; N is the problem size.

### Class and object terms

- **Composition versus aggregation**: both are has-a. If the container governs the life of the contained object, it is composition; if the contained object can outlive the container, it is aggregation. (see: [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Composition and aggregation (has-a)]])
- **Association**: one class calls another with no ownership tie. Not has-a, not is-a.
- **Delegation**: the container hands a job to the object it contains (the T2 shape in the practical tests).
- **Overloading, redefining, overriding**: overloading is the same name with different parameters (an assignment operator is overloading); redefining changes a non-virtual function in a derived class; overriding changes a virtual one.
- **Abstract data type**: a type where what it does is kept apart from how it is stored. The lecture gives a formal definition; quote it from the note, not from this line. (see: [[CSC01B1_Notes_S1_Foundation-Topics#15. Extending the type system]])

### File and DLL terms

- **Record**: one fixed size block in a binary file (a struct written with `write`). Record number counts from 0, so the 2nd record is index 1.
- **Header**: a block at the start of a file before the records. Add its size when computing an offset, subtract it when counting records.
- **seekg, seekp**: the read marker and the write marker. They are independent. Seeking only moves a marker; it reads nothing.
- **Padding**: unused bytes the compiler inserts so each member sits at an address that suits its alignment. Reordering members changes the total size.
- **DLL**: a file of ready-made functions that a program loads when it runs, instead of having the source built into it. Under Windows it is a Dynamic Link Library.
- **Implicit linking**: the program is built against the DLL and its header; Windows loads the DLL when the program starts, and refuses to start if it is missing.
- **Explicit linking**: the program loads the DLL itself with `LoadLibrary` and finds each function by name with `GetProcAddress`; it can carry on if the DLL is missing.
- **Exported function**: a function a DLL makes available. The header uses a macro that is `dllexport` when building the DLL and `dllimport` when using it.

### Exception terms

- **Exception**: an undesirable event detected while the program runs. It is a value matched to a `catch` block by type.
- **throw, try, catch**: raise it; the block where it may happen; the block that handles it.
- **what()**: the function that returns the message. It belongs to the library class `exception`. A class you write has one only if you write it.
- **Stack unwinding**: a function with no handler is abandoned and its locals are destroyed, outward through the callers until a matching `catch` is found or `terminate` ends the program.

## Material covered

### Before ST1 (S1 to S4)

Summary: [[CSC01B1_Summary_ST1]].

- [[CSC01B1_Notes_S1_Foundation-Topics]] binary, bitwise, memory model, pointers, arrays, function pointers, structs
- [[CSC01B1_Notes_S2_Modules]] C++20 modules
- [[CSC01B1_Notes_S3_Classes-Data-Abstraction]] classes and data abstraction
- [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance]] composition, aggregation, inheritance, the stream hierarchy

### Between ST1 and ST2 (S5 to S8)

Summary: [[CSC01B1_Summary_ST2]].

- [[CSC01B1_Notes_S5_Polymorphism]] virtual functions, abstract classes, slicing, virtual destructors, casting
- [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]] operator overloading and templates
- [[CSC01B1_Notes_S7_FileHandling]] file handling, random access, raw bytes, padding, DLLs
- [[CSC01B1_Notes_S8_ExceptionHandling]] exception handling

### After ST2 (S9 to S11)

These three were taught in drill format and are partial.

- [[CSC01B1_Notes_S9_LinkedLists]] linked lists. Taught: the node, head, traversal, insert at start, end and after a value, delete first, last, a specific node and the whole list. Not taught: the list class, iterators, ordered and unordered lists (slides 29 to 71), print in reverse, doubly linked and circular lists (74 to 88).
- [[CSC01B1_Notes_S10_StacksAndQueues]] stacks and queues. Taught: the idea of each and the linked versions. Not taught: array stacks and queues, postfix evaluation, printing backward with a stack, the queue simulation.
- [[CSC01B1_Notes_S11_ComplexityAnalysis]] complexity analysis. Taught: the counting method. Not taught: the sorting and searching slides (22 to 41); only their Big-O results are listed.

## Condensed concept pass

Entries for S1 to S8 point to the test summary that already holds them. S9 to S11 are written out because no test summary exists for them yet.

### Sessions 1 to 4

- Number systems, bitwise operations, two's complement, memory model, pointers, arrays and memory errors: see [[CSC01B1_Summary_ST1#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S1_Foundation-Topics#7. The C++ memory model]], [[CSC01B1_Notes_S1_Foundation-Topics#9. Pointers and references]], [[CSC01B1_Notes_S1_Foundation-Topics#12. Memory errors]].
- Function pointers and typedef (needed again for explicit DLL linking): [[CSC01B1_Notes_S1_Foundation-Topics#14. Function pointers]], [[CSC01B1_Notes_S1_Foundation-Topics#15. Extending the type system]].
- Modules: see [[CSC01B1_Summary_ST1#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S2_Modules#Building a first module]].
- Classes, constructors, destructors, static members, information hiding: see [[CSC01B1_Summary_ST1#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S3_Classes-Data-Abstraction#Constructors]], [[CSC01B1_Notes_S3_Classes-Data-Abstraction#Destructors]].
- UML class diagrams, association, composition and aggregation, inheritance, protected access, the stream hierarchy: see [[CSC01B1_Summary_ST1#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#UML class diagrams]], [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Composition and aggregation (has-a)]], [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#The C++ stream class hierarchy]].

### Sessions 5 to 8

- Virtual functions, overriding versus redefining, pure virtual and abstract classes, slicing, virtual destructors, casting, the vtable: see [[CSC01B1_Summary_ST2#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S5_Polymorphism#Core definitions]], [[CSC01B1_Notes_S5_Polymorphism#The slicing problem]].
- Operator overloading (member versus nonmember, assignment, pre and post increment, subscript): see [[CSC01B1_Summary_ST2#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Operator Overloading Quick Reference]].
- Templates (tested by the exam, not by ST2): `template <class Type>` covers one declaration; the parameter is resolved at compile time; definitions go in the client code, in one header, or in an implementation file included at the end of the header, and a separate compiled `.cpp` fails at link time. Notes: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Class Templates]], [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Where Template Definitions Must Live (Header and Implementation Files)]].
- File handling (text streams, open modes, seekg and seekp, raw `write` and `read`, padding): see [[CSC01B1_Summary_ST2#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S7_FileHandling#Two independent position markers]], [[CSC01B1_Notes_S7_FileHandling#Padding and byte alignment (slide 39)]].
- DLLs (tested by the exam, not by ST2): a header with the export or import macro, an implementation file that becomes the `.dll`, and a client linked either implicitly (header plus `-l`) or explicitly (`LoadLibrary`, `GetProcAddress`, a function pointer typedef). Notes: [[CSC01B1_Notes_S7_FileHandling#Reusable software components: DLLs (slides 42 to 51)]], [[CSC01B1_Notes_S7_FileHandling#Implicit linking (source, slides 48 and 49)]], [[CSC01B1_Notes_S7_FileHandling#Explicit linking (source, slide 50)]].
- Exceptions (try, catch, throw, catch order, the exception classes, rethrowing, stack unwinding): see [[CSC01B1_Summary_ST2#Condensed concept pass]]. Notes: [[CSC01B1_Notes_S8_ExceptionHandling#Stack unwinding]].

### Linked lists

- A list is nodes joined by pointers; `head` is a separate variable holding the first address, and you walk with a copy of it. (see: [[CSC01B1_Notes_S9_LinkedLists#What a linked list is]], [[CSC01B1_Notes_S9_LinkedLists#Pointers copy addresses, not nodes]])
- The exam node is templated: `template <typename T> struct Node { T data; Node<T> *next; };`. (see: [[CSC01B1_Notes_S9_LinkedLists#The node (slide 8)]])
- Which loop test stops where decides most operations (see the decision aid Which loop test stops where). (see: [[CSC01B1_Notes_S9_LinkedLists#Which loop test stops where]])
- Insert: the new node takes what follows first, then the earlier node is re-pointed. (see: [[CSC01B1_Notes_S9_LinkedLists#Insertion (slides 15 to 19)]])
- Delete: save in `temp`, bypass, then `delete`; the first node is its own case. (see: [[CSC01B1_Notes_S9_LinkedLists#Deletion (slides 20 to 22)]])
- Past papers 2021 to 2025, Q2.4 to Q2.6: the templated node (5) then two operations (5 each). (see: [[CSC01B1_Notes_S9_LinkedLists#Exam frequency (verified, 2021 to 2025, Q2.4 to Q2.6)]])

### Stacks and queues

- Stack is LIFO (push, top, pop at one end); queue is FIFO (add at the rear, delete from the front). (see: [[CSC01B1_Notes_S10_StacksAndQueues#Stack versus queue, side by side]])
- On a linked list a stack is insert at start and delete first, with `top` reading `head->data`. (see: [[CSC01B1_Notes_S10_StacksAndQueues#The linked stack (slides 31 to 45)]])
- A linked queue adds at the rear and deletes from the front; a tail pointer avoids walking. (see: [[CSC01B1_Notes_S10_StacksAndQueues#The linked queue (slides 90 to 96)]])

### Complexity analysis

- Count operations, not seconds, under the three assumptions. (see: [[CSC01B1_Notes_S11_ComplexityAnalysis#The three assumptions]])
- Nested loops multiply the pass counts, sequential loops add, drop constants, keep the highest power, count the worst case. (see: [[CSC01B1_Notes_S11_ComplexityAnalysis#The method (added)]])
- Sorting and searching results: [[CSC01B1_Notes_S11_ComplexityAnalysis#Sorting and searching (slides 22 to 41), results only]].

## Worked example notebook

Examples already in the earlier summaries are linked, not repeated: the UJImage operator drills, Pet and Dog slicing, padding, write and seek and read back, and the three-function unwinding trace are all in [[CSC01B1_Summary_ST2#Worked example notebook]]. The module's early examples are in [[CSC01B1_Summary_ST1#Worked example notebook]]. New for S9 to S11:

### Counting nodes in a list

(source: S9 session, the user's drill, corrected; see [[CSC01B1_Notes_S9_LinkedLists#Traversal (slides 13 and 14)]])

```cpp
int count = 0;
Node<string> *current = head;
while (current != nullptr)
{
    if (current->data == "S6") count++;
    current = current->next;
}
cout << count << endl;
```

### Inserting after a value

(source: S9 session; see [[CSC01B1_Notes_S9_LinkedLists#Insertion (slides 15 to 19)]]). Stop ON the node, then link the new node first.

```cpp
Node<string> *current = head;
while (current != nullptr && current->data != "T3") current = current->next;
if (current != nullptr) {
    newNode->next = current->next;
    current->next = newNode;
}
```

### Deleting a specific node

(source: S9 session; see [[CSC01B1_Notes_S9_LinkedLists#Deletion (slides 20 to 22)]]). Stop BEFORE the node; the first node is a separate case.

```cpp
if (head == nullptr) return;
if (head->data == "T3") { Node<string> *temp = head; head = head->next; delete temp; }
else {
    Node<string> *current = head;
    while (current->next != nullptr && current->next->data != "T3") current = current->next;
    if (current->next != nullptr) {
        Node<string> *temp = current->next;
        current->next = temp->next;
        delete temp;
    }
}
```

### Deleting the whole list

(source: S9 session, the user's own correct answer)

```cpp
Node<string> *current = head;
while (current != nullptr)
{
    Node<string> *temp = current;
    current = current->next;
    delete temp;
}
head = nullptr;
```

### Counting steps for a search

(source: S11 session, 2025-C `UJBuffer::search`; see [[CSC01B1_Notes_S11_ComplexityAnalysis#Worked example (2025-C UJBuffer::search)]]). The counted operations are `=`, `<`, `++`, `[]`, `==` and `return`, and N is `_end`. Outside the loop: 2 operations. Per pass: 4. Worst case: N passes.

$$T(N) = 4N + 2$$

T(N): operations counted for problem size N; the 4N is 4 operations in each of N passes; the 2 is the work outside the loop. The highest power is N, so the result is $O(N)$.

## What the tests showed

This section records what the user reported, in their words. Nothing is inferred from outside that account. The ST2 account is incomplete: the user had not seen their ST2 submission again when it was given, and planned to look at it on 28 October 2026.

### Semester test 1 (ST1)

- The user reported: "i got 30% in my ST1".
- The user reported that the test was 45 minutes and that the UML question took up the time: "it was the reason i wasted 45 minutes in my st1".
- Question 4 and Question 5 were not done: "i couldnt do question 4 or 5 that was 20 marks down the drain and the uml was only 10 marks".

### Semester test 2 (ST2)

- The paper: a 3 hour practical, marked by VPL (from [[CSC01B1_Summary_ST2#Paper shape]]).
- The user reported the mark as 49%, unmoderated, and said the lecturers told them a submission that does not compile is capped at 49%.
- The user reported that the marker's remark said the code did not compile, and said: "i distinctly remember it did compile" and "i vividly remember checking my code for the final time not having any errors".
- The user reported what the lecturers said at the query: the markers use their own batch file; from experience a "no compile" is likely still a "no compile" on remark, but it is an average; minor fixes can be made, and if the code does compile the marks are given. The user changed their own batch file.
- The user reported that someone else's UML went from 4/10 to 10/10 on remark, and said they would query the exception handling bonus if they did not see 10 out of 10.
- As of 27 October 2026 the ST2 remark was still pending.

### Where the marks stand

From the learning guide and the user's own screenshots on 27 October 2026. All can change after the ST2 remark.

- Rules: the semester mark is 10% PM, 25% ST1 and 65% ST2, and must be at least 40% to enter the exam. The final is 50% semester and 50% exam, with at least 50% overall and at least 40% in the exam.
- Marks reported: ST2 49 (unmoderated), the Class Test 100 (the user was told it is very likely the PM), a tentative semester mark of 51.
- Arithmetic from those rules: a 50% final needs about 49% in the exam, and a 65% final needs about 79%.
- In session practicals marked by VPL read 0 for compile failures (practicals 1, 2, 3, 4 and 6) and the lecturer said they are being remarked, on the basis that code which does not compile does not get the mark.

### Patterns across the tests

The user has not reported a pattern across the two tests. The patterns in Common mistakes come from the practice logs, not from this account.

## Common mistakes

Merged across both test summaries and every struggle log, grouped by pattern. Open items are in orange with "Open:" in front. Resolved items are one line.

### Writing from a blank page

- <span style="color:#f08c00">Open:</span> recognising the right answer is not the same as writing the code. This showed in S7 and again in S9. The exam is written, so practise on blank paper.
- <span style="color:#f08c00">Open:</span> operator signatures from memory (object parameter without `&`, trailing `const` the wrong way, `()` returning the wrong type). The ST2 decision tree exists; a second cold recall was never done. (see: [[CSC01B1_Summary_ST2#Operator signature decision tree]])
- <span style="color:#f08c00">Open:</span> the counting skeleton for a list, in production: `current` declared twice and a peek-ahead loop that never moved.

### Mixing look-alike patterns

- <span style="color:#f08c00">Open:</span> insert after a value (stop ON the node, link the new node first) against delete (stop BEFORE the node). The drill stopped before the node and linked in the wrong order, so the new node pointed at itself.
- <span style="color:#f08c00">Open:</span> delete a specific node: `next->next` was written where `next->data` was needed, and the first-node case was missed.
- <span style="color:#f08c00">Open:</span> delete last: the loop `while (current->next->next != nullptr)` stops one BEFORE the last node. In the quiz the answer chosen was B; the correct one is C.
- <span style="color:#f08c00">Open:</span> member versus friend when the left operand is not the class type, post-increment returning the saved copy, `[]` needing a const overload, copy constructor versus assignment.
- <span style="color:#f08c00">Open:</span> stack versus queue must be answered from the rule (LIFO or FIFO), not from real-world exceptions such as a printer.

### Treating two independent things as one

- <span style="color:#f08c00">Open:</span> `seekg` and `seekp` are separate markers; `.read()` uses `seekg`. Answered correctly in the S9 quiz, with the weakest evidence; the user says it still needs grinding.
- <span style="color:#f08c00">Open:</span> the default `=` with a pointer member compiles and copies the address (a leak and a double free); `template <class Type>` covers one declaration only; a class template member defined outside the class needs its own template line and `Box<Type>::`; template definitions in a separate `.cpp` fail at link time.
- Resolved: slicing is the assignment running on a smaller footprint; a derived object holds its own base subobject, so chained destructors do not double free.

### Pointers and list mechanics

- <span style="color:#f08c00">Open:</span> an empty list is `= nullptr`, never an uninitialised pointer. This was discussed but not produced under test.
- Resolved: the node struct has no `head` inside it (correct in two later retests); delete first and delete the whole list (correct under production); a pointer copies an address and not the node (discussion only, weakest evidence).

### Small copying slips

- <span style="color:#f08c00">Open:</span> variable names must be copied exactly (`NewNode` against `newNode` happened twice). Also `newNode->next = nullptr;` was left out of insert at end, and `ClassName::` was left off out-of-class definitions in the UJImage drills.
- Repeated lines pasted without changing the channel (the `+` operator), a missing `return`, and missing semicolons. From the ST2 drills.

### Jargon

- <span style="color:#f08c00">Open:</span> DLL syntax and jargon: the macro switch (`dllexport` or `dllimport`) and the `-D` flag, `.impl.cpp`, the typedef on a function pointer. The user says they do not understand DLLs. `extern "C"` was answered correctly in the S9 quiz. Q4 is worth 20 marks.
- <span style="color:#f08c00">Open:</span> padding placement, alignment of a compound member, what `reinterpret_cast` does, `.open()` taking one mode argument, `ifstream` against `fstream`, `if (!x.fail())` reporting an error on success, arrays cannot be assigned with `=`, `.read()` and `.write()` direction, header offset in record counting.
- Resolved in S8 (weakest evidence): what stack unwinding skips, a `catch` block is not forced to exist, `what()` belongs to `exception`.

### Complexity

- <span style="color:#f08c00">Open:</span> the three assumptions are not memorised (the quiz answer was a gut feeling), and it is unclear why the third changes: N is whatever the problem size is in that code.
- <span style="color:#f08c00">Open:</span> combining nested loops: the outer loop's own work is added once per outer pass, not multiplied by the inner loop.
- <span style="color:#f08c00">Open:</span> insert BEFORE a value and search were never practised, and both are in past papers.

## Decision aids

### Which question is this

From the 2023 A and 2025 C papers (2 hours, 100 marks, four questions). Marks vary slightly by paper.

```
Q1 (20)  1.1 UML diagram (5); 1.2 to 1.6 multiple choice A to E; short answers
         (abstract data type, the stream hierarchy, a stack on a linked list);
         name the OO concept from a sentence
Q2 (30)  2.1 a template class with an operator filled in (10); 2.2 an exception
         hierarchy of two classes (2); 2.3 using the template (3);
         2.4 templated node (5); 2.5 and 2.6 two list operations (5 each)
Q3 (30)  3.1 to 3.4 file handling (5 each); 3.5 Big-O on given code (10)
Q4 (20)  a DLL: the header file, then two further parts
```

Where to look:

- UML: [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#UML class diagrams]] and [[CSC01B1_Notes_S3_Classes-Data-Abstraction#UML class diagrams]].
- 2.1: [[CSC01B1_Summary_ST2#Operator signature decision tree]] and [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Operator Overloading Quick Reference]].
- 2.2: the exception recipe below.
- 2.4 to 2.6: the list aids below.
- Q3: [[CSC01B1_Notes_S7_FileHandling#Worked coding exercise: write, seek, read back (composite)]], [[CSC01B1_Notes_S7_FileHandling#Reaching a record and counting records (source, slides 40 and 41)]]; and the Big-O template below.
- Q4: [[CSC01B1_Notes_S7_FileHandling#Example: a three-function DLL (composite)]].

### Which loop test stops where

Say it out loud with a three node list A, B, C. (from S9)

| Loop test | Where `current` stops | Use for |
|---|---|---|
| `current != nullptr` | past the end (it is `nullptr`) | count, print, search, delete the whole list |
| `current->next != nullptr` | ON the last node (C) | insert at end |
| `current->next->next != nullptr` | one BEFORE the last node (B) | delete last |
| `current != nullptr && current->data != "X"` | ON the node X | insert after X |
| `current->next != nullptr && current->next->data != "X"` | BEFORE the node X | delete X, insert before X |

N.B `next->next` is two separate hops; `current` itself still moves one node per pass. Stop ON a node to insert after it, stop BEFORE a node to delete it or to insert before it.

### Linked list operations at a glance

| Operation | Special cases first | Core lines |
|---|---|---|
| Insert at start | none | `newNode->next = head; head = newNode;` |
| Insert at end | empty list; set `newNode->next = nullptr` | walk to the last node; `current->next = newNode;` |
| Insert after X | X not found | `newNode->next = current->next; current->next = newNode;` |
| Delete first | empty list | `temp = head; head = head->next; delete temp;` |
| Delete last | empty list; one node | stop BEFORE the last; save it; `current->next = nullptr;` delete it |
| Delete X | empty list; X is the first node; X not found | `temp = current->next; current->next = temp->next; delete temp;` |
| Delete all | none | `temp = current; current = current->next; delete temp;` then `head = nullptr;` |

### Insert before and search

(added) Both appear in the past papers and were never practised. 2025 C Q2.6 asks to insert "S5" before the first node containing "S6", and 2022 B Q2.6 asks for a search. This code was compiled and run with g++ in C++20 mode, with the list N, S6, T3, S6: it gave N, S5, S6, T3, S6, and the head case gave S5, S6. Treat it as a pattern to rehearse, then write it from a blank page.

```cpp
Node<string> *newNode = new Node<string>;
newNode->data = "S5";
if (head != nullptr)
{
    if (head->data == "S6")
    {
        newNode->next = head;
        head = newNode;
    }
    else
    {
        Node<string> *current = head;
        while (current->next != nullptr && current->next->data != "S6")
            current = current->next;
        if (current->next != nullptr)
        {
            newNode->next = current->next;
            current->next = newNode;
        }
        else delete newNode;
    }
}
```

Search: start from the counting skeleton, set a `bool found = false;` before the loop, set it to `true` when `current->data` matches, then step on.

### Stack or queue

| Question | Stack | Queue |
|---|---|---|
| Who leaves first | the last one in (LIFO) | the first one in (FIFO) |
| Where items go in | the top | the rear |
| Where items come out | the top | the front |
| Names in the lecture | push, top, pop | addQueue, deleteQueue, front, back |
| On a linked list | insert at start, delete first | insert at end (tail pointer), delete first |

Answer from the rule, then give the list version in one sentence (2025 C Q1.9 asks how a stack is built on a linked list, 2 marks).

### Counting steps and giving the Big-O

Write these in this order, every time. (see: [[CSC01B1_Notes_S11_ComplexityAnalysis#The three assumptions]])

1. State the three assumptions: the operations counted are a fair measure of time; each takes the same time; N is the problem size, and say what N is in this code.
2. List the operations you count (`=`, `<`, `++`, `[]`, `==`, `return`).
3. Count the operations outside the loop, the operations in one pass, and the passes in the worst case.

$$T(N) = \text{outside} + \text{passes} \times \text{cost per pass}$$

T(N): operations counted for problem size N; outside: operations run once; passes: how many times the loop body runs; cost per pass: operations in one pass.

4. Nested loops multiply the pass counts, sequential loops add. The outer loop's own work is added once per outer pass.
5. Drop constants and lower powers and write the Big-O: for example $T(N) = N^2 + N$ gives $O(N^2)$.

Results for the sorts and searches (from the lecture; the papers 2021 to 2025 never name them in a question):

| Algorithm | Worst case |
|---|---|
| insertion sort | $O(n^2)$ |
| selection sort | $O(n^2)$ |
| bubble sort | $O(n^2)$ |
| merge sort | $O(n \log n)$ |
| quick sort | $O(n \log n)$ |
| linear search | $O(n)$ |
| binary search | $O(\log n)$ |

### Two class exception hierarchy

(added) Q2.2 asks for a base exception type and a specific exception type. This was compiled with g++ in C++20 mode; the derived handler runs for a derived throw and the base handler for a base throw. Put the derived `catch` before the base `catch`. The ST2 version for the UJImage bonus is [[CSC01B1_Summary_ST2#The bonus plan]].

```cpp
class SensorException
{
public:
    SensorException(string strMsg) : _strMsg(strMsg) {}
    string what() const { return _strMsg; }
protected:
    string _strMsg;
};

class RangeException : public SensorException
{
public:
    RangeException(string strMsg) : SensorException(strMsg) {}
};
```

### Implicit or explicit linking

(from S7) The DLL header and implementation are built into `.dll`; the choice is how the client finds it.

| | Implicit | Explicit |
|---|---|---|
| Needs the header | yes | no |
| Client build | `-L.` and `-lname` | compiled normally |
| Functions found | by the linker | `GetProcAddress(handle, "name")` into a function pointer typedef |
| DLL missing at start | the program refuses to start | the program can test the handle and carry on |

Explicit order: `LoadLibrary`, `GetProcAddress`, call through the pointer, `FreeLibrary`. (see: [[CSC01B1_Notes_S7_FileHandling#Explicit linking (source, slide 50)]])

## Exam procedure

From the past papers the user supplied (2023 A and 2025 C read for this section) and from the user's ST1 account. Items marked (added) are plans, not facts about the paper.

- The paper is 2 hours and 100 marks. At 100 marks in 120 minutes that is 1.2 minutes per mark.
- Question 1 starts with a UML diagram worth 5 marks (1.1 in both papers). (added) 5 marks is about 6 minutes at the rate above, so give the UML a 6 minute cap. In ST1 the UML question used the time that Question 4 and Question 5 needed.
- (added) A budget that leaves 10 minutes spare: Q1 22 minutes, Q2 33, Q3 33, Q4 22. Write the finish time of each question at the top of the paper.
- (added) If a question stalls, write what you have, mark it, and move on. Come back with the spare time.
- Multiple choice items in Q1 are lettered A to E; read the question's wording for "most correct".
- Q2.4 to Q2.6 are about a depicted list. Read the picture first: the node's type comes from what the boxes hold (a string in the 2025 C and 2023 A papers).
- The exam is on paper, so no compiler will catch slips. Before moving on, read the code once for: names copied exactly, the empty list case, `newNode->next = nullptr;`, `ClassName::` on out-of-class definitions, and a `return` where one is needed.
- Q3.5 starts with the three assumptions and what N is; then the count.

## Tips

- Terminology trap: "composition" used loosely in S1 for any struct inside a struct; the precise has-a distinction (life-span) is S4. A precise question wants S4. (from [[CSC01B1_Summary_ST1#Tips]])
- Terminology trap: the lecture slides name things differently from the exam. List: `nodeType`, `info`, `link`, `NULL` in the slides, `Node<T>`, `data`, `next`, `nullptr` in the exam. Queue: `addQueue`, `deleteQueue` in the lecture, enqueue and dequeue elsewhere. The doubly linked back pointer is `back` in the lecture, not `prev`.
- Where a lecture slide states a soft rule, check what the compiler does before relying on it: the slide says `catch (...)` should be last, and g++ makes anything else a compile error.
- Each operator's meaning is defined by the paper, not by C++. Read that line for every operator, and follow a provided declaration where it disagrees with the paper text. (from [[CSC01B1_Summary_ST2#Reading the paper]])
- When a mechanism feels arbitrary, ask whether an earlier session showed the by-hand version: the self pointer before `this`, the node and `head` before a stack class. (from [[CSC01B1_Summary_ST1#Tips]])
- Doubly linked and circular lists are only in the 2018 and 2019 papers, and sorting and searching are never named in the 2021 to 2025 questions. Spend the time on the list operations, DLLs and the Big-O count first.
- Insert BEFORE a value and search are the two list tasks in the papers that were never practised.
