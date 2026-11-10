---
module: CSC01B1
topic: C++20 Modules
session: S2
tags: [definition]
---

# C++20 Modules (CSC01B1)

Covers the module system introduced in C++20: what a module is, writing a
first one, grouping exports, and separating a module's interface from its
implementation. Read top to bottom once, then use the headings as an index.

---

## Why modules exist

Any C++ program is built from small reusable entities: functions, types,
variables. That's enough for a small program, but as a codebase grows you
need a way to group related functionality so everyone, including you later,
knows where to look for it. C++20's answer is the module: a self contained
subcomponent of related functionality.

Modules vary widely in size. Some export a single type or constant; others,
like the standard library's `std` module, export a large library. Granularity
is your choice. Splitting an already large module into submodules is possible
but out of scope here.

## Module interface

```
A module can export any number of C++ entities (functions, constants, types,
and so on), which you can then use in any source file that imports the
module. A module may even export entire other modules. The combination of
all entities that a module exports is called the module interface. Entities
that are not part of the module's interface (directly or indirectly) can
only be seen and used from within the module itself.
```

The key distinction: exported entities are visible to anyone who imports the
module, everything else stays private to it. Client code, `main()` included,
can only reach what was actually exported (see: Import and usage below).

---

## Building a first module

Worked reference: a module `LibMath` exporting a function to determine the
oddity of an integer.

- CSC01B1 convention: module interface files use the `.cpp` extension. There
  is no universal convention across compilers for module file extensions.
- Apart from the `export` and `module` keywords, and the absence of a
  `main()`, a module interface file looks like an ordinary source file.

### Module declaration

```
Somewhere at the start of every module file is a module declaration. Every
module declaration contains the `module` keyword followed by the module's
name. If `module` is preceded by `export`, the file is a module interface
file.
```

> [!note] `export` in front of `module` is what makes it an interface file
> Exported entities alone don't do this; the `export module` declaration
> itself is the marker.

### Naming a module

Same rules as naming any other C++ entity, with one addition: dots may chain
identifiers inside a module name. `math.polynomials` and `a.b.c` are valid.
`123math`, `.polynomials`, `abc.`, and `a..b` are not. Dotted names are used
to simulate submodule hierarchies (submodules are out of scope for this
course).

Only module interface files may contain export declarations, and only after
the module declaration.

### Import and usage

The name used to `import` a module comes from the name declared in its
`export module` statement, not from the file's name. CSC01B1 always names
interface files `module_name.cpp` by convention, but this is not a technical
requirement; some compilers allow arbitrary file names for module interface
files.

Once a module is imported, all of its exported entities become usable. In
the `LibMath` example, `main()` can use `getOddity()` and the `Oddity`
enumeration because both are exported; nothing not exported by `LibMath`
would be reachable from `main()`.

---

## Export blocks

Exporting entities one at a time (as above) means one `export` declaration
per entity. An export block groups several exports into one statement.

```
An export block consists of the `export` keyword followed by a sequence of
declarations between curly braces.
```

This is purely a grouping convenience: it changes how the exports are
written, not which entities end up exported.

---

## Separating prototypes from implementations

Real function definitions can run to dozens of lines, and a module may need
several local helper functions or types to realise its exported interface.
Left inline, all of that implementation detail obscures the module's
interface, making it harder to see at a glance what the module actually
offers.

Two ways to fix this:

1. Within the module interface file itself: move function definitions to the
   bottom of the file, after the interface/prototypes.
2. A separate implementation file entirely (out of scope for this course).

```
You can, but do not have to, repeat the `export` keyword in front of a
definition placed at the bottom of the file. What is not allowed is adding
`export` in front of the declaration of an entity that was first declared
without `export`.
```

> [!warning] export cannot be added retroactively
> If an entity's first declaration omitted `export`, no later definition of
> that entity can add it. The exported/non-exported status is fixed at first
> declaration.

---

## Do not forget

- Exported entities are usable outside the module; everything else is
  private to it.
- `export` in front of `module` is what makes a file a module interface
  file.
- The name used in `import` comes from the `export module` declaration, not
  the file name.
- Module names may use dots to chain identifiers; nothing else in C++ naming
  allows this.
- An export block groups exports, it does not change what's exported.
- `export` can never be added to an entity's definition if its first
  declaration didn't have it.
