Supersedes S6.

## 1. OPEN ITEMS (unresolved, oldest first)
None open from this session.

## 2. RESOLVED THIS SESSION
```
concept                                  | correction
------------------------------------------|---------------------------------------------
Why so many stream-like objects exist     | Corrected the impression that cout, cin,
(cout, cin, ifstream, ofstream, fstream)  | ifstream, ofstream, fstream were separate,
                                           | unrelated mechanisms. They are all
                                           | instances of the same underlying stream
                                           | classes; cout is simply an ostream object
                                           | already wired to the terminal. Formatting
                                           | logic (setf/precision/width) is written
                                           | once and works identically regardless of
                                           | which stream it's called on.
------------------------------------------|---------------------------------------------
sizeof(struct) scope                      | Corrected the assumption that sizeof at
                                           | the end of a struct reports only the last
                                           | member's size. It reports the size of the
                                           | ENTIRE struct: every member plus any
                                           | padding inserted between/after them.
------------------------------------------|---------------------------------------------
Purpose of OR-combining setf/open flags   | Corrected uncertainty about what bitwise
                                           | OR-ing flags together (e.g. ios::fixed |
                                           | ios::showpos) is actually achieving.
                                           | Clarified it combines several independent
                                           | on/off settings into one argument for a
                                           | single function call, since each flag
                                           | occupies its own separate bit position.
                                           | The earlier '1 | 1 = 1' remark was only
                                           | reassurance that repeating/overlapping a
                                           | flag is harmless, not the goal itself.
------------------------------------------|---------------------------------------------
Direction of reading after a seek         | Corrected the assumption that reading
                                           | might continue in whatever direction the
                                           | pointer last arrived from (e.g. reversing
                                           | back toward the front after seeking from
                                           | the end). Reading always moves FORWARD
                                           | from the current position, regardless of
                                           | how that position was reached. Seeking to
                                           | the end and then reading fails outright
                                           | (nothing ahead to consume) rather than
                                           | wrapping or reversing.
------------------------------------------|---------------------------------------------
reinterpret_cast vs static_cast/          | Corrected uncertainty about what
dynamic_cast                              | reinterpret_cast<char*>(&record) does.
                                           | It performs no conversion and no runtime
                                           | check (unlike static_cast, a real value
                                           | conversion, and dynamic_cast, a runtime-
                                           | checked polymorphic cast) — it is pure
                                           | relabelling of an existing address so it
                                           | satisfies write()'s required char*
                                           | parameter type. The underlying bytes are
                                           | completely unchanged.
------------------------------------------|---------------------------------------------
Byte-offset calculation to a given record | Corrected uncertainty about the actual
index                                     | goal of the seekg arithmetic. Clarified as
                                           | two chained steps: (1) file size in bytes
                                           | via seekg(0, ios::end) + tellg(), divided
                                           | by sizeof(RecordType) to get record count;
                                           | (2) index * sizeof(RecordType) as the byte
                                           | offset for seekg/seekp to a specific
                                           | record. Confirmed with concrete worked
                                           | numbers (24-byte records, 120-byte file
                                           | = 5 records; index 2 -> byte 48).
------------------------------------------|---------------------------------------------
Struct padding — where and why it's       | Corrected uncertainty about where padding
inserted                                  | bytes actually go. Worked through byte-by-
                                           | byte with concrete offsets (int, char[10],
                                           | double): padding is inserted immediately
                                           | before whichever member's alignment
                                           | requirement the next free offset fails to
                                           | satisfy, only as many bytes as needed to
                                           | fix that one misalignment — not added
                                           | automatically "at the end" by default. A
                                           | second worked example (same three
                                           | members, double moved second) confirmed
                                           | that reordering members changes both
                                           | padding placement and total struct size
                                           | (24 bytes vs 32 bytes for the same data).
------------------------------------------|---------------------------------------------
#pragma pack — override mechanism for     | This was in the lecture slide (image
padding                                   | content, missed on first pass of this
                                           | topic and correctly flagged by the
                                           | student) but omitted from the initial
                                           | explanation. Corrected: #pragma
                                           | pack(push) saves the current alignment
                                           | setting, #pragma pack(1) forces 1-byte
                                           | alignment (no padding at all), and
                                           | #pragma pack(pop) restores the prior
                                           | setting — the actual "control this
                                           | behaviour" mechanism the slide referred
                                           | to as non-standard but available.
------------------------------------------|---------------------------------------------
write() output being unreadable "nonsense"| Corrected the concern that raw struct
                                           | output via write() being unreadable text
                                           | meant something was wrong. Clarified this
                                           | is expected and correct: write() copies
                                           | raw in-memory bytes exactly as-is, meant
                                           | to be read back via read() into the same
                                           | struct type, not opened as human-readable
                                           | text — contrasted directly with Part 4's
                                           | formatted, human-readable text output.
------------------------------------------|---------------------------------------------
Whether "the whole file is records" is    | Corrected the assumption that
knowable automatically                    | size_in_bytes / sizeof(RecordType) is
                                           | always valid. Clarified this is a file-
                                           | format design assumption imposed by the
                                           | programmer when the file was written, not
                                           | something detectable from the file
                                           | itself; if a header is present, its size
                                           | must be subtracted before both the
                                           | record-count division and any seek offset
                                           | calculation.
------------------------------------------|---------------------------------------------
Alignment of compound/class struct        | Corrected the assumption that a compound
members                                    | member's alignment requirement equals its
                                           | own sizeof. Clarified it is determined
                                           | recursively — the largest alignment
                                           | requirement among ITS OWN members, traced
                                           | down to a built-in type — which can be
                                           | smaller than its total size. Also
                                           | clarified that a genuinely abstract class
                                           | cannot appear as a plain (non-pointer)
                                           | struct member at all, since it cannot be
                                           | instantiated, and that a polymorphic
                                           | object's vtable pointer is meaningless
                                           | once written to disk and reloaded.
------------------------------------------|---------------------------------------------
ifstream cannot be made writable via flags| During the guided coding exercise:
                                           | corrected the assumption that passing
                                           | ios::out to an ifstream would grant write
                                           | capability. Write ability is a property
                                           | of the CLASS (fstream, or ofstream), not
                                           | something flags can add to a
                                           | structurally input-only class.
------------------------------------------|---------------------------------------------
.open() argument count                    | During the guided coding exercise:
                                           | corrected passing three separate flag
                                           | arguments to .open() instead of one
                                           | combined argument. .open() takes exactly
                                           | (filename, mode) — multiple flags must be
                                           | OR'd together into a single mode value
                                           | first.
------------------------------------------|---------------------------------------------
Inverted .fail() check logic              | During the guided coding exercise:
                                           | corrected if (!in_stream.fail()) — which
                                           | reads as "if it did NOT fail" and so
                                           | reported an error on SUCCESS — to
                                           | if (in_stream.fail()).
------------------------------------------|---------------------------------------------
Assigning a C-style array with =          | During the guided coding exercise:
                                           | corrected an attempt to assign a char[]
                                           | struct member with = after declaration.
                                           | Arrays cannot be assigned with = at all;
                                           | resolved using initializer-list syntax at
                                           | the point of declaration
                                           | (Score s1 = {"Alice", 90};).
------------------------------------------|---------------------------------------------
seekg vs seekp for a read operation       | During the guided coding exercise: called
(RECURRING PATTERN — see section 4)       | seekp immediately before a .read() call.
                                           | Corrected to seekg, since .read() consults
                                           | the read marker specifically, and seekp
                                           | only ever moves the write marker — this
                                           | is the exact seekg/seekp independence
                                           | point taught explicitly in Part 5,
                                           | recurring as a live mistake in application
                                           | shortly after.
------------------------------------------|---------------------------------------------
seekg called as a free function, and      | During the guided coding exercise:
conflating seeking with reading           | corrected seekg(...) called without a
                                           | stream object (must be in_stream.seekg(...),
                                           | a member call), and corrected an attempt
                                           | to assign seekg's return value directly
                                           | into a Score variable. seekg only moves
                                           | the position pointer and returns the
                                           | stream itself; fetching the actual data
                                           | still requires a separate .read() call.
------------------------------------------|---------------------------------------------
Off-by-one record indexing                | During the guided coding exercise:
                                           | corrected seeking to index 2 (2 *
                                           | sizeof(Score)) when asked for "the 2nd
                                           | record," which in 0-based indexing is
                                           | index 1.
------------------------------------------|---------------------------------------------
.read()/.write() naming vs direction of   | During the guided coding exercise: student
data flow                                 | asked directly why .read() "writes into" a
                                           | variable when the name suggests the
                                           | opposite. Clarified the function names
                                           | describe what happens to the FILE, not the
                                           | variable — write() sends data out to the
                                           | file, read() pulls data out of the file —
                                           | mirroring cin >> variable, which is never
                                           | called "writing" despite changing the
                                           | variable's contents.
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
None flagged as standalone notation confusion this session — all items above were resolved through worked examples and, for the coding-exercise items, through writing and correcting actual code.

## 4. PATTERNS ACROSS SESSIONS
Per the cross-session learnings on file, S5 and S6 struggles both centred on over-generalizing a mechanism's scope — assuming something is more shared or broader than it actually is (inheritance subobjects assumed shared rather than separate in S5; `=` and the copy constructor assumed merged, and template scope assumed to leak beyond one declaration, in S6). This session's "seekg vs seekp for a read operation" item (section 2, flagged RECURRING PATTERN) is a direct, dated recurrence of that exact same pattern: seekg and seekp were explicitly taught as two independent, non-shared position markers in Part 5's own N.B., and the assumption that one seek call would serve both directions resurfaced as a live coding mistake in the very same session, shortly after. This is now a three-session-running pattern (S5, S6, S7) and is worth actively watching for in any future lecture involving two or more parallel-but-independent tracking mechanisms (the same shape of trap that hit inheritance subobjects, `=`/copy-constructor, template scope, and now seekg/seekp).

A second, newer pattern worth noting: this session surfaced a recognition-vs-production gap directly ("I did okay [on the quiz] but if I were to write code... it would be blank"). Quiz performance (recognizing a correct answer among options) did not predict the ability to produce equivalent code from scratch without guidance — the guided coding exercise required correcting six distinct live mistakes despite every underlying concept having just been quizzed successfully. Worth building a short "write it yourself" exercise into future sessions' close-out, not just a recognition-style quiz, if retention is the goal.

## 5. RETEST FIRST (ranked)
1. Given a struct's member list and each member's size, calculate sizeof() by hand including padding placement (not just the final number).
2. seekg vs seekp: which one governs .read(), which governs .write(), and does moving one move the other?
3. What does reinterpret_cast<char*>(&x) actually do to the bytes of x, and how does that differ from static_cast or dynamic_cast?
4. Given a file size, a header size, and sizeof(RecordType), calculate the number of records and the correct seek offset to reach a given record index.
5. #pragma pack(1) — what does it change about a struct's layout, and why would you use it for disk records specifically?
6. Without looking anything up, write (not just describe) the four-line pattern: open with combined flags, write a record, seek to an index, read a record back.
