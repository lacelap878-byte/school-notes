---
module: CSC01B1
topic: Foundation Topics for Computer Science 1B
session: S1
tags: [definition, worked-example, common-mistake]
---

# Foundation Topics (CSC01B1)

Everything from the binary numeral system through to classes. Read top to bottom the first time; after that, the headings are the index. Cross references point by name, e.g. (see: Two's complement), not by number.

`N.B` marks the thing most likely to be tested or most easily forgotten. Code is reproduced exactly as the lecturer wrote it, quirks and all, because that is what you are examined on. Where the source code contains an actual bug, there is an `(added)` note next to it.

---

## 1. Binary and number representation

### Why binary
Classical hardware stores data as the presence or absence of one physical state, which has two values, so the natural base is 2 with symbols 0 and 1.
- Same idea in different media: indentations on punched tape, charge in RAM, magnetisation on a disk, opacity in optical storage.

### Positional notation
Both decimal and binary are positional: a digit's value is the digit times the base raised to its position, counted from 0 on the right.

### Binary to decimal
Multiply each bit by its power-of-two weight and add.
```
11101 = 1*2^4 + 1*2^3 + 1*2^2 + 0*2^1 + 1*2^0
      = 16 + 8 + 4 + 0 + 1
      = 29
```

### Decimal to binary
Divide by 2 repeatedly, keep each remainder, stop at quotient 0. Read the remainders bottom to top.
```
29 ->
14  r1
 7  r0
 3  r1
 1  r1
 0  r1      so 29 = 11101
```

---

## 2. Boolean and bitwise operations

Treat 1 as true and 0 as false. NOT, AND, OR, XOR act on each bit position on its own, so bitwise arithmetic and boolean logic are the same operation.

- `NOT(11101) = 00010` (flip every bit)
- `AND` gives 1 only where both are 1: `11101 & 10111 = 10101`
- `OR` gives 1 where either is 1: `11101 | 10111 = 11111`
- `XOR` gives 1 only where they differ: `11101 ^ 10111 = 01010`

### Bitmasking
C++ gives no direct handle on a single bit, so independent yes/no flags are packed into one int. Each flag is a distinct power of two (one bit set). OR a flag in to switch it on; AND with a flag to test it.

```cpp
const int CITIZEN = 1;       /*001*/
const int EMPLOYED = 2;      /*010*/
const int ENFRANCHISED = 4;  /*100*/
int person = 0 | CITIZEN | ENFRANCHISED; /* 101 */
int hasWork = person & EMPLOYED;
bool isEmployed = (hasWork > 0);
```

> [!warning] AND returns an int, not a bool
> `person & EMPLOYED` gives you the masked integer, not a true/false. That is why it is compared `> 0` to turn it into a bool. Forgetting the comparison is the classic bitmask slip.

---

## 3. Signed numbers and overflow

### Sign and magnitude
Pick one bit (usually the most significant) as the sign, leave the rest as the plain magnitude.
- With the leading bit as sign: `00011101 = 29`, `10011101 = -29`.
- Reads easily, but the hardware then needs special handling to add a positive and a negative, which is why it is not the scheme used.

### Two's complement
The signed scheme actually used. A negative is stored so that adding it to its positive counterpart wraps to zero, which means one adder handles both signs with no special case.

`N.B` Three fixed steps, in order: absolute value, invert all bits, add one.

```
-29 in 8-bit:
 29    = 00011101
 invert  11100010
 +1      11100011
```

### Overflow
A type has a fixed width, so only a finite range fits. Push a variable past the top and it wraps to the bottom, because the carry runs off the end and is lost.

```cpp
int i = 0;
unsigned int u = 0;
while(true)
{
  std::cout << i++ << std::endl;
  std::cout << u++ << std::endl;
}
```

---

## 4. Binary fractions

Digits after the point carry weights of 1/2, 1/4, 1/8, and so on. Convert a decimal fraction by repeatedly multiplying by 2: write 1 if the result is at least 1, else 0, drop the whole part, repeat until nothing fractional is left.

Many everyday values, such as 1/10, never terminate in binary, so they cannot be stored exactly.

> [!warning] Floating point equality fails for 0.1
> Because 0.1 has no exact binary form, adding it ten times does not land on exactly 1. Never test floats with `==`.
> ```cpp
> double a = 0.0;
> for(int k = 0; k < 10; k++)
>   a += 0.1;
> bool b1 = (a == 1);        //false
> bool b2 = (0.1 * 10 == 1); //false
> ```

---

## 5. Hexadecimal and octal

Both are shorthand for binary because their bases are powers of two, so each digit maps to a fixed group of bits: 4 for hex, 3 for octal. Conversion to and from binary is regrouping, no arithmetic.

### Hexadecimal (base 16)
Digits 0 to 9, then A to F for 10 to 15.
```
To decimal:  BEEF = 11*16^3 + 14*16^2 + 14*16^1 + 15
To binary:   each digit -> 4 bits, E1 = 1110 0001
From binary: group into 4s from the left, 1011 1110 1110 1111 = BEEF
```

### Octal (base 8)
Digits 0 to 7.
```
To decimal:  171 = 1*8^2 + 7*8^1 + 1*8^0
From binary: group into 3s, 110111 = 67
```

---

## 6. The compilation process

The compiler turns each source file into object (machine) code; the linker joins that object code with library code to produce the executable.

```
Source -> Compiler -> Object code -> Linker -> Executable
                                        ^
                                   Library code
```

---

## 7. The C++ memory model

Three ways C++ allocates memory:

| Kind | Where | Freed |
|---|---|---|
| Global | data segment | program lifetime (avoid variable globals) |
| Automatic | stack | automatically, at the block's closing brace |
| Dynamic | freestore / heap | by hand, with `delete` or `delete []` |

`N.B` Only freestore memory outlives its block, and only freestore memory must be freed manually.

### Stack scope
A variable lives until its block's closing brace. An inner block can declare a same-named variable that overshadows the outer one until the inner block ends.

```cpp
void f()
{
  int i = 1; /* i is allocated on the stack*/
  {
    int i = 2; /* Inner i is allocated */
    std::cout << i << std::endl; /* Output: 2*/
  } /* Inner i is freed*/
  std::cout << i; /* Output: 1*/
} /* Outer i is freed */
```

### Variable length arrays (VLAs)
C99 added stack arrays whose size is a runtime value. GCC/MinGW compiles them so they run in Code::Blocks, but they are not standard C++ (C++11 did not add them) and are not allowed here.

```cpp
int main()
{
  int length;        /* length allocated on stack */
  std::cin >> length; /* value read into length */
  int arr[length];   /* VLA - not C++ */
}
```

---

## 8. Freestore: new and delete

- `new` allocates freestore memory and returns its address; `delete` returns it. They must be paired.
- `new` / `delete` for a single variable; `new []` / `delete []` for a contiguous block. The bracket forms must match each other.

`N.B` `delete` does not NULL the pointer. It still holds the old, now invalid, address until you set it to NULL yourself.

---

## 9. Pointers and references

A pointer is a variable that holds a memory address, declared with `*`.

### Declaring pointers
On a line declaring several names, the `*` binds only to the name it sits on.
```cpp
int* a;          /* a is a pointer */
int* b, c;       /* only b will be a pointer */
int x, *y, *z;   /* y and z will be pointers */
```

### Address-of `&`
Takes the address of an existing identifier, so you can point at a variable you already have.
```cpp
int a = 1337;
int* ptr_a = &a;
```

### Wild and dangling pointers
An uninitialised pointer is **wild**; a pointer to freed memory is **dangling**. Both are unsafe.
- Initialise to NULL, and reset to NULL after `delete`.
```cpp
int* ptr_a = NULL; /* Assignment to 0 ok too*/
ptr_a = new int;
*ptr_a = 1337;
std::cout << *ptr_a;
delete ptr_a;
ptr_a = NULL;
```

### Dereference `*`
Printing the pointer shows the address; printing `*pointer` shows the value at that address.
```cpp
int a = 1337;
int* ptr_a = &a;
std::cout << ptr_a << std::endl; /*Output: Address */
std::cout << *ptr_a;             /*Output: 1337 */
```

---

## 10. Arrays and pointers

### Array name is a constant pointer
An array name is a constant pointer to element 0. You can copy it into a pointer, but you cannot assign to the array name.
```cpp
int a[10];
int* ptr_a;
ptr_a = a;      /* Address of first element assigned */
ptr_a = &a[0];  /* as above */
a = ptr_a;      /* ILLEGAL: array names are constant pointers */
```

> [!warning] You can point at an array, not overwrite its name
> `ptr = a` is fine; `a = ptr` never compiles. This is why an array cannot be reseated once declared.

### 2D dynamic arrays
A 2D dynamic array is an array of pointers: one `new []` for the row pointers, then one `new []` per row. Freeing reverses it, each row first, then the row array. The caller owns this memory and must free it.

```cpp
int** makeArray(int rows, int cols)
{
  int** aryReturn = new int*[rows];
  for(int r = 0; r < rows; r++)
    aryReturn[row] = new int[cols]; // (added) source writes 'row', loop var is 'r'
  return aryReturn;
}
```
```cpp
void caller()
{
  int** ary2D = makeArray(4,5);
  for(int r = 0; r < 5; r++)
    delete [] ary2D[row];          // (added) same 'row' vs 'r' slip
  delete [] ary2D;
  ary2D = NULL;
}
```

### Row major order
A multi-dimensional array is stored flat in row major order: all of row 0, then all of row 1. The 3x3 grid of primes sits in memory as one sequence:
```
2 3 5 7 11 13 17 19 23
```

---

## 11. Pointer arithmetic and sizeof

### Scaling
Pointer arithmetic is scaled: `pointer + 1` moves forward by `sizeof(pointed-to type)` bytes, not 1 byte. This is what lets you walk an array by incrementing a pointer until a stop value.

```cpp
char aryOdds = {'1', '3', '5', '7', '9', '\0'}; // (added) source omits [] on aryOdds
char* ptr = &aryOdds[0];
while(*ptr != '\0')
{
  std::cout << *ptr << std::endl;
  ptr++;
}
```

Because storage is flat (see: Row major order), the same scaled increment walks a whole multi-dimensional array in one loop.

### sizeof
Returns the byte size of a type. Takes either an identifier or a type name.
```cpp
int a = 1337;
int* ptr_a = &a;
std::cout << sizeof(int) << std::end; // (added) source writes std::end, should be std::endl
std::cout << sizeof(ptr_a);
```

### Indexing is pointer arithmetic
`N.B` `array[index] == *(array + index)`. Index 0 lands on the first element because it adds nothing to the base address, which is why indices start at 0.

---

## 12. Memory errors

**Leaks**
- Not freeing dynamic memory.
- Freeing only part of a multi-dimensional array by using `delete` where `delete []` was needed.

**Dangerous actions**
- Freeing a pointer twice.
- Freeing one never allocated.
- Dereferencing a freed pointer.
- Reading unallocated memory.
- Indexing or iterating past an array's end.
- Following a NULL pointer.

> [!warning] delete vs delete []
> On a block allocated with `new []`, plain `delete` frees only the first element and leaks the rest. Match the brackets: `new []` pairs with `delete []`.

---

## 13. Reference parameters

Two ways to pass a mutable parameter. Pointers work but need `*` to dereference and often `&` at the call. Reference parameters (`type &name`) let the function assign to the caller's variable directly, no operators.

```cpp
void foo(int* c)   { *c = 42; }
void bar(int &c)   {  c = 42; }
```

### const reference
`const` on a reference parameter keeps the argument unchanged; assigning to it is a compile error. Use it when you pass by reference for efficiency but must not modify.
```cpp
void bar(const int &c)
{
  c = 42; /* Would cause an error */
}
```

### Pointer passed by reference
`type* &name` is a pointer passed by reference, so reassigning the pointer inside the function is seen by the caller.
```cpp
void changeArray(int* &a)
{
  a = new int[ARRAY_SIZE];
}
```

---

## 14. Function pointers

A function pointer holds a function instead of a value, so a function can be chosen or swapped at runtime. Its type must match the target's return type and parameter list exactly.

Syntax: `returnType (*functionName)(parameter-list)`

```cpp
/*function pointer*/
double* (*m)(int*,int*,int);
/*function prototype*/
double* average(int*, int*, int);
/*A compatible function*/
double* average(int* a1, int* a2, int size)
{
  double* aryReturn = new int[size];
  for(int k = 0; k < size; k++)
    aryReturn[k] = (a1[k] + a2[k]) / 2.0;
  return aryReturn;
}
```
```cpp
int main()
{
  int up[3] = {1, 2, 3};
  int down[3] = {3, 2, 1};
  double* av = NULL;
  m = average;          /* Or m = &average; */
  av = m(up, down, 3);  /* Or *m(up, down, 3); */
}
```

**Limits**
- Still only loosely tied to the data it works on.
- New functions cannot be made at runtime.

---

## 15. Extending the type system

### typedef
Creates an alias for an existing type, which shortens awkward type names. Form: `typedef type alias`.
```cpp
typedef int* integerArray;
integerArray a = new int[5];
typedef (void (*m)()) voidFunction;
typedef int num;
```

### Programmer defined type vs abstract data type
- A **programmer defined type** is any new type you add to C++.
- An **abstract data type** is the stricter case: a programmer defined type where what it does (logical behaviour) is kept apart from how it does it (implementation).

---

## 16. Structs

`struct` groups related data into one named record.
- Without padding its size is the sum of its members; some compilers pad the end to align to a byte or word boundary.
- Instances can be declared right after the definition.

```cpp
struct recordName
{
  type var1;
  type var2;
  ...
} optional-list-of-instances;
```
```cpp
struct Student
{
  string name;
  int studentNumber;
} bob, thandi, suresh;
```

### Member access `.`
Reaches a struct's members to read or assign.
```cpp
Student linus;
linus.name = "Linus Torvalds";
linus.studentNumber = 123456;
cout << linus.name << endl;
```

### Returning a fixed array via a struct
Wrapping a fixed length array in a struct lets a function return it by value, unlike a raw array. Bonus: no `delete` needed, since nothing was dynamically allocated.
```cpp
struct FixedArray
{
  int val[5];
};
FixedArray makeArray()
{
  FixedArray a;
  for(int k = 0; k < 5; k++)
    a.val[k] = k;
  return a;
}
```

### Composition
A struct member can itself be a struct. This nesting is composition (also called aggregation), and it builds hierarchical records.
```cpp
struct BiographicalDetails
{
  string name;
  int age;
  bool gender;
};
struct Person
{
  string reasonForVisiting;
  BiographicalDetails details;
};
```

---

## 17. Object orientation techniques

Three techniques define object orientation (verbatim):

- **Encapsulation** The ability to combine data and the operations legal on those data in a single unit
- **Inheritance** The ability to derive new objects from existing objects
- **Polymorphism** The ability to use the same expression to denote different operations

---

## 18. Object orientation with C structs

A struct can hold a function pointer alongside its data, which almost gives encapsulation: data and its operation in one unit.
```cpp
struct EvenNumberGenerator
{
  int length;
  int* state;
  void (*generate)();
};
```
The problem: that `generate` has no way to know whose data to act on.

### The self pointer
Fix it by passing the instance itself. The function pointer takes a `NumberGenerator* self`, so each call is told which struct to operate on.
```cpp
struct NumberGenerator
{
  int length;
  int* state;
  void (*generate)(NumberGenerator* self);
};
```

> [!warning] The self pointer is what a class gives you for free
> Passing the instance by hand is the entire fragility of doing OO in C. A real class supplies `this` automatically; here, forget the argument and the operation acts on the wrong data or none.

### Lifecycle by hand
A `construct` function allocates and initialises an instance; a `destroy` function frees it and NULLs the pointer.
```cpp
NumberGenerator* construct(int length)
{
  NumberGenerator* gen = new NumberGenerator;
  *gen.length = length;              // (added) source uses *gen.length; correct form is gen->length
  *gen.state = new int[length];
  *gen.generate = generateEvenNumbers;
}
```
```cpp
void destroy(NumberGenerator* &gen)
{
  delete [] (*gen).state;
  delete gen;
  gen = NULL;
}
```

### The `->` operator
Combines pointer dereference with member access, so `(*gen).state` can be written `gen->state`.

---

## 19. Beyond C: classes

### Limits of the C-style approach
- Encapsulation works only if you always remember to pass the current instance.
- No mechanism for generalising existing structs (no inheritance).
- No automatic mechanism for polymorphism.

### The class keyword
A container for data and functionality, with built-in support for inheritance (generalisation) and polymorphic expressions.
```cpp
class ClassName
{
  type member;
  type memberFunction(paramater-list);
  ...
} optional-list-of-instances;
```

`N.B` Proper roles: **structs hold data; classes encapsulate data together with the functions legal on those data.**

---

## Do not forget

- Two's complement: absolute value, invert, add one, in that order.
- Never compare floats with `==`; 0.1 has no exact binary form.
- `new []` pairs with `delete []`; mismatching them leaks.
- An array name is a constant pointer, so `a = ptr` never compiles.
- `array[i]` is `*(array + i)`, which is why indices start at 0.
- Set pointers to NULL after `delete`; `delete` does not do it for you.
- C-style OO needs the self pointer passed by hand; a class supplies `this` automatically.
