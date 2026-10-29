---
module: CSC01B1
topic: File Handling
session: S7
tags: [definition, worked-example, common-mistake, exam-flagged, struggle, added]
---

# File Handling (CSC01B1, Lecture 6)

Covers secondary storage, streams, sequential file input and output, open modes and flags, output formatting, random access files, writing structs to disk (byte alignment and padding), and reusable components as DLLs. Read top to bottom the first time; after that the headings are the index. Cross references point by heading name.

`N.B` marks the thing most likely to be tested or forgotten. Slide code is reproduced as the lecturer wrote it. Where the slide code has an error, a fix is marked `(added)`. Content beyond the slides is marked `(added)`, and examples I built are marked `(composite)`. Every number and code block marked `(added)` or `(composite)` was compiled and run.

---

## Secondary storage and why files exist (slides 3 to 7)

### The memory hierarchy
Fast storage and large storage are hard to get in one device, so memory is arranged as a hierarchy, each level trading speed for capacity and price.

1. Registers: small, very fast, very expensive
2. Processor cache: small, very fast, very expensive
3. RAM: medium size, fast, affordable
4. Flash and USB memory: larger, slower, cheap
5. Hard drives: very large, slow, very cheap
6. Tape backup: very large, very slow, affordable

Registers, cache and RAM hold data only while the power is on (volatile). Everything from flash downward keeps its data with the power off. That non-volatile tier is what "secondary storage" means.

### Why use files
- A file stores data permanently: output written to a file lasts after the program ends.
- An input file can be reused over and over, so test data is not retyped on every run.
- Files let a program deal with data sets far larger than anyone would type by hand.

---

## Streams (slides 9 to 11)

### The standard streams
- `cin`: standard input stream (keyboard)
- `cout`: standard output stream (terminal)
- `cerr`: standard error stream (usually also the terminal)

They come from `#include <iostream>` and `using namespace std;`.

### What a stream is
A stream is a flow of characters (or other data). An input stream flows from some external source into the program. An output stream flows from the program to some external destination.

The stream is the channel, not the source or destination itself. Once a stream is connected to something, it is used with the insertion (`<<`) and extraction (`>>`) operators exactly as before:
```cpp
int i;
in_stream >> i;
```
Where the value comes from depends on what `in_stream` happens to be connected to. (See also the stream operators built in [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]].)

### Why there are so many "cout-like" objects (added)
`cout`, `cin`, `fin`, `fout` and `in_stream` are not different mechanisms. They are all objects of the same stream classes. `cout` is an `ostream` object that happens to be connected to the terminal already. `ofstream fout;` creates the same kind of object and you connect it to a file yourself. This is why `setf()`, `precision()` and `width()` work identically on any of them: the formatting code is written once and works whatever the stream is connected to.

### What a file is
A file is a named block of arbitrary information, typically on long-term storage. Data flowing from the file into the program is reading the file. Data flowing from the program into the file is writing it.

---

## Sequential file input and output (slides 12 to 19)

### The four-step pattern
Sequential access means the program reads from the start of the file and moves forward only. It cannot backtrack or fast-forward. That is the same behaviour as the keyboard.

1. Declare the stream object
2. Connect the stream to a file
3. Read or write
4. Close the connection

`N.B` A stream object cannot be assigned with `=` the way an `int` can. You connect it with `.open()`, not `=`. (Streams also cannot be copied, which is why they are passed by reference to functions; see Streams as function parameters.)

### Setting up and connecting
Needs `#include <fstream>` and `using namespace std;`. Two classes: `ifstream` for input, `ofstream` for output.
```cpp
ifstream in_stream;
ofstream out_stream;
in_stream.open("infile.dat");
out_stream.open("outfile.dat");
```
The names inside `.open()` are the file names as the operating system knows them.

The default `.open()` creates the file if it does not exist and empties it if it does.

Reading, writing and closing look exactly like `cin` and `cout`:
```cpp
int a;
in_file >> a;
out_file << a;
in_file.close();
out_file.close();
```

### Worked example (source, slide 16)
Reads three numbers from `infile.dat`, sums them, and writes the sum into `outfile.dat`. `infile.dat` is not changed. Nothing is read from the keyboard or shown on the screen.
```cpp
//Reads three numbers from the file infile.dat, sums the numbers,
//and writes the sum to the file outfile.dat.
#include <fstream>

int main( )
{
    using namespace std;
    ifstream in_stream;
    ofstream out_stream;

    in_stream.open("infile.dat");
    out_stream.open("outfile.dat");

    int first, second, third;
    in_stream >> first >> second >> third;
    out_stream << "The sum of the first 3\n"
               << "numbers in infile.dat\n"
               << "is " << (first + second + third)
               << endl;

    in_stream.close( );
    out_stream.close( );

    return 0;
}
```

### Checking that open succeeded
Opening can fail: the disk may be full, the file may belong to another user, it may be open exclusively elsewhere, or the permissions may not allow it. Test with `.fail()` right after each `.open()`.
```cpp
in_stream.open("in.dat");
if(in_stream.fail())
{
    cerr << "Error opening file" << endl;
    exit(EXIT_FAILURE);
}
```
Slide 18 applies this to both streams (source, slide 18):
```cpp
//Reads three numbers from the file infile.dat, sums the numbers,
//and writes the sum to the file outfile.dat.
#include <fstream>
#include <iostream>
#include <cstdlib>

int main( )
{
    using namespace std;
    ifstream in_stream;
    ofstream out_stream;

    in_stream.open("infile.dat");
    if (in_stream.fail( ))
    {
        cout << "Input file opening failed.\n";
        exit(1);
    }

    out_stream.open("outfile.dat");
    if (out_stream.fail( ))
    {
        cout << "Output file opening failed.\n";
        exit(1);
    }

    int first, second, third;
    in_stream >> first >> second >> third;
    out_stream << "The sum of the first 3\n"
               << "numbers in infile.dat\n"
               << "is " << (first + second + third)
               << endl;

    in_stream.close( );
    out_stream.close( );

    return 0;
}
```
If `infile.dat` does not exist, the screen shows `Input file opening failed.`

> [!warning] Test for failure, not for success
> `if (in_stream.fail())` reports the error when opening failed. Writing `if (!in_stream.fail())` reads as "if it did not fail" and reports an error on success. #struggle #common-mistake

### File-driven versus interactive programs
The prompt and wait pattern disappears. The same extraction works, from a different source:
```cpp
int age;
ifstream in;
in.open("in.dat");
in >> age;
in.close();
```
There is no prompt because there is no person on the other end of `in`.

---

## Opening modes and file flags (slides 20 to 27)

### Appending instead of overwriting
To add to a file instead of replacing its contents (a log file, for example), use the overloaded `.open()` that takes a second argument (source, slide 21):
```cpp
//Appends data to the end of the file data.txt.
#include <fstream>
#include <iostream>

int main( )
{
    using namespace std;

    cout << "Opening data.txt for appending.\n";
    ofstream fout;
    fout.open("data.txt", ios::app);
    if (fout.fail( ))
    {
        cout << "Input file opening failed.\n";
        exit(1);
    }

    fout << "5 6 pick up sticks.\n"
         << "7 8 ain't C++ great!\n";

    fout.close( );
    cout << "End of appending to file.\n";

    return 0;
}
```
`(added)` `exit` needs `#include <cstdlib>`, which the slide omits. The failure message says "Input" although the stream is an output stream.

### File names typed at runtime (source, slides 22 and 23)
A file name can be a `char` array the user fills in, instead of a literal. `.open()` does not care whether it receives a literal or a variable.
```cpp
char in_file_name[16], out_file_name[16];
cout << "Enter the input file name (maximum of 15 characters):\n";
cin >> in_file_name;
in_stream.open(in_file_name);
```
Everything after that (the `.fail()` check, reading, writing, closing) is unchanged. Slide 23 also writes `in_file_name` into the output text.

### fstream and the open mode
`fstream` opens a file for both input and output. Its default `.open()` opens the file as text with both read and write permission. To change that, use the two-argument `.open()`:
```cpp
myfstream.open("MyFile.dat", ios::binary);
```

| Flag | Meaning |
|---|---|
| `ios::app` | Append: set the file pointers to the end of the file for each output operation |
| `ios::ate` | At the end: set the file pointers to the end of the file on opening |
| `ios::trunc` | Truncate: current file contents are cleared |
| `ios::binary` | Binary I/O: no conversion of special characters such as `\n` |
| `ios::in` | Open the file with read privileges |
| `ios::out` | Open the file with write privileges |

> [!warning] app and ate are two different guarantees
> `ate` moves the pointer to the end once, at opening, and after that it can be moved anywhere. `app` forces the pointer to the end before every output operation, so even after a seek to earlier in the file, a write still lands at the end. #common-mistake

### Combining flags with OR, testing them with AND
A flag is a property that is either up or down. Each flag is a constant in the `ios_base` class with a single binary position set to 1. Several flags combine with the bitwise OR operator:
```cpp
myfstream.open("Myfile.dat", ios::in | ios::binary);
```
Slide 26 shows the layout (positions: read, write, text, trunc, app). The write flag is `0 1 0 0 0`, trunc is `0 0 0 1 0`, and the combination is `0 1 0 1 0`. Because `1 | 1 = 1`, repeating a flag (`ios::in | ios::in`) is harmless.

To test one flag, C++ uses bitwise AND against a mask, `binary_arg & mode_mask`. Slide 27 tests an argument `1 1 0 0 1` (read, write, app) against the write mask `0 1 0 0 0` and gets `0 1 0 0 0`, so the write bit is set. This is the same technique as [[CSC01B1_Notes_S1_Foundation-Topics#Bitmasking|Bitmasking]].

### What combining flags achieves (added)
`.open()` takes one mode argument. OR packs several independent yes/no settings into that one number without any of them overwriting the others, because each flag has its own bit. The `1 | 1 = 1` fact is only the reassurance that repeating a flag does no harm.

> [!warning] .open() takes exactly two arguments, and ifstream cannot write
> Three flags are one argument joined by OR: `.open("f.dat", ios::in | ios::out | ios::binary)`, not three comma-separated arguments. And a stream that must both read and write has to be an `fstream`. Passing `ios::out` to an `ifstream` does not give it write ability, because that is a property of the class, not of the flags. #struggle #common-mistake

`(added)` A file that does not exist yet, opened with `ios::in | ios::out`, may fail on some compilers because `ios::in` expects the file to exist. Adding `ios::trunc` (`ios::in | ios::out | ios::trunc`) gives a reliable "create it fresh, then read and write" open.

---

## Output formatting and further stream use (slides 28 to 34)

### Formatting with member functions
The layout of a program's output is its format. These are member functions of any stream object:
- `precision()` takes a number: the digits after the point (or significant figures, depending on the compiler).
- `setf()` takes binary flags and controls the output format. Flags are passed the same way as in the two-argument `.open()`.
- `unsetf()` clears a flag.
- `width()` works with the `setf` flags to control blank space before and after output.

| Flag | Meaning | Default |
|---|---|---|
| `ios::fixed` | Floating-point numbers are not written in e-notation (unsets `scientific`) | Not set |
| `ios::scientific` | Floating-point numbers are written in e-notation (unsets `fixed`). If neither is set, the system decides | Not set |
| `ios::showpoint` | A decimal point and trailing zeros are always shown for floating-point numbers | Not set |
| `ios::showpos` | A plus sign is output before positive integer values | Not set |
| `ios::right` | With a `width()` set, the item sits at the right end of the space; extra blanks go before it (unsets `left`) | Set |
| `ios::left` | With a `width()` set, the item sits at the left end of the space; extra blanks go after it (unsets `right`) | Not set |

### Worked example: make_neat (source, slides 30 to 32)
Reads every number in `rawdata.dat` and writes them one per line, in fixed-point notation, with a sign and a fixed field width, to both the screen and `neat.dat`.
```cpp
//Illustrates output formatting instructions.
//Reads all the numbers in the file rawdata.dat and writes the numbers
//to the screen and to the file neat.dat in a neatly formatted way.
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <iomanip>
using namespace std;

void make_neat(ifstream& messy_file, ofstream& neat_file,
               int number_after_decimalpoint, int field_width);
//Precondition: The streams messy_file and neat_file have been connected
//to files using the function open.
//Postcondition: The numbers in the file connected to messy_file have been
//written to the screen and to the file connected to the stream neat_file.
//The numbers are written one per line, in fixed-point notation (that is, not in
//e-notation), with number_after_decimalpoint digits after the decimal point;
//each number is preceded by a plus or minus sign and each number is in a field of
//width field_width. (This function does not close the file.)

int main( )
{
    ifstream fin;
    ofstream fout;

    fin.open("rawdata.dat");
    if (fin.fail( ))
    {
        cout << "Input file opening failed.\n";
        exit(1);
    }

    fout.open("neat.dat");
    if (fout.fail( ))
    {
        cout << "Output file opening failed.\n";
        exit(1);
    }

    make_neat(fin, fout, 5, 12);

    fin.close( );
    fout.close( );

    cout << "End of program.\n";
    return 0;
}

//Uses iostream, fstream, and iomanip:
void make_neat(ifstream& messy_file, ofstream& neat_file,
               int number_after_decimalpoint, int field_width)
{
    neat_file.setf(ios::fixed);
    neat_file.setf(ios::showpoint);
    neat_file.setf(ios::showpos);
    neat_file.precision(number_after_decimalpoint);
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.setf(ios::showpos);
    cout.precision(number_after_decimalpoint);

    double next;
    while (messy_file >> next)
    {
        cout << setw(field_width) << next << endl;
        neat_file << setw(field_width) << next << endl;
    }
}
```
Raw entries such as `10.37` and `-1.237568432e2` come out as `+10.37000` and `-123.75684`.

### I/O manipulators
An I/O manipulator is a global function used with the insertion and extraction operators. It calls the stream's member functions for you. It needs `#include <iomanip>`.
```cpp
cout.width(5);
cout << "Hello";
```
can be written
```cpp
cout << setw(5) << "Hello";
```
and `setprecision()` replaces `precision()` the same way.

### Streams as function parameters
Stream parameters must be call-by-reference: `void copy_file(ifstream& source_file, ofstream& destination_file);`

`(added)` Streams cannot be copied at all, the same fact behind "no `=` on a stream". Pass by value would need a hidden copy that C++ will not make, so a reference is the only option, not a style choice.

### Testing for end of file
```cpp
while(in_stream >> variable){
    //Do useful work involving extracted data
}
```
This works because `operator>>` returns a reference to the stream, and that stream reference converts to a Boolean: true while data can still be extracted, false once it cannot. The loop is testing "did the last read succeed", not the value of `variable`.

---

## Random access files (slides 35 to 37)

### Reframing random access
C++ makes no distinction between sequential and random access files. All are streams of characters (bytes), so by extension all reads and writes are sequential. Random access means moving where in the byte stream you are before you read or write, instead of always continuing from the last position. It is wanted because it can be much faster than retrieving every record in turn.

### Two independent position markers
C++ tracks the current read position and the current write position separately. The `fstream` class makes no assumption about whether a stream is used for input or output.
- `seekg()` (seek-get) moves the read marker.
- `seekp()` (seek-put) moves the write marker.
- `tellg()` returns the current byte position.

> [!warning] seekg and seekp are two markers, not one
> Moving one does not move the other. `.read()` starts wherever the read marker is, so a `seekp` before a `.read()` does nothing for it. Use `seekg` before reading and `seekp` before writing. #struggle #common-mistake

### Seeking (source, slide 36)
```cpp
myfile.seekg(0, ios::beg);  //seeks 0 bytes from the beginning of the file
myfile.seekg(0, ios::end);  //seeks 0 bytes from the end of the file
myfile.seekg(n, ios::cur);  //seeks n bytes away from the current file position
```
`seekg` and `seekp` are member functions and must be called on a stream (`in_stream.seekg(...)`). They only move the pointer, they do not fetch any data. Reading needs a separate `.read()` call. #struggle

### Reading always moves forward (added)
Reading moves forward from the current position, whichever way the pointer got there. After `seekg(0, ios::end)` a read fails, because nothing lies ahead. It does not wrap round and it does not read backwards. To read something earlier, seek back to it first.

### Designing a file format
To reach one record without reading the others, records must be a fixed size. Then the position of any record is arithmetic. Sizes given on slide 37: `int` 4, `char array[6]` 6, `double` 8, `float` 6, `string` variable.

> [!warning] The slide's float size is not the usual one
> `(added)` The slide lists `float` as 6 bytes. Compiled here, `float` is 4 bytes, `int` 4 and `double` 8. If an exam question gives sizes, use the sizes it gives. In your own programs use `sizeof`. A `string` is variable length, so it cannot sit in a fixed-size record by itself.

---

## Writing raw bytes to disk (slides 38 to 41)

### write and read
`ostream::write(char *data, int size)` and `istream::read(char *data, int size)`. `fstream` has both. The first parameter is `char*`, consistent with C++ treating a file as a sequence of characters, so data of another type must be cast to `char*`.
```cpp
myfile.write(reinterpret_cast<char*>(&record), sizeof(RecordType));
```
This works only when the struct is not of variable length.

### What reinterpret_cast does (added)
Casts compared:
- `static_cast` is a real conversion. `int` to `double` changes the bit pattern so the value stays the same.
- `dynamic_cast` is a runtime-checked cast for polymorphic types. It fails safely if the object is not really that type.
- `reinterpret_cast` does neither. It performs no conversion and no check.

`reinterpret_cast<char*>(&record)` relabels a `RecordType*` as a `char*`. The bytes of `record` do not change. It is needed because `.write()` insists on a `char*`, and a `char` is one byte, so "a `char*` plus a byte count" means "N raw bytes starting here".

### Why the file looks like nonsense (added)
`write()` copies the object's raw bytes exactly as they sit in memory, padding included. It is not text and is not meant to be opened in an editor. It is meant to be read back with `read()` into the same struct type. Formatted output (`<<`, `setf`, `setprecision`) does the opposite: it converts numbers to readable characters.

### Reaching a record and counting records (source, slides 40 and 41)
```cpp
myfile.seekp(pos * sizeof(RecordType), ios::beg);
```
```cpp
int size_in_bytes;
myfile.seekg(0, ios::end);
size_in_bytes = myfile.tellg();
return (size_in_bytes / sizeof(RecordType));
```
`N.B` The division is only valid if the file holds nothing but back-to-back fixed-size records from byte 0. That is a rule about how the file was designed, not something the file announces. With a header of `header_size` bytes: records = `(size_in_bytes - header_size) / sizeof(RecordType)`, and every seek offset gains `+ header_size`.

### Example: seeking to the 4th record (composite) #exam-flagged
`sizeof(Record)` is 24 bytes (worked out in the padding example below). A file holds 5 records with no header.
- Records in the file: 120 bytes / 24 = 5.
- The 4th record is index 3, because counting from 0.
- Offset: 3 * 24 = 72.
- Seek: `myfile.seekg(3 * sizeof(Record), ios::beg);`, then `myfile.read(reinterpret_cast<char*>(&r), sizeof(r));`

Compiled and run: 120 bytes, 5 records, and the read at offset 72 returned the 4th record. With a 20 byte header the offset would be 20 + 72 = 92.

> [!warning] Check whether the question means 4th or index 4
> "The 4th object" is index 3. "Index 4" is the 5th object. Marks are lost here. #common-mistake

---

## Padding and byte alignment (slide 39)

### What padding is
For efficient reading and writing, C++ by default tries to make certain members start at a memory address that is an exact multiple of some number of bytes, depending on the member's type, the compilation settings, and whether the OS is 16, 32 or 64 bit. It does this by adding padding: allocated memory that is ignored. This can be controlled, but the mechanism is not standard.

Padding does not show in normal member access, but `sizeof(RecordType)` includes it, so it matters for every offset calculation above. The earlier note on [[CSC01B1_Notes_S1_Foundation-Topics#16. Structs|Structs]] mentions the end-of-struct padding.

### The rule for placing members (added)
1. Place each member at the next offset that is a multiple of that member's own alignment (for the built-in types here, its size).
2. If the next free offset does not fit, insert just enough padding bytes before the member to reach one that does.
3. After the last member, round the total up to a multiple of the largest alignment among the members.

### Example 1 (composite) #exam-flagged
```cpp
struct Record { int id; char name[10]; double val; };
```
- `id`, 4 bytes: offset 0 to 3. Next free: 4.
- `name`, 10 bytes, no alignment restriction: offset 4 to 13. Next free: 14.
- `val`, 8 bytes, must start on a multiple of 8. 14 does not fit, so 2 bytes of padding at 14 and 15. `val` at 16 to 23. Next free: 24.
- 24 is already a multiple of 8, so no trailing padding.

`sizeof(Record)` = 24. Compiled: `name` at 4, `val` at 16, size 24.

### Example 2 (composite): the same members reordered
```cpp
struct Record { int id; double val; char name[10]; };
```
- `id`: 0 to 3. Next free: 4.
- `val` needs a multiple of 8: 4 bytes of padding at 4 to 7. `val` at 8 to 15. Next free: 16.
- `name`: 16 to 25. Next free: 26.
- Round 26 up to a multiple of 8: 6 bytes of trailing padding.

`sizeof(Record)` = 32. Compiled: `val` at 8, `name` at 16, size 32.

`N.B` The same three members give 24 bytes in one order and 32 in another. Padding goes immediately before the member whose alignment the next free offset fails, and only as many bytes as are needed.

### Example 3 (composite): the slide's struct
```cpp
struct MyStruct
{
    char m1;
    short m2;
    int m3;
    char m4;
};
```
- `m1`: offset 0. Next free: 1.
- `m2` (2 bytes, multiple of 2): 1 byte of padding, `m2` at 2 to 3. Next free: 4.
- `m3` (4 bytes, multiple of 4): fits at 4 to 7. Next free: 8.
- `m4`: offset 8. Next free: 9.
- Round 9 up to a multiple of 4: 3 bytes of trailing padding.

`sizeof(MyStruct)` = 12. Compiled: `m2` at 2, `m3` at 4, `m4` at 8, size 12.

### Controlling padding with #pragma pack (source, slide 39)
```cpp
#pragma pack(push)  /* save current alignment settings */
#pragma pack(1)     /* set alignment to 1 */

struct MyStruct
{
    char m1;
    short m2;
    int m3;
    char m4;
};

#pragma pack(pop)   /* undo changes to alignment settings */
```
`pack(push)` saves the current alignment setting. `pack(1)` forces every member to start straight after the previous one, so there is no padding at all. `pack(pop)` restores the saved setting, so the override covers only the struct between them. With `pack(1)` the struct above is 1 + 2 + 4 + 1 = 8 bytes, compiled and confirmed. This makes the layout of a disk record predictable across compilers.

> *`#pragma pack` was on the slide as an image and I first left it out. The student caught it, which is why it is here with a worked size.*

### Alignment of a struct or class member (added)
The rule is recursive. A compound member's alignment requirement is the largest alignment requirement among its own members, traced down to a built-in type. It is not the same number as its `sizeof`.
```cpp
struct Inner { char a; double b; };  //sizeof 16, alignment 8 (from the double)
struct Outer { int x; Inner y; };    //y must start on a multiple of 8
```
`x` sits at 0 to 3, so 4 bytes of padding, `y` at 8 to 23, and `sizeof(Outer)` = 24. Compiled: `Inner` 16, `Outer` 24, `y` at 8.

A class with a `virtual` function carries a hidden vtable pointer, whose alignment is 4 or 8 bytes depending on the system. A truly abstract class (a pure virtual function) cannot be instantiated, so it cannot be a plain member of a struct, only a pointer or reference to one. A vtable pointer is an address valid only inside one running program, so raw `write()` and `read()` of a polymorphic object to disk is unsafe. Raw struct I/O is for plain data only.

---

## Reusable software components: DLLs (slides 42 to 51)

> [!important] Module style is what is examined (amended S12) #exam-flagged
> The lecturer said the exam uses module interface files only, as in the 2025 papers, and does not test header files for DLLs. This comes from the user's report of what the lecturer said, not from a slide. The header version later in this section (slides 45 to 47) stays as reference and is not examined. Explicit linking (slide 50) is on hold until the lecturer says whether it is examined.

### Why not just ship the source
Programmers want to reuse tested components. You may not want to give the client programmer your `.h` and `.cpp` files. Even if you do, the functions are statically linked into the client's executable at compile time, so any update means a full recompile. What is wanted is library code that is loaded at runtime instead. Under Windows that is a Dynamic Link Library (DLL). Unix systems have DSOs (Dynamically Shared Objects).

### DLL characteristics (slide 44)
- There are several kinds: regular Win32 DLLs, Component Object Model DLLs, ActiveX OCX and DLL files.
- Functions are exported by ordinal number and optionally also by name.
- A DLL is loaded into the same address space as the application, so pointer-based data may be passed to exported functions.
- A DLL written in one language can often be used from another.

### The whole picture before any syntax (added)
Two separate files that talk while running. The library (the DLL) is a set of functions that does nothing alone. The application (the `.exe`) wants to use them without their source being pasted into it. A DLL is the library compiled so an application can call into it as a separate file.

This course names the implementation file `something.impl.cpp`. Three source files make the whole pattern:

| File | What it is | Becomes |
|---|---|---|
| `mylib.h` | The menu: lists each function's name and parameter types. Nothing runs here | Nothing alone, it is `#include`d by both other files |
| `mylib.impl.cpp` | The real function bodies | `mylib.dll` |
| `main.cpp` | Your program, which calls the functions | `main.exe` |

The header is shared so both sides agree word for word on every signature. If `main.cpp` thought `add` took two `int`s and the DLL had built it with two `double`s, the call would corrupt memory.

The number of functions is not fixed. Each is one line in the header and one body in the `.impl.cpp`. The slide shows two; the example below shows three.

### Example: a three-function DLL (composite)
`mylib.h`:
```cpp
#ifndef MYLIB_H
#define MYLIB_H

#ifdef BUILDING_MYLIB
  #define MYLIB_API __declspec(dllexport)
#else
  #define MYLIB_API __declspec(dllimport)
#endif

extern "C" {
    void MYLIB_API greet(const char* name);
    int  MYLIB_API add(int a, int b);
    int  MYLIB_API square(int x);
}

#endif
```
`mylib.impl.cpp`:
```cpp
#include <iostream>
#include "mylib.h"

void greet(const char* name)
{
    std::cout << "Hello, " << name << "!" << std::endl;
}

int add(int a, int b)
{
    return a + b;
}

int square(int x)
{
    return x * x;
}
```
`main.cpp`:
```cpp
#include <iostream>
#include "mylib.h"

int main()
{
    greet("Sithomo");
    std::cout << "add(2,3) = " << add(2, 3) << std::endl;
    std::cout << "square(5) = " << square(5) << std::endl;
    return 0;
}
```
Build in two steps. First the DLL, then the application linked to it:
```
g++ -c -DBUILDING_MYLIB mylib.impl.cpp -o mylib.o
g++ -shared -o mylib.dll mylib.o -Wl,--out-implib,libmylib.a
g++ main.cpp -o main.exe -L. -lmylib
```
The result is `mylib.dll` and `main.exe` side by side. This was cross-compiled with MinGW and all three commands succeeded. It was not run, because there is no Windows here.

### What happens when main.exe starts (added)
1. At link time the linker writes a note into `main.exe`: it needs `greet`, `add` and `square` from `mylib.dll`.
2. When you run it, Windows reads that note, finds `mylib.dll` (first in the same folder) and loads it into memory.
3. Windows fills in the real addresses of those functions.
4. Every call in `main.exe` jumps into the code inside the DLL.

If the DLL is missing at step 2, the program refuses to start.

### Reading the code, keyword by keyword (added)
Some words are fixed by the language or Windows and cannot be changed. Others were chosen by the author and can be renamed freely.

| Fixed | Made up |
|---|---|
| `#ifndef`, `#define`, `#ifdef`, `#else`, `#endif` | `MYLIB_H` |
| `__declspec`, `dllexport`, `dllimport` | `BUILDING_MYLIB` |
| `extern "C"` | `MYLIB_API` |
| `-c`, `-D`, `-shared`, `-L`, `-l`, `-o` | `mylib`, `greet`, `add`, `square` |
| `LoadLibrary`, `GetProcAddress`, `FreeLibrary`, `HINSTANCE` | `lib`, `TwoIntsToInt` |

The slide's `EXAMPLE_DLL_H`, `BUILDING_EXAMPLE_DLL` and `EXAMPLE_DLL` are the same three made-up names as `MYLIB_H`, `BUILDING_MYLIB` and `MYLIB_API`.

**The include guard.**
```cpp
#ifndef MYLIB_H
#define MYLIB_H
```
`#ifndef` means "if not defined". It asks whether the word `MYLIB_H` has been invented yet. The first time the file is read it has not, so reading continues and the next line invents it. If the header is included a second time, the word exists and everything down to the last `#endif` is skipped. This prevents "declared twice" errors.

**Choosing export or import.**
```cpp
#ifdef BUILDING_MYLIB
  #define MYLIB_API __declspec(dllexport)
#else
  #define MYLIB_API __declspec(dllimport)
#endif
```
- `#ifdef` means "if defined". It is the same tool as `#ifndef`, asking about a different word for a different job. This block sits inside the guard, which is why the file ends with two `#endif` lines.
- `#ifdef ... #else ... #endif` is if/else for the preprocessor. Exactly one branch applies in a given build, because a function cannot both be provided here and be fetched from elsewhere. The other branch is discarded before compiling.
- `#define MYLIB_API something` means: before compiling, replace every `MYLIB_API` with `something`. That replacement is a macro.
- `__declspec(...)` is a Microsoft keyword that attaches an extra property to the declaration after it. It is extra because standard C++ has no way to say "public in a DLL". Once any function carries the label, unlabelled functions stay private in the DLL.
- `dllexport` means "list this function as public in the DLL", like an entry in a phone book kept inside the DLL (the export table). `dllimport` means "this function lives in a DLL, fetch it from there".
- `BUILDING_MYLIB` is a switch. It exists only when the compile command includes `-DBUILDING_MYLIB`. That flag goes on the DLL build only, never the application build. Setting it from the command line lets one shared header serve both sides.

After the replacement, the compiler sees these declarations (checked with the preprocessor):
```
DLL build:   void __attribute__((dllexport)) greet(const char* name);
App build:   void __attribute__((dllimport)) greet(const char* name);
```
MinGW spells `__declspec` as `__attribute__` internally, with the same meaning.

**The function declarations.**
```cpp
extern "C" {
    void MYLIB_API greet(const char* name);
    int  MYLIB_API add(int a, int b);
}
```
- `extern "C" { ... }` means "keep the names inside these braces exactly as typed". C++ normally renames functions to support overloading. The exported names of the real DLL, with and without it:
```
with extern "C":      add          greet          square
without extern "C":   _Z3addii     _Z5greetPKc    _Z6squarei
```
  Another program looking for `add` cannot find `_Z3addii`. It only works on plain functions, because a class has no plain C name to keep.
- `void MYLIB_API greet(const char* name);` reads: returns nothing, carries the label, is called `greet`, takes text that it promises not to change. The semicolon means it is only a description.

**The implementation file.** `#include "mylib.h"` uses quotes, meaning "look in my own folder first", where `<iostream>` uses angle brackets for the compiler's built-in library. The function bodies are ordinary C++. They do not repeat `extern "C"` or `MYLIB_API`, because the compiler saw those on the declarations.

This is like defining a class's methods outside the class. The declaration is in the header and the body in the implementation file. A label written on the declaration is not repeated on the body, just as `virtual` and `static` are written inside a class and not on the outside definition. A plain function has no `ClassName::` to write, and the compiler matches the body to the declaration by name and parameter types.

**The file name.** A file name may contain any number of dots. Only the last one starts the extension, so `mylib.impl.cpp` is the name `mylib.impl` plus the extension `.cpp`, and the compiler reads only `.cpp`. `.impl` means "implementation". It is a convention that adds nothing technically, and it labels which file is which. `mylib.cpp` builds identically. One visible effect: with no `-o`, the object file is named `mylib.impl.o`.

**The compile commands.**
- `g++` is the compiler. `-c` means compile only, do not finish the program.
- `-DBUILDING_MYLIB` means "define". It is the same as writing `#define BUILDING_MYLIB` at the top of the file. It is what flips the header to `dllexport`.
- `-o mylib.o` names the output. A `.o` file is machine code that is not yet a complete program.
- `-shared` means "build a DLL instead of a program".
- `-Wl,` means "pass the next words to the linker", the tool that stitches compiled pieces together. `--out-implib,libmylib.a` asks it to also write a small file listing the DLL's public functions (the import library), which programs use at compile time.
- `-L.` means "also look for libraries in this folder", where the dot means here. `-lmylib` means "link with the library called mylib". The tool adds `lib` in front and `.a` on the end, so it looks for `libmylib.a`.

Turning `.impl.cpp` into `.o` is the normal process for any `.cpp`: preprocess, compile to machine code, write the object file. Two things are special for a DLL, and neither is in that step itself. `-DBUILDING_MYLIB` changes what the preprocessing produces, and the DLL file is only created afterwards by the linker because of `-shared`.

### The module style, the files you write (added)
This is the style the exam uses. The header file is replaced by a module interface file, and the names below come from the 2025 papers.

| File | What it is | Becomes |
|---|---|---|
| `LibFilter.cpp` | The module interface file: declares what the DLL offers | An object file (`LibFilter.o`) plus a compiled module, needed by both builds |
| `LibFilter.impl.cpp` | The implementation file: the function bodies | Part of the DLL |
| `main.cpp` | The program that calls the function | `main.exe` |

The DLL's own file name (for example `reading-filter.dll`) appears in neither source file. It is chosen in the build command.

The interface file (source: T10 implicit-linking `Library.cpp`, with the 2025-A names):
```cpp
export module LibFilter;

extern "C"
{
	export bool isInvalid(char arrReadings[], int intLength);
}
```
- `export module LibFilter;` makes this file the public face of a module called `LibFilter`. A program reaches it with `import LibFilter;`.
- `extern "C" { }` keeps the names inside exactly as typed. Normally C++ renames every function so that overloading works. "Exported without C++ name mangling" in a question means these braces.
- `export` in front of the function makes it visible to any file that imports the module. It is a declaration only: no body, and a semicolon.

The implementation file (source: T10 create `Library.impl.cpp`, with the 2025-A names and the body added):
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
- `module LibFilter;`, with no `export`, says this file belongs to the module and fills in its bodies. It needs no `#include` and no `import`.
- The same `extern "C"` braces wrap the body.
- A char is written with single quotes (`'?'`). Double quotes make a string, and comparing a `char` to a string does not compile.

> [!warning] Three checks for the implementation file #exam-flagged
> 1. `module Name;`, the same name as the interface, with no `.cpp` on the end.
> 2. `extern "C" { ... }` around the function, with its closing brace.
> 3. `'?'` for a char and `"?"` for a string.

(added) What the compiler does with mistakes here (compiled with a MinGW g++ cross-compiler, 13.2, and not run on Windows):
- With `extern "C"` missing in the implementation, g++ rejects it ("declaration conflicts with import").
- With `module LibFilter.cpp;` it looks for a module of that name and stops.
- With the closing brace missing it stops with "expected }".
- With `"?"` it stops with "comparison between pointer and integer".
- `import LibFilter;` as the first line was accepted in one test, but the tut and the course use `module Name;`, so use that.

(added) The T10 `create` folder's copy of the interface leaves `export` off the function. It still builds the DLL, but no program could import the function from it: `main.cpp` fails with "not declared in this scope". Use the version with `export`.

(added) A plain C++ `add` is stored in the object file as `_Z3addii`, and inside `extern "C"` as `add`.

### Building the DLL with a batch file (added)
A batch (`.bat`) file is a text file of command lines that Windows runs from top to bottom. Q4 asks for two kinds: one that builds the DLL, and one that builds a program that uses it.

Reading one command:
```
g++ -std=c++23 -fmodules-ts -c Library.cpp
```
- `g++` is the compiler.
- `-std=c++23` sets the language version. Modules need C++20 or newer.
- `-fmodules-ts` switches modules on. All three flags start with a dash: `-std`, `-fmodules-ts`, `-c`. Without the leading dash g++ treats `fmodules-ts` as a file name and the `import` line fails.
- `-c` means compile only: write a `.o` object file and do not link.
- Compiling an interface file also writes the compiled module into a `gcm.cache` folder, which other files need before they can use `import` or `module`.

Creating the DLL (source, T10 `create.bat`):
```bat
@echo off
g++ -std=c++23 -fmodules-ts -c Library.cpp
g++ -std=c++23 -fmodules-ts -c Library.impl.cpp
g++ -shared -o Library.dll Library.o Library.impl.o
pause
```
- Command 1 compiles the interface. It goes first because the implementation says `module Library;` and needs the compiled module that command 1 makes. Compiled in the wrong order, g++ stops with "failed to read compiled module".
- Command 2 compiles the implementation.
- Command 3 links both objects into a DLL. `-shared` means "build a DLL, not a program". The name after `-o` is the DLL's file name, which is where `util.dll` or `route-generator.dll` comes from.
- `@echo off` hides the command echo and `pause` keeps the window open. Neither earns marks.

> [!warning] The rule for "creates the DLL" #exam-flagged
> 1. Compile the interface with `-c`.
> 2. Compile the implementation with `-c`.
> 3. `g++ -shared -o NAME.dll` followed by the two `.o` files, where `NAME.dll` is the DLL name in the question.
>
> `-shared` belongs only in this command.

### Building a program that links implicitly (added)
Implicit linking ties the program to the DLL when the program is built. The linker writes a note into the `.exe` saying which functions it needs from which DLL. When the `.exe` runs, Windows reads that note, looks for the DLL (first in the same folder) and loads it. If the DLL is missing, the program refuses to start. The client needs the DLL and the interface file.

Building the program (source, T10 implicit-linking `compile.bat`):
```bat
@echo off
g++ -std=c++23 -c -fmodules-ts Library.cpp

g++ -c  -std=c++23 -fmodules-ts main.cpp

g++ -o app.exe -L. -lLibrary Library.o main.o

app.exe
pause
```
- Command 1 compiles the interface file, so that `main.cpp` can `import` it. Without it, compiling `main.cpp` stops with "failed to read compiled module".
- Command 2 compiles `main.cpp`.
- Command 3 links. `-o app.exe` names the program, `-L.` means "look for libraries in the current folder", and `-lLibrary` means "link against the DLL called Library".
- The line `app.exe` runs the program. The implementation file is not compiled here, because the function bodies live in the DLL.

The `-l` name is the DLL's file name with `.dll` taken off: `util.dll` gives `-lutil`, and `em-calculator.dll` gives `-lem-calculator`.

> [!warning] Three clues in the question become three flags #exam-flagged
> 1. "called main.exe" gives `-o main.exe`.
> 2. "stored in the same folder" gives `-L.`.
> 3. "expects to link to util.dll" gives `-lutil`, with `.dll` removed.
>
> Then the two objects at the end. `-shared` never appears in this command: it builds a DLL, not a program.

(added) Wrong forms, each compiled and checked with the cross-compiler: `-lutil.dll` fails with "cannot find -lutil.dll"; `-lutil` without `-L.` fails with "cannot find -lutil"; no `-l` at all fails with "undefined reference to isInvalid"; `-l.` fails with "cannot find -l."; and `-shared` in this command builds a DLL, not a program.

### The three names that never match (added)
Three names are separate things: the module name (the word after `module`), the interface file's name, and the DLL's file name. In the tut they all say `Library`, which hides that. In 2025-A the module is `LibFilter` and the DLL is `util.dll`.

Example (composite)
```
module name:          Calc        (interface file Calc.cpp)
DLL file:             maths.dll
program source:       run.cpp
program to build:     run.exe
```
```bat
g++ -std=c++23 -c -fmodules-ts Calc.cpp
g++ -std=c++23 -c -fmodules-ts run.cpp
g++ -o run.exe -L. -lmaths Calc.o run.o
```
COVERS: the tut's single name `Library`, split into its separate roles.

### How the 2025 Q4 questions map onto these files (added)
| Paper | Asks for | Needs |
|---|---|---|
| 2025-A | 4.1 module interface (module LibFilter), 4.2 implementation, 4.3 batch file for an implicitly linked `main.exe` with `util.dll` | the two files, and the implicit link command |
| 2025-B | 4.1 `main.cpp` that explicitly links to `route-generator.dll`, 4.3 batch file that creates the DLL from `RouteAPI.cpp` and `RouteAPI.impl.cpp` | explicit linking (on hold), and the DLL creation command |
| 2025-C | 4.1 module interface (module CalcLibrary), 4.2 batch file that links implicitly to `em-calculator.dll`, 4.3 `main.cpp` with a dynamic array of 10 random reals | the interface file, the implicit link command, and ordinary C++ |

Model answers (added). They were compiled with the cross-compiler and linked, and not run.

2025-A Q4.3 (the paper does not name the interface file, so `LibFilter.cpp` is assumed):
```bat
g++ -std=c++23 -fmodules-ts -c LibFilter.cpp
g++ -std=c++23 -fmodules-ts -c main.cpp
g++ -o main.exe -L. -lutil LibFilter.o main.o
```
2025-B Q4.3:
```bat
g++ -std=c++23 -fmodules-ts -c RouteAPI.cpp
g++ -std=c++23 -fmodules-ts -c RouteAPI.impl.cpp
g++ -shared -o route-generator.dll RouteAPI.o RouteAPI.impl.o
```
2025-C Q4.1:
```cpp
export module CalcLibrary;

extern "C"
{
	export double calculateEM(double* arrMarks);
}
```
2025-C Q4.2 (the question does not name the program, so `main.exe` is a sensible choice):
```bat
g++ -std=c++23 -fmodules-ts -c CalcLibrary.cpp
g++ -std=c++23 -fmodules-ts -c main.cpp
g++ -o main.exe -L. -lem-calculator CalcLibrary.o main.o
```
2025-C Q4.3:
```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

import CalcLibrary;

using namespace std;

int main()
{
	srand(time(0));

	double* arrMarks = new double[10];
	for (int i = 0; i < 10; i++)
	{
		arrMarks[i] = rand() / (double)RAND_MAX * 100;
	}

	cout << calculateEM(arrMarks) << endl;

	delete[] arrMarks;
	return 0;
}
```
- `double* arr[10]` is an array of ten pointers, not a dynamic array of ten numbers. `new double[10]` gives one pointer to ten doubles.
- A function cannot be written inside `main` (g++: "a function-definition is not allowed here"). The loop can call `rand()` directly.
- `rand() % 100` gives whole numbers from 0 to 99. `rand() / (double)RAND_MAX * 100` gives real numbers from 0 to 100 (a test run of 100000 values gave 0.0002 to 99.9994).
- Call `srand(time(0))` once, or every run gives the same numbers.



> [!note] Header style, not examined (amended S12)
> This example and the header based material down to the end of the slide 47 compile commands are the lecture's header version. They are kept as reference. The exam uses the module style (see: The module style, the files you write).

### The slide's example header (source, slide 45)
Two functions inside `extern "C"`, one C++ only function, and a class.
```cpp
#ifndef EXAMPLE_DLL_H
#define EXAMPLE_DLL_H

#ifdef BUILDING_EXAMPLE_DLL
#define EXAMPLE_DLL __declspec(dllexport)
#else
#define EXAMPLE_DLL __declspec(dllimport)
#endif
//The following functions' names will be unchanged
extern "C"
{
   void __stdcall EXAMPLE_DLL c_greet(const char *s);
   int EXAMPLE_DLL c_power(int a, int b);
}

// This function's name will be mangled during DLL compilation
void EXAMPLE_DLL cpp_greet(void);

// This class' name will be mangled during DLL compilation
class EXAMPLE_DLL Greeter
{
public:
        Greeter() {};
        virtual ~Greeter() {};
        void greet(void);
};

#endif
```
The slide's notes: the `#ifdef` block defines whether DLL symbols will be exported. `extern "C"` turns off C++ name mangling. `cpp_greet` will not be usable outside C++. Since C++ classes can only be used in C++, it would not make sense to export the class as `extern "C"`. Calling conventions refer to the way registers and the stack are used to pass arguments to functions, and `stdcall` is the calling convention of the Win32 API.

`(added)` The exports of this exact header, compiled here, are `c_greet` and `c_power` as plain names, and `cpp_greet` and `Greeter` as mangled names (`_Z9cpp_greetv`, `_ZN7Greeter5greetEv`).

`__stdcall` is a word placed before a function name meaning "use the Windows way of passing arguments". Caller and function must agree on how arguments are handed over and who tidies the stack, or memory is corrupted. Windows API functions use `__stdcall`, so the slide marks `c_greet` with it. On 64-bit Windows there is one calling convention and the compiler ignores the keyword, which is why the three-function example above needs none. Treat it as a fixed word to copy.

### The slide's implementation (source, slide 46)
```cpp
#include <iostream>
#include <string>

#include "example_dll.h"

using namespace std;

__stdcall void c_greet(const char *s)
{
        cout << "I will say hello to... ";
        while(*s != '\0')
        {
                cout << *s;
                s++;
        }
        cout << endl;
}

int c_power(int a, int b)
{
        int ret = 1;
        for(int k = 0; k < b; k++)
          ret *= a;
        return ret;
}

void cpp_greet(void)
{
        cout << "C++ function says hello" << endl;
}

void Greeter::greet(void)
{
        cout << "This is the C++ greeter class" << endl;
}
```
`(added)` The slide's header and implementation, cross-compiled here with the slide's own commands, build without errors.

### Compiling a DLL with MinGW (source, slide 47)
```
g++ -c -DBUILDING_EXAMPLE_DLL example_dll.cpp
g++ -shared -o example_dll.dll example_dll.o
-Wl,--out-implib,libexample_dll.a
```
The slide notes that you may need to add MinGW's (for example Dev-C++'s) bin directory to your PATH, or work from there directly. `-c` is do not link, `-D` defines the macro, `-shared` creates a DLL, `-o` names the output, and `-Wl,` sends the following arguments to the linker. `--out-implib` creates an import library called `libexample_dll.a`. The second and third lines above are one command that wrapped on the slide.

### Implicit linking (source, slides 48 and 49)
Implicit linking requires both the DLL and the header file to be given to the client programmer.
```
g++ -c implicit_exe.cpp
g++ -o implicit_exe.exe implicit_exe.o -L. -lexample_dll
```
`-L.` searches the current directory and `-lexample_dll` links against the library of that name.

`(added)` This is a hard dependency. If the DLL is missing when the program starts, Windows refuses to launch it. It suits a DLL that is a required, known part of the program.

### Explicit linking (source, slide 50)
It is possible to link to a DLL without having the `.h` file. This file may be compiled normally.
```cpp
#include <iostream>
#include <windows.h>

using namespace std;

typedef int (*TwoIntsToInt)(int,int);

int main()
{
   TwoIntsToInt power = NULL;
   HINSTANCE hndlLibrary = LoadLibrary("example_dll.dll");
   if (hndlLibrary)
   {
      power = (TwoIntsToInt)GetProcAddress(hndlLibrary, "c_power");
      if (power)
         cout << "2 to the power 4 is " << power(2, 4) << endl;
      FreeLibrary(hndlLibrary);
   }
   else
      cout << "Error Loading DLL" << endl;
   return 0;
}
```
`(added)` This was cross-compiled with no header and no `-l` flag.

What each line does:
- `<windows.h>` provides the functions for handling DLLs.
- `typedef int (*TwoIntsToInt)(int,int);` is a function pointer type matching the DLL function.
- `HINSTANCE` holds a handle to the DLL. A handle is a ticket number Windows gives you for the loaded file.
- `LoadLibrary("example_dll.dll")` asks Windows to load that file. It returns the handle, or `NULL` if loading failed.
- `GetProcAddress(hndlLibrary, "c_power")` looks the function up by its name as text. "Proc" means procedure. It returns a bare address with no type, so the `(TwoIntsToInt)` cast in front tells the compiler to treat it as a pointer to a function of that shape.
- `power(2, 4)` invokes the DLL function through the pointer.
- `FreeLibrary` unloads the library.

`(added)` The name string must match the exported name exactly, which is why `extern "C"` matters here. With a mangled name you would have to pass `"_Z3addii"`-style text.

`(added)` The trade-off against implicit linking: the program can start even if the DLL is missing. It tests `hndlLibrary` and `power`, and carries on or reports an error. That is why plugin systems use it. The cost is more code, and no compiler check that the typedef matches the real function. It is also the same mechanism as a function pointer, see [[CSC01B1_Notes_S1_Foundation-Topics#14. Function pointers|Function pointers]]: the address just comes from `GetProcAddress` instead of from a function named in source.

**typedef with a function pointer.** `typedef` is still an alias, see [[CSC01B1_Notes_S1_Foundation-Topics#15. Extending the type system|typedef]]. In `typedef int num;` and `typedef int* integerArray;` the new name comes last. A function pointer's syntax puts the name inside the brackets. To read it, cover the word `typedef`. What is left declares a variable called `TwoIntsToInt`, a pointer to a function taking two ints and returning an int. With `typedef` back in front, that name becomes a nickname for that type. Both of these are the same (compiled, output `3 7`):
```cpp
int (*p1)(int, int) = add;    //without the nickname
TwoIntsToInt p2 = add;        //with the nickname
```
Without the nickname, the cast above would read `(int (*)(int, int))GetProcAddress(hndlLibrary, "c_power")`.

### Explicit linking, the exam pattern (added)
Status: on hold, and probably not examined (the user's understanding, not yet confirmed). The user asked the lecturer to confirm whether explicit linking, and the function pointer `typedef` it needs, is examined. 2025-B Q4.1 (10 marks) asks for it, and 2025-A and 2025-C do not. Until the lecturer replies, treat it as unconfirmed. Function pointers are in the course material (see: [[CSC01B1_Notes_S1_Foundation-Topics#14. Function pointers|Function pointers]]), but the lecturers did not teach them. Those S1 notes were added for extra information only. To the user's knowledge function pointers are not examined in any form, and the email to the lecturer is a confirmation of that.

The T10 version (source, T10 `explicit-linking/main.cpp`):
```cpp
#include <windows.h>

#include <iostream>

typedef int (*fun)(int, int);
//using fun = int (*)(int, int);

using namespace std;

int main()
{
	fun add = nullptr;
	HINSTANCE handleLibrary = LoadLibrary("Library.dll");
	if (handleLibrary){
		add = (fun)GetProcAddress(handleLibrary, "add");
		if (add){
			int sum = add(5, 7);

			cout << "Result: " << sum << endl;
		}else
			cerr << "Failed to link to add function" << endl;

		FreeLibrary(handleLibrary);
	} else
		cerr << "Failed to load the library" << endl;

	return 0;
}
```
It builds with `g++ -o program.exe main.cpp`: no module flags, no `-L.` and no `-l`. The DLL does not have to exist at build time. It must sit next to the `.exe` when the program runs.

| | Implicit | Explicit |
|---|---|---|
| Interface file needed | yes | no |
| First lines of main.cpp | `import Name;` | `#include <windows.h>` |
| Build | `-o ... -L. -lname` and the objects | `g++ -o program.exe main.cpp` |
| When the DLL is loaded | at start, and the program will not start without it | when the `LoadLibrary` line runs, and a missing DLL gives your own message |

Three things must agree with the DLL: the `typedef` must match the function's signature (return type and each parameter type), the string in `GetProcAddress` must be the function's plain name in quotes (which works because of `extern "C"`), and the file name in `LoadLibrary` must be the DLL's exact file name. Leaving out the `(fun)` cast fails to compile ("invalid conversion from FARPROC").

Example (composite)
A DLL called shrink.dll exports, without name mangling, `double half(double dblValue);`. Load it explicitly and print the result of calling it with 9.
```cpp
#include <windows.h>
#include <iostream>

typedef double (*fun)(double);

int main()
{
	fun half = nullptr;
	HINSTANCE handleLibrary = LoadLibrary("shrink.dll");
	if (handleLibrary)
	{
		half = (fun)GetProcAddress(handleLibrary, "half");
		if (half)
		{
			std::cout << half(9.0) << std::endl;
		}
		else
		{
			std::cerr << "Failed to link to half function" << std::endl;
		}
		FreeLibrary(handleLibrary);
	}
	else
	{
		std::cerr << "Failed to load the library" << std::endl;
	}
	return 0;
}
```
COVERS: the tut's `int add(int, int)` with a different function. Five things change: the `typedef` types, the variable's name, the DLL's file name, the quoted function name and the call. Everything else stays the same. This compiled with the cross-compiler and was not run.

### DllMain (source, slide 51)
Should you wish to take certain actions at various stages of the DLL's life-cycle (for example when a program is linked to it), you may use the optional DLL entry point called `DllMain`. `(added)` The slide gives one line and no example, so none is shown here.

---

## Worked coding exercise: write, seek, read back (composite)
The task: open a binary file for reading and writing, define a record struct, write three records, seek to the 2nd and read only that one back, then print it. Compiled and run, the output is `Bob 75`.
```cpp
#include <iostream>
#include <cstdlib>
#include <fstream>

int main(){
    struct Score
    {
        char name[10];
        int value;
    };
    using namespace std;
    fstream in_stream;
    in_stream.open("scores.dat", ios::in | ios::out | ios::binary | ios::trunc);
    if(in_stream.fail()){
        cout << "Error opening file." << endl;
        exit(EXIT_FAILURE);
    }
    Score s1 = {"Alice", 90};
    Score s2 = {"Bob", 75};
    Score s3 = {"Carl", 88};
    in_stream.write(reinterpret_cast<char*>(&s1), sizeof(s1));
    in_stream.write(reinterpret_cast<char*>(&s2), sizeof(s2));
    in_stream.write(reinterpret_cast<char*>(&s3), sizeof(s3));

    in_stream.seekg(sizeof(Score), ios::beg);
    Score test;
    in_stream.read(reinterpret_cast<char*>(&test), sizeof(test));
    cout << test.name << " " <<test.value << endl;
    return 0;
}
```
- The class is `fstream`, because one stream must both read and write. The three flags are one OR-ed argument.
- `ios::trunc` guarantees a fresh file for a name that does not exist yet.
- The struct members are set with initializer lists at declaration. A `char` array cannot be assigned with `=` afterwards, so `s1.name = "Alice";` does not compile. `strcpy` from `<cstring>` is the other option. #struggle
- The 2nd record is index 1, so the seek is `1 * sizeof(Score)`. `sizeof(Score)` alone is the same number.
- A fourth variable, `test`, receives the read, so the result can only have come from the file. Reading into `s2` would show the same values that were already in memory.
- `.read()` and `.write()` are named from the file's point of view: `write` sends data out to the file, and `read` pulls data out of the file. This matches `cin >> variable`, which is not called "writing" even though the variable changes.

---

## Struggle items from this session
Each item below appeared as a live mistake or a repeated question, and is logged as still open until it is answered correctly under a retest. #struggle

- **seekg versus seekp.** In the exercise, `seekp` was chosen for a read, and `seekg` was first called without a stream object. The markers are independent, and seeking never fetches data. The same shape of mistake (assuming two independent things are one) came up in earlier sessions.
- **Writing code from scratch.** Quiz answers were recognised, but writing the exercise began as a blank page. It was built up one line at a time from corrections. Retest by writing the four-step pattern (open with combined flags, write a record, seek to an index, read it back) without help.
- **Padding.** Asked for again over several rounds: where the padding goes, why reordering changes the size, and how a compound member is aligned. Retest by working out `sizeof` by hand with the placement.
- **reinterpret_cast.** Asked for twice: it relabels the pointer type and changes no bytes.
- **DLL syntax and jargon.** The keywords, the macro switch, `extern "C"`, the two dots in `.impl.cpp`, and `typedef` on a function pointer all needed separate explanations. The concept of a DLL itself was understood. (added, S12) Later misses in the module style: `module`/`import` as the impl first line, `extern "C"` in both files, `-L.` versus `-l.`, `-shared` only in the DLL command, the leading hyphen on `-fmodules-ts`, and the `-l` name being the DLL file name without `.dll`.

---

## Do not forget
- The stream is the channel. The file is what it is connected to. Streams cannot be assigned with `=` or copied, so pass them by reference.
- `.open()` takes a file name and one mode. Join flags with `|`. Test with `if (x.fail())`, not `!fail()`.
- `ifstream` cannot write. A stream that reads and writes must be an `fstream`.
- `app` re-forces the pointer to the end on every write. `ate` only moves it once, at opening.
- `seekg` moves the read marker, `seekp` moves the write marker, and neither fetches data. Reading always moves forward.
- Record offset = index * `sizeof(RecordType)`, plus any header. "4th" is index 3.
- `sizeof` a struct includes padding. Place each member on a multiple of its alignment, then round the total up to the largest alignment. Reordering members changes the size.
- `#pragma pack(push)`, `pack(1)`, `pack(pop)` removes padding for the struct in between.
- `reinterpret_cast<char*>(&x)` relabels the address only. The bytes are unchanged.
- DLL build: `-DBUILDING_MYLIB` on the DLL compile only. Application build: link with `-L. -lmylib`, or load at runtime with `LoadLibrary`, `GetProcAddress`, `FreeLibrary`.
- (added, S12) Module style DLL, the exam style: interface file `export module Name;` with `extern "C" { export ... }`, implementation file `module Name;` with the same `extern "C"` braces and the body. Header style is not examined.
- (added, S12) Creating the DLL: compile the interface, compile the implementation, then `g++ -shared -o NAME.dll X.o Y.o`. `-shared` appears only here.
- (added, S12) Building the program that links implicitly: compile the interface, compile main.cpp, then `g++ -o prog.exe -L. -lname X.o main.o`. The `-l` name is the DLL's file name without `.dll`. All three flags in `-std`, `-fmodules-ts` and `-c` start with a dash.
- (added, S12) The module name, the interface file's name and the DLL's name are three separate names.
- `extern "C"` keeps names plain, for functions only. Classes stay mangled.

---

## See also
- [[CSC01B1_Notes_S1_Foundation-Topics]]
- [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]]

## Amendments
S12: Added the module style to the DLL section after the lecturer said, as reported by the user, that the exam uses module interface files only and does not test header files for DLLs. New sections: The module style, the files you write; Building the DLL with a batch file; Building a program that links implicitly; The three names that never match; How the 2025 Q4 questions map onto these files (with model answers for 2025-A Q4.3, 2025-B Q4.3 and 2025-C Q4); Explicit linking, the exam pattern. The header based material is kept and marked as not examined. Added bullets to Do not forget and an update to the DLL item under Struggle items. All code marked (added) was compiled with a MinGW g++ cross-compiler (13.2) and not run on Windows.

---
*CDG version: written under an earlier version that was not recorded (S7); amended with CDG v10 (S12, 2026-10-29).*
