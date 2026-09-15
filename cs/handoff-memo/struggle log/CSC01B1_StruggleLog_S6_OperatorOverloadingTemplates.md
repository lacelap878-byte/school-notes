Supersedes S1 to S5.

## 1. OPEN ITEMS (unresolved, oldest first)
None open from this session.

S1 to S5: not available this session, no handoff memo was provided to carry open items forward. If any are still outstanding, they will need to be re-flagged next session.

## 2. RESOLVED THIS SESSION
```
concept                                  | correction
------------------------------------------|---------------------------------------------
Scope of operator overloading requirement | Corrected the assumption that all classes
                                           | must implement operator overloading. Only
                                           | `=` and `.` are given to a class for free
                                           | by the compiler; every other operator
                                           | overload is optional and exists purely to
                                           | make the calling code read more naturally.
                                           | The one case where overloading `=` is
                                           | actually mandatory (paired with a copy
                                           | constructor and destructor) is when the
                                           | class has pointer member variables, since
                                           | the default memberwise copy only copies
                                           | the pointer's address.
------------------------------------------|---------------------------------------------
Relationship between the assignment       | Corrected the assumption that `=` and the
operator and the copy constructor         | copy constructor are the same or combined
                                           | mechanism. They are distinguished by when
                                           | they fire: the copy constructor runs when
                                           | a new object is being created from an
                                           | existing one; the assignment operator
                                           | runs when assigning into an object that
                                           | already exists. Both default to
                                           | memberwise copy and both break under
                                           | pointer members for the same reason, but
                                           | they remain two separate functions.
------------------------------------------|---------------------------------------------
Scope of a template declaration           | Corrected the assumption that a template
                                           | header might apply more broadly than one
                                           | declaration. `template <class Type>`
                                           | applies only to the single function or
                                           | class written directly beneath it; `Type`
                                           | does not exist outside that one scope.
                                           | Confirmed directly by a compiler error
                                           | ('Type' does not name a type) when Type
                                           | was reused in an unrelated function below
                                           | a function template.
------------------------------------------|---------------------------------------------
Whether class templates skip declaring    | Corrected the assumption that class
Type for member functions                 | template member functions don't need
                                           | Type written out. They do use Type
                                           | throughout (constructor parameter, return
                                           | types, etc.); what's actually skipped is
                                           | restating `template <class Type>` before
                                           | each member function, because the header
                                           | written once above the class covers the
                                           | whole class body for member functions
                                           | defined inline inside it. Member functions
                                           | defined outside the class body do need
                                           | template <class Type> repeated for each
                                           | one, plus ClassName<Type>:: qualification.
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
None flagged this session.

## 4. PATTERNS ACROSS SESSIONS
Not available this session, no prior session data was supplied to compare against. Per the existing cross-session learnings on file, struggle logs have been empty across S1 to S4 with no recurring difficulty pattern; this session's four resolved items are new and single-occurrence so far.

## 5. RETEST FIRST (ranked)
1. When is overloading `=` actually required versus optional, and what two other members must come with it?
2. What's the difference in trigger condition between the copy constructor and the assignment operator?
3. What exactly does `template <class Type>` apply to, and where does its scope end?
4. Why doesn't a class template need `template <class Type>` restated before every member function written inline inside the class, but does need it restated when a member function is defined outside the class body?
