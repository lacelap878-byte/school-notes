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
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
None flagged this session.

## 4. PATTERNS ACROSS SESSIONS
Not available this session, no prior session data was supplied to compare against. Per the existing cross-session learnings on file, struggle logs have been empty across S1 to S4 with no recurring difficulty pattern; this session's two resolved items are new and single-occurrence so far.

## 5. RETEST FIRST (ranked)
1. When is overloading `=` actually required versus optional, and what two other members must come with it?
2. What's the difference in trigger condition between the copy constructor and the assignment operator?
