---
module: CSC01B1
topic: Exception Handling
session: 8
tags: [definition, worked-example, common-mistake, exam-flagged, added]
---

# CSC01B1 S8: Exception Handling (Lecture 7)

This note retells Lecture 7 start to finish so it can be read without the slides. Content that goes beyond the slides is marked (added), and every code example was compiled and run with g++ in C++20 mode. This is the third ST2 bonus topic, after templates and DLLs. #exam-flagged

## What an exception is
An exception is an undesirable event that a program can detect while it runs: dividing by zero, a missing input file, a letter typed where a number was expected. #definition

The language cannot pick one correct reaction, because the right reaction depends on the application. A calculator can print a message and carry on. A batch job may have to stop. So C++ gives you a mechanism and lets you place the handling code at the point where the error can occur.

## assert
assert checks whether an expression meets a condition. If it does not, the program is terminated with an error message. The slide's example is a divisor of zero.

```cpp
assert(expression);
```

(added) assert is declared in the header cassert. When it fails, g++ prints something like `Assertion 'd != 0' failed` and the process aborts (exit code 134 on Linux), so no later line runs.

assert can only stop the program. It cannot recover and carry on, which is the gap try/catch fills.

## try, catch and throw
The mechanism has two halves. An exception is thrown inside a try block and is caught by a catch block.

- The try block holds the statements that may generate an exception. It also holds the statements that must not run once something fails, because the rest of the try block is skipped after a throw.
- A try block is followed by one or more catch blocks.

```cpp
try
{
    //statements
}
catch (dataType1 identifier)
{
    //exception-handling code
}
.
.
.
catch (dataTypen identifier)
{
    //exception-handling code
}
.
.
.
catch (...)
{
    //exception-handling code
}
```

The dots stand for further catch blocks.

### The catch parameter
A catch block specifies the type of exception it can catch and holds the handler. The data type of its parameter is what decides which exceptions it catches.

- A catch block can have at most one parameter.
- The parameter is a placeholder for the value thrown, so inside the handler you can use that value.
- With an ellipsis in place of the parameter, `catch (...)`, the block catches exceptions of all types. It has no parameter, so you cannot read the thrown value inside it.

### The throw statement
For try/catch to work, the exception must be thrown inside the try block.

```cpp
throw exception;
```

where expression is a constant value, variable, or object.

(added) The slide writes `exception` in the syntax line but `expression` in the description. They mean the same item, so read the line as `throw expression;`.

The thrown object can be a specific object or an anonymous object. In C++, an exception is a value, and its type is what gets matched against the catch parameters. #definition

### What happens when something is thrown
- Nothing thrown in the try block: all its catch blocks are ignored and execution resumes after the last catch block.
- Something thrown in the try block:
  - the remaining statements of the try block are ignored
  - the catch blocks are searched in order for an appropriate handler
  - if the thrown type matches the parameter type of a catch block, that block executes and the remaining catch blocks are ignored

### Worked example: dividing safely
(composite) Read two integers and divide the first by the second. If the divisor is zero, print a message instead of crashing. #worked-example

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int a, b;
    cin >> a >> b;
    try
    {
        if (b == 0)
            throw string("Division by zero");
        cout << a / b << endl;
    }
    catch (string msg)
    {
        cout << msg << endl;
    }
}
```

With b equal to 0 the string is thrown, the division line is skipped, the string matches `catch (string msg)`, msg holds the thrown value, and the program continues after the catch. With b equal to 2 nothing is thrown and the catch block is ignored. (Compiled and run for inputs 8 0 and 8 2.)

## Order of catch blocks
A catch block can catch all exceptions of one specific type, or all types of exceptions. The blocks are searched from top to bottom and the first match is the only one that runs.

> [!warning] catch (...) must come last
> The slide says a catch with an ellipsis "should" be the last block of its sequence. In g++ it is an error if it is not: `'...' handler must be the last handler for its try block`. (added, checked by compiling) Write it last every time.

(added) A related trap is a base class handler placed before a derived one. It compiles with a warning, and the base block runs because it matches first.

<span style="color:#e03131">Wrong:</span> `catch (exception &e)` first, then `catch (invalid_argument &e)`. Throwing an invalid_argument runs the first block, and the second can never run.

<span style="color:#2f9e44">Right:</span> `catch (invalid_argument &e)` first, then `catch (exception &e)`. Specific handlers go before general ones.

The slides' own rule for this lecture is simply: be careful about the order in which you list catch blocks. #exam-flagged #common-mistake

## The C++ exception classes
C++ supports exception handling through a hierarchy of classes. Class exception is the base of the exception classes provided by C++, and it lives in the header file exception. #definition

### what()
The what function returns a string describing the exception object thrown by the built-in exception classes. For a built-in class it returns the message the object was constructed with: after `throw invalid_argument("n must not be negative")`, calling `e.what()` in the handler returns that text.

> [!note] where what() belongs
> what() belongs to class exception, in the header exception. It does not belong to stdexcept. stdexcept only defines the subclasses, and they inherit what(). (added) Its declared form is `virtual const char * what() const noexcept`.

### The two subclasses and their children
Both are defined in the header stdexcept.

```
exception
  logic_error
    invalid_argument    illegal arguments used in a function call
    out_of_range        string subscript out of range
    length_error        a length greater than the maximum allowed for a string
  runtime_error
    overflow_error
    underflow_error
```

(added) The tree is a reorganisation of the slide's list, not a slide figure.

### Worked example: a built-in class
(composite) A function rejects a negative argument and the caller prints the message. #worked-example

```cpp
int checkNonNegative(int n)
{
    if (n < 0)
        throw invalid_argument("n must not be negative");
    return n;
}

int main()
{
    try { checkNonNegative(-4); }
    catch (invalid_argument e) { cout << e.what() << endl; }
}
```

Output: `n must not be negative`. (Compiled and run.)

> [!warning] catch by reference, not by value
> (added, checked by compiling) The slides catch by value, and that works when the catch type is the exact thrown type, but g++ warns about it. Catching a base class by value is worse. After `throw runtime_error("boom by value")`, `catch (exception e)` prints `std::exception` from e.what(), because the object is cut down to a plain exception and the message is lost. `catch (exception &e)` prints the real message. This is the slicing problem from the polymorphism session (S5, file name not verified in the index).

## Your own exception classes
You can create your own exception classes to handle specific exceptions. C++ processes them with the same mechanism: throw, then match a catch by type.

- The throw statement is used to throw your own exceptions.
- Any class can be an exception class.
- How you use the class is what makes it an exception class. There is no special keyword and no required base class.

An exception class with member variables typically includes constructors and the function what. The constructor stores the details of the failure when the object is thrown, and what hands them back to the handler. #definition

### Worked example: a user-defined class
(composite) Reject a withdrawal larger than the balance and report both numbers. #worked-example

```cpp
class NotEnoughFunds
{
public:
    NotEnoughFunds(int bal, int req) : balance(bal), requested(req) {}
    string what() const
    {
        return "Balance " + to_string(balance) +
               ", requested " + to_string(requested);
    }
private:
    int balance;
    int requested;
};

void withdraw(int balance, int amount)
{
    if (amount > balance)
        throw NotEnoughFunds(balance, amount);
    cout << "Withdrew " << amount << endl;
}

int main()
{
    try { withdraw(100, 250); }
    catch (NotEnoughFunds e) { cout << e.what() << endl; }
}
```

withdraw(100, 250) satisfies the check, so an anonymous NotEnoughFunds object is thrown and the handler prints `Balance 100, requested 250`. withdraw(100, 50) throws nothing and prints `Withdrew 50`. (Compiled and run both ways.)

> [!note] this what() is your own
> NotEnoughFunds does not derive from exception, so its what() is a function you wrote and named by convention. It returns a string, not a const char pointer. If a user-defined class did derive from exception, a handler for exception would also catch it. That goes beyond the lecture. #added

## Rethrowing
When an exception occurs in a try block, control passes straight to a catch block, and that block can do one of two things:

- handle the exception, or partially process it and then rethrow the same exception
- rethrow a different exception for the calling environment to handle

Why: the code that detects an error is often not the code that knows the right response, and rethrowing lets you keep the exception-handling code all in one place.

```cpp
throw;
```

rethrows the same exception that the catch block caught, and

```cpp
throw expression;
```

throws a different one, where expression is a constant value, variable, or object. The thrown object can be a specific object or an anonymous one.

(added) The slide that shows these two lines was never viewed while writing this note, so both forms are the standard C++ syntax, not copied from the slide. Check them against the slide.

> [!note] throw; versus throw expression;
> `throw;` with nothing after it rethrows the exception just caught. `throw expression;` starts a new one.

### Worked example: partial handling then rethrow
(composite) #worked-example

```cpp
void process(int n)
{
    try
    {
        if (n < 0)
            throw invalid_argument("negative");
        cout << "ok" << endl;
    }
    catch (invalid_argument e)
    {
        cout << "process saw: " << e.what() << endl;
        throw;
    }
}

int main()
{
    try { process(-1); }
    catch (invalid_argument e) { cout << "main saw: " << e.what() << endl; }
}
```

Output: `process saw: negative`, then `main saw: negative`. (Compiled and run.)

## The throw clause
A function specifies the exceptions it throws in its heading using the throw clause.

(added) Illustration, not from the slide:

```cpp
void f() throw(int, double);
```

> [!warning] the throw clause does not compile in modern C++
> (added, checked by compiling) g++ in C++20 mode rejects it: `ISO C++17 does not allow dynamic exception specifications`. In C++11 it is only a deprecation warning. Know the idea for the test, but do not write it in code you intend to compile.

## Three ways to handle an exception
When an exception occurs, the programmer usually has three choices. The right one depends on the program. #exam-flagged

### Terminate the program
Best when continuing is pointless. Example: an input file does not exist when the program starts. Output an appropriate error message and terminate.

### Fix the error and continue
Best when the user can retry. Example: a user types a letter instead of a number, so the input stream enters the fail state. Keep prompting until the entry is valid. (added) The standard way to do that is `cin.clear()` to reset the stream state and `cin.ignore(1000, '\n')` to discard the bad input. The fail state of a stream is covered in [[CSC01B1_Notes_S7_FileHandling]], whole file because no heading there was verified.

(composite)

```cpp
int x;
cout << "Enter a number: ";
cin >> x;
while (cin.fail())
{
    cin.clear();
    cin.ignore(1000, '\n');
    cout << "Try again: ";
    cin >> x;
}
```

### Log the error and continue
Best when the program must never stop. Examples: a program that runs a nuclear reactor or continuously monitors a satellite. Write the exception into a file and keep running.

## Stack unwinding
When an exception is thrown in a function, the function can do one of three things:

- do nothing
- partially process the exception and throw the same exception or a new one
- throw a new exception

In each case the function-call stack is unwound so the exception can be caught in the next try/catch block. #definition

When the stack is unwound, the function in which the exception was not caught and/or rethrown terminates, and the memory for its local variables is destroyed. Unwinding continues until a try/catch handles the exception, or until the program does not handle it, in which case the function terminate is called and the program ends.

Picture each running function as a frame on a stack, newest on top. Unwinding removes frames from the top, one at a time, asking each in turn whether it has a matching catch:

```
when c throws:      after c is removed:   after b is removed:    handler runs:

  c  <- no handler    b  <- no handler      a  <- handler found     a
  b                   a                     main                    main
  a
  main
```

(added) The picture is my own reorganisation, not a slide figure.

### Worked example: three functions, one handler
(composite) #worked-example

```cpp
void c() { throw runtime_error("boom"); cout << "c end" << endl; }
void b() { c(); cout << "b end" << endl; }
void a()
{
    try
    {
        b();
        cout << "a end" << endl;
    }
    catch (runtime_error e)
    {
        cout << "a caught: " << e.what() << endl;
    }
}
int main()
{
    a();
    cout << "main end" << endl;
}
```

Output: `a caught: boom`, then `main end`. The lines c end, b end and a end never print. (Compiled and run.)

Line by line:
- c throws and has no handler, so c terminates and its locals are destroyed.
- b has no handler either, so b terminates the same way.
- a's try block holds the call to b, so the rest of the try block (the a end line) is skipped, and the matching catch runs.
- Once the catch finishes, the exception counts as handled. a carries on after the try/catch and returns normally to main, which prints main end.

> [!warning] what exactly is skipped
> Only the rest of the try block is skipped in the function that has the handler. Anything after its try/catch still runs. The functions without a handler, b and c, are abandoned completely. #common-mistake

<span style="color:#e03131">Wrong:</span> "there has to be a catch block, so the program looks for one and finds it".

<span style="color:#2f9e44">Right:</span> nothing forces a handler to exist. The exception leaves each function in turn, and if no matching catch is found by the end of main, terminate is called. A matching type is also not automatic: with `catch (int e)` in a, the runtime_error would not match and the search would continue outward.

(Checked by compiling: the same program with the try/catch removed from a prints `terminate called after throwing an instance of 'std::runtime_error'` with what(): boom, and exits with code 134.)

## Lecture recap
- An exception is an undesirable event detectable during program execution.
- assert checks an expression against a condition and terminates the program if it is not met.
- try/catch handles exceptions. Statements that may generate one go in the try block.
- A catch block specifies the type it can catch and holds the handler. The type of its parameter decides what it catches.
- If nothing is thrown in a try block, all its catch blocks are ignored.
- exception is the base class for the exception classes, and what returns a string describing the exception thrown by the built-in classes.
- You can create your own exception classes. Any class can be an exception class, based on how it is used.
- A function specifies the exceptions it throws in its heading with the throw clause.
- If the program does not handle an exception, the function terminate terminates it.

## Do not forget
- ⚠️ catch (...) goes last. g++ makes anything else a compile error.
- ⚠️ A throw skips the rest of the try block only. Code after the try/catch still runs.
- First matching catch wins, and it is the only one that runs. Specific before general.
- what() belongs to class exception, not stdexcept. Your own class has one only if you write it.
- Catch by reference. Catching exception by value loses the message.
- An unhandled exception reaches terminate, not silence.
- Match the technique to the program: terminate, fix and continue, or log and continue.
- The throw clause does not compile from C++17 on.

## See also
- [[CSC01B1_Notes_S7_FileHandling]]
