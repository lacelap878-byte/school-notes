Supersedes S1 to S7.

## 1. OPEN ITEMS (unresolved, oldest first)
S6 items, carried in full. All came from the S6 session-end quiz (0 of 8 correct) and were not retested in S7 or S8, so all stay open.
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
Member vs friend, left operand not class  | S6         | Chose that 5.0 + m could be a member. A member is called   | 3
                                          |            | on its left operand, so 5.0 + m must be a nonmember.      |
Post-increment return value               | S6         | Thought returning *this fails for speed. The bug is that   | 3
                                          |            | it returns the already-incremented object; return the     |
                                          |            | saved copy (temp).                                         |
[] on a const object                      | S6         | Thought a non-const-only overload compiles because the     | 3
                                          |            | body only reads. The signature decides, so a const        |
                                          |            | overload must exist.                                       |
Copy constructor vs assignment trigger    | S6         | Chose a = b (both exist) as the copy constructor case.    | 3
                                          |            | Copy constructor: new object from existing (Clock c = b). |
Default = with a pointer member           | S6         | Thought it does not compile. It compiles and copies the   | 3
                                          |            | address: a leak and a double free.                         |
Scope of template <class Type>            | S6         | Thought it works when Type is int elsewhere. It covers    | 3
                                          |            | only the one declaration beneath it.                       |
Template definitions in a separate .cpp   | S6         | Thought it builds. It fails at LINK time with undefined   | 3
                                          |            | reference (also for function templates).                   |
Class template member defined outside    | S6         | Wrote Type Box::get() const. Needs its own template       | 3
                                          |            | <class Type> line and Box<Type>::.                         |
```

S7 items, carried in full. None were retested in S8, so all stay open.
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
seekg vs seekp                            | S7         | Used seekp before a .read(). The read marker (seekg) and   | 2
                                          |            | write marker (seekp) are independent; .read() uses seekg.  |
Recognition vs production                 | S7         | Can pick the right answer in a quiz but could not write    | 2
                                          |            | the code from scratch without guidance.                    |
Padding placement and reordering          | S7         | Unsure where padding goes; padding is inserted before a    | 2
                                          |            | member whose alignment the next offset fails, and          |
                                          |            | reordering members changes the total size.                 |
Alignment of a compound member            | S7         | Assumed it equals the member's sizeof; it is the largest   | 2
                                          |            | alignment among its own members.                           |
reinterpret_cast                          | S7         | Unsure what it does; it only relabels the pointer type,    | 2
                                          |            | with no conversion and no check.                           |
DLL syntax and jargon                     | S7         | Macro switch (dllexport/dllimport), extern "C", .impl.cpp  | 2
                                          |            | naming, typedef on a function pointer, -D flag.            |
.open() takes one mode argument           | S7         | Passed several flags as separate arguments; combine with   | 2
                                          |            | | into one.                                                |
ifstream vs fstream                       | S7         | Thought ios::out could make an ifstream writable; write    | 2
                                          |            | ability belongs to the class.                              |
!fail() check                             | S7         | Wrote if (!x.fail()), which reports an error on success.   | 2
Assigning a char array with =             | S7         | Arrays cannot be assigned after declaration; use an        | 2
                                          |            | initializer list.                                          |
seekg call form and seek vs read          | S7         | Called seekg without a stream object and expected it to    | 2
                                          |            | return the data; seeking only moves the marker.            |
Off-by-one record index                   | S7         | "2nd record" is index 1.                                   | 2
.read()/.write() direction                | S7         | Names describe what happens to the file, not the variable. | 2
Header offset in record counting          | S7         | Record count and seek offsets must subtract/add the header | 2
                                          |            | size.                                                      |
```

S8 items: none open. Two gaps surfaced in discussion and were checked by later quiz questions, see section 2. Two open items are marked there as worth one more check.

All items stay open until answered correctly under retest.

## 2. RESOLVED THIS SESSION
```
concept                                   | the correction that fixed it
------------------------------------------|--------------------------------------------------------------
What stack unwinding skips                | Traced a() calling b() calling c() and had the rest of a skipped. Only the rest of
                                          | a's try block is skipped. a's catch runs, then a continues after the try/catch and
                                          | returns normally. Functions with no handler (b, c) are abandoned entirely.
                                          | Checked by quiz Q1 and Q8 (both reported correct).
"There has to be a catch block"           | Nothing forces a handler to exist. The exception leaves each function in turn;
                                          | if no matching catch is found, terminate ends the program. A matching type is
                                          | also not automatic. Checked by quiz Q5 (reported correct).
Where what() belongs                      | Asked whether what() belongs to stdexcept. It belongs to class exception;
                                          | stdexcept only defines the subclasses, which inherit it. A user-defined class
                                          | has what() only if written. Checked by quiz Q3 (reported correct).
```
These were checked in the same session as the correction, so they have the weakest evidence. They are in the retest list as a single mixed question.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Jargon in the DLL material (dllexport, dllimport, __stdcall, extern "C", HINSTANCE, .impl.cpp, -D, -Wl,--out-implib) caused the most trouble in S7. Concepts were fine, keywords were not.
S8: "stack unwinding" as a term. The behaviour was understood from the trace, the name was the unfamiliar part.

## 4. PATTERNS ACROSS SESSIONS
Assuming two independent things are one shared thing: S5 (inheritance subobjects), S6 (= and copy constructor, template scope; still open), S7 (seekg and seekp). Watch any topic with parallel but independent mechanisms.

Recognition versus production (S7, still open): quiz answers were fine, but writing code from a blank page required six live corrections. S8 ran no write-it-yourself exercise, so this item has had no chance to close. Close future sessions with one.

Tracing control flow (S8): the unwinding trace was nearly all correct. The slip was over-skipping, treating the exception as ending more of a function than it does. Worth watching in any control-flow topic.

Lecture slides versus compiler behaviour (S8): the slide says catch (...) "should" be last, but g++ makes it a compile error. Where a slide states a soft rule, check the real behaviour before an exam answer assumes either.

## 5. RETEST FIRST (ranked)
S6 template items first (ST2 bonus topic), then S7 DLL items (ST2 bonus topic), then the rest.
S6e. Where template definitions must live and the link error; class template member outside the class; scope of template <class Type>.
S6a. Member vs friend when the left operand is not the class type.
S6b. Post-increment return value.
S6c. [] const and non-const overloads.
S6d. Default = with a pointer member; copy constructor vs assignment trigger.

S7 items:
1. Explain the dllexport/dllimport macro switch and why -DBUILDING_MYLIB is set only on the DLL build.
2. What does extern "C" change, and what does it not work on?
3. What does typedef do in a function pointer declaration?
4. Which of seekg and seekp governs .read() and which governs .write(), and does moving one move the other?
5. Write from scratch: open a binary fstream with combined flags, write records, seek to an index, read one back.
6. Calculate sizeof for a struct by hand, showing where padding goes, then reorder and recalculate.
7. Given file size, header size and sizeof(Record), find the record count and the seek offset to a given record.
8. What does reinterpret_cast<char*>(&x) do to the bytes of x?
9. Which alignment does a struct member of struct type get?
10. Why does .open() take one mode argument, and why does if (!fail()) go wrong?

S8 single mixed check:
11. Trace a call chain where only the outermost function has a try block: say which lines print, which function continues running after the catch, and what happens if the outermost handler is removed. Include where what() belongs.
