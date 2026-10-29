---
module: CSC01B1
topic: Operator Overloading and Templates
session: S6
tags: [definition, worked-example, common-mistake, exam-flagged, struggle, added]
---

# Operator Overloading and Templates

Lecture 5 covers two related generic-code tools in C++: **operator overloading**, which extends operators to work with class objects, and **templates**, which write one code body for a family of functions or classes.

> *A note on the dropdowns: those marked (added) come from the follow-up questions we worked through together, not from the lecture slides. The slides state the rules; the dropdowns explain why the rules hold. Expect the slide-level rules on a test first, and treat the dropdowns as the reasoning behind them.*

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

This access is exactly what lets a nonmember operator function reach into a class's private data, which is what decides whether an overloaded operator has to be a member or a friend.

> [!question]- Struggle (added, S12): a friend has no `this`, so where is the left operand? #struggle
> A member is called on an object, so `this` points to that object, the LEFT operand. In `a + b` written as a member, `this` is `a` and the parameter is `b`. A friend is an ordinary function, so there is no `this`. It takes both `a` and `b` as parameters. If you write the member form, you do not also pass the left object: the pointer already is the left object. Mixing the two (a member with two parameters, or a friend that uses `this`) is a compile error.

### The three const positions (added)
```cpp
const Money operator+(const Money& rhs) const;
//^ 1                 ^ 2               ^ 3
```
| Position | What it protects |
|---|---|
| 1. In front | The value that is returned cannot be changed |
| 2. Inside the brackets | The right operand is not changed |
| 3. Trailing | The left object, which is `this`, is not changed |

- A trailing const exists only on a member. A friend has no `this`, so there is nothing to protect.
- Assignment returns a reference to the left object, so it has no trailing const: `*this` is changed.
- Mistake made in S12: choosing "the returned element cannot be changed" for the trailing const. That is position 1. The trailing one protects the object the function is called on.

## Operator Functions as Member vs Nonmember Functions

Four operators can **only ever** be overloaded as a member of the class: `()`, `[]`, `->`, and `=`. #exam-flagged

For any other operator `op` overloaded for a class `opOverClass`, one rule decides member vs nonmember:

> [!important] Member vs friend rule #exam-flagged
> If the leftmost operand of `op` is an object of a **different type**, the overloading function must be a **nonmember (friend)**.
> If the overloading function for `op` is a **member** of `opOverClass`, then whenever `op` is applied to objects of type `opOverClass`, the leftmost operand must itself be of type `opOverClass`.

The leftmost operand's type is what decides member vs friend, this is the rule to reach for whenever a question asks "should this be a member or a friend function?"

> [!question]- Struggle (added): why can `m + 5.0` be a member but `5.0 + m` cannot? #struggle
> A member operator function is called *on* its left operand: `m + 5.0` is really `m.operator+(5.0)`. So the left operand has to be an object of the class. In `5.0 + m` the left operand is a `double`, which has no member functions to call, so the overload cannot be a member. It has to be a nonmember (friend) that takes both operands as parameters.
>
> ```cpp
> Money operator+(double) const;                       // member: handles  m + 5.0
> friend Money operator+(double, const Money&);        // nonmember: handles  5.0 + m
> ```
> If you want both orders to work, you need both overloads, and only the second one is forced to be a friend. The (Money, double) one could also be written as a friend; it just does not have to be.

### Overloading Binary Operators
Take `#` as a stand-in for any binary operator (e.g. `+` or `==`) being overloaded for `rectangleType`: it can be overloaded either as a member function of the class or as a friend function.

**As a member function**, only one explicit parameter, since the left operand is the invoking object itself, reached through the implicit `this`:
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

**As a friend function**, takes both operands explicitly:
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

Take the expression `cout << myRectangle;`, the leftmost operand is an `ostream` object, not a `rectangleType` object. By the member-vs-nonmember rule above, this **forces** the operator function that overloads `<<` for `rectangleType` to be a friend function. The same reasoning applies to `>>`.

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
Returns a reference to the stream object, this is what makes chaining (`cout << a << b;`) possible.

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

> [!question]- Struggle (added): does `myClock = yourClock;` even need an overload? #struggle
> **Yes, it works without writing anything**, because `=` is one of the two operators every class gets for free from the compiler (see the note at the top of this file). The compiler-supplied `operator=` performs a **memberwise copy**: each data member of `yourClock` is copied into the corresponding member of `myClock`, one at a time.
>
> **Does memberwise copy respect access specifiers?** No, `public`/`private`/`protected` only control access from *outside* the class. The compiler-generated `operator=` is part of the class's own machinery, so it copies **every** data member regardless of access level. If `hr`, `min`, `sec` are `private`, they still all get copied; you just couldn't reach them directly with `myClock.hr = yourClock.hr;` from outside code.
>
> **So does every class have to overload operator overloading?** No, that's a misconception worth correcting directly. Only `=` and `.` are automatic; every other operator overload (`+`, `==`, `<<`, `++`, ...) is purely optional, added only when it makes the class more convenient to use. The **one case where overloading `=` becomes mandatory** is covered next.

## Overloading Unary Operators
- **Member function**: takes no parameters, the one operand is the invoking object itself, via `this`.
- **Nonmember (friend) function**: takes exactly one parameter, there's no invoking object to supply it implicitly.

## Overloading `++` and `--`

These are worked through in full for `++`; `--` follows the exact same pattern in each of the four forms below.

**Pre-increment, member function**, only one object involved. The invoking object is incremented, then `*this` (same object, now updated) is returned:
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

**Post-increment, member function**, note the dummy `int` parameter, which exists only to distinguish this overload from pre-increment and is never used in the body:
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

> [!example]- (added) Why post-increment needs two objects but pre-increment needs one #worked-example
> **Pre-increment** has no `temp`: the object is incremented first, then the *same*, now-updated object is returned via `*this`. One object, one state, in and out.
>
> **Post-increment** creates two objects on purpose:
> 1. `temp`, a copy made **before** anything changes, holding the object's *old* value
> 2. the real invoking object (`*this`, or `incObj` in the friend form), this is the one that actually gets incremented
>
> The function then `return temp;`, **not** `*this`. The caller receives the old value, while the real object has already moved on to the new value.
>
> This mirrors plain `int` behaviour: `int y = x++;` leaves `y` holding the old value of `x` while `x` itself is incremented. `temp` plays the role of `y`; the object itself plays the role of `x`. Pre-increment skips the copy entirely because `++x`'s result *is* the new value, so returning `*this` directly is correct, and cheaper, since no copy is made.

> [!important] The one detail that tells the four forms apart #exam-flagged
> The unused `int` parameter in the prototype is the *only* thing distinguishing post- from pre-increment in the signature. And by return value: post-increment always returns the saved copy (`temp`); pre-increment always returns the object itself, after incrementing it.

## Operator Overloading: Member vs Nonmember as a Design Choice

Outside the operators forced one way or the other (`()`, `[]`, `->`, `=` must be members; `<<`, `>>` must be friends), some operators genuinely can go either way, and the choice becomes a design decision.

Binary arithmetic operators like `+` are the clearest example:
- **As a member**, `operator+` has direct access to the data members of one object (the invoking object, via `this`) and only needs the *other* object passed in as a parameter.
- **As a friend**, there's no invoking object, so both objects must be passed in as parameters, the resulting code can be somewhat clearer, since both operands are named explicitly and symmetrically.

| | Member function | Nonmember (friend) function |
|---|---|---|
| Parameters needed | one (the other operand) | two (both operands) |
| Access to left operand | via `this`, implicit | via a named parameter |
| Forced for | `()` `[]` `->` `=` | `<<` `>>` (left operand isn't the class) |
| Free choice for | `+`, `==`, and most other binary operators | same |

## Classes and Pointer Member Variables (Revisited)

The default (compiler-supplied) assignment operator copies member variables from one object to another of the same type, a memberwise copy. This does **not** work well when a member variable is a pointer, since it copies the *address*, not the data pointed to.

> [!warning] Mandatory overload trigger #exam-flagged #common-mistake
> Any class with pointer member variables **must** explicitly handle three things together:
> 1. overload the assignment operator (`=`)
> 2. include a copy constructor
> 3. include a destructor
>
> Fixing only one of the three still leaves the others doing the broken default, and the destructor is in the set because it's what eventually double-frees the shared pointer if the other two aren't fixed.

> [!question]- Struggle (added): isn't `=` "combined with" the copy constructor? #struggle
> No, they're two separate functions, triggered in two different situations:
> - **Copy constructor**: runs when a **new** object is being created from an existing one (`clockType c2 = c1;`, pass-by-value, return-by-value).
> - **Assignment operator**: runs when assigning into an object that **already exists** (`myClock = yourClock;`, where `myClock` was constructed earlier).
>
> They're grouped together in the pointer-member rule above only because both *default* to memberwise copy, and both fail for the same reason under pointer members, not because one does the other's job.

> [!question]- Struggle (added): what actually goes wrong with the default `=` on a pointer member? #struggle
> The default `=` always compiles and always runs. Nothing stops you from assigning objects that hold pointers. The problem is what it copies: the pointer's **address**, not the array it points to.
>
> ```cpp
> class IntArr {
> public:
>     IntArr(int n) : data(new int[n]) {}
>     ~IntArr() { delete [] data; }
> private:
>     int* data;
> };
>
> IntArr a(3), b(3);
> a = b;   // default =: a.data now holds the same address as b.data
>          // a's original array has no pointer left to it, so it is leaked
> // end of scope: ~b frees the shared array, then ~a frees the same array again
> ```
> Two separate faults come out of one assignment: a **leak** (a's old array is lost) and a **double free** (the shared array is deleted twice). Overloading `=` to copy the array contents fixes both, the copy constructor fixes the same problem for `IntArr c = a;`, and the destructor is the function that does the freeing.

## Operator Overloading: One Final Word

If an operator `op` is overloaded for a class, using `op` on objects of that class runs the body of the function that overloads `op` for it. Whatever code is placed in that body is therefore exactly what executes, there is no hidden default behaviour once an operator is overloaded; the overload's body **is** the operator's entire behaviour for that type.

## Overloading the Array Index (Subscript) Operator (`[]`)

Recall `[]` is one of the four operators that **must** be a member function, there's no friend-function alternative to weigh against it, unlike `+` or `<<`.

```cpp
// nonconstant arrays
Type& operator[](int index);

// constant arrays
const Type& operator[](int index) const;
```

> [!question]- Struggle (added): why does `[]` need two versions? #struggle
> The compiler picks between them based on whether the object being indexed is `const` at the call site:
> - a **plain (nonconstant)** object calls the first version, returning `Type&`, modifiable, so `myArray[2] = 10;` works.
> - a **`const`** object (or a `const` reference/pointer to one) calls the second version, returning `const Type&`, read-only.
>
> **If only the nonconst version existed**: any `const` object of the class could no longer be indexed at all, since a nonconst member function can't be called on a `const` object, code that receives the array by `const&` and reads `arr[i]` would fail to compile.
>
> **If only the const version existed**: every object, even ordinary modifiable ones, would only ever hand back read-only access, so `myArray[2] = 10;` would fail to compile everywhere.
>
> The pairing exists so `[]` behaves correctly regardless of whether the object itself is `const`, the same way the built-in array subscript does.

## Function Overloading (recap)

Overloading a function means writing several functions that share the same name but differ in their parameter lists. The parameter list of the call determines which overloaded version executes. Each version needs its own full definition, overloading a name doesn't let one definition stand in for several.

## Templates

A **template** is a single code body written once for a whole set of related functions (a **function template**) or classes (a **class template**). #definition

```cpp
template <class Type>
declaration;
```
- `class` here doesn't mean "class" in the OOP sense, it just introduces the template parameter, and accepts any user-defined *or* built-in type.
- `Type` is a formal parameter of the template, in the same sense a variable is a formal parameter of a function: where a function's parameters are variables, a template's parameters are **data types**.

### Function Templates
```cpp
template <class Type>
function definition;
```
`Type`, once supplied, is used throughout the definition to: specify the type of the function's parameters, specify the return type, and declare variables inside the function body.

### Class Templates
A class template is a single code segment for a set of related classes, also called **parameterized types**. #definition
```cpp
template <class Type>
class declaration
```
- A template instantiation can be created with either a built-in or a user-defined type.
- The function members of a class template are themselves considered function templates.

> [!question]- Struggle (added): where does a template declaration "stop"? #struggle
> `template <class Type>` applies to exactly **one** declaration: the single function or single class written directly beneath it. The moment that declaration's body closes, the template's scope is over, `Type` is not a real, floating type name available anywhere else in the file, it only exists within the one declaration the header introduced.
>
> Proven directly: adding an ordinary function right after a function template compiles fine and has no access to `Type` at all ,
> ```cpp
> template <class Type>
> Type maxOf(Type a, Type b) { return (a > b) ? a : b; }
>
> int square(int x) { return x * x; }   // ordinary function, unrelated to the template above
> ```
> Trying to reuse `Type` outside that scope fails to compile, with the compiler saying exactly that: #added
> ```cpp
> Type square(Type x) { return x * x; }   // ERROR: 'Type' does not name a type
> ```
> `error: 'Type' does not name a type`

> [!question]- Struggle (added): why didn't the class template need "Type" written for every member function? #struggle
> It did, go back and look: `Box(Type initial)`, `Type getContents() const`, and `void setContents(Type value)` all use `Type` explicitly. What was skipped was restating `template <class Type>` before each individual member function.
>
> The reason: `template <class Type>` written once above `class Box` covers the **entire class body** that follows, including every member function written **inline inside** the class definition. Those member functions are physically inside the scope that one header line opened, so they don't need their own copy of it.
>
> That stops being true the moment a member function's *definition* is written **outside** the class body (a style choice, seen already with `className::operator+` and friends throughout this lecture). Outside the class, the definition is back at file scope, so the template header has to be repeated for each member function, and the class name must be qualified as `Box<Type>::`, not plain `Box::`, since `Box` on its own isn't a complete type until paired with one: #added
> ```cpp
> template <class Type>
> class Box
> {
> public:
>     Box(Type initial);          // declared here, defined outside below
>     Type getContents() const;   // declared here, defined outside below
> private:
>     Type contents;
> };
>
> template <class Type>              // repeated, per member function
> Box<Type>::Box(Type initial) : contents(initial) {}
>
> template <class Type>              // repeated again
> Type Box<Type>::getContents() const { return contents; }
> ```
> Both styles (inline in the class, or split out with the header repeated) compile to the same behaviour; this is exactly why the section Where Template Definitions Must Live (Header and Implementation Files) matters: the compiler needs to see the class definition and every repeated `template <class Type>` member definition at compile time, whichever style is used.

> [!example]- (added) Worked example: this is the same mechanism as `std::vector` and `std::max` #worked-example #added
> `vector<int>`, `map`, `string`, and most of the standard library aren't special built-in language features, they're class templates someone else already wrote, using this exact syntax:
> ```cpp
> vector<int> nums = {10, 20, 30};
> Box<int> intBox(42);
> ```
> `<int>` is filling in `vector`'s own `Type` parameter, the same way `<int>` fills in `Box`'s. `vector` is shaped, in simplified skeleton, like:
> ```cpp
> template <class Type>
> class vector
> {
> public:
>     void push_back(Type value);
>     Type& operator[](int index);
> private:
>     Type* data;   // a pointer member -- which is exactly why vector needs
>                    // the overloaded =, copy constructor, and destructor
>                    // trio from the pointer-member-variables section
> };
> ```
> Function templates work the same way one level down. `std::max` is essentially the `maxOf` written earlier in this session:
> ```cpp
> template <class Type>
> const Type& max(const Type& a, const Type& b)
> {
>     return (a < b) ? b : a;
> }
> ```
> `std::sort` is the same idea doing more work: one function template body that reorders `vector<int>`, `vector<double>`, `vector<string>`, or anything whose elements support `<`, without a version written per type.

### Where Template Definitions Must Live (Header and Implementation Files)

> [!important] Key asymmetry #exam-flagged
> Passing a parameter to an ordinary function takes effect at **run time**. Passing a parameter to a class template takes effect at **compile time**. In practice the same holds for function templates too, even though the slides only state it for class templates.

Consequence: the implementation file of a class template **cannot** be compiled independently of the client code that uses it. "Client code" just means the file that uses the template, for example `main.cpp`. The real requirement is that the compiler sees the template's definitions in the same compilation as the code that uses it.

**The ways to lay it out** (the first three are the lecture's; there is no separate "declare it twice" step in any of them):

1. **Everything directly in the client code.** Put the class definition and the function template definitions in the file that uses them.
2. **Everything in one header file.** Put the class definition and all the function template definitions in the same header, and `#include` that header. This is the simplest and most common layout.
   ```cpp
   // Box.h
   #ifndef BOX_H
   #define BOX_H

   template <class Type>
   class Box
   {
   public:
       Box(Type v);
       Type get() const;
   private:
       Type contents;
   };

   template <class Type>
   Box<Type>::Box(Type v) : contents(v) {}

   template <class Type>
   Type Box<Type>::get() const { return contents; }

   #endif
   ```
   A function template needs no separate prototype; writing the full definition in the header is enough.
3. **Separate files, with the include at the end of the header.** The class definition goes in the header, the member definitions go in the implementation file, and the header ends with an `#include` of that implementation file.
   ```cpp
   // Box.h: the class, then the include at the very end
   template <class Type>
   class Box { /* declarations only */ };
   #include "Box.cpp"

   // Box.cpp: the member definitions, each with its own template header
   template <class Type>
   Box<Type>::Box(Type v) : contents(v) {}
   ```
   `Box.cpp` is never compiled on its own here. Compiling `main.cpp` alone works and prints the result; also passing `Box.cpp` to the compiler fails with `'Box' does not name a type`.

In all three, the function definitions and the client code end up compiled together.

**Not a valid layout:** class declaration in a header, definitions in a `.cpp` that is compiled separately and linked. This is the ordinary layout for non-template classes, and it fails for templates (see the dropdown below).

**Outside the lecture (added):** you can force a separate `.cpp` to generate specific versions with an explicit instantiation, for example `template class Box<int>;` and `template int maxOf<int>(int, int);` at the bottom of `Box.cpp`. This works only for the types you list; using `Box<string>` from `main.cpp` still fails to link.

> [!question]- Struggle (added): why does separate compilation fail for templates? #struggle
> A template is a recipe, not code. The compiler only writes real code when it sees a use with a concrete type, like `maxOf(3, 7)` or `Box<int>`, and to do that it needs the full body in front of it in that same compilation.
>
> With the definitions in a separately compiled `Box.cpp`:
> - `main.cpp` sees only the declaration. It compiles, but it cannot generate `Box<int>`'s code, so it leaves a note for the linker to find it elsewhere.
> - `Box.cpp` has the bodies, but nothing in it uses `Box<int>`, so the compiler generates nothing for it.
> - The linker looks for `Box<int>`'s members and finds nothing. The failure appears at **link** time, not compile time:
>
> ```
> undefined reference to `int maxOf<int>(int, int)'
> undefined reference to `Box<int>::Box(int)'
> undefined reference to `Box<int>::get() const'
> ```
> Moving the definitions into the header fixed it, and the program printed `7` and `42`. The same failure happens for a function template and a class template.

### Q2.1 blanks: what each one is (added)
The Q2.1 questions in the 2025 A, B and C papers give a class template with words missing. The same blanks keep coming back:

| Blank | Answer pattern | Why |
|---|---|---|
| Header line above the class | `template <typename T>` | Makes the class a template |
| Copy constructor parameter | `const UJList<T>&` (the `<T>` is the part people forget) | The class name alone is not a complete type inside a template |
| Assignment operator | `operator=` | Always a member |
| Subscript return type | `T&` | So the caller can read and write through it |
| Before `<<` and `>>` inside the class | `friend` | The left operand is a stream |
| The operator itself | `<<` for output, `>>` for input | `cout << x` is output, `cin >> x` is input |
| Template line before a friend | `template <typename E>`, and then `UJList<E>` | A friend template is a new template, so reusing `T` gives "shadows template parameter" |
| `const` or `static` blank | read the sentence: a `const` object or function is not changed, a `static` member belongs to the class | Decide from what the code around it needs |
| Pointer member | `T*` | A dynamic array of `T` is held through a `T*` |

> [!warning] Check the member or friend blank by the left operand #exam-flagged
> Missed twice in session S12. Ask what is on the left of the operator. A stream means friend. The class object, with `[]`, `=`, `()` or `->`, means member.

### Friend operators inside a class template (added)
A friend `<<` or `>>` declared inside `template <typename T> class UJList` is itself a template. Compiled and run natively, with `cout << a;` and `cin >> a;` working:
```cpp
template <typename E>
friend std::ostream& operator<<(std::ostream& osLHS, const UJList<E>& objRHS);
template <typename E>
friend std::istream& operator>>(std::istream& isLHS, UJList<E>& objRHS);
```
- It needs its own `template <typename E>` line. Using `T` again is an error ("shadows template parameter").
- Leaving the template line off gives a non-template friend warning, and the operator then does not match `UJList<int>`.
- `<<` takes a `const` object, because it only reads. `>>` takes a non-const object, because it fills it in.
- Both return the stream, so that `cout << a << b;` chains.

## Do Not Forget
- Only `=` and `.` are free on a class; every other operator overload is a choice, except when pointer members force `=` + copy constructor + destructor together.
- Five operators can never be overloaded: `.` `.*` `::` `?:` `sizeof`.
- `()`, `[]`, `->`, `=` must be members; `<<`, `>>` must be friends (leftmost operand isn't the class type).
- The dummy `int` parameter is the only signature difference between pre- and post-increment; post-increment returns the saved copy, pre-increment returns the updated object itself.
- `[]` needs both a const and nonconst overload so it works whether the object itself is const.
- Copy constructor fires on creation of a new object from an existing one; assignment fires on an already-existing object. Both default to memberwise copy, both break under pointer members.
- Template parameters are resolved at **compile time**, which is why template implementation files can't be compiled independently of client code.
- Valid layouts for template definitions: (1) directly in the client code, (2) everything in one header, (3) separate implementation file included at the **end** of the header. Definitions in a separately compiled `.cpp` fail at **link** time. This applies to function templates as well as class templates.
- Default `=` on a pointer member is legal but copies the address: leak plus double free. That is why `=`, the copy constructor and the destructor come as a set.
- `5.0 + m` cannot be a member (left operand is not the class type); `m + 5.0` can.
- `template <class Type>` covers exactly one declaration beneath it (one function, one class, or one out-of-class member definition); it never carries over to whatever comes next in the file.
- Inside a class body, one `template <class Type>` line covers every inline member function. Outside the class body, each member function definition needs the header repeated, plus `ClassName<Type>::`.
- `vector`, `map`, `string`, `max`, `sort` are ordinary templates, not language magic, the exact same `template <class Type>` mechanism covered in this lecture.
- (added, S12) Member or friend is decided by the LEFT operand: if it is the class type, a member is possible; if not (`5.0 + m`, `cout << m`), it must be a friend. `()`, `[]`, `->`, `=` are always members.
- (added, S12) `this` exists only in members and points to the LEFT operand. A friend has no `this`, so it takes both operands as parameters.
- (added, S12) Three const positions: in front, the returned value cannot be changed; in the brackets, the right operand is not changed; trailing, the left object (`this`) is not changed. Assignment has no trailing const.
- (added, S12) A default `=` always compiles. With pointer members it copies the address, so you get a leak and a double free at run time, not a compile error.
- (added, S12) Inside a class template, each friend `<<` or `>>` needs its own `template <typename E>` line and must write `UJList<E>`, not reuse `T`.

## Operator Overloading Quick Reference

| Operator | Mutates the Calling Object? | Member or Non-Member | Can it be a Friend? | When to use Friend vs Member | Example Implementation |
|---|---|---|---|---|---|
| `==` | No, builds and returns a `bool`, operands untouched | Non-Member (Friend), typical | Yes | Friend keeps both operands symmetric; there's no reason for one object to "own" the comparison over the other | `friend bool operator==(const className&,`<br>`                        const className&);` |
| `[]` (read & write) | No directly, returns a reference; the non-const version lets the *caller* mutate through it | **Must be Member** | No, forced | Leftmost operand is always the class object; grouped with `()`, `->`, `=` as always-member | `Type& operator[](int index);`<br>`const Type& operator[](int index) const;` |
| `+` | No, builds and returns a new object, operands untouched | Either (design choice) | Yes | Member if the left operand is always the class type; Friend when you want both operands treated symmetrically | `className operator+(const className& other) const;` *(member)*<br>`friend className operator+(const className&,`<br>`                            const className&);` *(friend)* |
| `--` prefix | **Yes**, decrements `*this`, then returns it | Member, typical | Yes | Member is simplest: no parameters needed, operand is `this` | `className operator--();`<br>`{ //decrement the object`<br>`  return *this; }` |
| `--` postfix | **Yes**, decrements `*this`, but returns the pre-decrement copy | Member, typical | Yes | Same tradeoff as prefix; the dummy `int` only exists to distinguish the signature | `className operator--(int u);`<br>`{ className temp = *this;`<br>`  //decrement the object`<br>`  return temp; }` |
| `++` prefix | **Yes**, increments `*this`, then returns it | Member, typical | Yes | Member is simplest: no parameters needed, operand is `this` | `className operator++();`<br>`{ //increment the object`<br>`  return *this; }` |
| `++` postfix | **Yes**, increments `*this`, but returns the pre-increment copy | Member, typical | Yes | Same tradeoff as prefix; the dummy `int` only exists to distinguish the signature | `className operator++(int u);`<br>`{ className temp = *this;`<br>`  //increment the object`<br>`  return temp; }` |
| `<<` | No, the class object (`cObject`) is passed `const`, only the stream is touched | **Must be Non-Member (Friend)** | Yes, forced | Leftmost operand is `ostream`, never the class type | `friend ostream& operator<<(ostream&,`<br>`                            const className&);` |
| `>>` | **Yes**, it fills the object from the stream, so the object is passed non-const | **Must be Non-Member (Friend)** | Yes, forced | Leftmost operand is `istream`, never the class type | `friend istream& operator>>(istream&,`<br>`                            className&);` (added, S12) |
| `=` | **Yes**, it overwrites the left object (`*this`) | **Must be Member** | No, forced | Always a member, grouped with `()`, `[]`, `->`. Pointer members need it together with the copy constructor and destructor | `const className& operator=(const className&);`<br>`{ if (this != &rightObject)`<br>`  { /* free, allocate, copy */ }`<br>`  return *this; }` (added, S12) |

> [!important] The one line to remember for `++`/`--` #exam-flagged
> Prefix and postfix differ in exactly two places: the dummy `int` parameter in the signature, and what gets returned, prefix returns `*this` **after** mutating; postfix saves a `temp` copy **before** mutating and returns that instead.

## Amendments
S12: Added the left operand rule for member versus friend with the `this` explanation, the three const positions, friend `<<` and `>>` inside a class template (compiled and run), a table of the Q2.1 blanks, rows for `=` and `>>` in the quick reference, and five bullets in Do Not Forget. Existing text was not changed. Prompted by misses in the S12 drills and quiz: member versus friend (twice), trailing const, and the default `=` compiling but failing at run time.

---
*CDG version: written under an earlier version that was not recorded (S6); amended with CDG v10 (S12, 2026-10-29).*
