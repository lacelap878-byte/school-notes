Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S6. Later evidence is added to each item as a Status line. The cumulative retest list is in the S13 log.

Source key used below: slide-level = the rule or requirement is stated on the lecture slides. chat-derived = the mechanism or example came from follow-up questions in the session, not the slides. Slide-level items are the more likely test material; chat-derived items are the reasoning behind them.

## 1. OPEN ITEMS (unresolved, oldest first)
All eight came from the S6 session-end check quiz (0 of 8 correct). A correction on the spot is not treated as resolution.

1. Post-increment return value (slide-level)
   - Chose "returns a copy, too slow to be legal" for a version that returns *this. Speed is irrelevant to legality. The bug is that it returns the already-incremented object; post-increment must return the saved pre-increment copy (temp).
   - Status: open. Not retested in S7 to S13.

2. `[]` on a const object with only a non-const overload (slide shows both overloads; the reason is chat-derived)
   - Chose "compiles, since it only reads". The compiler goes by the function's signature, not what the body does. A non-const member cannot be called on a const object, so the const overload must exist.
   - S13 (1 Nov): the user raised the two overloads himself ("we would need to handle the two types of list, the const and the normal one"). The pair is `T& operator[](int)` and `const T& operator[](int) const`. The return type for the 2025-A 1.6 style question (accessor and mutator, array of double) was right: `double&`. Production of the const overload was not retested.
   - Status: open, partly understood.

3. Copy constructor versus assignment operator trigger (chat-derived)
   - Chose `a = b;` (both already exist) as the copy constructor case. The copy constructor runs when a NEW object is created from an existing one (`Clock c = b;`). `Clock c; c = b;` is assignment because c already exists.
   - S13 (1 Nov): a compiled demo printed COPY CONSTRUCTOR for `Box c = a;`, `Box d(a);` and a by value parameter, and ASSIGNMENT OPERATOR for `b = a;`. The user said it did not make sense; the "photocopy onto a blank sheet versus onto a sheet that already has writing" picture was given. Not retested.
   - Status: open.

4. What the default `=` does with a pointer member (slide states the requirement; mechanism is chat-derived)
   - Chose "does not compile". The default `=` always compiles; it copies the address, so two objects share one array. Result: a leak (the old array is lost) and a double free (both destructors delete the same array).
   - S12 quiz Q6 wrong again. S13 (30 Oct): answered "copies the pointer address" but named only the double free and missed the leak; wrote operator= with `delete` instead of `delete[]`, no `return *this;`, the size never copied, no self check. S13 (1 Nov, Scores drill): 5 of 6 steps right (`delete[]`, size, `new[]`, copy loop, `return *this;`); the self check was `*this != other`, which does not compile (compiled: `no match for 'operator!=' (operand types are 'Scores' and 'const Scores')`); the right test is `this != &other`. 2025-A 1.8 correct (copy constructor, destructor, operator=).
   - Status: open for the self check; the other steps are right.

5. Scope of a template header (chat-derived)
   - Chose "works, but only when Type is int". `template <class Type>` covers exactly the one declaration beneath it; `Type` does not exist anywhere else.
   - Status: open. Not retested.

6. Templates with definitions in a separately compiled .cpp (slide states the rule; the link error is chat-derived)
   - Chose "everything builds and runs". main.cpp compiles, but nobody generates Box<int>'s code, so the failure is at LINK time with "undefined reference". Applies to function templates too.
   - Status: open. Not retested (it is also a True or False pattern in past papers).

7. Defining a class template member outside the class body (chat-derived)
   - Chose `Type Box::get() const`. It needs its own `template <class Type>` line and `Box<Type>::`.
   - S13 (1 Nov): asked "when I define the function outside the class do I still use the template marker?" The answer (yes, a template line and `StackType<T>::` in front of the name; also for the constructor and destructor) was compiled with a templated array stack. Not written from a blank page.
   - Status: open.

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
Member vs friend when the left operand is | First seen S6 (5.0 + m). Missed twice more in S12 drills, and
not the class type                        | [] had to be a member was unknown (drill 1d). S13 (30 Oct): first
                                          | retest partly right; second retest 4 of 4: a == 5 member,
                                          | 5 == a non member, a = 5 member, cin >> a non member. The rule:
                                          | left operand is the class means member; otherwise non member
                                          | (friend only if it needs the private data); = [] () -> are always
                                          | members. Marking is by standard C++ rules, not compiled.
```
Earlier in the session, four points were explained but never retested, so they were folded into the items above: whether every class must overload operators (only `=` and `.` are free; the mandatory case is pointer members, item 4), whether default `=` copies private members too (it does), whether `=` and the copy constructor are the same thing (item 3), and why class templates seemed to skip `Type` (item 7).

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
- `Box` versus `Box<Type>`: the bare name is not a complete type outside the class body (item 7).
- "Client code": the file that uses the template, for example main.cpp. It does not mean the template has to be written there.
- Compile time versus link time: the missing definition failure for templates shows up at link time (item 6).
- `this` is a pointer, so it is compared with an address: `this != &other` (item 4).

## 4. PATTERNS ACROSS SESSIONS
Assuming two independent things are one shared thing: S5 (inheritance subobjects), S6 (= and copy constructor, template scope; still open), S7 (seekg and seekp).

## 5. RETEST FIRST (ranked, from section 1)
1. Post-increment return value.
2. `[]` const and non const overloads (write both signatures).
3. operator= from a blank page with `this != &other`, `delete[]`, size, `new[]`, copy, `return *this`.
4. Copy constructor versus assignment trigger (`Box c = a;` against `b = a;`).
5. Where template definitions must live, and the link error.
6. Defining a class template member outside the class.
7. Scope of `template <class Type>`.

---
*CDG version: written under an earlier version that was not recorded (S6) | restructured S13 (v11) | 2026-11-01*
