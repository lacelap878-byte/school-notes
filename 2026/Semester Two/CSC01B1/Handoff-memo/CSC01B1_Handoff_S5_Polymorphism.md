Supersedes S1 to S4. This is the only handoff file needed.

1. OBJECTIVE (this session)
Produce hybrid-mode CDG notes for CSC01B1 Session 5, covering Lecture 4
(Polymorphism): virtual function basics and late binding, the Sale/
DiscountSale implementation, overriding vs redefining and the virtual
overhead trade-off, pure virtual functions and abstract base classes,
extended type compatibility and the slicing problem with its pointer fix,
virtual destructors, casting (upcasting and downcasting), and the inner
workings of virtual functions (virtual function table).

2. TOPIC LEDGER
S1 | Foundation Topics (binary and number systems, bitwise ops, signed numbers, memory model, pointers, arrays, structs, intro to classes) | full | open struggle no
S2 | C++20 Modules (module concept, first module, export blocks, prototypes vs implementation) | full | open struggle no
S3 | Classes and Data Abstraction (class syntax, UML, objects, scope, member function implementation, constructors/destructors, abstraction, ADTs, struct vs class, information hiding, static members) | full | open struggle no
S4 | Object Composition and Inheritance (OOD foundations and identifying classes, UML class diagrams incl. inheritance, association, composition/aggregation, inheritance syntax, overriding member functions, derived-class constructors/destructors, header files/protected members/access table, C++ stream hierarchy, OOD/OOP principles) | full | open struggle no
S5 | Polymorphism (virtual function basics and late binding, Sale/DiscountSale implementation, overriding vs redefining and virtual overhead, pure virtual functions and abstract base classes, extended type compatibility and slicing problem, virtual destructors, casting, virtual function table mechanics) | full | open struggle no

3. NOTES INDEX
S1 | Foundation Topics | CSC01B1_Notes_S1_Foundation-Topics.md | binary and number systems through to the class keyword
S2 | C++20 Modules | CSC01B1_Notes_S2_Modules.md | why modules exist, module declaration syntax and naming, export and export blocks, separating a module's interface from its implementation
S3 | Classes and Data Abstraction | CSC01B1_Notes_S3_Classes-Data-Abstraction.md | class definition and access, UML diagrams, objects, scope, member function implementation, constructors/destructors, abstraction/ADTs, struct vs class, information hiding, static members
S4 | Object Composition and Inheritance | CSC01B1_Notes_S4_Object-Composition-and-Inheritance.md | OOD foundations, identifying classes, UML inheritance diagrams, association, composition/aggregation, inheritance syntax, overriding functions, derived-class constructors/destructors, header files/protected members/access table, C++ stream hierarchy, OOD/OOP principles
S5 | Polymorphism | CSC01B1_Notes_S5_Polymorphism.md | virtual function basics and late binding, Sale/DiscountSale worked implementation, overriding vs redefining, virtual overhead, pure virtual functions and abstract base classes, extended type compatibility and the slicing problem, virtual destructors, upcasting/downcasting, virtual function table mechanics

4. CONTENT SUMMARY
S1 to S4: compressed to one line each, see TOPIC LEDGER.
S5 (this session, in detail): Worked through CSC01B12026L4.pdf (45 slides,
anchored L4) across 8 parts, hybrid mode (compressed like review, short
why clauses kept). Part 1 covered the definitions of polymorphism,
virtual, and virtual function, and motivated the whole topic through the
Figures example (Figure/Rectangle/Circle/Triangle), building to the
problem that Figure::center() cannot know at compile time which derived
draw() a future class like Triangle will need, and to late binding as the
fix. Part 2 covered the Sale/DiscountSale worked example in full: the
virtual keyword on Sale::bill(), that a virtual base function is
automatically virtual in a derived override without needing the keyword
repeated, and why DiscountSale::bill() gets used inside Sale::savings()
even though Sale was compiled before DiscountSale existed. Part 3 covered
the overriding/redefining terminology split (virtual changes are
overriding, non-virtual changes are redefining, cross referenced to S4)
and the storage/speed overhead trade-off of using virtual functions. Part
4 covered pure virtual functions (the = 0 syntax) and abstract base
classes, including that a derived class failing to implement every
inherited pure virtual function is itself still abstract. Part 5 covered
extended type compatibility (derived to base assignment only, never the
reverse), the Pet/Dog worked example, the slicing problem on plain
object assignment, and the pointer based fix, including a user question
and follow up discussion on where Dog's breed field physically lives
when accessed only through a Pet pointer. Part 6 covered virtual
destructors and why deleting through a base pointer needs one. Part 7
covered casting: upcasting via static_cast as always legal, downcasting
via dynamic_cast as legal but dangerous, and the two conditions the
source attaches to downcasting. Part 8 covered the virtual function
table mechanism (per class table of function pointers, per object
pointer to that table) and the lecture's own two part summary.
Link to S1: Part 6's virtual destructors heading cross references S1's
coverage of destructors needed to de-allocate dynamically allocated
data, since S1 already establishes why destructors matter at all.
Link to S3: Part 8's mention of not needing to know virtual function
table internals to use virtual functions cross references S3's
information hiding heading directly, same principle, applied here to
compiler internals rather than class design.
Link to S4: Part 3's overriding/redefining split cross references S4's
redefining a base class member function heading, since S4 already
establishes what redefining is for non-virtual functions.
Two struggles resolved this session, both after Part 8 was delivered.
First, during a Part 5 follow up thread, that stack based slicing is not
the assignment operator "breaking", it is the operator running
correctly but scoped only to the static type of the target variable
(Pet's operator has no concept of breed), whereas pointer assignment
never copies the object at all, it copies an address into an already
complete Dog object elsewhere. Second, a follow up thread on virtual
destructors surfaced a feared double free from destructor chaining,
traced back to a wrong mental model of inheritance as sharing or
referencing Base's members rather than each Derived object containing
its own complete, physically separate Base subobject (composition under
the hood, true even for private Base members that Derived's own code
cannot name). Once that model was corrected, chained destructors were
seen to free two distinct addresses, never the same one, and a genuine
double free was traced to its real cause, pointer aliasing, unrelated to
destructor chaining or virtual vs non-virtual. See struggle log for the
compressed form of both.

5. LAST POSITION
Part 8 of 8, Inner workings of virtual functions and summary. Session
material finished.

6. PARKED ITEMS
None.

7. RESUME BLOCK
Next CSC01B1 session: PROFILE cs, MODULE CODE CSC01B1. Provide the next
lecture PDF (e.g. CSC01B12026L5.pdf or CSC01B12026L6.pdf) and mode
(teach/review/hybrid).
