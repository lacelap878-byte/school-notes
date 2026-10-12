Supersedes S1 to S7. This is the only handoff file needed.

## 1. OBJECTIVE (this session)
Work through CSC01B1 Lecture 7 in full: exception handling, covering what an exception is, assert, try/catch/throw, the order of catch blocks, the C++ exception class hierarchy and what(), user-defined exception classes, rethrowing, the throw clause, the three handling techniques, and stack unwinding. This is the third and last ST2 bonus topic, after templates (S6) and DLLs (S7).

## 2. TOPIC LEDGER
```
S1 | Foundation Topics (binary and number systems, bitwise ops, signed numbers, memory model, pointers, arrays, function pointers, structs, intro to classes) | full | open struggle no
S2 | C++20 Modules (module concept, first module, export blocks, prototypes vs implementation) | full | open struggle no
S3 | Classes and Data Abstraction (class syntax, UML, objects, scope, constructors/destructors, ADTs, struct vs class, information hiding, static members) | full | open struggle no
S4 | Object Composition and Inheritance (OOD, UML, association, composition, inheritance syntax, overriding, derived-class constructors/destructors, protected members, stream hierarchy) | full | open struggle no
S5 | Polymorphism (virtual functions, late binding, pure virtual and abstract classes, slicing, virtual destructors, casting, vtable) | full | open struggle no
S6 | Operator overloading (fundamentals, this pointer, friend functions, binary/stream/assignment/unary/increment/subscript overloads) and templates (function and class, header layout) | full | open struggle yes (8 items, quiz 0 of 8)
S7 | File handling (secondary storage and streams, sequential file I/O, opening modes and flags, output formatting, random access, raw disk I/O, padding and #pragma pack, DLLs with implicit and explicit linking) | full | open struggle yes
S8 | Exception handling (exception, assert, try/catch/throw, catch order, exception classes and what(), user-defined exception classes, rethrowing, throw clause, handling techniques, stack unwinding) | full | open struggle no (S6 and S7 items stay open)
```

## 3. NOTES INDEX
```
S1 | Foundation Topics | CSC01B1_Notes_S1_Foundation-Topics.md |
     Binary, bitwise ops, memory, pointers, arrays, function pointers (14), typedef (15), structs (16)
S2 | C++20 Modules | file name unverified |
S3 | Classes and Data Abstraction | file name unverified |
S4 | Object Composition and Inheritance | file name unverified |
S5 | Polymorphism | file name unverified |
S6 | Operator overloading and templates | CSC01B1_Notes_S6_OperatorOverloadingTemplates.md |
     Lecture 5 retelling: operator overloading, then function and class templates
S7 | File handling | CSC01B1_Notes_S7_FileHandling.md |
     Lecture 6 retelling: streams, sequential and random access files, raw bytes, padding, DLLs
S8 | Exception handling | CSC01B1_Notes_S8_ExceptionHandling.md |
     Lecture 7 retelling: try/catch/throw, catch order, exception classes, rethrowing, handling techniques, stack unwinding
```

## 4. CONTENT SUMMARY
S8 covered Lecture 7 in teach mode, four parts:
- What an exception is; assert (terminates with a message, cannot recover); try/catch/throw; the catch parameter as a placeholder for the thrown value, at most one parameter; control flow (rest of the try block skipped, catch blocks searched in order, first type match runs, none thrown means all catch blocks ignored); an exception is a value matched by type.
- Order of catch blocks: first match wins. catch (...) catches any type and must be last (the slide says should; g++ rejects it as an error otherwise). A base class handler placed before a derived one compiles with a warning and the base block runs.
- Exception classes: class exception in the header exception is the base, what() belongs to exception (not to stdexcept). stdexcept defines logic_error (invalid_argument, out_of_range, length_error) and runtime_error (overflow_error, underflow_error). Any class can be an exception class by how it is used. A user-defined class with member variables typically has constructors and a what function, and its what is its own, not the inherited one unless it derives from exception.
- Rethrowing: a catch block handles, or partially processes and rethrows the same exception (throw;), or throws another for the calling environment. The throw clause in a function heading was covered; dynamic exception specifications are rejected from C++17 on, so know the idea only.
- Three handling techniques: terminate, fix and continue, log and continue, matched to the program type.
- Stack unwinding: a function with no handler terminates and its locals are destroyed, outward through callers until a matching catch is found or terminate ends the program. The rest of the try block is skipped, the rest of the function after the try/catch is not.
- Checked by compiling in g++ with C++20: the session examples, catch order, unhandled exception ending in terminate (exit 134), assert failure (abort), slicing when catching exception by value.
- Session-end check quiz: 8 questions, user reports 8 of 8, no screenshots. Q2 (catch (...) before catch (int)) had a wrong premise because that code does not compile, so it is void.

S7 (Lecture 6): file handling, DLLs, guided coding exercise; struggle items open. S6 (Lecture 5): operator overloading and templates, quiz 0 of 8, items open. S1 to S5: one line each in the ledger.

## 5. LAST POSITION
Part 4 of 4, Stack unwinding and summary, complete. Session-end check quiz run. Slide 22 (rethrow syntax) was never seen: its code lines are marked (added) in the notes. The S6 and S7 open items were not retested this session because no handoff memo was supplied at the start.

## 6. PARKED ITEMS
None.

## 7. RESUME BLOCK
```
PROFILE cs
MODULE CODE CSC01B1
Paste this handoff memo and CSC01B1_StruggleLog_S8_ExceptionHandling.md
at the start of the next session.
Run the session-start revision quiz first, S6 template items first (ST2 bonus topic), then S7 DLL items (ST2 bonus topic), then the remaining S6 and S7 items. Tell me first if the S6, S7 and S8 notes have not been re-read.
ST2 plan: run Revise ST2 S1 to S8 once the range is confirmed, folding the three bonus topics (templates S6, DLLs S7, exception handling S8) into the ST2 summary.
Project also holds CSC01B1-2026-L8.pdf (listed twice) and CSC01B1-2026-L9.pdf, not yet checked.
```
