---
module: CSC01B1
topic: Classes and Data Abstraction
session: S3
tags: [definition, worked-example]
---

# CSC01B1 — Classes and Data Abstraction (Lecture 2)

## Classes: definition and members

A **class** is a collection of a fixed number of components, called
**members**. This sits inside object-oriented design (OOD): objects are
the components of a solution, and a class is the blueprint an object is
built from. This picks up directly from where Foundation Topics left off
(see: S1 — The class keyword), which already drew the line that
**structs hold data; classes encapsulate data together with the
functions legal on those data** — this lecture is that line worked out
in full syntax and mechanics.

This also cashes out S1's definition of encapsulation (see: S1 — Object
orientation techniques): "the ability to combine data and the operations
legal on those data in a single unit" is exactly what a class member
list does — data members plus function members in one unit.

```cpp
class classIdentifier
{
    classMembersList
};
```
> [!note] A class *definition* only defines a data type — no memory is
> allocated until you declare an object of that type. The closing brace
> needs a semicolon, easy to forget since ordinary function bodies don't
> need one.

A member can be:
- a **variable**, declared like any ordinary variable, but never
  initialised at the point of declaration (that's a constructor's job,
  see below);
- a **function**, whose prototype sits in the class body while its code
  is written elsewhere. Function members can directly access any other
  member of their own class, public or private, no qualification needed.

## Access categories

- **private** (the default, if nothing is stated): unreachable from
  outside the class.
- **public**: reachable from outside the class.
- **protected**: a third level, relevant once inheritance is involved
  (not detailed in this lecture).

## UML class diagrams

UML notation graphically describes a class and its members:

| Symbol | Meaning |
|---|---|
| `+` | member is public |
| `-` | member is private |
| `#` | member is protected |

**Worked example (source, slide 11):**
```
clockType
-hr: int
-min: int
-sec: int

+setTime(int, int, int): void
+getTime(int&, int&, int&) const: void
+printTime() const: void
+incrementSeconds(): int
+incrementMinutes(): int
+incrementHours(): int
+equalTime(const clockType&) const: bool
```
Top compartment: class name. Middle: data members (all private here).
Bottom: function members (all public), with parameter and return types.
This `clockType` example recurs throughout the rest of the lecture.

## Declaring and accessing objects

```cpp
clockType myClock;          // declaring an object (a "class instance")
myClock.setTime(3, 48, 52); // classObjectName.memberName
```
The dot `.` is the **member access operator**. From outside the class it
only reaches public members; code inside a member function of the class
can reach both public and private members of an object of that class.

### Built-in operations on classes

Most built-in operators do **not** work on class objects automatically.
Only two do, with no extra work:
- member access (`.`)
- assignment (`=`)

Arithmetic operators need overloading first; relational operators can't
compare two objects for equality without it either.

**Assignment semantics:** `myClock = yourClock;` copies every member
variable from `yourClock` into `myClock`, member by member. Afterward
both objects hold identical values but remain two separate objects —
later changes to one do not affect the other.

## Class scope and objects as parameters

An object can be:
- **automatic** — created when its declaration is reached, destroyed
  when the surrounding block exits;
- **static** — created when its declaration is reached, destroyed only
  when the program terminates.

Objects can be passed to and returned from functions **by value** or
**by reference**:
- **By value**: the actual parameter's members are copied into the
  formal parameter's members. Correct, but potentially expensive for
  large classes.
- **By reference**: the formal parameter receives only the address of
  the actual parameter — efficient, but the function can now modify the
  caller's object through it.

> [!warning] Common trap
> Passing by reference alone lets a function silently mutate the
> caller's object. The fix is a **const reference** parameter — keeps
> the efficiency of pass-by-reference while blocking modification.
> This is the pattern to reach for whenever a function needs to read a
> large object without owning a copy.

This is the same `const &` pattern from S1 (see: S1 — Reference
parameters), just applied to a class object instead of a plain `int`:
efficiency of pass-by-reference, safety of pass-by-value.

## Implementing member functions

Prototypes stay in the class body; the actual code is written outside,
using the **scope resolution operator** `::` to tell the compiler which
class the function belongs to:

```cpp
returnType clockType::functionName(parameters)
{
    // body — can access private members of the class directly
}
```

Keeping prototypes in the class and definitions outside keeps the class
declaration small and hides the implementation from anyone just reading
the interface.

A program that uses/manipulates objects of a class is a **client** of
that class. Each object of a class carries its own separate copy of the
member variables — these per-object copies are **instance variables**.

### Accessor, mutator, constant functions

- **Accessor**: only reads member variable value(s).
- **Mutator**: modifies member variable value(s).
- **Constant function**: cannot modify member variables — enforced with
  `const` in the function heading (this is why `getTime`, `printTime`,
  and `equalTime` are all `const` in the UML diagram above).

### Order of public/private members

C++ imposes no fixed order for public vs private sections — you can mix
or group freely. A member left unspecified defaults to **private**, so
`public` must be stated explicitly.

## Constructors

Nothing so far guarantees an object's members hold a sensible value the
moment it's declared — **constructors** close that gap by running
automatically to initialise members.

- Name = the class's own name; **no return type at all**, not even `void`.
- Two kinds: with parameters, and without (the **default constructor**).
- A class can have several, each with a different parameter list
  (overloading). They execute automatically when an object enters scope
  — you never call one directly by name.

```cpp
className classObjectName;                       // invoke default ctor
className classObjectName(argument1, argument2);  // invoke with params
```
Example: `clockType yourClock;`

Arguments should match some constructor's parameter list in number,
type, and order. A mismatch triggers type conversion to find the
closest match; genuine ambiguity between candidates is a compile-time
error.

A constructor can carry **default parameters**, following the same
rules as any function's default parameters — a "default constructor" is
any constructor callable with zero arguments (either a true no-param
constructor, or one where every parameter defaults).

> [!warning] Common trap
> If a class defines **no constructor at all**, C++ supplies its own
> default constructor — but the object is still **uninitialised**. If a
> class defines a constructor **with parameters but no explicit default
> constructor**, C++ does **not** step in with one, so a no-argument
> declaration of that class becomes a compile error.

Declaring an **array of class objects** requires the class to have a
default constructor, since every element is default-constructed as the
array is created.

## Destructors

- Name: `~` followed by the class name, e.g. `~clockType();`
- No return type, exactly **one** per class, **no parameters** (no
  overloading, unlike constructors).
- Executes automatically the moment the object goes out of scope — the
  mirror image of a constructor firing on entry.

Constructors and destructors are what a class gives you for free in
place of the by-hand lifecycle from S1 (see: S1 — Object orientation
with C structs, "Lifecycle by hand"): there, a separate `construct`
function had to allocate and initialise the struct, and a separate
`destroy` function had to free it and NULL the pointer, both called
manually. A constructor/destructor pair does the same two jobs, but
triggered automatically by scope instead of by a remembered function
call.

## Abstraction, ADTs, struct vs class

**Abstraction**: separating design details from usage — the logical
properties (what something does) from the implementation details (how
it does it). Applied to data, this gives the **abstract data type
(ADT)**: a data type that separates logical properties of data and
operations from how they're actually implemented. This is the same
distinction S1 drew (see: S1 — Extending the type system, "Programmer
defined type vs abstract data type"): an ADT is the stricter case of a
programmer defined type, one where behaviour is deliberately kept apart
from implementation.

**struct vs class:**
- `struct` members are public by default; `class` members are private
  by default. A struct can use `private` to flip individual members.
- Modern C++ `struct` supports member functions, constructors, and
  destructors — the same capabilities as a class.
- Convention: if every member variable would be public and there are no
  member functions, use a `struct` (signals "plain data").

S1's struct coverage (see: S1 — Structs) only ever showed plain data
records with member access via `.`, no member functions. That fits the
convention above exactly: S1's structs had no functions, so `struct`
was the right choice; a class is what you reach for the moment function
members enter the picture.

## Information hiding

**Information hiding**: hiding the details of operations on data from
the code that uses that data.

- **Interface (header) file** (`.h`): specification only — function
  prototypes plus comments describing what each does, including
  preconditions/postconditions.
- **Implementation file** (`.cpp`): the actual code. Must `#include` its
  own header file.
- `#include` quoting: user-defined headers in double quotes
  (`"myHeader.h"`), system headers in angle brackets (`<iostream>`).
- **Precondition**: what must be true before the function is called.
- **Postcondition**: what is true after the function call completes.

## Static members of a class

- `static` marks a function or variable member as belonging to the
  **class itself**, not to any one object.
- A public static member is accessed via `ClassName::member`, no object
  needed.
- A static member variable exists even if **no object** of that class
  has ever been created.
- Non-static (instance) member variables: every object has its own
  separate copy. Static member variables: exactly **one** copy shared by
  every object of the class — changing it through one object is visible
  through all others.

## Do not forget

- Class definitions end with a semicolon after the closing brace.
- Only `.` (member access) and `=` (assignment) work on class objects
  without overloading.
- Pass large objects by `const &`, not by value or plain reference.
- A parameterised constructor without an explicit default constructor
  removes C++'s auto-supplied default — a no-argument declaration then
  fails to compile.
- Exactly one destructor per class, no parameters, name `~ClassName()`.
- `static` members belong to the class, not to individual objects.
