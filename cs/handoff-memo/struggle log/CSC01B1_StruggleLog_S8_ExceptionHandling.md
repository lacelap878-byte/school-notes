Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S8. S6 and S7 items that this log used to carry are in the S6 and S7 logs. Items first seen in the exam revision (S13) are in the S13 log. The cumulative retest list is in the S13 log.

## 1. OPEN ITEMS (unresolved, oldest first)
S8 items: none open. Two gaps surfaced in discussion and were checked by later quiz questions, see section 2. The S13 quick fire (30 Oct) found two exception misses that are about S8 material (handler order and the order destructors run during unwinding). They are logged in S13 because they were first seen there, and they put the weak S8 checks below back on the retest list.

## 2. RESOLVED (with the session that resolved it)
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
                                          | stdexcept only defines the subclasses, which inherit it. A user defined class
                                          | has what() only if written. Checked by quiz Q3 (reported correct).
```
These were checked in the same session as the correction, so they have the weakest evidence.
S13 evidence for the paper style questions: 2025-A 2.2 (a base exception class and a derived IndexException with a constructor chain) was correct on 1 Nov, and 2025-A 2.3 (try and catch around the client code, with the throw left to operator[]) was fixed on the second try. The True or False item "catch(...) must be the last handler" was answered correctly in the 1 Nov drill.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
S8: "stack unwinding" as a term. The behaviour was understood from the trace, the name was the unfamiliar part.

## 4. PATTERNS ACROSS SESSIONS
Tracing control flow (S8): the unwinding trace was nearly all correct. The slip was over skipping, treating the exception as ending more of a function than it does. Worth watching in any control flow topic. It came back in S13 as the destructor order slip (locals are destroyed before the handler runs).
Lecture slides versus compiler behaviour (S8): the slide says catch (...) "should" be last, but g++ makes it a compile error. Where a slide states a soft rule, check the real behaviour before an exam answer assumes either.
Recognition versus production (S7): S8 ran no write it yourself exercise. The 2025-A 2.2 and 2.3 answers in S13 are the first production evidence.

## 5. RETEST FIRST (ranked, from section 1)
1. Trace a call chain where only the outermost function has a try block: say which lines print, which function continues running after the catch, and what happens if the outermost handler is removed. Include where what() belongs.
2. Handler order and destructor order during unwinding (see the S13 log, items 3 and 4).

---
*CDG version not recorded | written S8 (S6 and S7 items moved to their own logs in S13) | amended S13 (v11) | 2026-11-01*
