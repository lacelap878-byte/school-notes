Supersedes S1 to S10. This is the only handoff file needed.

## 1. OBJECTIVE (this session)
Cover the last three exam topics in the semester: linked lists (Lecture 8), stacks and queues (Lecture 9) and complexity analysis, in drill format, for the CSC01B1 exam on Monday 2 November 2026 (2 hour written theory paper). The session also covered the ST2 mark query and the PM/Class Test question for the lecturers.

Exam context: semester mark 51 (tentative), so a pass needs about 49% in the exam. ST2 is 49 (unmoderated, capped for "no compile") and is being queried in person. Class Test 100 is very likely the PM. VPL in session practicals 1, 2, 3, 4 and 6 read 0 (compilation failed in the auto marker) and are being remarked. Goal: a 65% final for cum laude (needs about 79% in the exam).

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
S9 | Linked lists, Lecture 8 (node, head, traversal, insert start/end/after, delete first/last/specific/whole list; exam style Node<T>) | partial (slides 29 to 88 not taught: list class, iterators, ordered/unordered lists, doubly linked, circular) | open struggle yes
S10 | Stacks and queues, Lecture 9 (LIFO, FIFO, operations, linked stack and queue as list code) | partial (array stacks and queues, postfix, print backward, simulation not taught) | open struggle yes
S11 | Complexity analysis (three assumptions, counting T(N), Big-O, results table for sorts and searches) | partial (counting taught; sorting and searching slides 22 to 41 not taught) | open struggle yes
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
Memo written after the session-end check quiz. The Summary (Revise style) has been requested and is next. No timed UML drill has been run yet. The user stopped for the night.

## 6. PARKED ITEMS
```
Practice insert BEFORE a value and search in a list (both in past papers, never practised)
Doubly linked and circular lists: skim slides 74 to 88 (only in 2018 and 2019 papers)
Sorting and searching slides 22 to 41: the Big-O table only is needed
Several L8 code slides (42 to 44, 48 to 50, 54 to 55) did not read cleanly; code not captured
Big-O definition slides (complexity slides 6 to 9) not captured; re-read from the PDF
Timed UML drill, 6 minute cap (the ST1 UML cost 45 minutes)
Ask lecturers: will the Class Test line (the PM) change; ST2 live build and exception handling marks
```

## 7. RESUME BLOCK
```
PROFILE cs
MODULE CODE CSC01B1
Paste this handoff memo and CSC01B1_StruggleLog_S11_ComplexityAnalysis.md
at the start of the next session.
Run the session-start revision quiz first, from the RETEST FIRST list in the struggle log. Tell me first if the S9, S10 and S11 notes have not been re-read.
Plan to exam (Monday 2 November): blank-page retrieval of the linked list operations first; skim doubly linked and circular lists; learn the sorts and searches Big-O table; a timed UML capped at 6 minutes; practise insert BEFORE and search; a timed full past paper on Sunday. Next step in this chat: the Summary (Revise style) of S1 to S11.
```
