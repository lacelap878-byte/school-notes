# CSC01B1 Notes S13: Exam Revision (Block 3)

Exam: Monday 2 Nov 2026, 16:30, 2 hours, 100 marks. Newest past papers (2025) matter most. Marks below are my estimates, there is no verified 2025 memo.

## Exam procedure and time budget
| Part | Minutes |
|---|---|
| Q1 multiple choice and short answers | 22 |
| Q2 | 34 |
| Q3 | 34 |
| Q4 | 22 |
| Spare for checking | 8 |
- UML has a cap of 6 minutes. Classes only, as in my practicals; enums and structs appear only as types.
- Do the blank-page questions you know first, come back to the rest. A blank scores 0, so write the template even when unsure.
- Follow the paper's phrasing: `_head` and `_tail`, `Node<T>`, "Provide code for...".
- State the assumptions in Big-O answers and say "Operations counted as one each".

## Multiple choice patterns, 2020 to 2025
Five slots recur: 1.2 vocabulary, 1.3 relationships and principles, 1.4 True/False on new topics, 1.5 keyword, 1.6 terminology or return type.

| Clue in the question | Answer |
|---|---|
| blueprint | class |
| instance | object |
| no functionality (data only) | struct |
| replaced by modules | header files |
| shared code loaded at run time | DLL (Unix: DSO) |
| composition versus aggregation | lifecycle: composition, the part dies with the whole; aggregation, it survives |
| behaves differently by object | polymorphism |
| type T | generics (templates) |
| overloading, overriding, redefinition | overloading: same name, different parameters; overriding: virtual; redefinition: non virtual |
| one copy shared by all objects | static |
| sliced to the base part | slicing (base object assigned from derived) |
| two paths to one base | diamond problem |
- Return types: `[]` that also assigns returns `T&`; `==` returns `bool`; `<<` returns `ostream&`.
- "Most correct" traps: read all options before choosing; two can sound right, pick the one that fits every word of the stem.
- Mirror pairs: papers A, B and C often ask the same idea with swapped words, so an answer learned in one helps in the others.
- Scored 12/12 on the pattern drill; kept for the Monday morning retest.

## Lecturer scope (as reported by the user, no memo)
Examined: explicit linking (function pointer basics only), doubly and circular lists, stacks and queues (linked or array), Big-O counting. Iterators only as a word. Not examined: recursion, sorting and searching. Postfix and simulation unlikely.

## Paper 2025-A results (estimate about 63/100)
| Question | Estimate |
|---|---|
| 1.1 | 2.5/5 |
| 1.2 to 1.6 | 2/5 |
| 1.7 | 2/3 |
| 1.8 to 1.10 | 7/7 |
| 2.1 | 7/10 (blanks e, f, j lost) |
| 2.2, 2.3 | 2/2, 2/3 |
| 2.4 to 2.6 | 5/5, 4/5, 5/5 |
| 3.1 | blank |
| 3.2 | 2/5, right on retry |
| 3.3, 3.4 | blank, then 4/5 and 5/5 |
| 3.5 | about 7/10 |
| 4.1 to 4.3 | 4/5, 4 to 5/5, 7/10 |
The user's target ceiling is about 80%.

## Where each topic lives
- Operators, const, templates: S6 notes (S13 sections).
- Files, flags, explicit linking, modules: S7 notes (S13 sections).
- Exceptions: S8 notes (S13 sections).
- Linked lists: S9 notes (S13 sections).
- Stacks and queues: S10 notes (S13 sections).
- Big-O counting: S11 notes (S13 section).
- What went wrong and the cumulative retest order: the S13 struggle log, `RETEST FIRST` list.

## Short rules to read on Monday morning
- Const: front is what I hand back, brackets is what you gave me, end is the object I am called on.
- `this != &other`; operator= is six steps and ends with `return *this`.
- Copy constructor when the object is being created; assignment when it already exists.
- Text file: `getline` then `istringstream`. Binary file: `char` arrays, `read(reinterpret_cast<char*>(&rec), sizeof(Rec))`.
- Flag for all starts true; flag for at least one starts false.
- Explicit linking: header, typedef, LoadLibrary, GetProcAddress with the name in quotes and a cast, call, FreeLibrary.
- Doubly: set `back` as well as `next`. Circular: never test for nullptr.
- Delete the whole list ends with head and tail set to nullptr.
- Stack in at the front, queue in at the rear, both out at the front.
- T(N) = outside + (header + body) x iterations; check with N = 1, 2, 3.

## See also
- [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]]
- [[CSC01B1_Notes_S7_FileHandling]]
- [[CSC01B1_Notes_S8_ExceptionHandling]]
- [[CSC01B1_Notes_S9_LinkedLists]]
- [[CSC01B1_Notes_S10_StacksAndQueues]]
- [[CSC01B1_Notes_S11_ComplexityAnalysis]]

---
*CDG version not recorded | written S13 | 2026-11-01*
