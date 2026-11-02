---
module: CSC01B1
topic: Exam code sheet, code only
session: S14
tags: [exam-flagged, common-mistake, added]
---

> *Code only, nothing else. Read the heading, find the question, copy the shape. Names in the snippets come from the 2025 papers, so swap in the names your paper gives you. Full wrong and right pairs are in [[CSC01B1_Summary_ExamDayReview]].*

## Contents

- [[#Slips to check]] the nine lines that cost marks
- [[#Q2.1 blanks]] where the blank sits and what goes in it
- [[#Q2.2 and 2.3 exceptions]] the two class hierarchy and the try and catch
- [[#Q2.4 to 2.6 lists]] node, delete first, insert after, insert at the front, delete all, count, insert before
- [[#Q3.1 text files]] getline and istringstream, three versions
- [[#Q3.2 structs]] packed structs for A, B and C
- [[#Q3.3 and 3.4 binary files]] open, read, seek, record at an index, last record, count
- [[#Overwrite and append]] change one record, add a record
- [[#Q3.5 Big-O]] assumptions, counting rules, three worked results
- [[#Q4 DLLs]] module files, batch files, main files
  - [[#Interface and implementation files]] the block form of extern C
  - [[#Batch files that create the DLL]] explicit and implicit
  - [[#Main files]] explicit and implicit
  - [[#Batch files that build main.exe]] explicit and implicit
- [[#How this was checked]] what was compiled and what was not

## Slips to check

```
istringstream is(strLine);            the line goes in the brackets
int count = 0;                        inside the line loop
read(reinterpret_cast<char*>(&rec), sizeof(Rec))     binary uses read and write, never >> or <<
ios::in | ios::binary                 joined with |, never a comma
seekg(index * sizeof(Rec), ios::beg)  sizeof, not the type name
newNode->prev = nullptr;              when inserting at the front of a doubly list
typedef char* (*Name)(int);           a pointer to function
GetProcAddress(h, "genRoute")         name in quotes, cast in front
-fmodules-ts                          on both compile lines, interface file first
```

## Q2.1 blanks

```
first line  ___;                         module
export module ___;                       the name the question gives
before <typename T>                      export  template
inside the template brackets             typename
UJX(const UJX___ objOriginal)            <T>&    (just & if <T> is there)
operator=(___ UJX<T>& objRHS)            const
operator___(const UJX<T>& objRHS)        =
___ operator[](int intIndex)             T&      (and [] if the operator is the blank)
___ std::ostream& operator<<             friend  (then << and >>)
static ___ int DEFAULT_LENGTH            const   (or static if constexpr is given)
___* _data;                              T
```

## Q2.2 and 2.3 exceptions

```cpp
export class Exception {
public:
    Exception(string strMsg) : _strMsg(strMsg) {}
    string what() const { return _strMsg; }
private:
    string _strMsg;
};

export class FileException : public Exception {
public:
    FileException(string strMsg) : Exception(strMsg) {}
};
```

Paper A, the specific type is a range error:

```cpp
UJList<float> objList(10000);
try {
    objList[-1] = 10.65;
}
catch (RangeException& e) {
    cout << e.what() << endl;
}
```

Paper B and paper C, the specific type is a file error:

```cpp
try {
    list.readValuesFromFile("data.txt");       // paper C: objBuffer.saveToBIN("records.bin");
}
catch (FileException& e) {
    cout << e.what() << endl;
}
```

## Q2.4 to 2.6 lists

The node, for A and C. Paper B (doubly) adds `Node<T>* prev;`:

```cpp
template <typename T>
struct Node {
    T data;
    Node<T>* next;
};
```

Paper A, delete the first node:

```cpp
if (_head == nullptr) return;
Node<string>* temp = _head;
_head = _head->next;
if (_head == nullptr) _tail = nullptr;
delete temp;
```

Paper A, insert "T3.5" after "T3":

```cpp
Node<string>* current = _head;
while (current != nullptr && current->data != "T3")
    current = current->next;
if (current == nullptr) return;
Node<string>* newNode = new Node<string>;
newNode->data = "T3.5";
newNode->next = current->next;
current->next = newNode;
if (current == _tail) _tail = newNode;
```

Paper B, insert "N0" at the start of a doubly list:

```cpp
Node<string>* newNode = new Node<string>;
newNode->data = "N0";
newNode->prev = nullptr;
newNode->next = _head;
_head->prev = newNode;
_head = newNode;
```

Paper B, delete the whole list:

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

Doubly list, remove a value, every case:

```cpp
Node<T>* current = _head;
while (current != nullptr && current->data != value)
    current = current->next;
if (current == nullptr) return false;
if (current == _head && current == _tail) { _head = nullptr; _tail = nullptr; }
else if (current == _head) { _head = current->next; _head->prev = nullptr; }
else if (current == _tail) { _tail = current->prev; _tail->next = nullptr; }
else { current->prev->next = current->next; current->next->prev = current->prev; }
delete current;
return true;
```

Paper C (circular), count "S6":

```cpp
int count = 0;
if (_head != nullptr) {
    Node<string>* current = _head;
    do {
        if (current->data == "S6") count++;
        current = current->next;
    } while (current != _head);
}
```

Paper C (circular), insert "S5" before the first "S6":

```cpp
if (_head == nullptr) return;
Node<string>* previous = nullptr;
Node<string>* current = _head;
do {
    previous = current;
    current = current->next;
} while (current != _head && current->data != "S6");
if (current == _head) return;
Node<string>* newNode = new Node<string>;
newNode->data = "S5";
newNode->next = current;
previous->next = newNode;
```

A circular list ends with `!= _head`, never `nullptr`. This version does not find an "S6" in the first node, which cannot happen for the drawn list.

## Q3.1 text files

Open check, the same every time:

```cpp
fstream in_stream("file-name", ios::in);
if (in_stream.fail()) {
    cerr << "Error in opening file" << endl;
    return;
}
```

Paper A, at least one tap is `?` (the flag starts false):

```cpp
string strLine, strDay;
int intHour, intMinute;
char tap;
while (getline(in_stream, strLine)) {
    istringstream is(strLine);
    bool unclear = false;
    is >> strDay >> intHour >> intMinute;
    while (is >> tap) {
        if (tap == '?') unclear = true;
    }
    if (unclear) cout << strDay << " " << intHour << " " << intMinute << endl;
}
```

Paper B, tankers with fewer stops than required:

```cpp
string strLine, strID;
int intRq, seconds;
while (getline(in_stream, strLine)) {
    istringstream is(strLine);
    int count = 0;
    is >> strID >> intRq;
    while (is >> seconds) count++;
    if (count < intRq) cout << strID << endl;
}
```

Paper C, the highest mark per student:

```cpp
string strLine, strSN;
char chExt;
int mark;
while (getline(in_stream, strLine)) {
    istringstream is(strLine);
    is >> strSN >> chExt;
    int highest = 0;
    while (is >> mark) {
        if (mark > highest) highest = mark;
    }
    cout << strSN << " " << highest << endl;
}
```

## Q3.2 structs

Always `#pragma pack(push, 1)` above and `#pragma pack(pop)` below:

```cpp
struct Check {               // paper A, 1032 taps
    char chDay[10];
    int intHour;
    int intMinute;
    char chTaps[1032];
};
struct WaterTanker {         // paper B, up to 150 stops
    char charTanker[6];
    int intRqStops;
    int Stops[150];
};
struct Student {             // paper C, 9 character id, up to 10 marks
    char chName[9];
    char Edegree;
    int Pmarks[10];
};
```

## Q3.3 and 3.4 binary files

Open check, the same every time:

```cpp
fstream in_stream("file-name", ios::in | ios::binary);
if (in_stream.fail()) {
    cerr << "Error in opening file" << endl;
    return;
}
```

The one read, repeated in a loop that stops when it fails:

```cpp
while (in_stream.read(reinterpret_cast<char*>(&rec), sizeof(Student))) {
    // once per record
}
```

Paper A, 3.4, count the records:

```cpp
in_stream.seekg(0, ios::end);
int size = in_stream.tellg();
return size / sizeof(Check);
```

Paper A, 3.3, all taps unclear (the flag starts true):

```cpp
int intNum = countRecords(strFileName);
Check rec;
for (int i = 0; i < intNum; i++) {
    in_stream.read(reinterpret_cast<char*>(&rec), sizeof(Check));
    bool all = true;
    for (int j = 0; j < 1032; j++)
        if (rec.chTaps[j] != '?') all = false;
    if (all) cout << rec.chDay << " " << rec.intHour << " " << rec.intMinute << endl;
}
```

Paper B, 3.3, the record at an index:

```cpp
WaterTanker getRecord(int index) {
    fstream in_stream("water-tankers.dat", ios::in | ios::binary);
    WaterTanker rec;
    if (in_stream.fail()) { cerr << "Error in opening file" << endl; return rec; }
    in_stream.seekg(index * sizeof(WaterTanker), ios::beg);
    in_stream.read(reinterpret_cast<char*>(&rec), sizeof(WaterTanker));
    if (in_stream.fail()) { cerr << "Error in reading file" << endl; return rec; }
    return rec;
}
```

Paper B, 3.4, warn when a stop is longer than 10 800 seconds:

```cpp
int intNum = countRecords("water-tankers.dat");
for (int i = 0; i < intNum; i++) {
    WaterTanker rec = getRecord(i);
    for (int j = 0; j < rec.intRqStops; j++)
        if (rec.Stops[j] > 10800)
            cout << "Warning, tanker " << rec.charTanker << " spent more than 3 hours at a single stop." << endl;
}
```

Paper C, 3.3, the last record's student number:

```cpp
Student rec;
int size = sizeof(Student);
in_stream.seekg(-size, ios::end);
in_stream.read(reinterpret_cast<char*>(&rec), sizeof(Student));
cout.write(rec.chName, 9);
cout << endl;
```

Paper C, 3.4, is the number of records even:

```cpp
Student rec;
int count = 0;
while (in_stream.read(reinterpret_cast<char*>(&rec), sizeof(Student)))
    count++;
return count % 2 == 0;
```

## Overwrite and append

Overwrite record number `index` in place. It needs `ios::in | ios::out | ios::binary`, because `ios::out` alone wipes the file:

```cpp
fstream out_stream(filename, ios::in | ios::out | ios::binary);
if (out_stream.fail()) { cerr << "Error in opening file" << endl; return; }
out_stream.seekp(index * sizeof(Student), ios::beg);
out_stream.write(reinterpret_cast<const char*>(&newRec), sizeof(Student));
```

Add a record at the end. `ios::app` writes at the end, so no seek:

```cpp
fstream out_stream(filename, ios::app | ios::binary);
if (out_stream.fail()) { cerr << "Error in opening file" << endl; return; }
out_stream.write(reinterpret_cast<const char*>(&newRec), sizeof(Student));
```

## Q3.5 Big-O

The three assumptions to write:

```
1. Every operation takes the same time.
2. The number of operations is a fair measure of time.
3. N is the size of the problem.
Count each of = + < > == ++ [] return and a stream read as one operation. Loop header: 3 per pass.
Worst case: the if is true every pass.
```

Layout: mark each line with its count, write T(N), check with N = 1, 2, 3 by counting the code by hand, give the Big-O.

```
T(N) = outside + (header + body) x passes

array loop with one if       outside 3, per pass 6      T(N) = 6N + 2      O(N)
nested loop, inner own work  inner pass 7, outer pass 7N + 6, outside 2
                                                        T(N) = 7N^2 + 6N + 2    O(N^2)
file loop, while (in >> x)   outside 3, per pass 3      T(N) = 3N + 3      O(N)
```

Direct access is O(1): `getRecord(i)` and `countRecords` with `seekg` and `tellg`. Reading every record in a loop is O(N).

## Q4 DLLs

### Interface and implementation files

The module name comes from the question. `export` is inside the braces, in front of the function:

```cpp
export module LibFilter;

extern "C"
{
	export bool isInvalid(char arrReadings[], int intLength);
}
```

The implementation file repeats the function with its body. `module Name;` has the module's name, not the file name:

```cpp
module LibFilter;

extern "C"
{
	bool isInvalid(char arrReadings[], int intLength)
	{
		for (int i = 0; i < intLength; i++)
		{
			if (arrReadings[i] == '?')
			{
				return true;
			}
		}
		return false;
	}
}
```

### Batch files that create the DLL

Explicit linking, nothing extra:

```
g++ -std=c++23 -fmodules-ts -c RouteAPI.cpp
g++ -std=c++23 -fmodules-ts -c RouteAPI.impl.cpp
g++ -shared -o route-generator.dll RouteAPI.o RouteAPI.impl.o
```

Implicit linking, the import library added to the last line. It is `-Wl` with a lowercase L, and it has no spaces:

```
g++ -shared -o route-generator.dll RouteAPI.o RouteAPI.impl.o -Wl,--out-implib,libroute-generator.a
```

The import library name is `lib` + the DLL name without `.dll` + `.a`. The DLL name comes from the question.

### Main files

Explicit linking, paper B 4.1:

```cpp
#include <iostream>
#include <windows.h>
using namespace std;

typedef char* (*GenRouteFn)(int);

int main() {
    HINSTANCE h = LoadLibrary("route-generator.dll");
    if (h) {
        GenRouteFn f = (GenRouteFn)GetProcAddress(h, "genRoute");
        if (f) cout << f(10) << endl;
        FreeLibrary(h);
    }
    return 0;
}
```

Implicit linking, paper C 4.3, a dynamic array of 10 random reals in [0, 100]:

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
import CalcLibrary;
using namespace std;

int main() {
    srand(time(nullptr));
    double* arrMarks = new double[10];
    for (int i = 0; i < 10; i++)
        arrMarks[i] = 100.0 * rand() / RAND_MAX;
    cout << calculateEM(arrMarks) << endl;
    delete[] arrMarks;
    return 0;
}
```

### Batch files that build main.exe

Implicit, with `util.dll` already in the folder. Compile the interface file and `main.cpp`, then link. `-l` takes the DLL name without `.dll`:

```
g++ -std=c++23 -fmodules-ts -c LibFilter.cpp
g++ -std=c++23 -fmodules-ts -c main.cpp
g++ -o main.exe main.o -L. -lutil
```

Explicit, compiled normally, with no `-L` and no `-l`:

```
g++ -std=c++23 -c main.cpp
g++ -o main.exe main.o
```

## How this was checked

The snippets in the sections Q2.2 and 2.3 exceptions, Q2.4 to 2.6 lists, Q3.1 text files, Q3.3 and 3.4 binary files, and Overwrite and append were compiled with g++ 13 on Linux (C++20, with warnings on) and run on small test files. The module interface, implementation and implicit client were compiled and linked on Linux with a `.so` in place of a `.dll`.

Not run: the Windows only parts, which are `LoadLibrary`, `GetProcAddress`, `FreeLibrary`, the `.dll` file names, the import library, and the explicit main and its batch lines. The paper C random array `main` was typed from the paper's wording and not run. The Q2.1 table and the Big-O counts were read and counted by hand against the papers.

---
*CDG v11 | written S14 | 2026-11-02*
