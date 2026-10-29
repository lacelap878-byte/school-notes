Supersedes S1 to S10. This is the only handoff file needed.

## 1. OBJECTIVE (this session)
Cover the last three exam topics in the semester: linked lists (Lecture 8), stacks and queues (Lecture 9) and complexity analysis, in drill format, for the CSC01B1 exam on Monday 2 November 2026 (2 hour written theory paper). The session also covered the ST2 mark query and the PM/Class Test question for the lecturers.

Exam context (updated 28 October): ST2 is 72 (after the remark), ST1 is 35 (14 of 40), Class Test 100 is very likely the PM. Semester mark = 10% PM + 25% ST1 + 65% ST2, about 65.5. Final = 50% semester + 50% exam, with at least 50% overall and at least 40% in the exam, so about 64.5% in the exam gives a 65% final (the cum laude goal; the module target is 65% or above). The PM line and the in-session practical (VPL) remark are still pending and could change the semester mark.

## 2. TOPIC LEDGER
```
S1 | Foundation Topics (binary and number systems, bitwise ops, signed numbers, memory model, pointers, arrays, function pointers, structs, intro to classes) | full | open struggle no
S2 | C++20 Modules (module concept, first module, export blocks, prototypes vs implementation) | full | open struggle no
S3 | Classes and Data Abstraction (class syntax, UML, objects, scope, constructors/destructors, ADTs, struct vs class, information hiding, static members) | full | open struggle no
S4 | Object Composition and Inheritance (OOD, UML, association, composition, inheritance syntax, overriding, derived-class constructors/destructors, protected members, stream hierarchy) | full | open struggle no
S5 | Polymorphism (virtual functions, late binding, pure virtual and abstract classes, slicing, virtual destructors, casting, vtable) | full | open struggle no
S6 | Operator overloading (fundamentals, this pointer, friend functions, binary/stream/assignment/unary/increment/subscript overloads) and templates (function and class, header layout) | full | open struggle yes (8 items, quiz 0 of 8)
S7 | File handling (secondary storage and streams, sequential file I/O, opening modes and flags, output formatting, random access, raw disk I/O, padding and #pragma pack, DLLs with implicit and explicit linking) | full | open struggle yes
S8 | Exception handling (exception, assert, try/catch/throw, catch order, exception classes and what(), user-defined exception classes, rethrowing, throw clause, handling techniques, stack unwinding) | full | open struggle no (S6 and S7 items stay open)
S9 | Linked lists, Lecture 8 (node, head, traversal, insert start/end/after, delete first/last/specific/whole list; exam style Node<T>) | full for the drilled part; amended 28 Oct (all slides read and written as presented, N.B. low frequency on slides 23 to 40 and 62 to 92) | open struggle yes | amended
S10 | Stacks and queues, Lecture 9 (LIFO, FIFO, operations, linked stack and queue as list code) | full for the drilled part; amended 28 Oct (all 108 slides written as presented, N.B. low frequency on array versions, postfix, print backward, simulation) | open struggle yes | amended
S11 | Complexity analysis (three assumptions, counting T(N), Big-O, results table for sorts and searches) | full for the counting method; amended 28 Oct (Big-O definition, recursion, every sort and search with slide code, N.B. low frequency) | open struggle yes | amended
```

## 3. NOTES INDEX
```
S1  | Foundation Topics | CSC01B1_Notes_S1_Foundation-Topics.md |
      Binary, bitwise ops, memory, pointers, arrays, function pointers (14), typedef (15), structs (16)
S2  | C++20 Modules | CSC01B1_Notes_S2_Modules.md |
S3  | Classes and Data Abstraction | CSC01B1_Notes_S3_Classes-Data-Abstraction.md |
S4  | Object Composition and Inheritance | CSC01B1_Notes_S4_Object-Composition-and-Inheritance.md |
S5  | Polymorphism | CSC01B1_Notes_S5_Polymorphism.md |
S6  | Operator overloading and templates | CSC01B1_Notes_S6_OperatorOverloadingTemplates.md |
      Lecture 5 retelling: operator overloading, then function and class templates
S7  | File handling | CSC01B1_Notes_S7_FileHandling.md |
      Lecture 6 retelling: streams, sequential and random access files, raw bytes, padding, DLLs
S8  | Exception handling | CSC01B1_Notes_S8_ExceptionHandling.md |
      Lecture 7 retelling: try/catch/throw, catch order, exception classes, rethrowing, handling techniques, stack unwinding
S9  | Linked lists | CSC01B1_Notes_S9_LinkedLists.md |
      Lecture 8: node, traversal, insertion, deletion, loop stop table, exam frequency table
S10 | Stacks and queues | CSC01B1_Notes_S10_StacksAndQueues.md |
      Lecture 9: stack, queue, linked versions, lecture operation names
S11 | Complexity analysis | CSC01B1_Notes_S11_ComplexityAnalysis.md |
      Three assumptions, counting method, worked example, Big-O results table
```
Project also holds CSC01B1-2026-L8.pdf (listed twice) and CSC01B1-2026-L9.pdf. Both were read this session (L8: 92 slides, L9: 108 slides), plus the 41 slide complexity deck.

## 4. CONTENT SUMMARY
S9 to S11 covered in drill format, with the user writing code on paper from a blank page and photographing it.
- Linked lists: a node is data plus a next pointer; head is a separate pointer outside the nodes; never walk with head, copy it into current. Pointers copy addresses, not nodes. Empty list is = nullptr (an uninitialised pointer is garbage). Loop tests: `current != nullptr` walks off the end; `current->next != nullptr` stops ON the last node; `current->next->next != nullptr` stops one before the last. Insert after stops ON the node; delete stops BEFORE it. Link order on insert: the new node takes what follows first, then the earlier node is re-pointed. Delete pattern: save in temp, bypass, delete. Delete whole list: temp, move, delete, then head = nullptr. Full corrected code is in the S9 notes.
- Stacks and queues: stack LIFO (push, top, pop), queue FIFO (lecture names addQueue, deleteQueue, front, back). On a linked list: push is insert at start, pop is delete first, top is head->data; queue adds at the rear and deletes from the front, with a tail pointer.
- Complexity: three assumptions (operations are a fair measure; each takes the same time; N is the problem size). T(N) = outside + passes x per pass, worst case, nested multiplies, sequential adds, keep the highest power. Worked example 2025-C UJBuffer::search: T(N) = 4N + 2, O(N).
- Differences between lecture slides and what was taught: slides use nodeType/info/link/NULL, the exam uses Node<T>/data/next/nullptr; the lecture says addQueue/deleteQueue, not enqueue/dequeue; the doubly linked node pointer is `back`, not `prev`.
- Exam structure 2021 to 2025: Q1 (20) UML, concepts, stack vs queue; Q2 (30) template class fill-in, exception hierarchy, linked list Q2.4 templated node (5), Q2.5 (5), Q2.6 (5); Q3 (30) file handling (20) plus Q3.5 Big-O (10); Q4 (20) DLLs. Insert BEFORE (2025-C Q2.6) and search (2022-B Q2.6) appear in the papers and were never practised. Doubly linked and circular lists appear only in the 2018 and 2019 papers. Sorts and searches are never named in 2021 to 2025 question text.
- Session-end check quiz: gaps on Q3 (delete a specific node pattern), Q4 (delete-last loop stop, chose B, correct is C), Q9 (assumptions a gut feeling).

S1 to S8 are one line each in the ledger. S6 and S7 items stay open (see the struggle log).

## 5. LAST POSITION
Amended 28 October (evening): S9, S10 and S11 notes were amended with every unread slide (L8, L9 and the complexity deck), written as presented with N.B. lines saying low frequency means do not focus on them. The user then asked to go over the skipped material in study mode. Also on 28 October: pointer versus node was argued at length (see the struggle log), the delete-last lecture version (trailing pointer) was taught, and no timed UML, Big-O or insert BEFORE and search drill has been run yet. The Final summary is stale (old marks).

## 6. PARKED ITEMS
```
Practice insert BEFORE a value and search in a list (both in past papers, never practised)
Doubly linked and circular lists: skim slides 74 to 88 (only in 2018 and 2019 papers)
Sorting and searching slides 22 to 41: the Big-O table only is needed
Corrected 28 October: all unread slides have now been read as images and written into the notes (Amended S11). Still to GO OVER in study mode (priority): L8 slides 62 to 72, complexity slides 6 to 9 and 18 to 20, L9 postfix and print backward, then L8 29 to 40 and 74 to 88, then L9 array stacks and queues and the sorts and searches. All of it is low frequency.
Timed UML drill, 6 minute cap (the ST1 UML cost 45 minutes). First run 28 Oct (2022-C Q1.1, Musical Instrument): not finished at 6 minutes; inheritance chain and overrides drawn well, but the Musician relationship (aggregation with the diamond on the Musician side, 0..* multiplicity, add and remove operations) was left out, the starting note was typed string not char, and the RGB colour record had no struct of its own. Redo with the order: boxes and names, then relationship lines, then attributes and operations. Exam on Monday 2 November; the user says it starts at 16:30 (to confirm)
Ask lecturers: will the Class Test line (the PM) change; ST2 live build and exception handling marks
```

## 7. RESUME BLOCK
```
PROFILE cs
MODULE CODE CSC01B1
Paste this handoff memo and CSC01B1_StruggleLog_S11_ComplexityAnalysis.md
at the start of the next session.
Run the session-start revision quiz first, from the RETEST FIRST list in the struggle log. Tell me first if the S9, S10 and S11 notes have not been re-read.
First drill next session (cold, blank page, before looking at any note): insert S5 before the first S6 with previous and current (loop `current != nullptr && current->data != "S6"`, then three branches: not found, S6 first, middle or end), then delete a specific node and delete last, in mixed order. On 28 Oct the insert before drill was written in 5 minutes 26 seconds but missed the stop condition and the not-found case; both were then understood and the four-list check was answered correctly.
Plan to exam (Monday 2 November): blank-page retrieval of the linked list operations first; skim doubly linked and circular lists; learn the sorts and searches Big-O table; a timed UML capped at 6 minutes; practise insert BEFORE and search; a timed full past paper on Sunday. Next steps: go over the skipped material, then Q3.5 Big-O drill, a timed UML (6 minute cap), the insert BEFORE and search drill; tomorrow Q4 DLL (dynamic link library) and the Q2.1 template operator; Sunday a timed full paper. The Final summary needs a refresh with the new marks (ask the user first).
```
