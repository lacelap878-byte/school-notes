---
module: CSC01B1
topic: Object Composition and Inheritance
session: S4
tags: [definition, worked-example, common-mistake, added]
---

# CSC01B1 — Object Composition and Inheritance

Source: the Object Composition slide deck (31 slides, anchored OA) blended
with CSC01B12026L3.pdf, Has-a and Is-a Relationships (43 slides, anchored
L3).

## OOD foundations and identifying classes

OOP applies divide and conquer: a problem is decomposed into interacting
objects, and design quality comes down to how well those objects are
chosen — objects communicate with each other by message passing. A class
is built from a class name, attributes (the object's state), operations
(member functions), and associations with other classes (the pathways
those messages travel along).

The standard way in, from a plain problem description, is the nouns/verbs
technique: nouns become candidate classes, verbs tied to a single entity
become operations, relationships between objects become associations.

**Worked example (source, OA slide 6):** a Student class — attributes
`facts` (a Knowledge type) and `studentNumber`; operations `study`,
`writeExams`; association: a student *has* knowledge.

Not every noun earns its own class, though. A fuller worked example
(source, L3 slides 34–38) walks through a `cylinderType`: the dimensions,
surface area, and volume are all characteristics of the cylinder, not
separate classes. For each real candidate class, settle three things —
what operations an object can perform on itself, what operations can be
performed on it, and what information it must maintain. For `cylinderType`
that gives `input`, `calculate`, `print` as operations, with the
dimensions as its data.

> [!note] The nouns/verbs method is one OOD technique among several in the
> literature, not the only correct approach — don't treat it as a
> universal algorithm.

## UML class diagrams

The three-compartment box and the `+`/`-`/`#` visibility notation were
already built out in full in [[CSC01B1_Notes_S3_Classes-Data-Abstraction]]
(worked with `clockType`) — not repeated here. New in this deck: a class
diagram represents the *static structure* of a design only, it does not
model communication between objects.

What is new here is showing **inheritance** on a diagram. Each class still
gets its own three-compartment box, but the inheritance relationship
itself is drawn as a plain arrow from the derived class box up to the base
class box.

**Worked example (source, L3 slides 16–17):**
```
rectangleType
-length: double
-width: double

+setDimension(double, double): void
+getLength() const: double
+getWidth() const: double
+area() const: double
+perimeter() const: double
+print() const: void
+rectangleType()
+rectangleType(double, double)
```
`boxType` is derived from `rectangleType` by public inheritance, and
overrides `print` and `area`:
```
boxType
-height: double

+setDimension(double, double, double): void
+getHeight() const: double
+area() const: double
+volume() const: double
+print() const: void
+boxType()
+boxType(double, double, double)
```
```
rectangleType
     ^
     |
  boxType
```

## Relationship types and association

Instances of your classes interact in a handful of standard ways:
**association** (communicates with), **containment** (has-a / whole-part,
split into aggregation and composition), and **generalisation** (is-a).
The next two sections build out containment and generalisation in full;
association is the simplest of the three — one instance just sends a
message to an instance of another class, with no ownership or lifetime tie
created between them.

**Worked example (source, OA slides 15–16):** a `Student` sends a question
message to a `Lecturer`.
```cpp
void Student::study(int hours)
{
    while(hours > 0)
    {
        Questions q = codeForAnHour(hours);
        if(q)
        {
            Lecturer l;
            facts += l.answerQuestion(q);
        }
    }
}
```

## Composition and aggregation (has-a)

Both are containment relationships: one or more members of a class are
objects of another class type. The deciding question is life-span: does
the containing object's life-span govern the contained object's life-span?
If yes, that's **composition** (example: a Person has a brain). If the
contained object can outlive the container, that's **aggregation**
(example: a Course has Students, and the students survive when the course
ends).

Member-objects under composition are constructed in the order they are
*declared* in the class, not the order listed in the constructor's member
initialisation list, and they finish constructing before the containing
object's own constructor body runs. Arguments to a member-object's
constructor go in the heading of the containing class's own constructor
definition.

**Worked example: composition and delegation (source, OA slides 19–24)**
```cpp
class Worker            //This class will do the actual work
{
public:
    Worker();
    void work();
private:
    string algorithm;   //Data for work
};

class Manager
{
public:
    Manager();          //This will create a worker
    void work();         //Passed on to the worker
    ~Manager();          //This will destroy the worker
private:
    Worker* minion;      //Composition
};

Worker::Worker()
{
    algorithm = "Work work work";
}
void Worker::work()
{
    for(int k = 0; k < 100; k++)
        cout << algorithm << endl;
}

Manager::Manager()
{
    minion = new Worker;    //Create a worker
}
Manager::~Manager()
{
    delete minion;          //End of Manager: end of Worker
}
void Manager::work()
{
    minion->work();         //This is the act of delegation
}

int main()
{
    Manager m;
    m.work();
    return 0;
}
```
**Delegation** is when the containing class passes its own work on to a
contained class (`Manager::work` just forwards to `minion->work()`). Here
it rides on composition: the Manager's lifetime governs the Worker's, so
the Worker is created in Manager's constructor and destroyed in Manager's
destructor.

**Worked example: aggregation (source, OA slides 26–29)**
```cpp
class Course
{
public:
    void addStudent(Student* s);
    void removeStudent(int studentNumber);
    void assignWork();
private:
    vector<Student*> students;
};

void Course::addStudent(Student* s)
{
    students.push_back(s);
}
void Course::removeStudent(int studentNumber)
{
    for(unsigned int k = 0; k < students.size(); k++)
    {
        Student* sp = students[k];
        if(sp->getStudentNumber() == studentNumber)
            students.erase(students.begin() + k);
    }
}
void Course::assignWork()
{
    for(unsigned int k = 0; k < students.size(); k++)
        students[k]->work();   //Delegation
}
```
> [!warning] `Course` stores pointers and never deletes them in its own
> destructor — that absence is exactly what makes this aggregation rather
> than composition, the students survive the course. If you catch
> yourself writing a `delete` in a class that's meant to be aggregation,
> you've accidentally written composition instead.

## Inheritance (is-a)

Inheritance is the is-a relationship (example: every employee *is a*
person). It creates new classes from existing ones: the **derived class**
is the new one, the **base class** is the original — building on what
already exists rather than rewriting it.

- **Single inheritance:** a derived class has exactly one base class.
- **Multiple inheritance:** a derived class has more than one base class.
- **Public inheritance:** every public member of the base class is
  inherited as a public member of the derived class.

> [!warning] (added) The diamond problem. Not covered in either source
> deck, but it's the standard hazard multiple inheritance runs into: if
> classes B and C both inherit from A, and class D inherits from both B
> and C, then D ends up with two separate copies of A's members, one via
> B and one via C. A reference like `d.someAMember` becomes ambiguous,
> the compiler can't tell which path you mean, and it won't compile until
> you resolve it. C++'s fix is virtual inheritance —
> `class B : virtual public A` and `class C : virtual public A` — which
> makes B and C share a single A subobject instead of each carrying their
> own, so D only ever sees one copy.
#common-mistake #added

Inheritance forms a tree-like hierarchy:
```
        shape
       /     \
   circle   rectangle
                |
              square
```

**Derived class syntax (source, L3 slide 13):**
```cpp
class className: memberAccessSpecifier baseClassName
{
    member list
};
```
`memberAccessSpecifier` is `public`, `protected`, or `private` (private is
the default if nothing is stated).

> [!warning] Private members of a base class stay private to the base
> class — a derived class cannot directly access them, no matter what
> `memberAccessSpecifier` is used. That specifier controls what happens to
> the base class's *public* and *protected* members on the way in, not
> whether private members leak through.

What the derived class gains: public members of the base class can be
inherited as either public or private members of the derived class
(depending on `memberAccessSpecifier`); the derived class can add its own
new members on top; the derived class can redefine a public member
function of the base class, but that redefinition only applies to objects
of the derived class; and every member variable of the base class is also
a member variable of the derived class.

## Redefining base class functions, and derived-class constructors/destructors

To redefine (override) a public member function, the corresponding
function in the derived class must have the same name, and the same
number and types of parameters, as the base class version. Overriding
replaces which version runs for derived-class objects, but the base
class's own version still exists and is still reachable.

**Calling the overridden base class version explicitly (source, L3 slide 15):**
```cpp
BaseClassName::functionName(argument list)
```
This is the same `::` operator used to implement a member function outside
its class (defined in: [[CSC01B1_Notes_S3_Classes-Data-Abstraction]]),
here it disambiguates *which class's* version of an overridden name you
mean, rather than which class a definition belongs to.

**Constructors of derived and base classes:** a derived class constructor
cannot directly access private members of the base class, it can directly
initialise only the base class's public member variables. When a derived
class object is declared, it must execute one of the base class's
constructors, and that call is specified in the heading of the derived
class constructor's own definition — the same member initialisation-list
pattern used for composition above.

**Destructors in a derived class:** a destructor deallocates any dynamic
memory the objects of a class allocated. When a derived class object goes
out of scope, its destructor is automatically invoked; when that derived
class destructor finishes executing, it automatically invokes the base
class's own destructor in turn.

## Header files, protected members, and access

New classes are defined in new header files, same as any class; to create
a derived class, the header file includes a command specifying where the
base class's own definition can be found, and member function definitions
can still be placed in a separate file. The preprocessor command
`#include` brings a header file into a program (the preprocessor runs
before compilation), and certain preprocessor commands placed in the
header file itself stop a file being included more than once (not
detailed further in the source).

A derived class cannot directly access private members of its base class.
To give it direct access, declare that member **protected** instead of
private.

**Access table for public, protected, private inheritance (source, L3 slides 25–27)**

Assume class B is derived from class A.

| `memberAccessSpecifier` | A's public members become... | A's protected members become... | A's private members |
|---|---|---|---|
| public | public in B, directly accessible | protected in B, accessible by B's member/friend functions | hidden in B, reachable only through A's own public/protected members |
| protected | protected in B, accessible by B's member/friend functions | protected in B, accessible by B's member/friend functions | hidden in B, reachable only through A's own public/protected members |
| private | private in B, accessible by B's member functions | private in B, accessible by B's member/friend functions | hidden in B, reachable only through A's own public/protected members |

> [!note] Across all three specifiers, a base class's private members are
> never directly reachable from the derived class — they only ever come
> in through the base class's own public or protected members. What
> changes with the specifier is the access *level* of the inherited
> public/protected members inside B, not whether private members leak
> through.

## The C++ stream class hierarchy

`ios` is the base class for every stream class, and holds the formatting
flags plus the member functions to access and modify those flags.
```
              ios
             /   \
        istream   ostream
           |          |
       ifstream   ofstream
```
`istream` and `ostream` provide the operations for moving data between
memory and devices: `istream` defines the extraction operator `>>` along
with `get` and `ignore`, `ostream` defines the insertion operator `<<`
(the one `cout` itself uses). `ifstream` and `ofstream` are for file I/O
specifically, and their definitions live in the header file `fstream`.

This is the same is-a chain from the Inheritance section playing out in a
library you already use constantly: `ifstream` is-an `istream` is-an
`ios`, which is exactly why an `ifstream` object can already use `>>`
without redefining it.

## The three OOD/OOP principles

- **Encapsulation:** combines data and the operations on that data into a
  single unit.
- **Inheritance:** creates new classes from existing classes (see above).
- **Polymorphism:** the ability to use the same expression to denote
  different operations.

In OOD the object is the fundamental entity, debugging happens at the
class level, and a program is a collection of interacting objects. OOD
encourages code reuse; OOP is what actually implements OOD's ideas in a
language, and C++ supports OOP through classes. Objects are created when
class variables are declared, and they interact via function calls.

Polymorphism in C++: function names and operators can be overloaded, and
a polymorphic function or operator is one with many forms (example:
division behaves differently for floating point operands versus integer
operands). Templates provide parametric polymorphism. Virtual functions
implement polymorphism across an inheritance hierarchy specifically,
allowing the right member function to be selected at run time.

Every object has an internal state and an external state: private members
form the internal state, public members form the external state.

> [!note] Only the object itself can manipulate its own internal state —
> this is encapsulation in practice, not just a definition. The
> private/public split that runs through every class in this session is
> what actually enforces it.

## Do not forget

- The has-a decision hinges on life-span: composition if the container
  governs the contained object's lifetime, aggregation if it doesn't.
- A private base class member is never directly reachable from a derived
  class under any `memberAccessSpecifier` — only public/protected members
  pass through, and the specifier changes their level in the derived
  class, not their reachability.
- `BaseClassName::functionName(...)` is how you reach an overridden base
  class function from inside a derived class.
- A derived class object executes a base class constructor first, and a
  derived class destructor triggers the base class destructor after it.
- `ifstream`/`ofstream` are a real, everyday is-a chain: they inherit
  `>>`/`<<` from `istream`/`ostream` rather than redefining them.

## See also

- [[CSC01B1_Notes_S3_Classes-Data-Abstraction]] — UML notation basics and
  the scope resolution operator, both assumed known in this session.
