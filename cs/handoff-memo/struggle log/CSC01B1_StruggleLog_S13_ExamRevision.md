Struggle log for S13, the exam revision (30 Oct to 1 Nov 2026, exam on Monday 2 Nov at 16:30). Per session logs started here: every earlier session has its own log, and this one holds the items first seen during the revision plus the cumulative retest list. Status words: open, resolved (with the evidence). Evidence is compiled or run output where code was involved. Where it was only marking by hand, the entry says the verdict rests on Claude's marking alone.

Sources for this session: the 30 Oct afternoon carry over (quick fire drills, evidence recorded there), the 2025 paper A timed attempt (31 Oct, marked at about 63 of 100, no verified memo, marked by C++ rules and compiling where possible), and the drills of 31 Oct and 1 Nov, including the 1 Nov evening drills (exceptions and the text file template, 18:50 to 19:25). The timed paper 2025-B was postponed by the user to the morning of 2 Nov.

## 1. OPEN ITEMS (unresolved, oldest first)

1. Exceptions: handler order (30 Oct quick fire)
   - Q1 answered B; correct is A: handlers are tried top to bottom, the first match wins, and a base class handler placed before a derived class handler catches the derived exception. Q5 answered "compiles, prints any"; it does NOT compile (`'...' handler must be the last handler for its try block`), confirmed on the user's g++ 15.2.0 (only -fpermissive lets it through). R1 was right on the retest.
   - 1 Nov: the True or False item "catch(...) may come first" was answered correctly in the 12 question drill.
   - 1 Nov evening cold retest (Q1, a base class handler before a derived class handler and `catch (...)`): answered AD, correct. The base class handler is first, so it catches the derived exception and the derived handler is never reached.
   - Status: resolved on this retest (one question, weak evidence).

2. Exceptions: destructor order during unwinding (30 Oct quick fire)
   - Q4 answered ckd; correct is cdk: locals are destroyed before the handler runs. Retest R2 answered "c c k"; correct is c1 c2 d2 d1 k (destructors run in reverse order BEFORE the handler).
   - 1 Nov evening, three drills with the same struct K (constructor prints c plus the name, destructor prints d plus the name). Drill 1 (a1 and b2, then throw, then catch): answered `cdcdx`; correct `c1c2d2d1X`. The names were left out and each object was destroyed right after it was created. Drill 2 (x, an inner block with y, then z, then throw): answered `ABCZ`; correct `cAcBdBcCdCdAZ`. The c and d events were left out. Drill 3 (m in main, then P, Q, an inner block R, then throw): answered `SccPcQcrDrdPdQZSD`; correct `cScPcQcRdRdQdPZdS`. All nine events were found and the end of h() was nearly right; the slips were the letters written name first and `dP` written before `dQ`. What helped: writing a list of what is alive with one event per line, and the stack of plates image.
   - Status: open but improving (wrong order of two destructors in the last drill).

3. File handling: seekp overwrite and the eof loop (30 Oct quick fire)
   - ios::app adds to the end (taught after "don't know"). seekg is the read position and seekp the write position, and a write overwrites: R1 answered ABCDEF, correct A then AZZDEF. `while (!in.eof())` repeats the last value (1, 2, 3, 3); R3 answered "don't know", fix `while (in >> x)`. ios::app versus the default was not retested.
   - Status: open. (Padding, R2 right, and Q1, a plain ofstream wipes the file, were right.)

4. Delete a, b, c, d, e, f on the list 4, 9, 7 (carry over question)
   - The worked example of the delete cases was given (empty, first node, somewhere with current and previous, last so `last` moves back, not found; a one node delete must set last to nullptr). The question about first, last and count after each delete was posed and not answered. On 31 Oct the user chose the blank page delete drill instead.
   - Status: open. See the S9 log, item 1, for the delete function itself.

5. Text file reading with lines of different lengths (2025-A 3.1)
   - Left blank in the timed paper. 1 Nov cold rerun: opening lines and the declarations were right (`ifstream`, fail check, `string strDay; int intHour; int intMinute; char chTap;`); it stopped at `while (getline(is,`. The user found `istringstream` confusing and had not used `get` before (checked: no `.get(` in any practical; the practicals read text with `>>` and use `getline` only to discard a header line). The user then said to skip it.
   - The template that stays (compiled): `getline(file, strLine)` in a while loop, `istringstream objLine(strLine);`, `objLine >> strDay >> intHour >> intMinute;`, a flag, `while (objLine >> chTap)`, print if the flag is set. Two other versions were compiled and offered: `>>` for the first three values then `getline(is, strTaps)` for the rest of the line, and `>>` with a loop of 1032 taps. Papers 2025-B and 2025-C have a 3.1 of the same kind.
   - 1 Nov evening (19:11 and 19:24), two cold reruns with new questions (rain.txt: print the cities whose total is above 50; scores.txt: print the names whose average is 60 or more). First attempt: `istream is("rain.txt", ios::in)` (should be `ifstream`), `getline(is, intRain)` (getline fills a string), no `istringstream`, `sum` not set to 0 and the test outside the loop. Second attempt (after the template was mapped onto his own lines and `iss` was explained as only a variable name): ifstream, fail check, getline, `istringstream iss`, `iss >> Name`, the inner `while (iss >> mark)`, the average and the test inside the outer loop, all in place. Slips: `total` declared once above the loop and never reset; the line variable declared as `strLine` but read as `Line`; `istringstream iss;` appears to lack `(strLine)` (as far as the handwriting can be read); the average was printed although only the name was asked; `>` or `>=` for "60 or more" not clear on the page. Marking is by hand only (not compiled). Estimated 4 of 5.
   - Status: open, much improved. One more cold run tomorrow morning.

6. Flags for "all" and "at least one"
   - Confusion between 3.1 (at least one `?`: flag starts false) and 3.3 (all taps are `?`: flag starts true, a tap that is not `?` makes it false). The user's own wording: "proof by contradiction", then "we check if it is clear but we start out assuming the water is clear" (a flag meaning "all clear"), which answers the opposite question. Recipe given: "all" starts true and one counterexample sets false; "at least one" starts false and one example sets true; the start value is the answer for an empty list.
   - 3.3 attempt: `bool unclear = true;`, `if (Tap[i] != '?') unclear = false;`, print if `unclear`: the logic was right and the flag sat inside the record loop. Mini drill: both start values right; "not positive" was written `< 0`, the reverse of "above 0" is `<= 0`.
   - Status: resolved for the logic (3.3 production, 1 Nov). Open for the boundary slip `<` versus `<=`.

7. 2025-A 3.3 and 3.4 slips (binary records)
   - 3.4 (countRecords): full marks (seekg, tellg, divide by sizeof(WaterCheck); compiled with names made consistent: 4 records counted). It was labelled 3.3 on the page. 3.3: 4 of 5; compiled logic printed the right records. Slips: a bare `Tap[i]` for `rec.Tap[i]`, `rec.day` for `rec.Day`, no function header, an inner loop reusing `i` (g++ -Wshadow warning), a variable named `istream`.
   - 3.2: first answer had `string strDay`, `char Tap[2][1032]` and an unnamed struct; second answer correct (`char Day[10]`, `char Tap[1032]`, named WaterCheck, packed). The user's reason for the 2 dimensions was reading T as a character; T0 to TN is "the status of tap 0 to N", one char per tap, the index is the tap number. A 4 byte day (3 letters) would break the layout when the file holds full day names (compiled: the second record read as garbage).
   - Status: 3.2 and 3.4 resolved (production). 3.3 open for the case and naming slips (S9 item 3).

8. What head is
   - See the S11 log, item 3. First raised in S13 as "head can be two things at once". The user's reading: `_head->back` treats head as the first node, `_head = newNode` treats it as independent. Agreed model: a label on a box.
   - Status: open (not retested).

9. Doubly linked list: insert at the front, insert at the back (own attempt, 31 Oct)
   - Front: `newNode->next = head->next; head->next = newNode;` inserts AFTER the head. Correct: `newNode->next = head; newNode->back = nullptr; head->back = newNode; head = newNode;`. Back: the loop `while (current != nullptr)` then `current = current->back` dereferences nullptr (crash); `current->next = new Node;` made a second node instead of using newNode; `newNode->back = current;` missing. Corrected versions of all four list functions compiled and ran (1 2 3 4 forwards, 4 3 2 1 backwards).
   - 2025-B 2.5 (insert "N0" at the start): the user's four lines were right for a non empty list but `_head->back = newNode;` and `newNode->back = nullptr;` were missing (run: the backward walk lost N0). 2.4 (templated node with next and back) was correct. The empty list case is a safeguard, not a requirement, for the list as drawn (user's point, accepted).
   - Status: open. The rule: every time a next changes, ask which other pointer must change too (back in a doubly list, the last node in a circular one).

10. Circular linked list (own attempt 31 Oct and 2025-C 2.5)
    - Front insert: `newNode->next = head; head = newNode;` leaves the last node pointing at the old head, so the circle never returns to the new node (a loop waiting for current == head never ends). Fix: find the last node with `while (current->next != head)`, set `current->next = newNode`. Back insert: the do while and `current->next != head` were right, but the empty case was not separated with an else.
    - 2025-C 2.5 (count "S6"): `while (current != nullptr)` never ends in a circular list (run: still looping after a million steps, count 166,666). Fix: do { ... } while (current != _head). 2.6 (insert "S5" before the first "S6", peek ahead) correct (run: S1 S2 S3 S4 S5 S5 S6).
    - Status: open for the end test (the end of a circular list is `current->next == _head`, never nullptr).

11. Explicit linking, 2025-B 4.1
    - First attempt (stopped at `HINSTANCE : LoadLibrary("route-generator.dll");`): `typedef char* (Name)(int);` lacked the star, so Name was a function type, not a function pointer (should be `(*Name)`); the handle had no variable name. Completion: `"genRoute"` was written without quotes (the name is a string); the call `f(10)` was right. The user's objection: function pointers were never taught and he expected only a batch file. Lecturer, as reported 30 Oct: explicit linking is examined, function pointers only at a basic level. Slide: L6 slide 50. Explicit linking needs no special batch command (the file may be compiled normally).
    - Template kept: the 7 parts (header, typedef, handle, load, get address and cast, call, unload) with blanks for the typedef, the DLL file name, the function name string and the call. The names: the typedef is the shape for the compiler; the string is the name for Windows. Compiled only against stand-in Windows declarations (not run on Windows).
    - Status: open for one more cold run.

12. 2025-A Q1.1 UML
    - Relationships correct (aggregation, inheritance, composition) and the style matches the practicals (classes only; an enum or struct appears only as a type). Missing: deliverPrograms and suspendPrograms (bool) on UniversityNetwork and AcademicUnit (overridden in ResearchCenter), getters and the setter, add, update and remove unit, constructors with parameters; the grant capacity is a double (written int) and its setter returns void (written int); EducationDepartment needs deliver; use the paper's class names. Estimated 2.5 of 5.
    - Status: open. The cold rerun was not done (6 minute cap).

13. 2025-A Q2.1 blanks (e), (f), (j)
    - Wrong twice: (e) `[]` for `=`, (f) `UJList<T>&` for `T&`, (j) `int` then `<T>` for `T`. Retest on a new class (Box) 1 Nov: `=`, `T&`, `T`, all right. The rule: the operator with an `int` index is `[]` and returns the element type by reference; the operator with a same class parameter is `=`.
    - Status: open until checked again tomorrow (the retest came right after the correction).

14. 2025-A Q3.5 Big-O (own attempt, 31 Oct)
    - Assumptions right. Derivation: outside 6 (right), inside 4n + 4n = 8n, T(N) = 8n + 6, then T(2) = 20 and T(3) = 26 (those are the values of 6n + 8; from 8n + 6 they are 22 and 30), O(N) correct. The second array access `[]` in `temp[i] = _data[i]` was missed (so 4 per iteration instead of 5 or 6), the breakdown was not shown, and the counting of new, delete and the two function calls was not stated. With the lecturer's counting (header counts `=`, `<`, `++`, body `=` and two `[]`): T(N) = 12N + 6, T(1) = 18, T(2) = 30, T(3) = 42. Estimated 7 of 10.
    - Status: open. See the S11 notes for the counting rule.

15. Stack and queue: queueRear
    - Asked whether queueRear means a doubly linked list. It is a second pointer held by the queue to the last node (lecture slide 91), not a back pointer inside the nodes. Asked whether pop and deleteQueue are the same operation: on a linked list both remove the first node; the queue also fixes queueRear when it becomes empty; the real difference is where data is ADDED (stack at the front, queue at the end).
    - Status: resolved (discussion, weak evidence).

16. Local objects follow a stack, not a queue (1 Nov evening)
   - After the destructor drill the user asked why `dP` before `dQ` is wrong, because he thought "FIFO is the way this works". Local objects live on the call stack and are removed newest first (LIFO). Explained with socks and shoes and with the plates image; he then asked whether that is why the memory is called a stack, and it was confirmed (the function that was called last finishes first, and `new` memory is the heap, which is not a stack). A table was given: queue (first in first out, a shop line, deleteQueue) against stack (last in first out, push and pop, destructors, function calls).
   - Status: resolved by discussion (weak evidence). Retested through item 2.

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
2025 multiple choice slots                | Paper A 1.2, 1.3 and 1.5 were wrong (D, E, E expected: header files,
                                          | generics, const rather than constexpr). The pattern drill of 12
                                          | lecturer style questions on 1 Nov: 12 of 12 (weak: built from the
                                          | same patterns). The decision table is in the S13 notes.
2025-A 2.3 protect with try and catch     | First attempt: array declaration objList[10000] and a throw in the
                                          | try. Rerun: declaration objList(10000), no throw (the throw is in
                                          | operator[]), catch by reference. Resolved. Small things to check:
                                          | lower case float and catch, return 1 in main, print e.what().
2025-A 2.5 delete the first node          | See the S9 log (resolved).
Q4 batch files (2025-C 4.2, 2025-B 4.3)   | See the S12 log (resolved except -fmodules-ts).
Member vs friend                          | See the S6 log (4 of 4).
Template stack on an array                | Asked whether a class template must overload an operator (no; only
                                          | the operations the member functions use on T, here assignment) and
                                          | whether out of class members still need the template line (yes).
                                          | Compiled a templated array stack with string and double.
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
- Const positions: front (the returned value, matters only when the return type has &), brackets (the right operand), end (the left object).
- Names that look alike in the DLL answers: the module name, the interface file name, the DLL file name, and the `-l` name (the DLL name without .dll).
- `Node<string>` with a lower case `string`; a capital in `Float`, `String`, `Catch` or `Rec` on the page would not compile.
- The paper's pointer names are `_head` and `_tail` (a leading underscore).

## 4. PATTERNS ACROSS SESSIONS
Recognition versus production (S7, S9, S12, S13): the answers are mostly fine once a shape or a skeleton is given. A shape to copy works better than an explanation (explicit linking, the text file template, the flag recipe, the stack and queue snippets).
Small slips, not concepts (S9, S11, S12, S13): a missing `[]`, a missing `&`, the case of a letter, `<` for `<=`, one missing back pointer, one missing flag. They are caught by re reading an answer once against a checklist.
The user's learning preferences, stated in S13: a worked example before any question; complete programs for new code, but snippets only for the exam style answers and no whole file when he asked for none; previous and current for lists; the time limit stated for every drill; short rules and decision trees over long explanations; planning and revision in separate chats. When a topic is solid he does not want it repeated.

## 5. RETEST FIRST (ranked, cumulative; the home log of each item is in brackets)
Blank paper, timed, in this order. Paper B and C versions of 3.1 reuse the same template.
1. The 3.1 text file template from a blank page (S7 item 2; S13 item 5). Evening 1 Nov: structure right, four slips; one more cold run.
2. Doubly linked list: insert at the front and the back, and delete the whole list ending with `_head = nullptr; _tail = nullptr;` (S13 items 9; S9 item 5).
3. Circular list: front insert (find the last node), back insert with an else, count with a do while (S13 item 10).
4. Delete a specific node with previous and current (S9 item 1); insert BEFORE and search (S9 item 4).
5. operator= with `this != &other`; post-increment; the `[]` const pair; copy constructor against assignment (S6 items 1 to 3, 4).
6. Explicit linking cold: `typedef char* (*Name)(int);`, `"genRoute"` in quotes, a named handle (S13 item 11).
7. Module interface and implementation files, `-fmodules-ts` on every compile line, and the 2025-C 4.3 main.cpp with the random array (S12 items 2 to 4).
8. Exceptions: destructor order during unwinding, newest first (S13 items 2 and 16). Handler order came right on the 1 Nov evening retest.
9. seekp overwrite and `while (in >> x)` (S13 item 3).
10. Q3.5 Big-O cold with the three assumptions, the counting rule stated, substitution computed from the formula (S13 item 14).
11. The UML 1.1 operations with a 6 minute cap (S13 item 12); the Q2.1 blanks (e), (f), (j) (S13 item 13).
12. Template items from S6 (scope, link error, out of class member) and the 3.3 naming and case slips (S6 items 5 to 7; S13 item 7).

---
*CDG v11 | written S13 | 2026-11-01*
