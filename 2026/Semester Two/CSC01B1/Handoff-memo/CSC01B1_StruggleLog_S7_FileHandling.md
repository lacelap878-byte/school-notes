Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S7. Later evidence is added to each item as a Status line. The cumulative retest list is in the S13 log.

## 1. OPEN ITEMS (unresolved, oldest first)

1. seekg versus seekp
   - Used seekp before a .read(). The read marker (seekg) and the write marker (seekp) are independent; .read() uses seekg. Answered correctly in the S9 quiz (weakest evidence).
   - S13 (30 Oct quick fire): the overwrite question was wrong: after a seek and a write the file should read A then AZZDEF, the answer given was ABCDEF. S13 (1 Nov): `tellp` does not exist on an `ifstream` (compiled: `has no member named 'tellp'; did you mean 'tellg'?`); on an `fstream` both agree, tellp = tellg = 10 after seeking to the end of a 10 byte file. The seekg and tellg calls in 3.4 were correct.
   - Status: open for seekp and the overwrite behaviour. Closed for seekg and tellg when reading (see section 2).

2. Recognition versus production
   - Can pick the right answer in a quiz but could not write the code from scratch without guidance (six live corrections in S7). Showed again in S9 drills and in S12 (module files and batch commands).
   - S13: 2025-A 3.1 was left blank in the paper; the cold rerun stopped at `while (getline(is,`; 3.3 needed a skeleton of comments; 3.2 was right on the second try; 3.4 was right once the skeleton was seen. Answers improve when the shape is given.
   - Status: open. The biggest exam risk, because the exam is written.

3. Alignment of a compound member
   - Assumed it equals the member's sizeof; it is the largest alignment among its own members.
   - Status: open. Not retested.

4. Assigning a char array with =
   - Arrays cannot be assigned after declaration; use an initializer list (or strcpy for text).
   - Status: open. Not retested.

5. Off by one record index
   - "2nd record" is index 1.
   - Status: open. The S13 worked examples state that records are numbered from 0; not retested.

6. Header offset in record counting
   - Record count and seek offsets must subtract and add the header size.
   - Status: open. Not needed by the 2025 papers; not retested.

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
Padding placement and reordering          | S13: struct of char + int, two records is 16 bytes (30 Oct, one
                                          | correct answer). 1 Nov: the packed struct for 3.2 was right on the
                                          | second try (#pragma pack(push, 1) ... pop), measured 1050 bytes
                                          | packed against 1052 unpacked (compiled).
reinterpret_cast                          | S13: used correctly in the 3.3 answer
                                          | (.read(reinterpret_cast<char*>(&rec), sizeof(WaterCheck))). It only
                                          | relabels the address as char*; it converts nothing.
.open() takes one mode argument           | S13: ios::binary | ios::in and ios::in | ios::binary in the 3.3 and
                                          | 3.4 answers. Combine flags with | in a single argument.
ifstream vs fstream                       | S13: the user prefers fstream with explicit flags. Compiled: ios::in
                                          | with binary reads and cannot write; ios::out alone wipes the file
                                          | (10 bytes to 0); ios::binary alone does not open (fail = 1).
!fail() check                             | S13: if (istream.fail()) correct in the 3.3 and 3.4 answers and in
                                          | the 3.1 attempts.
seekg call form and seek vs read          | S13: istream.seekg(0, ios::end); then tellg() for the size, with a
                                          | stream object. 3.4 correct, 5 of 5 (compiled: 4 records counted).
.read()/.write() direction                | S13: read takes bytes FROM the file INTO the variable; used correctly
                                          | in 3.3.
DLL syntax and jargon (header style)      | Closed by scope. The lecturer said, as reported on 29 Oct, that the
                                          | exam uses module style DLLs only. The dllexport and dllimport macro
                                          | switch and the -D flag are no longer examined. The module style,
                                          | explicit linking and batch commands continue in the S12 and S13 logs.
Seek record index and seekg usage         | S9 quiz Q6 correct (weakest evidence; the user said it needed
                                          | grinding). Backed up by the S13 answers above.
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Jargon in the DLL material (dllexport, dllimport, __stdcall, extern "C", HINSTANCE, .impl.cpp, -D, -Wl,--out-implib) caused the most trouble. Concepts were fine, keywords were not. For the exam, only the module style names matter (see the S12 log).

## 4. PATTERNS ACROSS SESSIONS
Assuming two independent things are one shared thing: S5 (inheritance subobjects), S6 (= and copy constructor), S7 (seekg and seekp).
Recognition versus production (item 2): close every session with a write it yourself exercise.

## 5. RETEST FIRST (ranked, from section 1)
1. Write the 3.1 text file reading template from a blank page (open, getline loop, istringstream, flag, print).
2. Which of seekg and seekp governs .read() and .write(), and what a write after seekp does to the old bytes.
3. Calculate the padding of a struct by hand once more (the resolved item rests on one answer plus one production).
4. Alignment of a struct member of struct type.
5. Initialise a char array after declaration, and record index versus record number.

---
*CDG version: written under an earlier version that was not recorded (S7) | restructured S13 (v11) | 2026-11-01*
