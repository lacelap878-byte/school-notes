---
module: CSC01B1
topic: Operator Overloading and Templates
session: S6
tags: [definition, worked-example, common-mistake, exam-flagged, struggle]
---

# Operator Overloading and Templates

Lecture 5 covers two related generic-code tools in C++: **operator overloading**, which extends operators to work with class objects, and **templates**, which write one code body for a family of functions or classes.

## Why Operator Overloading Is Needed

A class only gets you so far with named member functions. For a `clockType` object you can write `myClock.printTime()`, `myClock.incrementSeconds()`, or `if (myClock.equalTime(yourClock))`, but some operations read far more naturally as operators: `myClock++`, or `if (myClock == yourClock)`. #definition

> [!note] What C++ gives a class for free
> Assignment (`=`) and member selection (`.`) are the **only** operators a class object gets automatically. Every other operator cannot be applied directly to a class object until you overload it.

**Operator overloading** extends the definition of an operator so it also works with a user-defined data type. Most existing C++ operators can be extended this way, but **no new operators can ever be created**, only new meanings given to ones that already exist. #exam-flagged

An **operator function** is the function that overloads an operator. Its name is the reserved word `operator` followed by the operator's symbol.

### Syntax for Operator Functions
```cpp
returnType operator operatorSymbol(formal parameter list)
```
- It is a value-returning function; `operator` is a reserved word.
- To overload an operator for a class: include the operator function declaration in the class definition, then write the definition of the operator function.

### Restrictions on Operator Overloading
Fixed no matter what you overload:
- precedence and associativity cannot change
- default parameters cannot be used
- the number of parameters cannot change
- no new operators can be invented

> [!warning] Five operators can never be overloaded #exam-flagged
> `.`  `.*`  `::`  `?:`  `sizeof`

How an operator works on built-in types stays the same; you only add new meaning for user-defined objects, or for a mix of user-defined and built-in operands.

## The `this` Pointer and Friend Functions

Every object of a class maintains a **hidden pointer to itself called `this`**. When an object invokes a member function, `this` is what the member function uses to refer back to the invoking object. #definition

A **friend function** of a class is a nonmember function that still gets access to all the class's members, including its private ones. #definition Declared inside the class definition using the reserved word `friend` in the function prototype:
```cpp
class classIllusFriend
{
    friend void two(/*parameters*/);
    .
    .
    .
};
```
When writing the friend function's own definition, the word `friend` does **not** appear, and neither does the class name or the scope resolution operator (`::`), since a friend is not a member of the class:
```cpp
void two(/*parameters*/)
{
    .
    .
    .
}
```
> [!note] A friend function looks exactly like an ordinary standalone function; only its prototype inside the class (with `friend`) marks it as having special access.

This access is exactly what lets a nonmember operator function reach into a class's private data — which is what decides whether an overloaded operator has to be a member or a friend.

## Operator Functions as Member vs Nonmember Functions

Four operators can **only ever** be overloaded as a member of the class: `()`, `[]`, `->`, and `=`. #exam-flagged

For any other operator `op` overloaded for a class `opOverClass`, one rule decides member vs nonmember:

> [!important] Member vs friend rule #exam-flagged
> If the leftmost operand of `op` is an object of a **different type**, the overloading function must be a **nonmember (friend)**.
> If the overloading function for `op` is a **member** of `opOverClass`, then whenever `op` is applied to objects of type `opOverClass`, the leftmost operand must itself be of type `opOverClass`.

The leftmost operand's type is what decides member vs friend — this is the rule to reach for whenever a question asks "should this be a member or a friend function?"

### Overloading Binary Operators
Take `#` as a stand-in for any binary operator (e.g. `+` or `==`) being overloaded for `rectangleType`: it can be overloaded either as a member function of the class or as a friend function.

**As a member function** — only one explicit parameter, since the left operand is the invoking object itself, reached through the implicit `this`:
```cpp
// prototype (in class definition)
returnType operator#(const className&) const;

// definition
returnType className::operator#
                        (const className& otherObject) const
{
    //algorithm to perform the operation

    return value;
}
```

**As a friend function** — takes both operands explicitly:
```cpp
// prototype (in class definition)
friend returnType operator#(const className&,
                             const className&);

// definition
returnType operator#(const className& firstObject,
                            const className& secondObject)
{
    //algorithm to perform the operation

    return value;
}
```
Compare the two forms: a friend takes both operands as parameters and drops the `className::` qualifier and the trailing `const`, since it is not a member of the class.

## Overloading `<<` and `>>`

Take the expression `cout << myRectangle;` — the leftmost operand is an `ostream` object, not a `rectangleType` object. By the member-vs-nonmember rule above, this **forces** the operator function that overloads `<<` for `rectangleType` to be a friend function. The same reasoning applies to `>>`.

**Stream insertion (`<<`):**
```cpp
friend ostream& operator<<(ostream&, const className&);

ostream& operator<<(ostream& osObject, const className& cObject)
{
    //local declaration, if any
    //Output the members of cObject.
    //osObject << . . .

    //Return the stream object.
    return osObject;
}
```
Returns a reference to the stream object — this is what makes chaining (`cout << a << b;`) possible.

**Stream extraction (`>>`):**
```cpp
friend istream& operator>>(istream&, className&);

istream& operator>>(istream& isObject, className& cObject)
{
        //local declaration, if any
        //Read the data into cObject.
        //isObject >> . . .

        //Return the stream object.
    return isObject;
}
```
> [!warning] `cObject` is **not** `const` here, unlike every other overload in this lecture, because `>>` has to write into it. #exam-flagged

## Overloading the Assignment Operator (=)
```cpp
// prototype
const className& operator=(const className&);

// definition
const className& className::operator=
                                (const className& rightObject)
{
        //local declaration, if any
    if (this != &rightObject)  //avoid self-assignment
    {
        //algorithm to copy rightObject into this object
    }
        //Return the object assigned.
    return *this;
}
```
The `if (this != &rightObject)` check guards against self-assignment (`x = x;`); without it, an assignment operator that frees memory before copying could destroy the source object before it's copied. Assignment must always be a member function.

> [!question]- Struggle: does `myClock = yourClock;` even need an overload? #struggle
> **Yes, it works without writing anything**, because `=` is one of the two operators every class gets for free from the compiler (see the note at the top of this file). The compiler-supplied `operator=` performs a **memberwise copy**: each data member of `yourClock` is copied into the corresponding member of `myClock`, one at a time.
>
> **Does memberwise copy respect access specifiers?** No — `public`/`private`/`protected` only control access from *outside* the class. The compiler-generated `operator=` is part of the class's own machinery, so it copies **every** data member regardless of access level. If `hr`, `min`, `sec` are `private`, they still all get copied; you just couldn't reach them directly with `myClock.hr = yourClock.hr;` from outside code.
>
> **So does every class have to overload operator overloading?** No — that's a misconception worth correcting directly. Only `=` and `.` are automatic; every other operator overload (`+`, `==`, `<<`, `++`, ...) is purely optional, added only when it makes the class more convenient to use. The **one case where overloading `=` becomes mandatory** is covered next.

## Overloading Unary Operators
- **Member function**: takes no parameters — the one operand is the invoking object itself, via `this`.
- **Nonmember (friend) function**: takes exactly one parameter — there's no invoking object to supply it implicitly.

## Overloading `++` and `--`

These are worked through in full for `++`; `--` follows the exact same pattern in each of the four forms below.

**Pre-increment, member function** — only one object involved. The invoking object is incremented, then `*this` (same object, now updated) is returned:
```cpp
className operator++();

className className::operator++()
{
    //increment the value of the object by 1
    return *this;
}
```

**Pre-increment, friend function:**
```cpp
friend className operator++(className&);

className operator++(className& incObj)
{
    //increment incObj by 1
    return incObj;
}
```

**Post-increment, member function** — note the dummy `int` parameter, which exists only to distinguish this overload from pre-increment and is never used in the body:
```cpp
className operator++(int);

className className::operator++(int u)
{
    className temp = *this;    //use this pointer to copy
                                //the value of the object
    //increment the object

    return temp;  //return the old value of the object
}
```

**Post-increment, friend function**, same dummy-`int` trick, object passed explicitly:
```cpp
friend className operator++(className&, int);

className operator++(className& incObj, int u)
{
    className temp = incObj; //copy incObj into temp

    //increment incObj

    return temp;  //return the old value of the object
}
```

> [!example]- Why post-increment needs two objects but pre-increment needs one #worked-example
> **Pre-increment** has no `temp`: the object is incremented first, then the *same*, now-updated object is returned via `*this`. One object, one state, in and out.
>
> **Post-increment** creates two objects on purpose:
> 1. `temp` — a copy made **before** anything changes, holding the object's *old* value
> 2. the real invoking object (`*this`, or `incObj` in the friend form) — this is the one that actually gets incremented
>
> The function then `return temp;`, **not** `*this`. The caller receives the old value, while the real object has already moved on to the new value.
>
> This mirrors plain `int` behaviour: `int y = x++;` leaves `y` holding the old value of `x` while `x` itself is incremented. `temp` plays the role of `y`; the object itself plays the role of `x`. Pre-increment skips the copy entirely because `++x`'s result *is* the new value, so returning `*this` directly is correct — and cheaper, since no copy is made.

> [!important] The one detail that tells the four forms apart #exam-flagged
> The unused `int` parameter in the prototype is the *only* thing distinguishing post- from pre-increment in the signature. And by return value: post-increment always returns the saved copy (`temp`); pre-increment always returns the object itself, after incrementing it.

## Operator Overloading: Member vs Nonmember as a Design Choice

Outside the operators forced one way or the other (`()`, `[]`, `->`, `=` must be members; `<<`, `>>` must be friends), some operators genuinely can go either way, and the choice becomes a design decision.

Binary arithmetic operators like `+` are the clearest example:
- **As a member**, `operator+` has direct access to the data members of one object (the invoking object, via `this`) and only needs the *other* object passed in as a parameter.
- **As a friend**, there's no invoking object, so both objects must be passed in as parameters — the resulting code can be somewhat clearer, since both operands are named explicitly and symmetrically.

| | Member function | Nonmember (friend) function |
|---|---|---|
| Parameters needed | one (the other operand) | two (both operands) |
| Access to left operand | via `this`, implicit | via a named parameter |
| Forced for | `()` `[]` `->` `=` | `<<` `>>` (left operand isn't the class) |
| Free choice for | `+`, `==`, and most other binary operators | same |

## Classes and Pointer Member Variables (Revisited)

The default (compiler-supplied) assignment operator copies member variables from one object to another of the same type — a memberwise copy. This does **not** work well when a member variable is a pointer, since it copies the *address*, not the data pointed to.

> [!warning] Mandatory overload trigger #exam-flagged #common-mistake
> Any class with pointer member variables **must** explicitly handle three things together:
> 1. overload the assignment operator (`=`)
> 2. include a copy constructor
> 3. include a destructor
>
> Fixing only one of the three still leaves the others doing the broken default — and the destructor is in the set because it's what eventually double-frees the shared pointer if the other two aren't fixed.

> [!question]- Struggle: isn't `=` "combined with" the copy constructor? #struggle
> No — they're two separate functions, triggered in two different situations:
> - **Copy constructor**: runs when a **new** object is being created from an existing one (`clockType c2 = c1;`, pass-by-value, return-by-value).
> - **Assignment operator**: runs when assigning into an object that **already exists** (`myClock = yourClock;`, where `myClock` was constructed earlier).
>
> They're grouped together in the pointer-member rule above only because both *default* to memberwise copy, and both fail for the same reason under pointer members — not because one does the other's job.

## Operator Overloading: One Final Word

If an operator `op` is overloaded for a class, using `op` on objects of that class runs the body of the function that overloads `op` for it. Whatever code is placed in that body is therefore exactly what executes — there is no hidden default behaviour once an operator is overloaded; the overload's body **is** the operator's entire behaviour for that type.

## Overloading the Array Index (Subscript) Operator (`[]`)

Recall `[]` is one of the four operators that **must** be a member function — there's no friend-function alternative to weigh against it, unlike `+` or `<<`.

```cpp
// nonconstant arrays
Type& operator[](int index);

// constant arrays
const Type& operator[](int index) const;
```

> [!question]- Struggle: why does `[]` need two versions? #struggle
> The compiler picks between them based on whether the object being indexed is `const` at the call site:
> - a **plain (nonconstant)** object calls the first version, returning `Type&` — modifiable, so `myArray[2] = 10;` works.
> - a **`const`** object (or a `const` reference/pointer to one) calls the second version, returning `const Type&` — read-only.
>
> **If only the nonconst version existed**: any `const` object of the class could no longer be indexed at all, since a nonconst member function can't be called on a `const` object — code that receives the array by `const&` and reads `arr[i]` would fail to compile.
>
> **If only the const version existed**: every object, even ordinary modifiable ones, would only ever hand back read-only access, so `myArray[2] = 10;` would fail to compile everywhere.
>
> The pairing exists so `[]` behaves correctly regardless of whether the object itself is `const`, the same way the built-in array subscript does.

## Function Overloading (recap)

Overloading a function means writing several functions that share the same name but differ in their parameter lists. The parameter list of the call determines which overloaded version executes. Each version needs its own full definition — overloading a name doesn't let one definition stand in for several.

## Templates

A **template** is a single code body written once for a whole set of related functions (a **function template**) or classes (a **class template**). #definition

```cpp
template <class Type>
declaration;
```
- `class` here doesn't mean "class" in the OOP sense — it just introduces the template parameter, and accepts any user-defined *or* built-in type.
- `Type` is a formal parameter of the template, in the same sense a variable is a formal parameter of a function: where a function's parameters are variables, a template's parameters are **data types**.

### Function Templates
```cpp
template <class Type>
function definition;
```
`Type`, once supplied, is used throughout the definition to: specify the type of the function's parameters, specify the return type, and declare variables inside the function body.

### Class Templates
A class template is a single code segment for a set of related classes — also called **parameterized types**. #definition
```cpp
template <class Type>
class declaration
```
- A template instantiation can be created with either a built-in or a user-defined type.
- The function members of a class template are themselves considered function templates.

### Header File and Implementation File of a Class Template

> [!important] Key asymmetry #exam-flagged
> Passing a parameter to an ordinary function takes effect at **run time**. Passing a parameter to a class template takes effect at **compile time**.

Consequence: the implementation file of a class template **cannot** be compiled independently of the client code that uses it. Layout options:
- put the class definition and function template definitions directly in the client code
- put the class definition and function template definitions together in the same header file
- put them in **separate files**, with an include directive to the implementation file placed at the **end** of the header file

Whichever layout is used, the function definitions and the client code end up compiled together.

## Do Not Forget
- Only `=` and `.` are free on a class; every other operator overload is a choice, except when pointer members force `=` + copy constructor + destructor together.
- Five operators can never be overloaded: `.` `.*` `::` `?:` `sizeof`.
- `()`, `[]`, `->`, `=` must be members; `<<`, `>>` must be friends (leftmost operand isn't the class type).
- The dummy `int` parameter is the only signature difference between pre- and post-increment; post-increment returns the saved copy, pre-increment returns the updated object itself.
- `[]` needs both a const and nonconst overload so it works whether the object itself is const.
- Copy constructor fires on creation of a new object from an existing one; assignment fires on an already-existing object. Both default to memberwise copy, both break under pointer members.
- Template parameters are resolved at **compile time**, which is why template implementation files can't be compiled independently of client code.
