# CSC01B1 — Lecture 6: File Handling

## 1. Secondary storage, why files, and the stream concept

**The memory hierarchy.** Two properties storage can have: fast, and high capacity — hard to have both at once, so real systems trade one for the other across a hierarchy: processor registers → processor cache → RAM → flash/USB → hard drives → tape backup, getting slower and cheaper (but larger) at each step down. Registers, cache, and RAM are **volatile** ("power on" — lost when power is cut); flash memory downward is **non-volatile** ("power off" — survives). This non-volatile tier is what "secondary storage" refers to.

**Why files.** A file gives **persistence**: data written to it outlives the program run that wrote it. Practically: input files can be reused run after run, output can be inspected later, and you can work with data sets far larger than you'd type by hand.

**C++ standard streams.** `cin` (input, keyboard), `cout` (output, terminal), `cerr` (error, terminal) — from `<iostream>`, already familiar.

**The stream abstraction.** A stream is a flow of characters — the channel, not the source/destination itself. Once connected to something (keyboard, terminal, or a file), you use `<<`/`>>` exactly as before. `cin`, `cout`, and a file stream are all instances of the same underlying stream class machinery — `cout` is simply an `ostream` object already wired to the terminal by default. This is why formatting logic written once (Section 4) works identically regardless of which stream it's called on.

**Files specifically.** Reading = data flows from file into the program. Writing = data flows from program into file.

---

## 2. Sequential file I/O

**Sequential access**: read from the start, move forward only — no backtracking (same model as `cin`).

**Four-step pattern** for any file stream: declare → connect (open) → read/write → close.

> A stream object **cannot be assigned with `=`** — connecting goes through `.open()`, not `=`.

```cpp
#include <fstream>
ifstream in_stream;
ofstream out_stream;
in_stream.open("infile.dat");
out_stream.open("outfile.dat");
```
Default `.open()` behaviour: **creates** the file if absent, **truncates** (empties) it if present.

```cpp
int a;
in_stream >> a;      // read, like cin
out_stream << a;      // write, like cout
in_stream.close();
out_stream.close();
```

**Worked example** — reads three numbers from `infile.dat`, sums them, writes a formatted sentence to `outfile.dat`. `infile.dat` is untouched; no console output at all — the whole exchange is file-to-file.

**Checking success.** Opening can fail (disk full, permissions, file locked elsewhere):
```cpp
in_stream.open("in.dat");
if (in_stream.fail())
{
    cout << "Input file opening failed.\n";
    exit(1);
}
```
Applied per-stream, each with its own message and `exit(1)`.

**Interactive vs. file-driven.** The prompt/wait pattern disappears — `cin >> age` (with a `cout` prompt) becomes `in >> age` (no prompt, no human on the other end).

---

## 3. Opening modes and file flags

**Appending** — override the default truncate-on-open behaviour:
```cpp
ofstream fout;
fout.open("data.txt", ios::app);
```
Existing content stays; new writes land after it.

**Filenames at runtime.** A filename can be a `char` array filled by the user via `cin >>` instead of a hardcoded literal — everything downstream (`.fail()`, reading, writing, `.close()`) works identically; `.open()` doesn't care whether the string is a literal or a variable.

**File flags.** `fstream` can open a file for **both** input and output. Default `.open()` behaviour: text mode, both read and write privileges. Override via the two-argument form:

| Flag | Meaning |
|---|---|
| `ios::app` | Append — pointer forced to end **before every write** |
| `ios::ate` | At-end — pointer moved to end **once, on opening**, then free to move elsewhere |
| `ios::trunc` | Truncate — clear existing contents |
| `ios::binary` | Binary I/O — no `\n`-style character conversion |
| `ios::in` | Read privileges |
| `ios::out` | Write privileges |

> `app` and `ate` are **not the same guarantee**: `ate` only repositions once, at open; `app` re-forces the pointer to the end on *every* write, so a prior seek elsewhere can never cause an accidental overwrite.

**Combining flags — bitwise OR.** Each flag is one independent bit; `|` combines several into a single argument for one function call:
```cpp
myfstream.open("Myfile.dat", ios::in | ios::binary);
```
Repeating a flag (`ios::in | ios::in`) is harmless (`1 | 1 = 1`) — OR-ing is about **combining independent settings into one call**, not a special trick; each flag occupies its own bit position so none get lost. **Testing** a flag uses bitwise AND: `binary_arg & mode_mask` isolates one bit without needing to know the rest.

---

## 4. Output formatting and further stream usage

**Member functions** (callable on any stream, including `cout`): `setf()` (set formatting flags), `precision()` (decimal places), `unsetf()` (clear a flag), `width()` (field width, used with left/right).

**setf flags:**

| Flag | Meaning | Default |
|---|---|---|
| `ios::fixed` | No e-notation (unsets `scientific`) | Not set |
| `ios::scientific` | Always e-notation (unsets `fixed`) | Not set |
| `ios::showpoint` | Always show decimal point + trailing zeros | Not set |
| `ios::showpos` | Show `+` before positive numbers | Not set |
| `ios::right` | Pad left of value within `width()` | Set |
| `ios::left` | Pad right of value within `width()` (unsets `right`) | Not set |

**Worked example — `make_neat()`:**
```cpp
void make_neat(ifstream& messy_file, ofstream& neat_file,
               int number_after_decimalpoint, int field_width)
{
    neat_file.setf(ios::fixed); neat_file.setf(ios::showpoint); neat_file.setf(ios::showpos);
    neat_file.precision(number_after_decimalpoint);
    cout.setf(ios::fixed); cout.setf(ios::showpoint); cout.setf(ios::showpos);
    cout.precision(number_after_decimalpoint);

    double next;
    while (messy_file >> next)
    {
        cout << setw(field_width) << next << endl;
        neat_file << setw(field_width) << next << endl;
    }
}
```
`+10.37000` style output, consistently, to screen and file simultaneously.

**I/O manipulators** — shorthand, need `#include <iomanip>`: `setw(n)` ⟺ `.width(n)`; `setprecision(n)` ⟺ `.precision(n)`.

**Streams as function parameters** must be **call-by-reference** (`ifstream&`, `ofstream&`) — a stream can't be copied at all (same underlying fact as "can't use `=` on a stream" from Section 2); pass-by-value would require a hidden copy the compiler won't generate.

**End-of-file via truth value:**
```cpp
while (in_stream >> variable) { ... }
```
Works because `operator>>` returns a stream reference, which has an implicit `bool` conversion — true while extraction keeps succeeding, false on failure (typically EOF). The loop is testing "did the last read succeed," not the value read.

---

## 5. Random access files and raw disk I/O

**Reframing "random access."** C++ makes no real distinction between sequential and random-access files — everything is a stream of bytes, and all reads/writes are fundamentally sequential character operations. "Random access" = moving *where* in that byte stream you are before reading/writing, rather than always continuing from the last position. Desirable because it avoids reading every record just to reach one further in.

**Two independent position markers.** `fstream` tracks read and write positions **separately**; it makes no assumption about whether a given stream is input or output.
- `.seekg(offset, dir)` — moves the **read** marker
- `.seekp(offset, dir)` — moves the **write** marker
- `.tellg()` — returns the current (read) byte position

> These are genuinely two independent trackers. Moving one does not move the other — a `seekp` before a `.read()` does nothing useful, because `.read()` consults the read marker, which `seekp` never touches.

**Reading direction.** Reading always moves **forward** from wherever the pointer currently is, regardless of how it got there. Seeking to the end and then reading fails outright (nothing ahead to consume) — there is no reverse-read or wraparound. To read something earlier, seek backward explicitly first.

**Seeking syntax:**
```cpp
myfile.seekg(0, ios::beg);   // start of file
myfile.seekg(0, ios::end);   // end of file
myfile.seekg(n, ios::cur);   // n bytes from current position
```

**Designing a fixed-size record format.** For index → offset arithmetic to work, records must be **fixed size**. Reference sizes: `int` = 4 bytes, `char array[6]` = 6 bytes, `double` = 8 bytes, `float` = 6 bytes (this course's figures); `string` is variable-length and unsafe for fixed-record math on its own.

**Writing raw bytes.** `ostream::write(char* data, int size)` / `istream::read(char* data, int size)` — `fstream` has both. First parameter must be `char*` (files are byte sequences), so non-`char*` data needs casting:
```cpp
myfile.write(reinterpret_cast<char*>(&record), sizeof(RecordType));
```
`reinterpret_cast` performs **no conversion and no check** — unlike `static_cast` (a real value conversion, e.g. `int`→`double`) or `dynamic_cast` (a runtime-checked polymorphic cast). It purely relabels an existing address as a different pointer type; the bytes of `record` are completely unchanged. This matters here because `.write()` wants "a raw byte sequence starting here," and a `char*` + byte count is exactly that — no printing or human-readability implied; the output is meant to be read back via `.read()` into the same struct type, not opened as text.

**Jumping to a specific record:**
```cpp
myfile.seekp(pos * sizeof(RecordType), ios::beg);
```
General procedure: `index * sizeof(RecordType)` gives the byte offset for any record index (0-based — "the 2nd record" is index 1). If the file has a header of known size, that header's size must be added to every offset, and subtracted before dividing to get record count.

**File size / record count:**
```cpp
int size_in_bytes;
myfile.seekg(0, ios::end);
size_in_bytes = myfile.tellg();
return (size_in_bytes / sizeof(RecordType));
```
Valid **only if the file is known, by design, to contain nothing but back-to-back fixed-size records from byte 0** — this is a file-format assumption imposed by whoever wrote the file, not something detectable from the file's bytes alone. A header changes the arithmetic: `(size_in_bytes - header_size) / sizeof(RecordType)`.

**Struct padding and byte alignment.** The compiler inserts padding (unused bytes) so each member starts at a memory address that's a multiple of that member's own alignment requirement (depends on type, compiler settings, 16/32/64-bit OS). Padding is invisible to normal member access but affects `sizeof(RecordType)` directly — relevant for any offset arithmetic using it.

*Worked example 1:*
```cpp
struct Record { int id; char name[10]; double val; };
```
- `id` (4 bytes, 4-byte aligned): offset 0–3. Next free: 4.
- `name` (10 bytes, 1-byte aligned, no restriction): offset 4–13. Next free: 14.
- `val` (8 bytes, needs multiple of 8): 14 isn't a multiple of 8 → **2 bytes padding at 14–15** → placed at offset 16–23. Next free: 24.
- Trailing: round 24 up to a multiple of 8 (largest member) → already 24. **`sizeof(Record) = 24`.**

*Worked example 2 — same members, `val` moved second:*
```cpp
struct Record { int id; double val; char name[10]; };
```
- `id`: 0–3. Next free: 4.
- `val` needs multiple of 8: 4 isn't → **4 bytes padding at 4–7** → placed at 8–15. Next free: 16.
- `name`: 16–25. Next free: 26.
- Trailing: round 26 up to multiple of 8 → 32 → **6 bytes trailing padding**. **`sizeof(Record) = 32`.**

Same data, different member order → different total size (24 vs. 32 bytes). Padding is inserted immediately before whichever member's alignment the next free offset fails to satisfy — not automatically tacked on "at the end" by default.

**`#pragma pack` — the actual override mechanism:**
```cpp
#pragma pack(push)   // save current alignment setting
#pragma pack(1)       // force 1-byte alignment — NO padding at all
struct MyStruct { char m1; short m2; int m3; char m4; };
#pragma pack(pop)     // restore prior setting
```
`pack(1)` forces members edge-to-edge with zero padding, making `sizeof` fully predictable and portable — directly useful for disk-record formats where exact, cross-platform layout matters. `push`/`pop` scope the override to just the struct(s) in between.

**Alignment of compound (class/struct) members.** The rule applies recursively: a compound member's own alignment requirement is the **largest alignment requirement among its own members**, traced down to built-in types — **not** the same number as its own `sizeof`.
```cpp
struct Inner { char a; double b; };   // sizeof(Inner) = 16, but alignment requirement = 8 (from b)
struct Outer { int x; Inner y; };      // y needs offset multiple of 8, not multiple of 16
```
A genuinely **abstract class** (pure virtual function present) cannot be instantiated at all, so it can never appear as a plain (non-pointer) struct member — only as a pointer/reference, where only the pointer's own alignment matters. Even a concrete polymorphic class carries a hidden vtable pointer (an address valid only within that one program run) — raw `write()`/`read()` of such objects to disk is unsafe, since the vtable pointer becomes meaningless once reloaded elsewhere or later.

---

## 6. Files for logic — reusable software components (DLLs)

**Why not just ship source?** Reusing tested components beats reinventing them, but source code compiled in normally gets **statically linked** into the client's executable at compile time — any update requires a full recompile of everything using it. The fix: modular library code **dynamically loaded at runtime**. On Windows: a **DLL** (Dynamic Link Library); Unix equivalent: **DSO**.

**DLL characteristics.** Several kinds exist (regular Win32, COM, ActiveX). Functions exported by ordinal and optionally by name. A DLL loads into the **same address space** as the calling application, so pointer-based data can pass safely across the boundary. Can often be called cross-language.

**Example DLL header, full walkthrough (this is the entire `example_dll.h`, line by line):**
```cpp
#ifndef EXAMPLE_DLL_H
#define EXAMPLE_DLL_H
```
- Standard **include guard**: if this header ever gets `#include`d twice in the same compilation (directly or via two other headers that both include it), the second inclusion is skipped entirely — `EXAMPLE_DLL_H` is already defined by then, so everything up to the matching `#endif` at the bottom is ignored the second time round. Not DLL-specific — this is the same include-guard pattern used for any header — but essential here since this header will genuinely be pulled in from more than one place (the DLL's own `.cpp`, and any client `.cpp` that uses the DLL).

```cpp
#ifdef BUILDING_EXAMPLE_DLL
  #define EXAMPLE_DLL __declspec(dllexport)   // building the DLL → export symbols
#else
  #define EXAMPLE_DLL __declspec(dllimport)   // using the DLL → import symbols
#endif
```
- Defines a **macro named `EXAMPLE_DLL`** that expands to either `__declspec(dllexport)` or `__declspec(dllimport)`, depending on whether `BUILDING_EXAMPLE_DLL` is defined at compile time. Every function/class declaration below then just writes `EXAMPLE_DLL` in front of it — one macro name standing in for "whichever of export/import applies to this build."

```cpp
extern "C"
{
    void __stdcall EXAMPLE_DLL c_greet(const char *s);
    int EXAMPLE_DLL c_power(int a, int b);
}
```
- Two plain functions, wrapped in `extern "C"` (no mangling → callable from C or any language) and marked `EXAMPLE_DLL` (expands to export/import as above) and `__stdcall` (Win32 calling convention) on `c_greet`.

```cpp
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
- `cpp_greet` and the `Greeter` class are **still exported/imported** (via `EXAMPLE_DLL`) but **not** wrapped in `extern "C"` — so their names *are* mangled, meaning only other C++ code can call them (a C caller, or `GetProcAddress` by plain name, would have no way to guess the mangled symbol). This is a deliberate design choice on the slide, not an oversight: `cpp_greet` is offered as a C++-only convenience alongside the C-callable `c_greet`/`c_power`, and `Greeter` couldn't be `extern "C"` at all even if you wanted it to be — C has no classes for `extern "C"` to correspond to.
- Final `#endif` closes the include guard opened at the top.
`BUILDING_EXAMPLE_DLL` is defined only while compiling the DLL itself, so the same header switches between export and import. `extern "C"` disables C++ name mangling, making functions callable from C (or other languages) — but only applies to plain functions; a class can never be `extern "C"`, since C has no classes for it to correspond to. `__stdcall` is the calling convention the Win32 API uses.

**`__declspec(dllexport)`/`dllimport` — mechanically, not just as boilerplate.** These aren't decoration; they change what the compiler/linker actually produce. `dllexport` tells the compiler to add that symbol's name to the DLL's **export table** — a literal list, baked into the compiled `.dll`, of symbols other programs are permitted to look up. `dllimport` tells the compiler not to assume the symbol is defined locally, and instead generate code that fetches its address from an external DLL's import table at load time. The same header is read in two different roles — once while compiling the DLL itself (export mode), once by a client program calling into an already-built DLL (import mode) — and `#ifdef BUILDING_EXAMPLE_DLL` is exactly what selects which role applies.

**`extern "C"` — the specific problem it solves.** C++ **mangles** function names to support overloading: `c_power(int,int)` doesn't compile down to the literal symbol `c_power`, but to something like `_Z7c_poweri i` encoding the parameter types (exact scheme is compiler/version-specific). That's invisible within one C++ program, but breaks DLL interoperability — another program (C, Python, a different C++ compiler) has no way to predict that mangled name. `extern "C"` disables mangling for those declarations, so the exported symbol is the stable literal string `"c_power"`, lookupable by name from any language. This is precisely why it can only wrap plain functions: mangling exists *because of* C++ overloading, and a class was never a C-style symbol to begin with, so there's nothing for `extern "C"` to "un-mangle" there.

**`__stdcall` — the concrete failure it prevents.** A calling convention fixes two things: which side (caller or callee) cleans up the stack after a call, and in what order arguments are pushed. Caller and callee disagreeing on either corrupts the stack at runtime — wrong values, crashes — often with **no compile error**, since the mismatch is purely at the binary calling level. `__stdcall` means "callee cleans the stack, arguments pushed right-to-left," matching every Win32 API DLL; a DLL meant to be called the way Windows API functions are called must match that convention explicitly rather than relying on the compiler's own default (often `__cdecl`, caller-cleans).

**Compiling a DLL (MinGW), flag by flag:**
```
g++ -c -DBUILDING_EXAMPLE_DLL example_dll.cpp
```
- `-c`: compile to an object file (`.o`) only, no linking yet.
- `-DBUILDING_EXAMPLE_DLL`: defines that macro from the command line — equivalent to `#define BUILDING_EXAMPLE_DLL` at the top of the file — this is literally what flips the header to export mode for this build.
```
g++ -shared -o example_dll.dll example_dll.o -Wl,--out-implib,libexample_dll.a
```
- `-shared`: tells the linker to produce a shared library (a DLL), not a standalone executable.
- `-o example_dll.dll`: names the output file.
- `-Wl,--out-implib,libexample_dll.a`: passes `--out-implib` through to the underlying linker (`ld`), also producing an **import library** (`.a`) — the file an implicit-linking client links against (`-lexample_dll`) so the compiler knows what symbols exist and where to resolve them, without the DLL's actual code being copied in.

**Implicit linking.** Client needs **both** the `.dll` and the `.h`; compiled/linked at compile time via the linker (`-lexample_dll`); resolved automatically when the program loads. This is a **hard dependency**: if the DLL isn't present at launch, Windows refuses to start the program at all. Suits a DLL that's a required, known-in-advance part of the program.

**Explicit linking.** No `.h` needed at all — resolved **at runtime**, by name. Used for plugin systems, optional features, or choosing between DLL versions/paths at runtime — the program **can start even if the DLL is missing**, check success (`if (hndlLibrary)`, `if (power)`), and degrade gracefully instead of refusing to launch — at the cost of more manual bookkeeping (`LoadLibrary`/`GetProcAddress`/`FreeLibrary`):
```cpp
typedef int (*TwoIntsToInt)(int, int);
TwoIntsToInt power = NULL;
HINSTANCE hndlLibrary = LoadLibrary("example_dll.dll");
if (hndlLibrary)
{
    power = (TwoIntsToInt)GetProcAddress(hndlLibrary, "c_power");
    if (power) cout << power(2, 4) << endl;
    FreeLibrary(hndlLibrary);
}
```
`LoadLibrary` → handle to the DLL; `GetProcAddress` → looks up a function **by name string**, returns its address cast to a matching function-pointer type; `FreeLibrary` → unloads it. Implicit and explicit linking are genuinely separate mechanisms — implicit resolves everything before the program runs (needs the header), explicit resolves everything while already running (needs only a string name).

> (see: [[CSC01B1_Notes_S1_Foundation-Topics#14. Function pointers]]) `power` here is an ordinary function pointer, no different in kind from `m` in S1's `average` example or `op` in S1's second worked example — declare a variable of function-pointer type, assign a function's address to it, call through it. The only new part in this DLL context is *where* the address comes from: not a function named directly in source, but whatever `GetProcAddress` returns after looking a name up in an already-loaded DLL at runtime.

**DllMain.** Optional entry point for code that should run at specific points in a DLL's life-cycle (loaded, unloaded, etc.).

---

## Worked coding exercise (from this session, compiled and verified)

Goal: open a binary file for read+write, define a fixed-size record struct, write three records, seek to and read back a specific one.

```cpp
#include <iostream>
#include <cstdlib>
#include <fstream>

int main()
{
    struct Score { char name[10]; int value; };
    using namespace std;

    fstream in_stream;
    in_stream.open("scores.dat", ios::in | ios::out | ios::binary | ios::trunc);
    if (in_stream.fail())
    {
        cout << "Error opening file." << endl;
        exit(EXIT_FAILURE);
    }

    Score s1 = {"Alice", 90};
    Score s2 = {"Bob", 75};
    Score s3 = {"Carl", 88};
    in_stream.write(reinterpret_cast<char*>(&s1), sizeof(s1));
    in_stream.write(reinterpret_cast<char*>(&s2), sizeof(s2));
    in_stream.write(reinterpret_cast<char*>(&s3), sizeof(s3));

    in_stream.seekg(sizeof(Score), ios::beg);   // record index 1 = the 2nd record
    Score test;
    in_stream.read(reinterpret_cast<char*>(&test), sizeof(test));
    cout << test.name << " " << test.value << endl;   // output: Bob 75

    return 0;
}
```

Points this exercise reinforced in practice: `fstream` (not `ifstream`) is required for read+write on one object; multiple `.open()` flags must be OR'd into a single argument; `ios::in | ios::out` needs `ios::trunc` too if the file doesn't exist yet; `if (fail())` not `if (!fail())`; C-style arrays need initializer-list syntax, not `=`, to set their contents; `seekg` (not `seekp`) governs where `.read()` starts; `seekg`/`.open()` are member calls on the stream object, not free functions; seeking alone does not fetch data — a separate `.read()` call is required; "the 2nd record" is index 1 in 0-based counting; and `.read()`/`.write()` are named from the **file's** perspective (data leaving/entering the file), not the variable's.
