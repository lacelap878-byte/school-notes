---
module: CSC01B1
topic: ST2 Summary (S5 to S8)
test_label: ST2
tags: [summary]
---

# CSC01B1 ST2 Summary (Sessions 5 to 8)

Built for fast review before ST2 (Friday 16 October 2026, a 3 hour practical, VPL marked), not first learning. If something here does not click, follow the link back to the full session note.

Scope: S5 to S7 are tested. Templates (in the S6 note) and DLLs (in the S7 note) are not tested. Exception handling (S8) is the bonus. `cs` PROFILE has no proof content, so no Proofs file accompanies this one.

Reliability: where this file and an older session log disagree, the practice sessions of 14 and 15 October 2026 (the UJImage drills) are the most reliable record of what is known and what is not.

## Contents

Click a link to jump to it.

- [[#Definitions]] signature, parameter, argument, operand, image parameter and the rest, with a labelled example
- [[#Material covered]] which session notes feed which task
- [[#Condensed concept pass]] polymorphism, operators, files, exceptions in short
- [[#Worked example notebook]] code examples, including the UJImage `operator=`
- [[#Common mistakes]]
  - [[#Mistakes from the UJImage drills]] 14 and 15 October, the most reliable record
  - [[#Not yet covered]]
  - [[#Mistakes from the older struggle logs]]
- [[#Tips]]
  - [[#Operator signature decision tree]] start here when you forget a signature
  - [[#Reading the paper]] what each operator means, and how often it appears
  - [[#Paper shape]] T0 to T5 and the bonus, with marks
  - [[#What the past papers show]] the 2018 to 2025 patterns
  - [[#What is provided]] files you get on the day
  - [[#Final checks before submitting]]
  - [[#The bonus plan]] the exception hierarchy recipe
  - [[#Tooling note]]

## Definitions

Words used in this file, and what each one points at. Anatomy of one signature:

```
 return type    name           parameters (in the brackets)     after the brackets
     |            |                       |                            |
  UJImage&   operator=      ( const UJImage& objRHS )                  (const)
 "what comes   "which       "what the caller hands in"           "promise about the
  back"         operator"                                         LEFT object"
```

- **Signature**: the whole first line of a function: return type, name, parameters, and the `const` after the brackets. Learning to write signatures is learning to write that one line.
- **Parameter**: one item inside the brackets. It is a type plus a name, like `const UJImage& objRHS`. It describes what the caller must hand in.
- **Argument**: the actual value handed in when the function is called. In `a = b`, the argument is `b`; the parameter is `objRHS`.
- **Return type**: the type written before the function name. It is what the caller gets back.
- **Operand**: a thing an operator works on. In `a + b`, `a` and `b` are the operands.
- **Left operand**: the one on the left of the operator (`a` in `a + b`). For a member operator it is the object itself, so it is not written in the brackets. In the code it is called `this`.
- **Right operand**: the one on the right (`b`). For a member operator it is the only thing in the brackets. It is called `objRHS` ("object, right hand side").
- **Image parameter**: a parameter whose type is `UJImage`, in other words "the other image on the right". It is the same thing as the right operand, seen from inside the function. When this file says "another image on the right?" it asks: is there a `b` in `a + b`? Then the parameter is `const UJImage& objRHS`.
- **Member operator**: an operator written inside the class. The left operand is `this`, so the brackets only hold the right operand.
- **Nonmember operator**: an operator written outside the class, used when the left operand is not the class (`cout << a`). Every operand is a parameter, so a binary one has two. A nonmember that needs private members is declared `friend` inside the class.
- **Unary operator**: only one operand (`!a`, `a++`). No right operand, so no image parameter.
- **Dummy `int`**: an `int` in the brackets of `operator++(int)` that carries no value. Its only job is to tell the compiler this is the post form (`a++`).
- **Reference (`&`)**: an alias to the real object, not a copy. Used so big things are not copied, and so the function can change the original.
- **`const` on a parameter** (`const T&`): the function promises not to change what was handed in.
- **`const` after the brackets**: the function promises not to change the left object (`this`).
- **`const` in front of the return type**: the returned thing cannot be changed by the caller. Museum picture: the `const` after the brackets is the museum's promise ("we change nothing in here"), and the `const` in front is the sign on the display case ("look, don't touch"). A museum that promised to change nothing would not hand visitors a hammer, so the read version of `()` has both, and the write version has neither.
- **`*this`**: the left object itself. Returning it with `return *this;` is how `=`, pre `++`, and `!` hand back "the same image" so the call can be chained.
- **Mutator**: a function that changes the object (`=`, `++`, `!` in these drills). An accessor only reads it (`==`, `+`, read `()`).
- **Temporary**: a short-lived value made while evaluating an expression, like the result of `a + b`. Never return a reference to one or to a local variable.

## Material covered

- [[CSC01B1_Notes_S5_Polymorphism]] polymorphism, the T3 material
- [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]] operator overloading, the T4 material (the templates half is not tested)
- [[CSC01B1_Notes_S7_FileHandling]] file handling, the T5 material (the DLL half is not tested)
- [[CSC01B1_Notes_S8_ExceptionHandling]] exception handling, the bonus
- T1 to T3 (class basics, composition, inheritance) lean on S3 and S4, see [[CSC01B1_Summary_ST1]]
- Practice: the UJImage drills of 14 and 15 October 2026 (no note file; the source is those sessions and the ST2 handoff kept in the project)

## Condensed concept pass

**Why virtual exists**: a base class function that calls a virtual function runs the derived version, chosen at run time (late binding), even for classes written after the base was compiled; without `virtual` the base version is fixed at compile time. `virtual` on the base function carries down to derived overrides automatically. (see: [[CSC01B1_Notes_S5_Polymorphism#Core definitions]], [[CSC01B1_Notes_S5_Polymorphism#The problem virtual functions solve]])

**Overriding versus redefining**: changing a virtual function in a derived class is overriding, changing a non-virtual one is redefining; virtual costs extra storage and speed. (see: [[CSC01B1_Notes_S5_Polymorphism#Overriding vs redefining]], [[CSC01B1_Notes_S5_Polymorphism#The cost of virtual]])

**Pure virtual and abstract classes**: `= 0` makes a function pure virtual and its class abstract (no objects can be made); a derived class that leaves any inherited pure virtual function unimplemented is itself still abstract. (see: [[CSC01B1_Notes_S5_Polymorphism#Pure virtual functions and abstract base classes]])

**Type compatibility and slicing**: a derived object can be assigned to a base variable, never the reverse. Plain object assignment slices: the assignment runs correctly but only on the base's own members, so the derived data is lost. A base pointer to a derived object copies only an address, so the whole object survives and virtual calls work. (see: [[CSC01B1_Notes_S5_Polymorphism#Worked example: Pet and Dog]], [[CSC01B1_Notes_S5_Polymorphism#The slicing problem]])

**Virtual destructors**: deleting a derived object through a base pointer needs a virtual destructor so the derived destructor runs first and the base one after it. They free two separate subobjects at different addresses, so there is no double free. (see: [[CSC01B1_Notes_S5_Polymorphism#Virtual destructors]])

**Casting**: upcasting with `static_cast` is always legal; downcasting with `dynamic_cast` is legal but dangerous. (see: [[CSC01B1_Notes_S5_Polymorphism#Upcasting]], [[CSC01B1_Notes_S5_Polymorphism#Downcasting]])

**How virtual works inside**: each class has a table of function pointers, and each object holds a pointer to its class's table. (see: [[CSC01B1_Notes_S5_Polymorphism#Inner workings of virtual functions]])

**Which operators come free**: only `=` and `.` work on a class object without writing anything; every other operator overload is optional. Overloading `=` becomes mandatory when the class has pointer members. (see: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Why Operator Overloading Is Needed]], [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Overloading the Assignment Operator (=)]])

**Member versus nonmember**: a member function is called on its left operand, so the left operand must be the class type. `m + 5.0` can be a member or a friend; `5.0 + m` and `cout << m` must be nonmembers. `=`, `[]`, `()` and `->` must always be members. (see: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Operator Functions as Member vs Nonmember Functions]])

**Stream operators**: `<<` and `>>` are friends, with the stream as the first parameter, returned by reference so `cout << a << b` chains. `>>` takes the class object non-const because it writes into it. (see: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]], the section Overloading << and >>, linked at file level because its heading contains backticks)

**The assignment operator**: `if (this != &rightObject)` guards self assignment; inside it free the old memory, allocate to the new size, copy, then `return *this;` after the `if`. The compiler supplied `=` copies every member including private ones, but for a pointer member it copies only the address, so two objects share one array: the old array leaks and the shared one is freed twice. The copy constructor is the other case: it builds a NEW object from an existing one (`Clock c = b;`), so it owns nothing yet; `c = b;` on an existing `c` is assignment. (see: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Overloading the Assignment Operator (=)]], [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Classes and Pointer Member Variables (Revisited)]])

**Pre and post increment and decrement**: pre changes `*this` and returns it; post saves a copy first, changes `*this`, and returns the saved old copy. The dummy `int` only tells the compiler which one is which. `--` is the same with the opposite change. (see: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Overloading Unary Operators]], [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Operator Overloading Quick Reference]])

**Subscript**: two versions, `Type& operator[](int index);` and `const Type& operator[](int index) const;`. The compiler picks by whether the object is const, so a const object needs the const version or it cannot be indexed at all. (see: [[CSC01B1_Notes_S6_OperatorOverloadingTemplates#Operator Overloading Quick Reference]])

**Streams and open modes**: `.open()` takes one mode argument, so combine flags with `|`. `ifstream` is read only by class; `fstream` takes the mode. Check success with `if (x.fail())` for an error. (see: [[CSC01B1_Notes_S7_FileHandling#The four-step pattern]], [[CSC01B1_Notes_S7_FileHandling#Combining flags with OR, testing them with AND]])

**Random access**: there are two independent markers: `seekg` for reading and `seekp` for writing. Seeking only moves a marker and reads nothing. A record index counts from 0, so the 2nd record is index 1; add the header size when computing an offset and subtract it when counting records. (see: [[CSC01B1_Notes_S7_FileHandling#Two independent position markers]], [[CSC01B1_Notes_S7_FileHandling#Seeking (source, slide 36)]])

**Raw bytes**: `write` and `read` are named for what happens to the file. `reinterpret_cast<char*>(&x)` only relabels the pointer type, with no conversion and no check, which is why the file looks like nonsense in a text editor. (see: [[CSC01B1_Notes_S7_FileHandling#What reinterpret_cast does (added)]], [[CSC01B1_Notes_S7_FileHandling#Why the file looks like nonsense (added)]])

**Padding and alignment**: padding goes before a member whose alignment the next offset fails, and reordering members changes the total size. A struct member's alignment is the largest alignment among its own members. `#pragma pack` controls padding. `sizeof(RGBColour)` is 12 (three ints). (see: [[CSC01B1_Notes_S7_FileHandling#Padding and byte alignment (slide 39)]], [[CSC01B1_Notes_S7_FileHandling#Alignment of a struct or class member (added)]])

**DLLs**: not tested in ST2, so not condensed here. (see: [[CSC01B1_Notes_S7_FileHandling#Reusable software components: DLLs (slides 42 to 51)]])

**Try, catch, throw**: an exception is a value matched to a catch block by type. After a throw the rest of the try block is skipped, the first matching catch runs, and if nothing is thrown every catch block is ignored. `assert` ends the program with a message and cannot recover. (see: [[CSC01B1_Notes_S8_ExceptionHandling#try, catch and throw]], [[CSC01B1_Notes_S8_ExceptionHandling#assert]])

**Order of catch blocks**: the first match wins. `catch (...)` catches any type and must be last (g++ rejects anything after it). A base class handler placed before a derived one compiles with a warning and the base block runs. (see: [[CSC01B1_Notes_S8_ExceptionHandling#Order of catch blocks]])

**Exception classes**: `exception` (header `exception`) is the base class and owns `what()`. `stdexcept` defines `logic_error` (invalid_argument, out_of_range, length_error) and `runtime_error` (overflow_error, underflow_error). Any class can be an exception class by how it is used; a user class with member variables typically has constructors and its own `what`. (see: [[CSC01B1_Notes_S8_ExceptionHandling#The C++ exception classes]], [[CSC01B1_Notes_S8_ExceptionHandling#Your own exception classes]])

**Rethrowing and handling techniques**: a handler can handle the exception fully, process it partly and `throw;` the same one, or throw a different one. The three techniques are terminate, fix and continue, and log and continue. (see: [[CSC01B1_Notes_S8_ExceptionHandling#Rethrowing]], [[CSC01B1_Notes_S8_ExceptionHandling#Three ways to handle an exception]])

**Stack unwinding**: a function with no handler is abandoned and its locals destroyed, outward through the callers until a matching catch is found or `terminate` ends the program. Only the rest of the try block is skipped; the code after the try/catch still runs. (see: [[CSC01B1_Notes_S8_ExceptionHandling#Stack unwinding]])

## Worked example notebook

- Pet and Dog: plain assignment slices, pointer assignment keeps the whole Dog. (source: [[CSC01B1_Notes_S5_Polymorphism#Worked example: Pet and Dog]])
- Padding: the same members reordered give a different `sizeof`. (source: [[CSC01B1_Notes_S7_FileHandling#Example 2 (composite): the same members reordered]])
- Write, seek, read back with a binary `fstream`. (source: [[CSC01B1_Notes_S7_FileHandling#Worked coding exercise: write, seek, read back (composite)]])
- Three functions, one handler: what is skipped and what keeps running. (source: [[CSC01B1_Notes_S8_ExceptionHandling#Worked example: three functions, one handler]])
- UJImage `operator=` (source: the user's R2 drill, 15 October 2026, passing all checks):

```cpp
UJImage& UJImage::operator=(const UJImage& objRHS){
	if(this != &objRHS){
		dealloc();
		alloc(objRHS._intRows, objRHS._intCols);
		for(int i = 0; i < _intRows; i++){
			for(int j = 0; j < _intCols; j++){
				this->_pPixels[i][j] = objRHS._pPixels[i][j];
			}
		}
	}
	return *this;
}
```

- UJImage post increment, capped at 255, returns the old image (source: the user's R2 drill, 15 October 2026):

```cpp
UJImage UJImage::operator++(int){
	UJImage tempObj(*this);
	for(int i = 0; i < _intRows; i++){
		for(int j = 0; j < _intCols; j++){
			if(this->_pPixels[i][j].intRed < 255) this->_pPixels[i][j].intRed++;
			if(this->_pPixels[i][j].intBlue < 255) this->_pPixels[i][j].intBlue++;
			if(this->_pPixels[i][j].intGreen < 255) this->_pPixels[i][j].intGreen++;
		}
	}
	return tempObj;
}
```

- UJImage `+` as a pixelwise average, one line per channel, integer division of the sum (source: the user's R2 drill, 15 October 2026). The sum of two values up to 255 is at most 510, so the average never passes 255 and no cap is needed:

```cpp
objResult._pPixels[i][j].intRed = (_pPixels[i][j].intRed + objRHS._pPixels[i][j].intRed) / 2;
```

- UJImage `!` as the R2 drill defined it, a yes or no check that is true only if every pixel is `{0,0,0}`. Warning: that meaning is the drill's own, not the papers' (see Tips, What the 2018 to 2025 papers show). The part to keep is the loop pattern: return `false` on the first counterexample, `return true;` after the loops (source: the user's R2 drill, 15 October 2026):

```cpp
if(this->_pPixels[i][j].intRed != 0 || this->_pPixels[i][j].intGreen != 0 || this->_pPixels[i][j].intBlue != 0){
	return false;
}
```

- One pixel from `RGBColour** _pPixels`: `_pPixels[intRow]` is a row, `_pPixels[intRow][intCol]` is one `RGBColour`. No conversion, just two subscripts. (source: the user's `getPixel`, 15 October 2026)

## Common mistakes

Evidence from the 14 and 15 October 2026 practice sessions comes first, because it is the most recent record. Out of ST2 scope and skipped: the S6 template items and the S7 DLL jargon items.

### Mistakes from the UJImage drills

- <span style="color:#f08c00">Open:</span> operator signatures from memory. A cold recall of the eight declarations got one right (`++(int)`). The slips: object parameter written without `&` (four of eight), trailing `const` the wrong way (put on `=`, missing on `+` and on the read `()`), `()` returning `UJImage` instead of `RGBColour&`, and `!` given a parameter. The decision tree under Tips was written afterwards; a second cold recall has not been done yet.
- <span style="color:#f08c00">Open:</span> `operator=` was missed on the 14 October quiz (3.5 of 5, the miss was that `=` returns `UJImage&` and ends with `return *this;`) and again on 15 October. The first attempt compared contents instead of addresses for the self check, tried to call the copy constructor on an existing object (`*this(objRHS);`), and left out `dealloc()` and the arguments to `alloc`. The cause was believing `this` is a fresh object; in `operator=` it already exists and owns memory. This is the S6 item copy constructor versus assignment, showing up in code.
- Forgetting the class name on out-of-class definitions (`UJImage::`): `!=` on 14 October, `+` and `!` on 15 October.
- Any versus every in `operator!`: the first version returned `true` at the first black pixel. To prove "every pixel is black", stop at the first counterexample (a pixel with colour) and return `false`; `true` only after the loops. It is the same shape as `==`.
- Repeated lines copied without changing the channel: in `+`, the blue and green lines both used `intRed` on the left side.
- A reference return cannot fall back to `return {0, 0, 0};` because that is a reference to a temporary: a compile error for the non-const version, a dangling reference for the const one. The fix was no range check in `()`; the proper guard is an exception.
- Small compile slips: a missing `return tempObj;` in `++(int)`, missing semicolons, one extra parenthesis, a typo `_Pixels`, and a lowercase versus capital variable name (`ObjResult`). `setPixel` checked only the upper bounds; negatives need `>= 0` as well.
- Stated correctly in the user's own words on 15 October, not yet retested: `const` in front of the return type means what comes back already exists and cannot be changed through it; `const` at the end means `this` is not changed.
- Progress to keep: copy constructor, `==`, `!=` and `getPixel` were right first time; Round 1 (T2 and T3 from a blank page) passed 9 of 9 unaided; Round 2 (the whole UJImage module from a blank page) now passes 20 of 20 with address and undefined behaviour checking on.

### Not yet covered

- `alloc` and `dealloc` written from memory (Round 2 copied them from an earlier backup file).
- `readTXTFile` and `writeBINFile` written from memory.
- `<<` on the user's own machine (the Linux test machine crashes on it, see Tips), the exception classes, and a timed mock on the 2025 B paper.

### Mistakes from the older struggle logs

- Resolved in S5: slicing is the assignment running correctly on a smaller footprint, not breaking; and a derived object holds its own separate base subobject, so chained destructors do not double free.
- <span style="color:#f08c00">Open:</span> member versus friend when the left operand is not the class type; the post-increment return value (the saved copy, not the changed object); `[]` on a const object needs the const overload because the signature decides; default `=` with a pointer member compiles and copies the address; copy constructor versus assignment.
- <span style="color:#f08c00">Open:</span> file handling: `seekg` versus `seekp`; recognising an answer versus writing the code from a blank page; where padding goes and the effect of reordering; alignment of a compound member; what `reinterpret_cast` does; `.open()` taking one mode argument; `ifstream` versus `fstream`; `if (!x.fail())` reporting an error on success; arrays cannot be assigned with `=` after declaration; the off-by-one record index; `.read()` and `.write()` direction; the header offset in record counting.
- S8, resolved in the same session as the correction so with the weakest evidence: what stack unwinding skips, a catch block is not forced to exist, and `what()` belongs to `exception`, not `stdexcept`.
- Pattern across sessions: treating two independent things as one shared thing (S5 subobjects, S6 `=` versus the copy constructor, S7 `seekg` versus `seekp`).

## Tips

### Operator signature decision tree

Answer the questions in order.

```
1. Is the LEFT operand not the class (cout << a, 5.0 + a)?
     yes -> nonmember friend, and << and >> always are:
            friend ostream& operator<<(ostream&, const UJImage&);
            friend istream& operator>>(istream&, UJImage&);   (no const, it is written into)
            In a module, declare it outside the class with export, and make it a friend only
            if it touches private members. Not yet tested on the user's machine (the << round).
2. Otherwise it is a member. What does it give back?
     a yes or no answer (==, !=)            -> bool
     a pixel or element (() and [])         -> RGBColour&  (write)  and  const RGBColour&  (read)
     the same image (=, pre ++, pre --, !)  -> end with:  return *this;
                                               returns UJImage&
     a NEW image (+, post ++, post --)      -> UJImage, by value
3. Is there another image on the right (a + b, a == b, a = b)?
     yes -> the parameter is:  const UJImage& objRHS
     no  -> no image parameter: ! takes nothing, post ++ and -- take a dummy (int),
            () takes two ints, [] takes one index (an int, or a const string& id, as in 2021 morning)
4. Does it change the LEFT image?
     yes (=, ++, --, !, write ())      -> nothing after the brackets
     no  (+, ==, !=, read ())          -> const after the brackets
5. The read version of () also has const in FRONT:
            const RGBColour& operator()(int intRow, int intCol) const;
6. Every parameter in the brackets, ask two things:
     Does the function change it?   yes -> T&        no -> const T&
     Is it small (an int)?          yes -> by value  no -> by reference (&)
   Streams can never be copied, so they are always ostream& / istream&.
   << : ostream&  (receives output, changes)   and  const UJImage&  (only read)
   >> : istream&  (reading advances it)        and  UJImage&        (overwritten)
   The stream is the first parameter and is also what you return.
   A member's left operand is this, covered by the trailing const (step 4).
```

Worked through: `==` is a yes or no answer (bool), has an image on the right (`const UJImage& objRHS`), and does not change the left image (`const` at the end), giving `bool operator==(const UJImage& objRHS) const;`.

The pre and post forms:

```cpp
UJImage& operator++();     // pre,  ++a   no (int)
UJImage operator++(int);   // post, a++   has the dummy (int)
```

Two places where the lecture note and the past papers differ, and either compiles: the lecture shows `=` returning `const className&` and pre `++` returning `className` by value, while the past papers' declarations use `UJImage&`. Where a paper provides a declaration, copy its return type. The lecture's `[]` is `Type& operator[](int index);` plus a const version, for a one dimensional container; past UJImage papers use `()` with two ints for the 2D case (`()` or `[]` appeared in 10 of 17 papers), so read what the paper says `[]` should return.

### Reading the paper

Each operator's meaning is defined by the paper, not by C++: `+` meant a pixelwise average and `!` changed every pixel (in the drill, to white; check what each paper says). Read that line for every operator. Operator frequency in the 2018 to 2025 papers (17 papers, recounted from the paper text on 15 October 2026): `=` 17, `()` or `[]` 10, `<<` 9, `==` or `!=` 4, `!` 4, `++` or `--` 3, `>>` 2, `+` 1. The 2025 paper A asks for `=` (deep copy), `++` post increment capped at 255, and `+` (pixelwise average of two images).

### Paper shape

Project is UJImage (a dynamic 2D array of `RGBColour` pixels) as a C++20 modules project. T0 UML class diagram saved as PDF 10, T1 class basics 20, T2 composition and delegation 20, T3 inheritance and polymorphism 20, T4 operator overloading 15, T5 file handling 15, bonus 20 as a separate submission. The core is 100.

### What the past papers show

- Every paper has T0 to T5 plus a 20 mark bonus, of which you pick one (Templates, DLLs or Exception Handling). In 2025 the paper says 120 marks are available but the maximum is 100, so the bonus can cover lost core marks. Marks: T0 10, T1 20 (constructors 5, destructors 5, information hiding 5, .h and .cpp 3, comments 2), T2 20 (has-a 5, lifecycle 5, delegation 5, algorithm 5), T3 20 (abstract base 5, overriding 5, polymorphism 5, member visibility 5), T4 15 (5 per operator), T5 15 (define structure 5, write 5, read 5).
- T2 is always the same shape: a container class creates a helper object in its constructor, deletes it in its destructor, and delegates one void member function to it. T3 turns the helper into an abstract base class with one pure virtual function and two derived classes whose constructors take parameters (a threshold, a flag, a seed); the container then calls it polymorphically. Variants seen: a pure virtual `clone` (2020) and virtual mutators (2019 B).
- T4 always has three operators and `=` (deep copy) is always one of them. The other two come from: `()` or `[]` 10 of 17, `<<` 9, `==` or `!=` 4, `!` 4, `++` or `--` 3, `>>` 2, `+` 1.
- `!` has never been a yes or no check. It changed the image: reset the grid (2021 afternoon), flip active and inactive pixels (2024 C), set every value to 255 (2025 B and C). The 2025 B main calls it as a plain statement, `!objCopy;`. So `!` is a mutator: no `const` after the brackets, and `UJImage&` with `return *this;` is a safe return.
- T5: in 14 of 17 papers the read (text) and write (binary) are member functions of UJImage. In 2025 they are free functions in main.cpp with fixed signatures: `UJImage readTXTFile(string strFileName);` and `void writeBINFile(string strFileName, const UJImage& objImage);`. The direction flipped twice (2019 B and 2025 C): read a binary file and write a text file in P3 format, with signatures `void readBINFile(string strFileName, UJImage& objImage);` and `void writeTXTFile(string strFileName, const UJImage& objImage);`. Practise both directions.
- Bonus wording: "errors related to indexing and file handling using an inheritance hierarchy of exception classes. Update main accordingly." is the wording in every paper from 2022 to 2025. Older wordings: numerical ranges (2019 A, 2020), file handling (2019 B), impossible values (2021 afternoon), any error types (2018). So have ready a base class plus `IndexException` and `FileException`; a third derived class for a bad value or range (a colour above 255) covers the older wordings.
- The provided main.cpp is what gets compiled, so follow it where it disagrees with the paper text. In 2025 B the paper says `invertImage` but main calls `applyFilter`, and the paper calls `==` the "post increment" operator.
- `<<` risk: all three 2025 main files do `cout << objImage << endl;` but the 2025 T4 lists do not ask for `<<`, and the paper does not say where it comes from. Be ready to write it (P3: the magic number `P3`, columns and rows, max intensity, then red green blue per pixel).
- Utils risk: all three 2025 main files `import Utils;` and build.bat compiles `utils.cpp` first, but no utils.cpp is provided and the paper text never mentions it. Its place in the build order (before UJImage.cpp) and T5 asking you to define `RGBColour` suggest the packed `RGBColour` struct may belong in Utils. This is an inference, not something the paper states. On the day, look at the file list first: if utils.cpp exists, read it before writing anything; if it does not, create it.

### What is provided

Only `main.cpp`, `build.bat` and the data file. `build.bat` compiles `utils.cpp`, which is not provided, so do not assume `alloc`, `dealloc` or the getters are given: write the whole class. `build.bat` also runs `del *.bak`.

### Final checks before submitting

Every out-of-class definition starts with `ClassName::`. Every function that returns a value has its `return`. Object parameters are `const UJImage&`. `operator=` uses `this != &objRHS`. Run the whole thing once with `build.bat` before submitting.

### The bonus plan

One module `UJImageException` (a class with a string message, a constructor and a `what()` function), with `IndexException` and `FileException` derived from it, each in its own module, but only as many as the bonus question asks for. The user's reading of the spec is that one place that throws is enough, either a range check in `operator()` (an `enforceRange` helper called first thing, throwing `IndexException`) or a file that fails to open (`FileException`); confirm that against the bonus question itself. `getPixel` and `setPixel` keep ignoring out of range, because the spec and the tests say so. Keep the exception modules out of the core submission, since `build.bat` compiles a fixed list of modules; work in a separate copy of the project.

### Tooling note

The g++ 11.4 test machine crashes when a module defines `operator<<` for `ostream` and the importing file uses `std::string`. This looks like a GCC 11 limit, not a code error, so test `<<` on the user's own machine.
