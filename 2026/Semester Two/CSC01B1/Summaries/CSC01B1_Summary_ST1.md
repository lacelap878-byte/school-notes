---
module: CSC01B1
topic: ST1 Summary (S1 to S4)
test_label: ST1
tags: [summary]
---

# CSC01B1 — ST1 Summary (Sessions 1 to 4)

Built for fast review before the test, not first learning. If something
here doesn't click, follow the link back to the full session note.

`cs` PROFILE has no proof content, so no Proofs.md accompanies this file.

## Material covered

- [[CSC01B1_Notes_S1_Foundation-Topics]] — binary and number representation
  through to the class keyword
- [[CSC01B1_Notes_S2_Modules]] — C++20 modules
- [[CSC01B1_Notes_S3_Classes-Data-Abstraction]] — classes and data
  abstraction
- [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance]] — object
  composition and inheritance (Object Composition deck + L3)

## Condensed concept pass

**Binary, bases, and bitwise** — positional notation, binary/decimal/
hex/octal conversion, and bitwise NOT/AND/OR/XOR treated as boolean logic
applied per bit; bitmasking packs independent flags into one int. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#1. Binary and number representation]],
[[CSC01B1_Notes_S1_Foundation-Topics#2. Boolean and bitwise operations]])

**Signed numbers** — two's complement (absolute value, invert, add one)
is used over sign-and-magnitude because it needs no special-case adder;
fixed width means overflow wraps rather than errors. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#3. Signed numbers and overflow]])

**Binary fractions** — many decimal fractions (0.1 included) never
terminate in binary, hence never compare floats with `==`. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#4. Binary fractions]])

**Compilation** — compiler turns source into object code, linker joins it
with library code into an executable. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#6. The compilation process]])

**Memory model** — global (data segment), automatic (stack, freed at the
closing brace), dynamic (freestore, freed by hand). Only freestore
outlives its block and only freestore must be freed manually. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#7. The C++ memory model]])

**Pointers and references** — a pointer holds an address; `&` takes one,
`*` dereferences; wild (uninitialised) and dangling (freed) pointers are
both unsafe, fixed by NULLing on declare and after delete. Reference
parameters (`type &`) give the same mutability as a pointer parameter
without the `*`/`&` operators, and `const &` blocks mutation while
keeping pass-by-reference efficiency. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#9. Pointers and references]],
[[CSC01B1_Notes_S1_Foundation-Topics#13. Reference parameters]])

**Arrays** — an array name is a constant pointer to element 0, so it can
be read into a pointer but never reassigned; `array[i]` is `*(array + i)`.
(see: [[CSC01B1_Notes_S1_Foundation-Topics#10. Arrays and pointers]])

**Memory errors** — leaks (unfreed memory, or `delete` where `delete []`
was needed) versus dangerous actions (double free, freeing unallocated
memory, dereferencing freed memory, out-of-bounds access, following NULL).
(see: [[CSC01B1_Notes_S1_Foundation-Topics#12. Memory errors]])

**Function pointers, typedef, ADTs** — a function pointer lets the
function called vary at runtime, matched exactly on return type and
parameters; `typedef` aliases a type; an abstract data type is a
programmer-defined type where logical behaviour is deliberately kept
apart from implementation. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#14. Function pointers]],
[[CSC01B1_Notes_S1_Foundation-Topics#15. Extending the type system]])

**Structs, and OO by hand in C** — a struct groups data under one name; a
struct member can itself be a struct (composition/aggregation, used
loosely at this stage). A struct holding a function pointer plus a
"self" pointer argument approximates encapsulation by hand, with manual
`construct`/`destroy` functions standing in for what a class later gives
automatically. (see: [[CSC01B1_Notes_S1_Foundation-Topics#16. Structs]],
[[CSC01B1_Notes_S1_Foundation-Topics#18. Object orientation with C structs]])

**The three OO techniques (first stated)** — encapsulation, inheritance,
polymorphism, defined verbatim; the `class` keyword is C++'s built-in
answer to all three, where the C-struct approach above only ever
approximates encapsulation. (see:
[[CSC01B1_Notes_S1_Foundation-Topics#17. Object orientation techniques]],
[[CSC01B1_Notes_S1_Foundation-Topics#19. Beyond C: classes]])

**Why modules exist, and building one** — a module groups related
functionality and exports a chosen subset (the module interface);
`export module name` marks a module interface file; import uses the
name from that declaration, not the file name. (see:
[[CSC01B1_Notes_S2_Modules#Why modules exist]],
[[CSC01B1_Notes_S2_Modules#Building a first module]])

**Export blocks and interface/implementation split** — export blocks
group several export declarations under one `export { }`; large modules
move definitions to the bottom of the interface file (or a separate
implementation file) to keep the exported interface readable; `export`
can never be added retroactively to an entity first declared without it.
(see: [[CSC01B1_Notes_S2_Modules#Export blocks]],
[[CSC01B1_Notes_S2_Modules#Separating prototypes from implementations]])

**Class definition and access** — a class is a fixed set of members
(variables and functions); private is the default access level, public
and protected are the other two; a class definition only defines a type,
no memory until an object is declared. (see:
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Classes: definition and members]],
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Access categories]])

**UML class diagrams (notation)** — three compartments (name, data,
functions), visibility shown as `+` public, `-` private, `#` protected.
(see: [[CSC01B1_Notes_S3_Classes-Data-Abstraction#UML class diagrams]])

**Objects: declaring, scope, passing** — `.` and `=` are the only
built-in operators that work on class objects unaided; assignment is a
member-by-member copy leaving two separate objects; objects can be
automatic or static, and passed by value, by reference, or (best for
large objects) by `const &`. (see:
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Declaring and accessing objects]],
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Class scope and objects as parameters]])

**Implementing member functions** — defined outside the class body with
`ClassName::functionName`; accessor/mutator/constant functions
categorise what a member function is allowed to do to the object's
state. (see:
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Implementing member functions]])

**Constructors and destructors** — constructor name matches the class,
no return type, can be overloaded and take default parameters; a
parameterised constructor with no explicit default constructor removes
C++'s auto-supplied one; exactly one destructor per class, `~ClassName()`,
no parameters, fires automatically at scope exit. (see:
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Constructors]],
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Destructors]])

**Abstraction, ADTs, struct vs class, info hiding, static members** —
abstraction separates logical properties from implementation; struct
defaults to public members, class to private, otherwise both support the
same features; information hiding splits interface (`.h`) from
implementation (`.cpp`); a `static` member belongs to the class itself,
one shared copy regardless of object count. (see:
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Abstraction, ADTs, struct vs class]],
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Information hiding]],
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Static members of a class]])

**Identifying classes (OOD)** — nouns in a problem description become
candidate classes, verbs become operations, relationships become
associations; not every noun earns a class, characteristics of an object
stay as its data. (see:
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#OOD foundations and identifying classes]])

**UML class diagrams (inheritance)** — a class diagram shows static
structure only, never object-to-object communication; inheritance is
drawn as a plain arrow from the derived class box to the base class box.
(see: [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#UML class diagrams]])

**Association vs containment vs generalisation** — association is a bare
message call with no ownership tie; containment (has-a) and
generalisation (is-a) are built out fully in the next two entries. (see:
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Relationship types and association]])

**Composition vs aggregation (has-a)** — the deciding question is
life-span: composition if the container governs the contained object's
lifetime, aggregation if the contained object can outlive it;
member-objects under composition construct in declared order, finishing
before the containing constructor's body runs. (see:
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Composition and aggregation (has-a)]])

**Inheritance (is-a)** — derived class syntax
`class className: memberAccessSpecifier baseClassName`; single vs
multiple vs public inheritance; a base class's private members are never
directly reachable from a derived class under any specifier. (see:
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Inheritance (is-a)]])

**Overriding, and derived-class construction/destruction** —
`BaseClassName::functionName(...)` reaches an overridden base version
explicitly; a derived object executes a base constructor first, and a
derived destructor triggers the base destructor after it finishes. (see:
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Redefining base class functions, and derived-class constructors-destructors]])

**Protected members and the access table** — `protected` gives a derived
class direct access a private member wouldn't allow; across public,
protected, and private inheritance, a base class's private members never
pass through directly, only public/protected members do, at a level set
by the specifier. (see:
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Header files, protected members, and access]])

**The C++ stream hierarchy, and the three OOD/OOP principles restated** —
`ios` is the base of `istream`/`ostream`, in turn base of
`ifstream`/`ofstream`, a real-world is-a chain; encapsulation,
inheritance, and polymorphism (function/operator overloading, templates,
and virtual functions specifically for run-time selection across a
hierarchy) are OOD's three principles, implemented in C++ via classes.
(see: [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#The C++ stream class hierarchy]],
[[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#The three OOD-OOP principles]])

## Worked example notebook

- Two's complement of -29 in 8-bit: absolute value, invert, add one.
  (source: [[CSC01B1_Notes_S1_Foundation-Topics#3. Signed numbers and overflow]])
- Bitmasking with CITIZEN/EMPLOYED/ENFRANCHISED flags packed into one int.
  (source: [[CSC01B1_Notes_S1_Foundation-Topics#2. Boolean and bitwise operations]])
- `NumberGenerator` struct with a self pointer and manual
  `construct`/`destroy` functions, standing in for what a class later
  automates. (source:
  [[CSC01B1_Notes_S1_Foundation-Topics#18. Object orientation with C structs]])
- `LibMath` module: `export module` declaration, exporting `getOddity()`
  and the `Oddity` enum. (source:
  [[CSC01B1_Notes_S2_Modules#Building a first module]])
- `clockType`: UML diagram, declaring an object, and its accessor/mutator/
  constant member functions. (source:
  [[CSC01B1_Notes_S3_Classes-Data-Abstraction#UML class diagrams]])
- `rectangleType`/`boxType`: UML diagram showing inheritance, `boxType`
  overriding `print` and `area`. (source:
  [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#UML class diagrams]])
- `Worker`/`Manager`: composition plus delegation, `Manager` creates and
  destroys its `Worker` in its own constructor/destructor. (source:
  [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Composition and aggregation (has-a)]])
- `Course`/`Student`: aggregation, `Course` holds pointers to `Student`
  objects it never deletes. (source:
  [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Composition and aggregation (has-a)]])

## Common mistakes

No struggle log entries exist across S1 to S4 to pull from: S1 predates
the struggle log system (no log was ever generated for it), and the S2,
S3, and S4 logs are all on file but empty. Per protocol, a session with
no populated struggle log simply contributes nothing here, nothing is
invented to fill the gap.

## Tips

- When a C++ class mechanism doesn't make sense on its own, check
  whether S1 already showed the manual, by-hand version of it: the self
  pointer standing in for `this`, and `construct`/`destroy` functions
  standing in for constructors/destructors. S3's handoff memo draws
  exactly this line for constructors/destructors, `const &` parameters,
  and ADTs, it is worth doing the same check for anything from S4 that
  feels arbitrary.
- Terminology trap: S1 uses "composition" loosely for any struct nested
  inside another struct, and even calls it interchangeable with
  "aggregation". S4 draws the real distinction between the two based on
  life-span. If a question uses "composition" or "aggregation"
  precisely, S4's definition is the one being tested, not S1's looser
  usage.
