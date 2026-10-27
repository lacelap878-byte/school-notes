Supersedes S1 to S10.

## 1. OPEN ITEMS (unresolved, oldest first)
S6 items, carried in full. None were retested in S9 to S11, so all stay open.
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
Member vs friend, left operand not class  | S6         | Chose that 5.0 + m could be a member. A member is called   | 6
                                          |            | on its left operand, so 5.0 + m must be a nonmember.      |
Post-increment return value               | S6         | Thought returning *this fails for speed. The bug is that   | 6
                                          |            | it returns the already-incremented object; return the     |
                                          |            | saved copy (temp).                                         |
[] on a const object                      | S6         | Thought a non-const-only overload compiles because the     | 6
                                          |            | body only reads. The signature decides, so a const        |
                                          |            | overload must exist. (Right but unsure in S9 quiz.)        |
Copy constructor vs assignment trigger    | S6         | Chose a = b (both exist) as the copy constructor case.    | 6
                                          |            | Copy constructor: new object from existing (Clock c = b). |
Default = with a pointer member           | S6         | Thought it does not compile. It compiles and copies the   | 6
                                          |            | address: a leak and a double free.                         |
Scope of template <class Type>            | S6         | Thought it works when Type is int elsewhere. It covers    | 6
                                          |            | only the one declaration beneath it.                       |
Template definitions in a separate .cpp   | S6         | Thought it builds. It fails at LINK time with undefined   | 6
                                          |            | reference (also for function templates).                   |
Class template member defined outside    | S6         | Wrote Type Box::get() const. Needs its own template       | 6
                                          |            | <class Type> line and Box<Type>::. (Missed in S9 quiz.)    |
```

S7 items still open.
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
Recognition vs production                 | S7         | Can pick the right answer in a quiz but cannot write the   | 5
                                          |            | code from a blank page without guidance. Showed again in   |
                                          |            | S9 linked list drills.                                     |
Padding placement and reordering          | S7         | Unsure where padding goes; padding is inserted before a    | 5
                                          |            | member whose alignment the next offset fails, and          |
                                          |            | reordering members changes the total size.                 |
Alignment of a compound member            | S7         | Assumed it equals the member's sizeof; it is the largest   | 5
                                          |            | alignment among its own members.                           |
reinterpret_cast                          | S7         | Unsure what it does; it only relabels the pointer type,    | 5
                                          |            | with no conversion and no check.                           |
DLL syntax and jargon                     | S7         | Macro switch (dllexport/dllimport, -DBUILDING_DLL),        | 5
                                          |            | extern "C" (answered correctly in S9 quiz), .impl.cpp,     |
                                          |            | typedef on a function pointer. Says he does not            |
                                          |            | understand DLLs.                                           |
.open() takes one mode argument           | S7         | Passed several flags as separate arguments; combine with   | 5
                                          |            | | into one.                                                |
ifstream vs fstream                       | S7         | Thought ios::out could make an ifstream writable; write    | 5
                                          |            | ability belongs to the class.                              |
!fail() check                             | S7         | Wrote if (!x.fail()), which reports an error on success.   | 5
Assigning a char array with =             | S7         | Arrays cannot be assigned after declaration; use an        | 5
                                          |            | initializer list.                                          |
.read()/.write() direction                | S7         | Names describe what happens to the file, not the variable. | 5
Header offset in record counting          | S7         | Record count and seek offsets must subtract/add the header | 5
                                          |            | size.                                                      |
seekg vs seekp                            | S7         | Used seekp before a .read(). The read marker (seekg) and   | 5
                                          |            | write marker (seekp) are independent; .read() uses seekg.  |
                                          |            | Answered correctly in the S9 quiz (weakest evidence);      |
                                          |            | "needs grinding". Keep on the retest list once more.       |
```

S9 to S11 items (new).
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
Insert after a node (stop ON; link order)  | S9         | Loop stopped BEFORE the node (peek-ahead pattern) and the  | 1
                                          |            | two link lines were reversed, so the new node points at    |
                                          |            | itself. Stop ON the node, link newNode->next first.        |
Delete a specific node                    | S9         | Could not use temp at first. Later wrote next->next where  | 1
                                          |            | next->data was needed and missed the first-node case.      |
                                          |            | Save in temp, bypass, delete; handle head separately.      |
Delete last, stop position                | S9         | Quiz: answered B, correct is C. The loop is                | 1
                                          |            | while (current->next->next != nullptr), stopping one      |
                                          |            | BEFORE the last node, to unlink it.                        |
Counting skeleton in production           | S9         | Declared current twice, used a peek-ahead loop that never  | 1
                                          |            | moved forward, compared a pointer to a string.             |
Variable name case (NewNode vs newNode)   | S9         | Typed NewNode in one line and newNode in another, twice.   | 1
                                          |            | C++ is case sensitive; copy names exactly.                 |
Missing newNode->next = nullptr           | S9         | Left it out in insert at end.                              | 1
Insert BEFORE and search                  | S9         | Never practised. Both appear in past papers (2025-C Q2.6   | 1
                                          |            | and 2022-B Q2.6).                                          |
Stack vs queue from the rule              | S10        | Over-brought real-world detail (printers) instead of       | 1
                                          |            | answering by LIFO or FIFO.                                 |
Three assumptions                         | S11        | Could not recall the third (N is the problem size); the    | 1
                                          |            | quiz answer was a gut feeling. Not memorised.              |
Nested loop combining                     | S11        | Multiplied a term that should be added. Outer loop         | 1
                                          |            | overhead is added once per outer pass.                     |
```

All items stay open until answered correctly under retest.

## 2. RESOLVED THIS SESSION
```
concept                                   | the correction that fixed it
------------------------------------------|--------------------------------------------------------------
Node struct with head inside              | Wrote Node* head inside the node. head is a separate variable outside the nodes.
                                          | Correct in two later retests.
Delete first                              | Correct under production once and correct in the quiz (Q6).
Delete entire list                        | Correct under production (temp = current; current = current->next; delete temp;
                                          | head = nullptr). Note: the user was right when it was first misread.
Copying addresses and where head lives    | Discussion only (current is like a mailman; a pointer copies an address, not the
                                          | node). Weakest evidence, no retest.
Seek record index (S7) and seekg usage    | Answered correctly in the S9 quiz Q6. Marked resolved with the weakest evidence;
                                          | the user says it still needs grinding.
```
These were checked in the same session as the correction, so they have the weakest evidence.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Linked lists: `->` chains such as `current->next->next` (two hops, current moves one node per pass), and `Node<string> *` (what the <> and the star mean). Slide names (nodeType, info, link, NULL) differ from exam names (Node<T>, data, next, nullptr). Queue names: addQueue, deleteQueue. Doubly linked back pointer is `back`.
DLL jargon from S7 remains unfixed.

## 4. PATTERNS ACROSS SESSIONS
Recognition versus production (S7, S9): quiz answers are mostly fine, but writing from a blank page needs prompts. This is the biggest exam risk, because the exam is written.
Mixing similar patterns (S9): stop ON versus BEFORE, delete-all versus delete-specific.
Assuming two independent things are one shared thing (S5, S6, S7): watch topics with parallel mechanisms.
Over-bringing real-world detail into questions (S10): answer from the rule.
Time management (ST1): the UML wasted 45 minutes. Plan a 6 minute cap, a time budget at the top of the paper, and skip and return.
Small copying slips (S9): variable names and missing lines. Re-read the code once at the end.

## 5. RETEST FIRST (ranked)
Blank paper, timed, in this order.
1. Write the Node<T> struct and these operations from scratch: count, insert at start, insert at end, delete first, delete last.
2. Insert after "X" and delete "X" (stop ON versus stop BEFORE; the link order; temp).
3. Insert BEFORE "X" and search for "X" (never practised).
4. Delete the whole list.
5. Write the three assumptions for Big-O from memory and name N for a given function.
6. Derive T(N) for a nested loop and give the Big-O.
7. Stack versus queue: LIFO and FIFO, which operations on the linked list.
S6 and S7 items:
8. Where template definitions must live and the link error; class template member outside the class; scope of template <class Type>.
9. Member versus friend when the left operand is not the class type; post-increment return value; [] const overload.
10. The dllexport/dllimport macro switch and -D flag; extern "C"; typedef on a function pointer.
11. seekg versus seekp; padding for a struct by hand; .open() with combined flags.
