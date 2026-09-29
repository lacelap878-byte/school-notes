Supersedes S1 to S5.

Source key used below: slide-level = the rule or requirement is stated on the lecture slides. chat-derived = the mechanism or example came from follow-up questions in the session, not the slides. Slide-level items are the more likely test material; chat-derived items are the reasoning behind them.

## 1. OPEN ITEMS (unresolved, oldest first)
All eight came from the session-end check quiz (0 of 8 correct). None has been answered correctly under retest yet, so all stay open. A correction on the spot is not treated as resolution.

```
concept | first seen S6 | what the misconception was | sessions persisting | source

1. Member vs friend when the left operand is not the class type
   Chose that `5.0 + m` (double, Money) could be a member. A member
   function is called on its left operand, so the left operand must be the
   class type; `5.0 + m` must be a nonmember. `m + 5.0` can be either.
   | S6 | 1 session | slide-level (leftmost-operand rule)

2. Post-increment return value
   Chose "returns a copy, too slow to be legal" for a version that returns
   *this. Speed is irrelevant to legality. The bug is that it returns the
   already-incremented object; post-increment must return the saved
   pre-increment copy (temp).
   | S6 | 1 session | slide-level (post-increment definitions)

3. `[]` on a const object with only a non-const overload
   Chose "compiles, since it only reads". The compiler goes by the
   function's signature, not what the body does. A non-const member cannot
   be called on a const object, so the const overload must exist.
   | S6 | 1 session | slide shows both overloads; the reason is chat-derived

4. Copy constructor vs assignment operator trigger
   Chose `a = b;` (both already exist) as the copy constructor case. The
   copy constructor runs when a NEW object is created from an existing one
   (`Clock c = b;`). `Clock c; c = b;` is assignment because c already exists.
   | S6 | 1 session | chat-derived (slide only says both are required)

5. What the default `=` does with a pointer member
   Chose "does not compile". The default `=` always compiles; it copies
   the address, so two objects share one array. Result: a leak (the old
   array is lost) and a double free (both destructors delete the same array).
   | S6 | 1 session | slide states the requirement; mechanism is chat-derived

6. Scope of a template header
   Chose "works, but only when Type is int". `template <class Type>` covers
   exactly the one declaration beneath it; `Type` does not exist anywhere
   else, so using it in an ordinary function is a compile error.
   | S6 | 1 session | chat-derived

7. Templates with definitions in a separately compiled .cpp
   Chose "everything builds and runs". main.cpp compiles, but nobody
   generates Box<int>'s code, so the failure is at LINK time with
   "undefined reference". Applies to function templates too.
   | S6 | 1 session | slide states the rule; the link error is chat-derived

8. Defining a class template member outside the class body
   Chose `Type Box::get() const`. It needs its own `template <class Type>`
   line and `Box<Type>::`, because Box alone is not a complete type.
   | S6 | 1 session | chat-derived
```

Earlier in the session, four points were explained but never retested, so they are folded into the items above rather than listed as resolved: whether every class must overload operators (only `=` and `.` are free; the mandatory case is pointer members, item 5), whether default `=` copies private members too (it does), whether `=` and the copy constructor are the same thing (item 4), and why class templates seemed to skip `Type` (item 8).

## 2. RESOLVED THIS SESSION
None.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
- `Box` vs `Box<Type>`: the bare name is not a complete type outside the class body (item 8).
- "Client code": means the file that uses the template, for example main.cpp. It does not mean the template has to be written there.
- Compile time vs link time: the missing-definition failure for templates shows up at link time (item 7).

## 4. PATTERNS ACROSS SESSIONS
None identifiable. No earlier struggle log was supplied, and a pattern needs two or more sessions.

## 5. RETEST FIRST (ranked, drawn from section 1)
Slide-level items first, since they are the likeliest to be tested.
1. Member vs friend when the left operand is not the class type (item 1)
2. Post-increment return value (item 2)
3. `[]` const and non-const overloads (item 3)
4. Default `=` with a pointer member, and why `=`, copy constructor and destructor come together (item 5)
5. Copy constructor vs assignment trigger (item 4)
6. Where template definitions must live, and the link error (item 7)
7. Defining a class template member outside the class (item 8)
8. Scope of `template <class Type>` (item 6)
