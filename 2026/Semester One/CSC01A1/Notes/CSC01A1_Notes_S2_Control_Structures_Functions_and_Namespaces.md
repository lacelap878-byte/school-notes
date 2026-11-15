---
module: CSC01A1
topic: Control Structures, Functions and Namespaces
session: S2
tags: [definition, worked-example, common-mistake, added]
---

# CSC01A1 Notes S2: Control Structures, Functions and Namespaces

Source: L03 "Control Structures" (selection and repetition), L04 "Functions: An in-depth look" and L05 "Libraries of Functions and Namespaces" (2026 slides). Short revision notes in syntax-sheet style: the code is my own, written to fit each lesson.

Checked: every snippet comes from programs compiled with g++ 13 (`-std=c++23 -Wall -Wextra`) and run, with the outputs shown in the comments; the three-file library was compiled separately and linked, on 15 Nov 2026.

## Relational and logical operators (source: L03)

- A program runs in sequence, by selection (branching), by repetition (looping) or by calling a function.
- Relational operators: `==  !=  <  <=  >  >=`. Logical operators: `!` (not), `&&` (and), `||` (or). A logical expression gives `true` (1) or `false` (0); any nonzero value counts as true.

| Precedence | Operators |
|---|---|
| 1 | `!`, unary `+`, unary `-` |
| 2 | `*  /  %` |
| 3 | `+  -` |
| 4 | `<  <=  >=  >` |
| 5 | `==  !=` |
| 6 | `&&` |
| 7 | `\|\|` |
| last | `=` |

- Equal levels go left to right; brackets override.
- Strings compare character by character by ASCII code: `"Hello" < "Hi"` (e before i), `"Hello" == "hello"` is false ('H' is 72, 'h' is 104), and if one string is the start of the other, the shorter one is less (`"Bill" < "Billy"`).
- Short-circuit evaluation: evaluation stops as soon as the answer is known, so `d != 0 && 10 / d > 1` never divides by zero.

> [!warning] Three silent traps (source: L03)
> - `0 <= num <= 10` is always true: it becomes `(0 <= num) <= 10`, which is `1 <= 10` or `0 <= 10`. Write `0 <= num && num <= 10`.
> - `if (x = 5)` assigns 5 and is always true. It compiles, so it is a logic error, not a syntax error. Use `==`.
> - Do not compare doubles with `==`: `3.0/7 + 2.0/7 + 2.0/7 == 1.0` is false. Use `fabs(x - y) < 0.000001` (from `<cmath>`).

## Selection (source: L03)

```cpp
if (mark >= 75)
    cout << "Distinction\n";
else if (mark >= 50)              // nested if: each else pairs with the nearest unpaired if
    cout << "Pass\n";
else
{                                 // a block { } acts as one statement
    cout << "Fail\n";
    cout << "Rewrite\n";
}

int biggest = (a >= b) ? a : b;   // conditional (ternary) operator: condition ? value1 : value2

switch (grade)                    // selector must be integral: int, char, bool, enum
{
case 'A':
case 'B':                         // 'A' and 'B' share this action
    cout << "Good\n";
    break;                        // without break, execution falls through to the next case
case 'C':
    cout << "Average\n";
    break;
default:
    cout << "Unknown\n";
}

#include <cassert>
assert(b != 0);                   // if false: the program stops and reports the line
```

- Without braces, only the first statement after `if` or `else` belongs to it; indentation does not change that.
- If `cin` fails (letters typed for an `int`), the stream enters a fail state and later reads are ignored; check it with `if (!cin)`.
- `#define NDEBUG` placed before `#include <cassert>` switches every `assert` off once the program is tested.
- Pseudocode (informal C++ and English) and walk-throughs with a wide range of values help find logic errors.

## Loops (source: L03)

```cpp
int counter = 0;                  // counter-controlled: number of runs known
while (counter < 5) { cout << counter * 5 << " "; counter++; }   // 0 5 10 15 20

cin >> value;                     // sentinel-controlled: a special value (-1) ends input
while (value != -1) { sum += value; cin >> value; }

bool found = false;               // flag-controlled: a bool decides when to stop
while (!found) { if (n * n > 50) found = true; else n++; }

while (cin >> value)              // EOF-controlled: stops when input runs out (Ctrl+Z on Windows)
    total += value;

for (int i = 1; i <= 4; i++)      // for (initial; condition; update)
{
    for (int j = 1; j <= i; j++) cout << "*";   // nested loop: a triangle of stars
    cout << "\n";
}

do { cout << "menu\n"; cin >> choice; } while (choice != 0);   // posttest: runs at least once

for (int i = 1; i <= 10; i++)
{
    if (i % 2 == 0) continue;     // skip to the next iteration
    if (i > 7) break;             // leave the loop now
    cout << i << " ";             // 1 3 5 7
}
```

- `while` and `for` are pretest loops (may run zero times); `do...while` is posttest (runs at least once).
- Choosing: number of runs known in advance, `for`; unknown and possibly zero, `while`; unknown but at least one, `do...while`.
- `for (;;)` is a legal infinite loop. A `;` straight after `for (...)` is a semantic error: the loop body becomes empty.
- The most common loop bug is off by one. A loop invariant (something true every time the body runs) helps debugging. Fix the cause, not the symptom (no patches).
- `rand() % 100` (from `<cstdlib>`) gives a whole number from 0 to 99.

## Function basics (source: L04)

```cpp
void printLine(int);                            // prototype: return type, name, parameter types
double area(double length, double width = 1.0); // default argument (in the prototype only)
auto square(int x) -> int;                      // trailing return type (C++11)

void printLine(int n)                           // void function: called for its effect
{
    if (n <= 0) return;                         // early exit from a void function
    cout << string(n, '-') << "\n";
}
double area(double length, double width) { return length * width; }   // area(3.0) is 3

auto x = 3.5 * 2;          // auto infers the type (double); it cannot change later
decltype(x) y = 1;         // decltype: "the same type as x"
```

- A function must be declared before it is called and fully defined by the end of compilation. The formal parameters act as local variables.
- A value-returning function computes a result to be used in an expression.

## Parameters, overloading and variadic functions (source: L04)

```cpp
void byValue(int x)      { x = 99; }   // copy: the caller's variable is unchanged
void byReference(int& x) { x = 99; }   // & makes x an alias: the caller's variable changes
int countVowels(const string& s);      // const reference: no copy and no changes (large data)

int    maxOf(int a, int b);            // overloading: same name,
double maxOf(double a, double b);      // different parameter lists

int sumAll(initializer_list<int> values)   // variadic: any number of ints
{
    int total = 0;
    for (int v : values) total += v;
    return total;
}
// sumAll({1, 2, 3, 4}) is 10
```

- Overloads must differ in their parameter lists; a different return type alone is not enough.
- Of the three variadic techniques, the course uses the safe one where all arguments share one type (`initializer_list`). Mixed types safely needs metaprogramming (CSC01B1); the C-style way is unsafe and deprecated.

## Recursion (source: L04)

A recursive function calls itself. It needs a base case (stops) and a recursive case on a smaller problem.

```cpp
int sumTo(int n)          { return n == 1 ? 1 : n + sumTo(n - 1); }       // sumTo(4) is 10
long long factorial(int n) { return n <= 1 ? 1 : n * factorial(n - 1); } // factorial(5) is 120
int fib(int n)            { return n <= 1 ? n : fib(n - 1) + fib(n - 2); }
// fib: 0 1 1 2 3 5 8 13 ...  fib(7) is 13
```

- Each call makes a new copy of the function in memory, so recursion with no base case eventually runs out of memory.

## constexpr and lambda expressions (source: L04)

```cpp
constexpr int cube(int x) { return x * x * x; }
constexpr int SIZE = cube(3);                     // worked out at compile time: 27

auto isEven = [](int n) { return n % 2 == 0; };   // [capture](parameters) { body }
int limit = 10, calls = 0;
auto underLimit = [=](int n) { return n < limit; };   // [=] reads locals by value
auto counter    = [&]() { calls++; };                 // [&] can change locals

#include <functional>
bool applyTest(int value, function<bool(int)> test) { return test(value); }
// applyTest(9, [](int n) { return n > 5; }) is true
```

- `constexpr` forces compile-time evaluation when the arguments are constants. The slide lists the C++11 limits: a single return statement (not void), no local variables, no loops, no side effects, so iteration is done by recursion.
- (added) From C++14 on (the course uses C++23), constexpr functions may have local variables and loops. Learn the slide's list for the exam, but expect modern compilers to accept more.
- Lambda parts: capture list `[]`, optional `()` parameters, optional `mutable`, optional `noexcept`, optional `-> type`, body `{}`. The shortest lambda is `[]{}`; the return type is inferred.
- Captures: `[]` none, `[&]` all by reference, `[=]` all by value (read only), `[a, &b]` named ones, `[&, a]` all by reference except `a`, `[=, &b]` all by value except `b`.
- A lambda's type is written `function<R(PL)>` (return type R, parameter types PL) from `<functional>`, so functions can take other functions as parameters.

## Separate compilation (source: L05)

Three files: the interface (header), the implementation, and the application (driver).

```cpp
// geometry.h  (interface: prototypes only; never compiled on its own)
#ifndef GEOMETRY_H        // include guard: skip everything if already included
#define GEOMETRY_H
namespace geometry
{
    double circleArea(double radius);
}
#endif

// geometry.cpp  (implementation)
#include "geometry.h"
namespace                 // unnamed namespace: helpers private to this file
{
    const double PI = 3.14159265358979;
    double square(double x) { return x * x; }
}
namespace geometry
{
    double circleArea(double radius) { return PI * square(radius); }
}

// main.cpp  (application)
#include <iostream>       // < > : system headers
#include "geometry.h"     // " " : your own headers, searched in the current folder first
int main() { std::cout << geometry::circleArea(2.0) << "\n"; }   // 12.5664
```

```text
g++ -c geometry.cpp      (compile the implementation once)
g++ -c main.cpp          (compile the application)
g++ geometry.o main.o -o app      (the linker joins them)
```

- The preprocessor pastes the header's text wherever it is included, so both .cpp files see it.
- Benefits: the library is reused without rewriting, compiled once, retested less, and can change without changing the programs that use it.
- Include-guard name convention: the file name in capitals with `_` for `.` (`GEOMETRY_H`).

## Namespaces (source: L05)

- A namespace is a collection of name definitions; it stops two libraries' identical names from clashing. Code not in any namespace is in the global namespace.
- `using namespace std;` (a using directive) makes every name in `std` available; `using std::cout;` (a using declaration) makes only one. `ns1::greet()` qualifies a single use with the scope resolution operator `::`.
- A using directive's scope is the block it is in; at the top of a file, the whole file.
- Same name in two namespaces: use them in separate blocks, or qualify each call. Two using directives for clashing names are fine as long as the name is never used; two using declarations for the same name are illegal even if unused.
- The unnamed namespace makes names local to one compilation unit (a .cpp file plus everything it includes). Global names are visible in all files. To keep namespace names unique, add your surname or reverse your domain (`namespace zaacuj`).

## Do not forget

- `0 <= x <= 10` and `if (x = 5)` both compile and are both wrong.
- `switch` needs `break`, or the next case runs too.
- Pass by `&` to change the caller's variable; `const &` to avoid copying without changing it.
- Every recursive function needs a base case.

## See also

- [[CSC01A1_Notes_S1_Command_Line_Numeracy_and_CPP_Basics]]

---
*CDG v13 | written S2 | 2026-11-15*
