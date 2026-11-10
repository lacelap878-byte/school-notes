Supersedes S1 to S4.

1. OPEN ITEMS (unresolved, oldest first)
None carried in from prior sessions and none open at end of this session.

2. RESOLVED THIS SESSION
Stack based slicing framed as the assignment operator "breaking" | Pet's
assignment operator does not fail or malfunction when vpet = vdog runs.
It executes correctly, but it is scoped only to Pet's own members
(name), since Pet's class definition has no concept of breed at all.
Slicing is the operator doing its job on a smaller footprint than the
source object actually has, not an error. The correction: pointer
assignment (ppet = pdog) never copies the object at all, it copies an
address into an already complete Dog object that still exists
unmodified on the heap, which is why breed survives through a pointer
but not through plain object assignment.

Feared double free from chained destructors, traced to a wrong model of
inheritance | assumed a Derived object somehow shares or references
Base's members rather than containing a genuinely separate copy of them,
so a chained destructor call (Derived's then Base's, automatic once
Derived's destructor is virtual) looked like it could free the same
memory twice. The correction: inheritance is composition under the
hood, every Derived object physically contains a complete, distinct Base
subobject in its own memory, including private Base members, access
control (public/protected/private) only governs which code may name a
member, not whether it exists or where it lives. Chained destructors
each free only what their own constructor allocated, at two different
addresses, so no overlap occurs. A double free only happens from actual
pointer aliasing (two pointers set to the same address), which is a data
ownership bug unrelated to destructor chaining or virtual vs
non-virtual.

3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
None noted.

4. PATTERNS ACROSS SESSIONS
None yet.

5. RETEST FIRST
None.
