---
module: CSC01B1
topic: Exam day review, mistakes and advice
session: S14
tags: [common-mistake, exam-flagged, struggle, added]
---

> *It is 14:05 on exam day as I write this. Everything below is something that went wrong for you at least once today, so none of it is new theory. If a line here does not make sense, trust the code block and not my wording.*

## Contents

- [[#Definitions]] words used in this note, one plain line each
- [[#Exam procedure]] time plan, what to do first, last five minutes check
- [[#Open items to check first]] slips that have not yet been fixed under retest
- [[#Mistakes by pattern]] every slip from today, grouped
  - [[#Text files]] istringstream, counters, reading order
  - [[#Binary files]] read and write, seekg, unknown record counts
  - [[#Lists and templates]] doubly list, insert at the front, delete the list
  - [[#Linking and batch files]] explicit and implicit linking, batch lines
  - [[#UML and short answers]] UML points, exceptions, Big-O, object concepts
- [[#Code to know]] checked code you can rewrite from memory
  - [[#Text file template]] getline and istringstream
  - [[#Binary read and write]] read, write, seek, read until it fails
  - [[#Doubly list remove]] every case
  - [[#Insert at the front and delete the whole list]] two short patterns
  - [[#Explicit linking main]] the LoadLibrary pattern
  - [[#Batch files]] creating a DLL, explicit versus implicit
- [[#Advice from today]] working habits that helped
- [[#Scope as reported]] what the lecturer said is and is not examined
- [[#How this was checked]] what was compiled and what was not

## Definitions

- istringstream: a stream that reads from a string instead of a file. The string goes in the brackets.
- getline: reads one whole line from a stream into a string.
- binary file: a file of raw bytes, one record after another. You use `read` and `write`, never `>>` or `<<`.
- record: one struct stored in a binary file. Every record is `sizeof(Type)` bytes, so record number `Index` starts at `Index * sizeof(Type)`.
- seekg and seekp: move the read position and the write position, counted in bytes. `ios::beg` counts from the start, `ios::end` from the end, so going backwards from the end needs a negative number.
- explicit linking: the program loads the DLL itself while running, with `LoadLibrary`, `GetProcAddress` and `FreeLibrary`.
- implicit linking: the DLL is connected when the program is built, so you call the function like a normal one. It needs the import library.
- import library: the small `.a` file made when the DLL is built with `-Wl,--out-implib,lib<name>.a`. The client links to it with `-L. -l<name>`.
- module interface file: the `.cpp` that starts with `export module Name;` and declares what is exported.
- extern "C": turns off C++ name mangling, so the DLL function keeps its plain name.
- aggregation versus composition: both are has-a. In aggregation the whole does not manage the lifetime of its parts (hollow diamond). In composition it does (filled diamond).
- slicing: copying a derived object into a base object, which throws away the derived part.
- stack versus queue: a stack is last in, first out. A queue is first in, first out.

Anatomy of the explicit linking line, so each word points at something:

```cpp
GenRouteFn f = (GenRouteFn)GetProcAddress(h, "genRoute");
// GenRouteFn   the pointer to function type, from the typedef
// (GenRouteFn) the cast of what GetProcAddress returns
// h            the handle LoadLibrary gave back
// "genRoute"   the function name, in quotes
```

## Exam procedure

- Time plan agreed on Sunday for a 2 hour, 100 mark paper: Q1 22 minutes, Q2 34, Q3 34, Q4 22, 8 spare.
- UML is capped at 6 minutes. In paper 2025-B it took you 20 minutes. Draw only what the question lists, then move on.
- In a file handling question decide first: text file or binary file. Text means `getline` and `istringstream`. Binary means `read` and `write` with `&rec` and `sizeof`.
- If the number of records is unknown, loop until the read fails.
- If a list function stops making sense, trace it with a three node list, 5, 7, 9, before writing more.
- Last five minutes, check these in order:
  - `istringstream is(strLine)` has the line in the brackets
  - every counter is set to 0 inside the line loop
  - modes are joined with `|`
  - `sizeof(Type)` is there wherever bytes are counted
  - `-fmodules-ts` is on both compile lines
  - `FreeLibrary(h)` is there
  - every function that returns a value has `return` on every path
  - braces are balanced
- Skipping a sub-question loses its whole mark. Writing only the file opening and error check still earns something.

## Open items to check first

<span style="color:#f08c00">Open:</span> the line goes in the istringstream brackets, `is(strLine)`. Slipped three times today, once right after answering it correctly.

<span style="color:#f08c00">Open:</span> counters and `i` are declared inside the line loop with `= 0`, not above it, and not inside the inner mark loop.

<span style="color:#f08c00">Open:</span> `>>` does not work on a binary file. Use `read` and `write`.

<span style="color:#f08c00">Open:</span> `-fmodules-ts` on both compile lines of the batch file, interface file first.

<span style="color:#f08c00">Open:</span> explicit linking: `typedef char* (*Name)(int);`, the function name in quotes with a cast, and `FreeLibrary`. The retake was skipped.

<span style="color:#f08c00">Open:</span> inserting at the front: `newNode->prev = nullptr;`.

<span style="color:#f08c00">Open:</span> exceptions are destroyed newest first, like a stack of plates.

<span style="color:#f08c00">Open:</span> the copy constructor takes `const UJVector<T>&`, with the `&`.

<span style="color:#f08c00">Open:</span> Big-O: say it is the worst case, count `[]` as an operation, and write the final line O(N).

<span style="color:#f08c00">Open:</span> "A Student writes an Exam" is association.

Resolved today: `seekg` needs `Index * sizeof(Type)`. Binary modes use `|`. Doubly list delete, case by case. Delete the whole list inside a loop. Reading until the read fails.

> *The istringstream slip is the one to watch. It is a single line, and it is the first thing to check when you finish a text file question.*

## Mistakes by pattern

### Text files

```cpp
istringstream is(chName);                      // wrong: the string in the brackets is not the line
istringstream is(strLine);                     // right

int count;  while (getline(in, strLine)) { }   // wrong: never reset, carries over to the next line
while (getline(in, strLine)) { int count = 0; }// right

is >> Edegree;                                 // wrong: the id or name was never read first
is >> strSN >> Edegree;                        // right: read in the order they appear on the line

int Pmarks[];                                  // wrong: an array needs a size, and you did not need one
int highest = 0; while (is >> mark) if (mark > highest) highest = mark;   // right

sizeof(Pmarks) - 1                             // wrong: that is bytes, not the number of marks
```

A student number or id of 9 or 6 characters needs room for the terminator if you read it into a `char` array with `>>`. Reading into a `string` avoids that.

### Binary files

```cpp
in_stream >> rec.charTanker;                                        // wrong on a binary file
in_stream.read(reinterpret_cast<char*>(&rec), sizeof(WaterTanker)); // right

fstream f(name, ios::in, ios::binary);         // wrong: comma, and in is for reading
fstream f(name, ios::out | ios::binary);       // right for writing

reinterpret_cast<char*>(student[i])            // wrong: needs the address
reinterpret_cast<const char*>(&students[i])    // right when the array is const

seekg(Index * WaterTanker, ios::beg);          // wrong: a type is not a number
seekg(Index * sizeof(WaterTanker), ios::beg);  // right

for (i < maxCount) { read; count++; }          // wrong: counts failed reads too
while (count < maxCount && in.read(...)) count++;   // right
```

A record is one block of bytes. Reading it in one go fills the id, the stop count and all the stops together, so nothing needs to be skipped. If you read it piece by piece, use `read` with exact sizes and always read the whole fixed size, or the next record starts in the wrong place.

### Lists and templates

```cpp
newNode->next = _head;                         // wrong: prev was never set, it holds junk
newNode->prev = nullptr;                       // add this line before next = _head
```

- Doubly list delete: ask who points at the node. The node before it, the node after it, `_head` if it is first, `_tail` if it is last. Fix every one that applies.
- A singly list answer fixes only one neighbour. In a doubly list that leaves the next node's `prev` pointing at a deleted node.
- Delete the whole list inside the loop: keep `temp`, move `current` on, then `delete temp`. After the loop set `_head` and `_tail` to `nullptr`.
- Copy constructor: `UJVector(const UJVector<T>& objOriginal);`. Without the `&` it copies by value and cannot work.
- Template header: member functions defined outside the class need `template <typename T>` above them.

### Linking and batch files

```cpp
typedef char* Name(int);                       // wrong: that is a function type
typedef char* (*Name)(int);                    // right: pointer to function

GetProcAddress(h, genRoute);                   // wrong: not in quotes, no cast
(Name)GetProcAddress(h, "genRoute");           // right

FreeMemory;                                    // wrong: not a function
FreeLibrary(h);                                // right
```

- Batch file: add `-fmodules-ts` to both compile lines, interface file first.
- The import library line is only for DLLs that will be linked implicitly.
- The function name in `extern "C"` is what the DLL exposes, with no mangling.

### UML and short answers

- A real number is `double`.
- If a value is accessible after creation, it needs a getter.
- A collection gets a multiplicity such as `0..*`, not a single attribute.
- Values set during creation go into the constructor as parameters.
- 1.4 (iostream is both an istream and an ostream, so multiple inheritance): you appeared to choose the flawed option. I believe the answer is True. This was not checked against a memo.
- Association: A Student writes an Exam. Composition or aggregation: an Assessment belongs to a Module. Inheritance: an Exam is an Assessment. The middle one was not checked against a memo.

## Code to know

### Text file template

```cpp
fstream in_stream("orders.txt", ios::in);
if (in_stream.fail()) {
    cerr << "Error" << endl;
    return;
}
string strLine, strID;
int intRq, price;
while (getline(in_stream, strLine)) {
    istringstream is(strLine);
    int count = 0;
    is >> strID >> intRq;
    while (is >> price) count++;
    if (count < intRq) cout << strID << endl;
}
```

Highest mark per line, no array:

```cpp
while (getline(in_stream, strLine)) {
    istringstream is(strLine);
    is >> strSN >> Edegree;
    int highest = 0;
    int mark;
    while (is >> mark) {
        if (mark > highest) highest = mark;
    }
    cout << strSN << " " << highest << endl;
}
```

### Binary read and write

Write all records:

```cpp
fstream out_stream(filename, ios::out | ios::binary);
for (int i = 0; i < count; i++)
    out_stream.write(reinterpret_cast<const char*>(&students[i]), sizeof(Student));
```

Read the record at an index:

```cpp
fstream in_stream("water-tankers.dat", ios::in | ios::binary);
in_stream.seekg(Index * sizeof(WaterTanker), ios::beg);
in_stream.read(reinterpret_cast<char*>(&rec), sizeof(WaterTanker));
```

Read until it fails, which also gives the last record and the count:

```cpp
Student rec, last;
int count = 0;
while (in_stream.read(reinterpret_cast<char*>(&rec), sizeof(Student))) {
    last = rec;
    count++;
}
// last is the last record, count % 2 == 0 means an even number of records
```

Last record by seeking from the end:

```cpp
int size = sizeof(Student);
in_stream.seekg(-size, ios::end);
in_stream.read(reinterpret_cast<char*>(&rec), sizeof(Student));
```

Warn when a stop is longer than 3 hours, using `getRecord`:

```cpp
int n = countRecords("water-tankers.dat");
for (int i = 0; i < n; i++) {
    WaterTanker rec = getRecord(i);
    for (int j = 0; j < rec.intRqStops; j++)
        if (rec.Stops[j] > 10800)
            cout << "Warning, tanker " << rec.charTanker << " spent more than 3 hours at a single stop." << endl;
}
```

> *You asked how to skip the name and the stop count. You do not skip fields. Read the whole record in one go, or use getRecord, and the fields are already separated.*

### Doubly list remove

```cpp
template <typename T>
bool DList<T>::remove(const T& value)
{
    Node<T>* current = _head;
    while (current != nullptr && current->data != value)
        current = current->next;
    if (current == nullptr)
        return false;

    if (current == _head && current == _tail) { _head = nullptr; _tail = nullptr; }
    else if (current == _head) { _head = current->next; _head->prev = nullptr; }
    else if (current == _tail) { _tail = current->prev; _tail->next = nullptr; }
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
    }
    delete current;
    return true;
}
```

> *You fixed this one case by case after tracing 5, 7, 9. If a list function stumbles in the exam, do that trace first.*

### Insert at the front and delete the whole list

```cpp
Node<string>* newNode = new Node<string>;
newNode->data = "N0";
newNode->prev = nullptr;
newNode->next = _head;
_head->prev = newNode;
_head = newNode;
```

```cpp
Node<string>* current = _head;
while (current != nullptr) {
    Node<string>* temp = current;
    current = current->next;
    delete temp;
}
_head = nullptr;
_tail = nullptr;
```

### Explicit linking main

```cpp
#include <iostream>
#include <windows.h>
using namespace std;

typedef char* (*GenRouteFn)(int);

int main() {
    HINSTANCE h = LoadLibrary("route-generator.dll");
    if (h) {
        GenRouteFn f = (GenRouteFn)GetProcAddress(h, "genRoute");
        if (f) {
            cout << f(10) << endl;
        }
        FreeLibrary(h);
    }
    return 0;
}
```

### Batch files

Creating the DLL, for explicit linking:

```
g++ -std=c++23 -fmodules-ts -c RouteAPI.cpp
g++ -std=c++23 -fmodules-ts -c RouteAPI.impl.cpp
g++ -shared -o route-generator.dll RouteAPI.o RouteAPI.impl.o
```

Creating the DLL, for implicit linking: the same, with the import library added at the end of the last line.

```
g++ -shared -o route-generator.dll RouteAPI.o RouteAPI.impl.o -Wl,--out-implib,libroute-generator.a
```

Building a client that links implicitly:

```
g++ -std=c++23 -fmodules-ts -c CalcLibrary.cpp
g++ -std=c++23 -fmodules-ts -c main.cpp
g++ -o main.exe main.o -L. -lem-calculator
```

Module interface file for that DLL:

```cpp
export module CalcLibrary;

export extern "C" double calculateEM(double* arrMarks);
```

Telling the questions apart: "explicitly links" means the `LoadLibrary` main. "creates the DLL" means compile each file, then `-shared -o`. "implicitly link" means the client batch with `-L.` and `-l`.

## Advice from today

- Do the question you can finish first, then come back. In 2025-B you left the UML to the end and finished the rest with time to spare.
- When you do not know how many records or marks there are, do not look for the count. Let the loop stop when the read fails.
- When a technical word does not land, ask for the code, not the explanation. Several things today only made sense as a short block of code.
- When a function is wrong, trace it with a tiny example. Five, seven, nine found three list bugs in a few minutes.
- Writing only the file opening and the error check, which you did for one sub-question of paper C, is better than a blank page, but it is the least you can write. The read until it fails loop would have earned more.
- Do not learn anything new before the paper. Today's new material was implicit linking, and it is not on your must know list.

> *You finished paper B with time to spare, and the slips that cost you are on this page. Read it once, then rest.*

## Scope as reported

As you reported it on 1 November, with no memo to confirm it: explicit linking and function pointer basics are examined, doubly and circular lists are examined, stacks and queues are examined. Recursion, sorting and searching are not examined.

## How this was checked

The code in the sections Text file template, Binary read and write, Doubly list remove, and Insert at the front and delete the whole list was compiled with g++ 13 on Linux (C++20, with warnings on) and run on small test files. The results matched what each snippet is meant to do.

The module interface file, the implementation file, the batch lines and the implicit client were compiled and linked on Linux with a `.so` in place of a `.dll`. The Windows only parts were not run: `LoadLibrary`, `GetProcAddress`, `FreeLibrary`, and the `.dll` and import library file names. Those follow your lecture 6 slides.

Marks given on the practice papers were my own estimates, with no memo, and are not recorded here.

---
*CDG v11 | written S14 | 2026-11-02*
