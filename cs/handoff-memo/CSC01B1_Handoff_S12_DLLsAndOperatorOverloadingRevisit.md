Supersedes S1 to S11. This is the only handoff file needed.

## 1. OBJECTIVE (this session)
Teach from the beginning the two things the user said were blank or new: DLLs (how to write and link them, module style only) and operator overloading in general (for Q2.1), with drills on paper, marking, a cold recall and a timed Q4, a 9 question end check quiz, then amend the affected notes and update the protocol to v11. Exam context is unchanged from S11: Monday 2 November 2026, 2 hour written theory paper, user says it starts at 16:30 (to confirm). Semester mark about 65.5 (10% PM, 25% ST1 at 35, 65% ST2 at 72); about 64.5% in the exam gives a 65% final. The PM line and the in-session practical remark are still pending.

The user's own assessment of the session (his words, 29 October): the quality was low, especially from him, he did not understand much of what was being taught, the session will likely need to be redone in future, and he hopes to hold on to it as he did with linked lists, even if partly.

## 2. TOPIC LEDGER
```
S1 | Foundation Topics (binary and number systems, bitwise ops, signed numbers, memory model, pointers, arrays, function pointers, structs, intro to classes) | full | open struggle no
S2 | C++20 Modules (module concept, first module, export blocks, prototypes vs implementation) | full | open struggle no
S3 | Classes and Data Abstraction (class syntax, UML, objects, scope, constructors/destructors, ADTs, struct vs class, information hiding, static members) | full | open struggle no
S4 | Object Composition and Inheritance (OOD, UML, association, composition, inheritance syntax, overriding, derived-class constructors/destructors, protected members, stream hierarchy) | full | open struggle no
S5 | Polymorphism (virtual functions, late binding, pure virtual and abstract classes, slicing, virtual destructors, casting, vtable) | full | open struggle no
S6 | Operator overloading (fundamentals, this pointer, friend functions, binary/stream/assignment/unary/increment/subscript overloads) and templates (function and class, header layout) | full | open struggle yes (8 items, quiz 0 of 8) | amended S12
S7 | File handling (secondary storage and streams, sequential file I/O, opening modes and flags, output formatting, random access, raw disk I/O, padding and #pragma pack, DLLs with implicit and explicit linking) | full | open struggle yes | amended S12 (module style DLLs added, header style marked not examined)
S8 | Exception handling (exception, assert, try/catch/throw, catch order, exception classes and what(), user-defined exception classes, rethrowing, throw clause, handling techniques, stack unwinding) | full | open struggle no (S6 and S7 items stay open)
S9 | Linked lists, Lecture 8 (node, head, traversal, insert start/end/after, delete first/last/specific/whole list; exam style Node<T>) | full for the drilled part; amended 28 Oct (all slides read and written as presented, N.B. low frequency on slides 23 to 40 and 62 to 92) | open struggle yes | amended
S10 | Stacks and queues, Lecture 9 (LIFO, FIFO, operations, linked stack and queue as list code) | full for the drilled part; amended 28 Oct (all 108 slides written as presented, N.B. low frequency on array versions, postfix, print backward, simulation) | open struggle yes | amended
S11 | Complexity analysis (three assumptions, counting T(N), Big-O, results table for sorts and searches) | full for the counting method; amended 28 Oct (Big-O definition, recursion, every sort and search with slide code, N.B. low frequency) | open struggle yes | amended
S12 | Revisit session, no new notes file: DLLs in module style (interface and implementation files, batch commands for creating a DLL and for implicit linking, 2025 Q4 A, B, C), operator overloading for Q2.1 (left operand rule, this, const positions, friend in class template, default =); taught into S6 and S7 as amendments | full for the module style DLL and the Q2.1 operator patterns; explicit linking on hold | open struggle yes | amended S6 and S7
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
      Lecture 5 retelling: operator overloading, then function and class templates. Amended S12: left operand rule, this, three const positions, friend in class template, Q2.1 blanks table, = and >> rows
S7  | File handling | CSC01B1_Notes_S7_FileHandling.md |
      Lecture 6 retelling: streams, sequential and random access files, raw bytes, padding, DLLs. Amended S12: module style DLL files, batch commands, 2025 Q4 model answers, explicit linking on hold
S8  | Exception handling | CSC01B1_Notes_S8_ExceptionHandling.md |
      Lecture 7 retelling: try/catch/throw, catch order, exception classes, rethrowing, handling techniques, stack unwinding
S9  | Linked lists | CSC01B1_Notes_S9_LinkedLists.md |
      Lecture 8: node, traversal, insertion, deletion, loop stop table, exam frequency table
S10 | Stacks and queues | CSC01B1_Notes_S10_StacksAndQueues.md |
      Lecture 9: stack, queue, linked versions, lecture operation names
S11 | Complexity analysis | CSC01B1_Notes_S11_ComplexityAnalysis.md |
      Three assumptions, counting method, worked example, Big-O results table
S12 has no file of its own: its content is in the S6 and S7 amendments above.
```
Project also holds CSC01B1-2026-L8.pdf (listed twice) and CSC01B1-2026-L9.pdf, the lecture PDFs L1 to L7, and ObjectAssociationHasA.pdf.

## 4. CONTENT SUMMARY
S12 (this session), taught in small steps with the user writing on paper and photographing.
- Lecturer scope (user reported, 29 October): the exam uses module style DLLs only (module interface files as in the 2025 papers); header files for DLLs are not tested. The user says function pointers were in the course material but were not taught, that he added them to his own notes for extra information, and that to his knowledge they are not examined in any form. He sent an email to the lecturer (addressed to Mr Tamala, copying Mr Ogwok, the course coordinator who is travelling, and the other lecturers) to confirm. Topics in it: function pointers and explicit linking, doubly linked and circular lists and iterators, sorts and searches. The UML question was removed because polymorphism teaching never raised it. No reply yet. If no reply by Saturday: teach the typedef explicit linking pattern as a fixed template.
- DLLs, module style: interface file `export module Name;` with `extern "C" { export ... }`; implementation file `module Name;` with the same `extern "C"` braces and the body; program uses `import Name;`. Omitting `export` makes the function invisible to importers. Omitting extern "C" from the implementation gives a g++ error. Module name, interface file name and DLL file name are three separate names.
- Batch commands (compiled with a MinGW 13.2 cross compiler, not run on Windows): create a DLL = compile interface with `-c`, compile implementation with `-c`, then `g++ -shared -o NAME.dll X.o Y.o`; link a program implicitly = compile interface, compile main.cpp, then `g++ -o prog.exe -L. -lname X.o main.o` where the `-l` name is the DLL file name without `.dll`. All flags need their leading hyphen. `-shared` appears only in the DLL creation command.
- 2025 Q4 mapping: A (4.1 interface LibFilter, 4.2 implementation, 4.3 implicit batch with util.dll), B (4.1 explicit main.cpp with route-generator.dll, on hold; 4.3 batch that creates the DLL), C (4.1 interface CalcLibrary, 4.2 implicit batch with em-calculator.dll, 4.3 main.cpp with a dynamic array of 10 random reals in 0 to 100). Model answers are in the S7 amendments.
- Operator overloading for Q2.1: member versus friend is decided by the LEFT operand; `()`, `[]`, `->`, `=` are always members; `this` exists only in members and points to the left operand; a friend takes both operands. Three const positions (front = returned value, brackets = right operand, trailing = left object; assignment has no trailing const). Default `=` always compiles but copies the pointer address (leak, double free). Friend `<<` and `>>` inside a class template need their own `template <typename E>` and must use `UJList<E>` (compiled and run). Q2.1 blank patterns are in the S6 amendments.
- Other: LeetCode advice given (when to start, whether to do it) and an email draft to the lecturers.
- Drills this session: operator overloading Parts 1 and 2 with photos, 2023-B Q2.1 answers, cold recall and a timed Q4 (2025-A Q4.3 attempt, 8 minutes 12 seconds left, several errors; 2025-B Q4.3 attempt, stopped early on the batch file), 2025-C Q4 attempts (3 photos) after the lunch break. Session end check quiz: 9 questions, 2 wrong (Q5 trailing const, Q6 default `=`); the user says none of the other 7 were guessed.
- Notes amended in place on 29 October: S6 and S7 (see Amendments sections in each file). S1, S9, S10, S11 not changed. The Final summary is stale for the S7 DLL section and for the old marks.
- Protocol updated to CDG v11 on 29 October (R10 to R13, rules for every state, STATE A item 6, footer, PROTOCOL VERSIONS and FRICTION LOG sections in this memo).

S1 to S11 are one line each in the ledger.

## 5. LAST POSITION
End of S12 on 29 October, about 17:15 (after the quiz and the note amendments). No timed Q3.5 Big-O, no timed UML re-run and no insert BEFORE and search drill has been done since S11. The Memo is the last step of the session.

## 6. PARKED ITEMS
```
Lecturer reply pending: function pointers and explicit linking examined or not; doubly linked and circular lists and iterators; sorts and searches. If no answer by Saturday 31 October, teach the typedef explicit linking pattern as a fixed template (S7 amendments, Explicit linking, the exam pattern).
Practice insert BEFORE a value and search in a list (both in past papers, never practised)
Doubly linked and circular lists: skim slides 74 to 88 (only in 2018 and 2019 papers), waiting on the lecturer reply
Sorting and searching slides 22 to 41: the Big-O table only is needed
Still to GO OVER in study mode (all low frequency): L8 slides 62 to 72, complexity slides 6 to 9 and 18 to 20, L9 postfix and print backward, then L8 29 to 40 and 74 to 88, then L9 array stacks and queues and the sorts and searches.
Timed UML drill, 6 minute cap (the ST1 UML cost 45 minutes). First run 28 Oct (2022-C Q1.1): not finished at 6 minutes; the Musician relationship, the starting note type, and the colour record struct were missed. Redo with the order: boxes and names, then relationship lines, then attributes and operations.
Ask lecturers: will the Class Test line (the PM) change; ST2 live build and exception handling marks
Final summary refresh: stale (S7 DLL section and old marks). Ask the user before rebuilding.
```

## 7. RESUME BLOCK
```
PROFILE cs
MODULE CODE CSC01B1
Paste this handoff memo, CSC01B1_StruggleLog_S12_DLLsAndOperatorOverloadingRevisit.md and CDG.md (v11) at the start of the next session.
Read CDG.md from context first (R10) and name the version. Ask whether any tuts, assignments, past papers or lecturer replies have arrived, and say that scope may have changed.
Run the session-start revision quiz first, from the RETEST FIRST list in the struggle log. Tell me first if the S6 and S7 amendments have not been re-read.
First drill next session (cold, blank page, before looking at any note): 2025-C Q4.2 and Q4.3 (implicit batch file with `-L.` and `-lem-calculator`, and main.cpp with a dynamic array of 10 random reals), then the Q2.1 blanks for a class template (`template`, `typename`, `<T>` on the copy constructor, `=`, `T&`, `friend`, `<<`, `>>`, `E`), then insert before a value and delete a specific node.
Plan to exam (Monday 2 November): Friday template and Q2.1 patterns, exceptions, Q3 file handling; Saturday Q1 theory and a timed 2025-A paper; Sunday timed 2025-B and 2025-C; a timed UML capped at 6 minutes; insert BEFORE and search; Big-O drill. Lecturer reply may change the plan for explicit linking, doubly and circular lists and sorts. The Final summary needs a refresh with the new marks and the S7 amendments (ask the user first).
```

## 8. PROTOCOL VERSIONS
```
file                                              | written with            | amended with
--------------------------------------------------|-------------------------|-----------------------------------
Notes S1 to S5, S8                                | version not recorded    | none
Notes S6                                          | version not recorded    | S12 (v10)
Notes S7                                          | version not recorded    | S12 (v10)
Notes S9, S10, S11                                | version not recorded    | S11 on 28 Oct (version not recorded)
Handoff S11 and StruggleLog S11 (superseded)      | version not recorded    | none
Handoff S12 and StruggleLog S12 (this pair)       | v11 (S12)               | none
```
S6 and S7 were amended under v10 on 29 October, before v11 was written the same afternoon. Their footers say so. Files written before v11 carry no footer except S6 and S7, which now have one.

## 9. FRICTION LOG
```
S12 | function pointers | Saw them in the Foundation Topics slides and the S1 notes and took that as proof they had been taught, so flagged the user's email as wrong | He had added them to his own notes as extra reading; the lecturers had not taught them; the email was only a confirmation | He explained; S7 reworded; v11 R11 added (ask before concluding on a scope conflict)
S12 | pace on explicit linking | Put explicit linking and the function pointer typedef into one step | "Too much too quickly", he had not done function pointers | Paused that part, smaller steps, held explicit linking until the lecturer replies
S12 | header versus module DLLs | Taught from the slides, which are header style | The lecturer told the class the exam uses module files only | He reported the lecturer's statement; S7 amended module first, header style marked not examined
S12 | name mangling | Used the word without having seen it in the course | "We weren't told anything about mangling", he worked from gut instinct | Explained with compile evidence (_Z3addii versus add), tied to extern "C" in both files
S12 | this versus the right operand | Said the member takes one parameter and `this` is the left operand | He asked why the right operand is not needed since this points to it | Re-explained that this is the LEFT operand; the parameter is the right one
S12 | const positions | Taught three positions | He compressed them to two ("right const means left object not modified, left const means right side not modified"), partly reversed | Wrote the three position table into S6; the trailing const protects the left object
S12 | session pace and quality | Packed several new ideas in one session after a blank start | He said he was rushed, did not understand, and the session would need redoing | Smaller steps, a single idea per message, retest in the morning
```
Fold the repeated patterns into the protocol when this log passes about 15 entries (7 now).

---
*CDG v11 | written S12 | 2026-10-29*
