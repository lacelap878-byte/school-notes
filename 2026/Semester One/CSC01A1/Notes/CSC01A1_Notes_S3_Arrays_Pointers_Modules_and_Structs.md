---
module: CSC01A1
topic: Arrays, Pointers, Modules and Structs
session: S3
tags: [definition, worked-example, common-mistake, added]
---

# CSC01A1 Notes S3: Arrays, Pointers, Modules and Structs

Source: L06 "Fixed Length Arrays", L07 "Pointers and Dynamic Arrays" (with the supplementary function pointers), L08 "Modular Programming" and L09 "Structures and Enumerations" (2026 slides). Short revision notes in syntax-sheet style: the code is my own, written to fit each lesson.

Checked: every snippet comes from programs compiled with g++ 13 (`-std=c++23 -Wall -Wextra`, plus `-fmodules-ts` for the module) and run, with the outputs shown in the comments, on 15 Nov 2026.

## One-dimensional arrays (source: L06)

An array is a collection of a fixed number of components, all of the same data type (a structured data type). The size must be a constant expression; indexes run from 0 to size - 1.

```cpp
const int SIZE = 5;
double sales[] = {12.25, 32.50, 16.90, 23, 45.68};   // size 5, taken from the initialiser
int list[10] = {8, 5, 12};                            // list[3] to list[9] are 0
int zeros[10] = {0};                                  // all 0

for (int i = 0; i < 10; i++) cin >> list[i];          // process an array with a loop

int copy[10];
for (int i = 0; i < 10; i++) copy[i] = list[i];       // copy = list; is illegal (no aggregate operations)

double largest(const double list[], int size)         // passed by reference, no &; const stops changes
{
    double max = list[0];
    for (int i = 1; i < size; i++)
        if (list[i] > max) max = list[i];
    return max;
}

int seqSearch(const int list[], int size, int item)   // sequential (linear) search
{
    for (int i = 0; i < size; i++)
        if (list[i] == item) return i;
    return -1;                                         // not found
}
```

- C++ does not check bounds: `list[10]` in a size-10 array compiles and reads or overwrites other memory.
- Aggregate operations (assigning, comparing, reading or printing a whole array at once) are not allowed, except input and output of C-strings.
- The base address is the address of `list[0]`; passing an array passes its base address, so a size given in the parameter is ignored.
- A function cannot return an array type (return a pointer, or wrap the array in a struct).
- Parallel arrays: two arrays where the same index holds related data (`studentId[i]` and `grade[i]`).

## C-strings (source: L06)

```cpp
#include <cstring>
char name[16] = "John";     // holds at most 15 characters plus the null '\0'
char other[] = "Johnny";    // size 7: six letters + '\0'
strlen(name);               // 4
strcmp(name, other) < 0;    // true: compares character by character
strcpy(name, "Ann");        // assignment for C-strings
cin.get(name, 16);          // reads up to 15 characters, including spaces
string s = "Hello";
strlen(s.c_str());          // c_str() turns a string into a C-string: 5
```

- `'A'` is one character; `"A"` is a C-string of two characters, `'A'` and `'\0'`. `cout << name` prints until it meets `'\0'`, so a missing null prints garbage.
- `cin >> name` stops at whitespace. `strcmp` gives a negative number, 0, or a positive number; by ASCII, `"Air" < "An"`, `"Bill" < "Billy"`, `"Hello" < "hello"`.

## Two-dimensional arrays (source: L06)

```cpp
int matrix[2][3] = {{1, 2, 3}, {4, 5}};    // rows in braces; missing values are 0
for (int r = 0; r < 2; r++)                // print row by row with nested loops
{
    for (int c = 0; c < 3; c++) cout << matrix[r][c] << " ";
    cout << "\n";
}                                          // 1 2 3 / 4 5 0

int rowSum(const int m[][3], int row)      // the first size may be omitted, the second may not
{
    int sum = 0;
    for (int c = 0; c < 3; c++) sum += m[row][c];
    return sum;
}                                          // rowSum(matrix, 1) is 9
```

- Stored in row order. Row processing fixes the row and loops over columns; column processing does the opposite.
- Arrays of `string` (`string list[100];`) allow assignment, comparison and I/O on each element. An n-dimensional array uses n indexes.

## Pointers (source: L07)

A pointer holds the memory address of a variable of one particular type.

```cpp
int v1 = 0;
int *p1, *p2;          // * before EACH pointer name; int *p, q; makes q a plain int
p1 = &v1;              // &: "address of", so p1 points to v1
*p1 = 42;              // *: dereference, "the variable p1 points to"; v1 is now 42

p2 = p1;               // pointer assignment: p2 points where p1 points
*p2 = *p1;             // value assignment: copies the pointed-to values

int* n = new int(17);  // dynamic variable on the heap (freestore), no name, only a pointer
delete n;              // return the memory
n = nullptr;           // a deleted pointer still holds the old address (dangling); clear it

typedef int* IntPtr;   // a named pointer type: IntPtr p; is the same as int* p;
```

- `&` has two closely related uses: address of, and call-by-reference parameters (which pass the address).
- A pointer is an address, not a number to do maths with. Old compilers return NULL when `new` fails; new ones stop the program with an error.
- Dynamic variables are created and destroyed while the program runs (`new`, `delete`). Local (automatic) variables are created when the function is called and destroyed when it ends.
- Pitfall: a pointer passed by value is a copy. Changing where the parameter points does not change the caller's pointer, but changing `*p` does change the caller's data.

## Dynamic arrays (source: L07)

```cpp
int size;
cin >> size;                       // size known only while the program runs
double* d = new double[size];
d[2] = 2.5;
cout << *(d + 2);                  // pointer arithmetic: same as d[2]
delete[] d;                        // [] for arrays
d = nullptr;

int* makeArray(int n)              // return a pointer, since an array type cannot be returned
{
    int* a = new int[n];
    for (int i = 0; i < n; i++) a[i] = i * i;
    return a;                      // the caller must delete[] it
}

int a[3] = {1, 2, 3};
int* p = a;                        // legal: p points to a[0]
p++;                               // *p is now 2; only + and - (and ++, --) work on pointers
// a = p;                          // illegal: an array name is a constant pointer

int** m = new int*[3];             // 3 by 4 dynamic 2D array: an array of row pointers
for (int r = 0; r < 3; r++) m[r] = new int[4];
for (int r = 0; r < 3; r++) delete[] m[r];   // free each row, then the row array
delete[] m;
```

- A fixed array forces you to guess the maximum size; a dynamic array gets exactly the size needed at run time.
- (added) The slide calls the array name a `const int *`. Strictly it behaves like `int * const`: a constant pointer (it cannot be moved) to data that can still change.

## Function pointers (source: L07 supplement)

```cpp
int twice(double x) { return static_cast<int>(2 * x); }
typedef int (*FunPtr)(double);     // the prototype with (*name) and typedef in front
FunPtr f = &twice;                 // or: FunPtr f = twice;
cout << f(3.4);                    // 6
```

- Compiled code is in memory too, so a pointer can hold a function; it can be a parameter or return type, which lets behaviour be chosen while the program runs.
- (added) The slide writes `fun_ptr = &fun;`, but `fun_ptr` is the typedef (a type). Declare a variable of that type first, as above.

## Modules (source: L08)

From C++20, a module groups related functions, types and constants. Only what it exports can be used by a file that imports it.

```cpp
// libmath.cpp  (module interface file)
export module LibMath;                 // module declaration; "export" makes it the interface

export enum class Oddity { Even, Odd };
export Oddity getOddity(int n);        // exported prototype

export                                 // export block: several entities at once
{
    bool isEven(int n) { return n % 2 == 0; }
    int square(int n) { return n * n; }
}

int helper(int n) { return n < 0 ? -n : n; }   // not exported: private to the module

Oddity getOddity(int n)                // definition lower down; export need not be repeated
{
    return helper(n) % 2 == 0 ? Oddity::Even : Oddity::Odd;
}

// main.cpp
#include <iostream>
import LibMath;                        // uses the declared module name, not the file name
int main() { std::cout << square(5); } // 25
```

```text
g++ -std=c++23 -fmodules-ts -c libmath.cpp
g++ -std=c++23 -fmodules-ts -c main.cpp
g++ libmath.o main.o -o app
```

- The exported entities together form the module interface. Only module interface files may contain `export`, and only after the module declaration.
- Module names may contain dots (`math.polynomials`); `123math`, `.polynomials`, `abc.` and `a..b` are invalid.
- You may not add `export` to an entity that was first declared without it. The course uses `.cpp` for module files; a separate implementation file is beyond the course.

## Enumerations (source: L09)

```cpp
enum Status { SUCCESS, CONVERSION_ERROR, NOT_POSITIVE, OUT_OF_RANGE };   // 0, 1, 2, 3
enum Colour { RED = 10, GREEN = 20, BLUE };                               // BLUE is 21

Status check(int n)
{
    if (n <= 0) return NOT_POSITIVE;
    if (n > 100) return OUT_OF_RANGE;
    return SUCCESS;
}
```

- An enum replaces a set of integer constants and makes a new type that can only take those values. The first is 0 by default and each next one is 1 more; values can be set by hand.

## Structures (source: L09)

A struct groups values of different types into one record.

```cpp
struct Location { int row; int col; };   // 1. definition: note the ; after }

struct Player
{
    string name;
    Location pos;          // nested struct
    int scores[3];         // fixed size array member
    int* history;          // dynamic array member
};

Player p;                  // 2. declaration
p.name = "Thandi";         // 3. initialisation, member by member with the dot operator
p.pos = {2, 3};
p.pos.col++;               // nested access: 2,4
p.history = new int[4]{};  // allocate the dynamic member (delete[] it later)

void moveRight(Player& p) { p.pos.col++; }    // by reference: the caller's struct changes
int totalScore(const Player& p);              // const reference: read only, no copy

struct Triple { int values[3]; };
Triple makeTriple() { return {{1, 2, 3}}; }   // a struct can carry an array out of a function

Location* grid = new Location[3];             // dynamic array of structs
grid[2] = {2, 4};
delete[] grid;
```

- Structs can be passed by value (the caller's copy is safe), by reference (changes allowed), and returned from functions.
- Structs and enums make parameters and return types shorter and clearer.

## Do not forget

- Arrays start at 0, have no bounds checking, and cannot be assigned or compared as a whole.
- `delete` for one dynamic variable, `delete[]` for a dynamic array; then set the pointer to `nullptr`.
- `p2 = p1` copies the address; `*p2 = *p1` copies the value.
- In a module, only exported entities can be used by the importing file.

## See also

- [[CSC01A1_Notes_S1_Command_Line_Numeracy_and_CPP_Basics]]
- [[CSC01A1_Notes_S2_Control_Structures_Functions_and_Namespaces]]

---
*CDG v13 | written S3 | 2026-11-15*
