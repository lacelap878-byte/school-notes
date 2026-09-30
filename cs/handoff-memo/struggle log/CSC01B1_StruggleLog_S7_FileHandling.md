Supersedes S1 to S6.

## 1. OPEN ITEMS (unresolved, oldest first)
S6 items, carried in full from the S6 struggle log. All came from the S6 session-end quiz (0 of 8 correct) and were not retested in S7, so all stay open.
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
Member vs friend, left operand not class  | S6         | Chose that 5.0 + m could be a member. A member is called   | 2
                                          |            | on its left operand, so 5.0 + m must be a nonmember.      |
Post-increment return value               | S6         | Thought returning *this fails for speed. The bug is that   | 2
                                          |            | it returns the already-incremented object; return the     |
                                          |            | saved copy (temp).                                         |
[] on a const object                      | S6         | Thought a non-const-only overload compiles because the     | 2
                                          |            | body only reads. The signature decides, so a const        |
                                          |            | overload must exist.                                       |
Copy constructor vs assignment trigger    | S6         | Chose a = b (both exist) as the copy constructor case.    | 2
                                          |            | Copy constructor: new object from existing (Clock c = b). |
Default = with a pointer member           | S6         | Thought it does not compile. It compiles and copies the   | 2
                                          |            | address: a leak and a double free.                         |
Scope of template <class Type>            | S6         | Thought it works when Type is int elsewhere. It covers    | 2
                                          |            | only the one declaration beneath it.                       |
Template definitions in a separate .cpp   | S6         | Thought it builds. It fails at LINK time with undefined   | 2
                                          |            | reference (also for function templates).                   |
Class template member defined outside    | S6         | Wrote Type Box::get() const. Needs its own template       | 2
                                          |            | <class Type> line and Box<Type>::.                         |
```

S7 items.
```
concept                                   | first seen | misconception                                              | sessions persisting
------------------------------------------|------------|------------------------------------------------------------|--------------------
seekg vs seekp                            | S7         | Used seekp before a .read(). The read marker (seekg) and   | 1
                                          |            | write marker (seekp) are independent; .read() uses seekg.  |
Recognition vs production                 | S7         | Can pick the right answer in a quiz but could not write    | 1
                                          |            | the code from scratch without guidance.                    |
Padding placement and reordering          | S7         | Unsure where padding goes; padding is inserted before a    | 1
                                          |            | member whose alignment the next offset fails, and          |
                                          |            | reordering members changes the total size.                 |
Alignment of a compound member            | S7         | Assumed it equals the member's sizeof; it is the largest   | 1
                                          |            | alignment among its own members.                           |
reinterpret_cast                          | S7         | Unsure what it does; it only relabels the pointer type,    | 1
                                          |            | with no conversion and no check.                           |
DLL syntax and jargon                     | S7         | Macro switch (dllexport/dllimport), extern "C", .impl.cpp  | 1
                                          |            | naming, typedef on a function pointer, -D flag.            |
.open() takes one mode argument           | S7         | Passed several flags as separate arguments; combine with   | 1
                                          |            | | into one.                                                |
ifstream vs fstream                       | S7         | Thought ios::out could make an ifstream writable; write    | 1
                                          |            | ability belongs to the class.                              |
!fail() check                             | S7         | Wrote if (!x.fail()), which reports an error on success.   | 1
Assigning a char array with =             | S7         | Arrays cannot be assigned after declaration; use an        | 1
                                          |            | initializer list.                                          |
seekg call form and seek vs read          | S7         | Called seekg without a stream object and expected it to    | 1
                                          |            | return the data; seeking only moves the marker.            |
Off-by-one record index                   | S7         | "2nd record" is index 1.                                   | 1
.read()/.write() direction                | S7         | Names describe what happens to the file, not the variable. | 1
Header offset in record counting          | S7         | Record count and seek offsets must subtract/add the header | 1
                                          |            | size.                                                      |
```

All items stay open until answered correctly under retest.

## 2. RESOLVED THIS SESSION
None.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Jargon in the DLL material (dllexport, dllimport, __stdcall, extern "C", HINSTANCE, .impl.cpp, -D, -Wl,--out-implib) caused the most trouble. Concepts were fine, keywords were not.

## 4. PATTERNS ACROSS SESSIONS
Assuming two independent things are one shared thing: S5 (inheritance subobjects), S6 (= and copy constructor, template scope; still open), S7 (seekg and seekp). Watch any topic with parallel but independent mechanisms.

Recognition versus production (S7): quiz answers were fine, but writing code from a blank page required six live corrections. Close future sessions with a write-it-yourself exercise.

## 5. RETEST FIRST (ranked)
S6 slide-level items first (likeliest on ST2), then S7.
S6a. Member vs friend when the left operand is not the class type.
S6b. Post-increment return value.
S6c. [] const and non-const overloads.
S6d. Default = with a pointer member; copy constructor vs assignment trigger.
S6e. Where template definitions must live and the link error; class template member outside the class; scope of template <class Type>.

S7 items:
1. Which of seekg and seekp governs .read() and which governs .write(), and does moving one move the other?
2. Write from scratch: open a binary fstream with combined flags, write records, seek to an index, read one back.
3. Calculate sizeof for a struct by hand, showing where padding goes, then reorder and recalculate.
4. Given file size, header size and sizeof(Record), find the record count and the seek offset to a given record.
5. What does reinterpret_cast<char*>(&x) do to the bytes of x?
6. Explain the dllexport/dllimport macro switch and why -DBUILDING_MYLIB is set only on the DLL build.
7. What does extern "C" change, and what does it not work on?
8. Which alignment does a struct member of struct type get?
9. What does typedef do in a function pointer declaration?
10. Why does .open() take one mode argument, and why does if (!fail()) go wrong?
