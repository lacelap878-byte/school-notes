---
module: CSC01A1
topic: Command Line, Numeracy and C++ Basics
session: S1
tags: [definition, worked-example, common-mistake, added]
---

# CSC01A1 Notes S1: Command Line, Numeracy and C++ Basics

Source: L01 "Command Line Interface Usage and Numeracy for Computer Scientists" and L02 "An Overview of Computers and Programming Languages and Basic Elements of C++" (2026 slides). CommandLineInterfaceUsage.pdf is an older version of the L01 CLI half and adds nothing new. Short revision notes in syntax-sheet style: the code is my own, written to fit each lesson, not copied from the slide screenshots.

Checked: every C++ snippet was compiled with g++ 13 (`-std=c++23 -Wall -Wextra`) and run; the base conversions were checked with `std::bitset` on 15 Nov 2026. The cmd.exe commands were not run (no Windows shell here).

## Command line interfaces (source: L01)

A command line interface (CLI), or terminal, controls the computer through text. Every instruction has the form:

```text
PROMPT  COMMAND  PARAMETER-LIST
```

- PROMPT: the system is waiting; usually shows the current directory.
- COMMAND: the action (built into the CLI, the OS, or an executable).
- PARAMETER-LIST: options, input sources, output destinations.

cmd.exe (the Windows Command Processor, once the "DOS prompt"):

| Task | Command |
|---|---|
| Show current directory | `echo %cd%` |
| Change drive | `T:` |
| Change drive and directory | `cd /d T:\` |
| Go to a subdirectory / parent | `cd DirectoryName` / `cd..` |
| List directory / show a text file | `dir` / `type file.txt` |
| Make directory | `mkdir DirectoryName` |
| Delete file / empty directory / whole tree | `del file` / `rmdir Dir` / `del /s /q Dir` |
| Copy / move / rename | `copy Src Dest` / `move Src Dest` / `rename Old New` |
| Help on any command | `command /?` |

- `.` is the current directory, `..` the parent. Put names with spaces in quotes: `cd "My Files"`. TAB auto-completes names.
- Batch file: commands saved in a `.BAT` file. `@ECHO OFF` hides the commands, `*` is a wildcard (`DEL *.PNG` deletes every file ending in .PNG), `PAUSE` waits for a key.
- Redirection sends output to files or other programs. (added: `>` writes to a file, `>>` appends, `<` reads input from a file, `|` pipes output into another program, e.g. `dir > list.txt`.)
- PowerShell: the object-oriented successor to cmd.exe. Commands are cmdlets named verb-noun, case insensitive; `get-help` explains them, and output can be piped.

## Number systems (source: L01)

- Modern numbers are positional: a digit's place sets its weight. The base (radix) is the number of distinct digits.
- Computers use binary (base 2) because data is stored as the presence or absence of a state.

```text
Binary to decimal:  11101 (base 2) = 1x2^4 + 1x2^3 + 1x2^2 + 0x2^1 + 1x2^0 = 16 + 8 + 4 + 0 + 1 = 29
Decimal to binary:  divide by 2, keep the remainders, read them bottom up
  29 / 2 = 14 r 1
  14 / 2 =  7 r 0
   7 / 2 =  3 r 1
   3 / 2 =  1 r 1
   1 / 2 =  0 r 1   ->  11101
```

- Hexadecimal (base 16, digits 0 to 9 then A to F): each hex digit is 4 bits. BEEF (base 16) = 11x16^3 + 14x16^2 + 14x16^1 + 15x16^0 = 48879; E1 (base 16) = 1110 0001.
- Octal (base 8, digits 0 to 7): each digit is 3 bits. 171 (base 8) = 1x64 + 7x8 + 1 = 121; 110 111 (base 2) = 67 (base 8).
- (added) When grouping binary into 4s (hex) or 3s (octal), start from the right and pad the left with zeros. The slide says start from the left, which only works when the length is already a multiple of the group size.
- Binary Coded Decimal: each decimal digit becomes its own 4 bits. 123 = 0001 0010 0011.
- Bit = one 0 or 1; nibble = 4 bits; byte (octet) = 8 bits; word size = the number of bits the architecture handles in one operation (affects range and accuracy).

## Boolean logic and binary arithmetic (source: L01)

- 1 is true and 0 is false. Bitwise: NOT 11101 = 00010; 11101 XOR 10111 = 01010.
- Precedence: NOT, then AND, then XOR, then OR.
- The operators are associative, distributive and commutative. De Morgan: NOT(A OR B) = NOT(A) AND NOT(B); NOT(A AND B) = NOT(A) OR NOT(B).
- Addition: 1 + 1 = 0 carry 1. Subtraction: 0 - 1 = 1 borrow 1. Multiplication: only 1 x 1 = 1.

Negative numbers:
- Sign and magnitude: the leftmost bit is the sign, so 00011101 is 29 and 10011101 is -29. Addition then needs extra work.
- Two's complement (8-bit): flip every bit (one's complement), then add 1.

```text
-29:  29 = 00011101  ->  NOT = 11100010  ->  +1 = 11100011
```

## Computers and programming languages (source: L02)

- Hardware: CPU, main memory (RAM: every program and its data must be loaded here to run; lost when power is off; cells have addresses), secondary storage (permanent), input and output devices.
- Software: system programs (the operating system manages memory, I/O and storage) and application programs.
- Machine language is 0s and 1s; assembly uses mnemonics (`LOAD rate`, `MULT hours`, `STOR wages`) translated by an assembler; high-level languages (C++, Java, Python) are translated by a compiler.
- 1 KB = 2^10 = 1024 bytes, 1 MB = 2^20 bytes, 1 GB = 2^30 bytes, and so on in steps of 1024. ASCII has 128 characters ('A' is 65, '3' is 51).
- Processing a C++ program: write source (.cpp) in an editor, the preprocessor handles `#` lines, the compiler checks syntax and produces object code, the linker joins it with library code into an executable, the loader puts it in memory, then it runs. The course uses Notepad++ and the VPL, not an IDE.
- A compiler guarantees the program follows the language rules, not that it is correct.
- Algorithm: a step-by-step problem-solving process that finishes in finite time. Analyse the problem, split it into subproblems, design and test the algorithm, then code it.
- Structured design (CSC01A1) divides a problem into smaller subproblems (top-down, stepwise refinement, modular programming); object-oriented design comes in CSC01B1.
- C++ was designed by Bjarne Stroustrup at Bell Labs in the early 1980s. Standards: 1998, C++11, 14, 17, 20, 23. This course uses C++23.

## C++ program structure and tokens (source: L02)

```cpp
#include <iostream>   // preprocessor directive: no semicolon
#include <string>
using namespace std;  // cin, cout and string live in namespace std

int main()            // heading of main; every program has exactly one main
{
    // body: declaration and executable statements, each ending in ;
    return 0;
}
```

- A statement is the basic unit and always ends with a semicolon. Syntax rules say what is legal; semantic rules give meaning. `2 + 3 * 5` and `(2 + 3) * 5` are both legal but mean different things.
- Comments: `// one line` and `/* many lines */`.
- Tokens: special symbols (`+ - * / ; , <= != == >=`), reserved words (`int`, `double`, `char`, `const`, `void`, `return`, `bool`, `true`, `false`), identifiers.
- Identifier rules: letters, digits and underscore, starting with a letter or underscore; case sensitive. Illegal: `employee Salary` (space), `Hello!`, `one+two`, `2nd`. `cin` and `cout` are predefined identifiers (can be redefined, but do not).

## Data types (source: L02)

| Type | Values | Size |
|---|---|---|
| `bool` | `true`, `false` | 1 byte |
| `char` | -128 to 127, one character in single quotes: `'A'`, `' '` | 1 byte |
| `int` | -2147483648 (-2^31) to 2147483647 (2^31 - 1) | 4 bytes |
| `long long` | -2^63 to 2^63 - 1 | 8 bytes |
| `float` | about 6 or 7 significant digits (single precision) | 4 bytes |
| `double` | about 15 significant digits (double precision) | 8 bytes |

- (added) The slide's table has two typos: the `int` minimum is -2147483648, and `long long` takes 8 bytes (64 bits), not 64 bytes. Both were checked with `sizeof`.
- `unsigned` types store only non-negative values in the same space. Sizes and ranges can differ between compilers.
- `string` (from `<string>`) is a sequence of characters in double quotes; positions start at 0; `"William Jacob"` has length 13.

## Variables, expressions and input and output (source: L02)

```cpp
const double CM_PER_INCH = 2.54;   // named constant: value fixed, set when declared
int feet {5};                      // braced initialiser (rejects narrowing conversions)
int inches(10);                    // functional notation
double total = (feet * 12 + inches) * CM_PER_INCH;   // assignment notation; 177.8

cout << 7 / 2 << " " << 7 % 2 << " " << 7.0 / 2;      // 3 1 3.5
cout << static_cast<double>(7) / 2;                   // 3.5
cout << static_cast<int>(3.9);                        // 3 (truncates, does not round)
cout << 3 * 7 - 6 + 2 * 5 / 4 + 6;                    // 23

int x = 5;  int y = ++x;    // pre-increment: x becomes 6, then y = 6
int a = 5;  int b = a++;    // post-increment: b = 5, then a becomes 6
x += 4;                     // compound: same as x = x + 4 (also -=, *=, /=, %=)

string name;
cin >> name;                // >> stops at the first whitespace
cin >> feet >> inches;      // several values at once
cout << "Hi " << name << "\n" << "Next line" << endl;
```

- Arithmetic: `+ - * / %`. `%` works only on integers. `/` on two integers truncates.
- Precedence: brackets, then `* / %`, then `+ -`; equal levels go left to right. Assignment goes right to left, so `x = y = z` assigns `z` to `y`, then to `x`.
- Mixed expression: if an operator has one `int` and one `double` operand, the `int` is converted and the result is `double`. Implicit conversion is type coercion; `static_cast<type>(expr)` is explicit.
- Every variable must be declared (and given a value) before use.
- Escape sequences: `\n` newline, `\t` tab, `\b` backspace, `\r` return to line start, `\\`, `\'`, `\"`. `endl` is a manipulator that ends the line.
- Always print a prompt line before `cin`.

> [!warning] Integer division (added)
> `5 / 2` is 2, not 2.5. Make one operand a `double` (`5.0 / 2` or `static_cast<double>(5) / 2`) before dividing.

- Debugging: the compiler reports syntax errors with line numbers (a missing `;`, an undeclared identifier). Fix the first error first; one mistake can cause several messages.
- Style: self-documenting names (`CENTIMETERS_PER_INCH`, `annualSale` or `annual_sale`), one declaration per line, comments for purpose and author.

## Do not forget

- Two's complement: flip the bits, then add 1.
- Group binary from the right when converting to hex or octal.
- `int / int` truncates; `%` is integers only.
- `++x` changes x before it is used; `x++` uses the old value first.

---
*CDG v13 | written S1 | 2026-11-15*
