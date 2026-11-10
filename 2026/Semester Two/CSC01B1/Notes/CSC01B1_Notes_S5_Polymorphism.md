---
module: CSC01B1
topic: Polymorphism
session: S5
tags: [definition, worked-example, common-mistake, struggle, added]
---

# Polymorphism

## Core definitions

**Polymorphism**: associating many meanings to one function name. Virtual
functions provide this capability, and it is a fundamental principle of
object oriented programming.

**Virtual**: existing in "essence" though not in fact.

**Virtual function**: a function that can be "used" before it is
"defined".

These three are worth knowing precisely, the rest of the topic is built
on them.

## The problem virtual functions solve

The motivating case is a set of figure classes (Rectangle, Circle, Oval,
etc.) all deriving from one parent class Figure, each needing its own
`draw()` logic. Giving each class its own `draw()` is unremarkable on its
own:

```cpp
Rectangle r;
Circle c;
r.draw();  // Calls Rectangle class's draw
c.draw();  // Calls Circle class's draw
```

The trouble starts when the parent class itself needs to call `draw()`.
`Figure::center()` erases a figure and redraws it, so it must call
`draw()`, but Figure cannot know in advance which derived class's
`draw()` that should be.

> [!warning] The real trap
> A new class, say Triangle, derived from Figure *after* `center()` was
> already written and compiled, still inherits `center()`. That inherited
> `center()` must end up calling `Triangle::draw()`, not `Figure::draw()`,
> even though `Figure::center()` was compiled before Triangle existed and
> cannot possibly know about it.

**Virtual functions** are the fix. Marking a function virtual tells the
compiler: do not decide which version to run yet, wait until the
function is actually called at runtime, then take the implementation
from the real object instance. This mechanism is called **late binding**
(or dynamic binding), and virtual functions are how C++ implements it.

## Worked implementation: Sale and DiscountSale #worked-example

A more thorough example, an automotive parts sales program. Only regular
retail sales exist at first, but discount sales and others will be added
later, each computing a bill differently, so "compute a bill" is made
virtual from the outset.

```cpp
class Sale {
public:
   Sale();
   Sale(double thePrice);
   double getPrice() const;
   virtual double bill() const;
   double savings(const Sale& other) const;
private:
   double price;
};
```

```cpp
double Sale::savings(const Sale& other) const {
   return ( bill() - other.bill() );
}
```

Sale on its own represents a single item with no discounts or charges.
Only `bill()` is virtual, not `savings()`, because `savings()` is meant
to pick up whichever `bill()` belongs to the actual object, and marking
`bill()` virtual is exactly what makes that possible.

```cpp
class DiscountSale : public Sale {
public:
   DiscountSale();
   DiscountSale(double thePrice, double theDiscount);
   double getDiscount() const;
   void setDiscount(double newDiscount);
   double bill() const;
private:
   double discount;
};
```

```cpp
double DiscountSale::bill() const {   // No virtual qualifier
   double fraction = discount/100;
   return (1 - fraction)*getPrice();
}
```

A virtual function in the base class is automatically virtual in every
derived class. The derived class's declaration and definition are not
required to repeat `virtual` (the definition never takes it regardless),
though the declaration is usually written with it anyway, purely for
readability.

Because `bill()` is virtual, `DiscountSale::bill()` is used for every
DiscountSale object instead of falling back to Sale's version. Sale,
including `savings()`, was written and compiled before DiscountSale
existed, yet:

```cpp
DiscountSale d1, d2;
d1.savings(d2);
```

resolves the `bill()` call inside `savings()` to DiscountSale's version.
This is late binding at work: the compiler waits until the function is
actually called, then decides which definition to use based on the
calling object.

## Overriding vs redefining

- Changing a **virtual** function's definition in a derived class is
  called **overriding**.
- Changing a **non-virtual** (standard) function in a derived class is
  called **redefining** (see: [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance#Redefining a public base class member function]]).

The two terms signal whether late binding is involved: overriding is
virtual, redefining is not.

## The cost of virtual

Virtual functions carry real overhead: more storage, and late binding
decides things "on the fly" at runtime, which slows programs down. A
function should not be made virtual unless it is actually needed.

## Pure virtual functions and abstract base classes

Sometimes a base class cannot give a meaningful definition for one of
its own members, because its whole purpose is to be derived from. Figure
is the case in point, every real figure is an object of some derived
class, and Figure itself has no idea how to draw. The fix is a **pure
virtual function**:

```cpp
virtual void draw() = 0;
```

The `= 0` is what makes a virtual function pure: the function has no
definition at all in this class.

- A pure virtual function requires no definition, and forces every
  derived class to define its own version.
- A class with one or more pure virtual functions is an **abstract base
  class**. It can only be used as a base class, no object can ever be
  created directly from it, since it lacks complete definitions of all
  its members.
- If a derived class fails to define even one inherited pure virtual
  function, that derived class is itself an abstract base class too.
  Abstractness only ends once every pure virtual function in the
  inheritance line has a real definition somewhere.

## Extended type compatibility and the slicing problem #common-mistake

If Derived is a derived class of Base, a Derived object can be assigned
to a Base object, never the reverse. In the Sale/DiscountSale example, a
DiscountSale "is a" Sale, but a Sale is not necessarily a DiscountSale.

### Worked example: Pet and Dog

```cpp
class Pet {
public:
   string name;
   virtual void print() const;
};
class Dog : public Pet {
public:
   string breed;
   virtual void print() const;
};
```

```cpp
Dog vdog;
Pet vpet;
```

(member variables are public here only to keep the example short, this
is not typical style)

Anything that "is a" Dog "is a" Pet:

```cpp
vdog.name = "Tiny";
vdog.breed = "Great Dane";
vpet = vdog;             // legal, assigning up
```

Values can be assigned up to the parent type, never down. A Pet "is
not" necessarily a Dog.

### The slicing problem

After `vpet = vdog;`, vpet has lost its breed field entirely.
`cout << vpet.breed;` produces an error, since Pet's type has no breed
member at all. This loss is the **slicing problem**. It is a genuine
nuisance in C++: the object still "is" a Great Dane named Tiny, and
there are real cases where breed still needs to be reachable even while
the object is being handled as a Pet.

> [!example] The fix: pointers to dynamic variables
> ```cpp
> Pet *ppet;
> Dog *pdog;
> pdog = new Dog;
> pdog->name = "Tiny";
> pdog->breed = "Great Dane";
> ppet = pdog;
> ```
> `ppet->breed` is still illegal (Pet's interface has no breed member),
> but a virtual function call through the pointer reaches the real
> object:
> ```cpp
> ppet->print();     // calls Dog::print(), because print() is virtual
> ```
> C++ waits to see what object ppet is actually pointing to before
> binding the call.

> [!warning] Why the pointer version does not lose breed (struggle, resolved S5)
> Plain assignment (`vpet = vdog;`) is a **value copy**: vpet is a
> separately allocated Pet-sized object, and Pet's assignment operator
> only knows about Pet's own members. It runs correctly and completely
> for a Pet, it is simply never told breed exists, so nothing is copied
> for it. The operator is not failing, it is scoped to the static type
> of the target variable.
>
> Pointer assignment (`ppet = pdog;`) copies an **address**, not an
> object. The full Dog object, allocated once on the heap via `new Dog`,
> still exists exactly as written, with breed intact. ppet is just a
> Pet-typed pointer looking at that same Dog object. The compiler
> refuses `ppet->breed` because Pet's interface does not expose it, but
> `ppet->print()` (virtual) uses late binding to run Dog::print(), which
> is written with full knowledge of breed and reaches it directly from
> inside the real Dog object it belongs to.

## Virtual destructors

Destructors are needed to de-allocate dynamically allocated data (see:
[[CSC01B1_Notes_S1_Foundation-Topics]]). Consider:

```cpp
Base *pBase = new Derived;
...
delete pBase;
```

This calls Base's destructor, even though pBase is actually pointing to
a Derived object, the same root issue as slicing: the pointer's declared
type, not the real object's type, decides what runs, unless something
forces late binding. Making the destructor virtual fixes this, the
correct derived class destructor runs instead.

> [!warning] Practice
> It is good policy to make all destructors virtual. If a base class is
> ever deleted through a base class pointer and its destructor is not
> virtual, whatever the derived class added risks leaking, since the
> derived destructor never runs.

> [!warning] Chained destructors do not cause a double free (struggle, resolved S5) (added)
> It is natural to worry that if `~Derived()` and `~Base()` both run in
> one chain, and both free memory, they might free the *same* memory
> twice. They do not, as long as each class only frees what it itself
> allocated.
>
> The reason is physical, not procedural: inheritance is composition
> under the hood. Every Derived object contains a complete, genuinely
> separate Base subobject in its own memory, including any private Base
> members (defined in: Access table, S4, access control only governs
> which code may *name* a member, not whether it exists or where it
> lives). So a Base pointer member and a Derived pointer member sitting
> in one Derived object are two distinct pointer variables at two
> distinct addresses, not a shared or referenced value.
>
> Construction runs Base's constructor first, then Derived's, each
> allocating its own resources. Destruction runs the reverse: Derived's
> destructor frees what Derived allocated, then Base's destructor
> automatically runs after it and frees what Base allocated, two
> different addresses, no overlap.
>
> A genuine double free is a different bug entirely: it comes from two
> pointers being set to the *same* address (aliasing), for example a
> derived constructor doing `pDerivedData = pBaseData;` instead of its
> own `new`. That is a data ownership mistake to fix at the design
> level, it is not caused by destructor chaining, and not caused by
> marking a destructor virtual.

## Casting

### Upcasting

```cpp
Pet vpet;
Dog vdog;
...
vdog = static_cast<Dog>(vpet);   // ILLEGAL!
```

Casting a Pet to be a Dog is not allowed. Casting the other way is fine:

```cpp
vpet = vdog;                      // Legal!
vpet = static_cast<Pet>(vdog);    // Also legal!
```

**Upcasting**, from a descendant type to an ancestor type, is always
okay.

### Downcasting

**Downcasting**, from an ancestor type to a descendant type, is
dangerous. It assumes information is being "added" that the ancestor
type never had. It can be done with `dynamic_cast`:

```cpp
Pet *ppet;
ppet = new Dog;
Dog *pdog = dynamic_cast<Dog*>(ppet);
```

Legal, but risky, and rarely done. Two conditions attach to it: every
bit of information assumed "added" by the derived type must actually be
tracked as valid, and every member function involved must be virtual.

## Inner workings of virtual functions

Using virtual functions correctly does not require knowing how they
work internally, this follows the principle of information hiding (see:
[[CSC01B1_Notes_S3_Classes-Data-Abstraction#Information hiding]]).

The compiler builds a **virtual function table** for any class with
virtual members. It holds a pointer for each virtual member function,
pointing to the location of the correct code for that function. Every
object of such a class also carries its own pointer, pointing to that
virtual function table. This table-of-pointers-plus-object-pointer pair
is the actual mechanism behind late binding: at the call, the object's
table pointer is followed to find which function body actually runs.

## Lecture summary

- Late binding delays the decision of which member function runs until
  runtime. C++ virtual functions use late binding.
- Pure virtual functions have no definition. A class with at least one
  is abstract, no objects can be created from it, it exists strictly as
  a base for others to derive from.
- Derived class objects can be assigned to base class objects (casting),
  but base class members are lost in the process, the slicing problem.
- Pointer assignment to dynamic objects allows a fix to the slicing
  problem.
- Making all destructors virtual is good practice, it ensures memory is
  correctly de-allocated.

## Do not forget

- Overriding is virtual, redefining is not (see: Overriding vs
  redefining).
- A virtual base function is automatically virtual in the derived
  override, the keyword is not required again but is usually written
  for readability.
- Plain object assignment slices, pointer assignment does not, because
  pointer assignment never copies the object.
- Upcasting is always safe, downcasting needs `dynamic_cast` and is
  still risky.
- Make destructors virtual whenever deletion might happen through a base
  class pointer.

## See also
- [[CSC01B1_Notes_S1_Foundation-Topics]]
- [[CSC01B1_Notes_S3_Classes-Data-Abstraction]]
- [[CSC01B1_Notes_S4_Object-Composition-and-Inheritance]]
