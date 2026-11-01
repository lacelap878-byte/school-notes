Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S12, the revisit session on DLLs (module style) and operator overloading. The S6, S7, S9, S10 and S11 items this log used to carry are in their own logs. The S12 session taught into the S6 and S7 notes as amendments. Each item below records the exact wrong answer and the evidence. Where the evidence is a rule and not a test, the entry says so. The cumulative retest list is in the S13 log.

## 1. OPEN ITEMS (unresolved, oldest first)

1. this versus the right operand
   - First seen S12. Asked why the right operand is needed since this points to it. `this` is the LEFT operand; the parameter is the right one. A friend has no this and takes both. Evidence: the lecture rule only, not compiled.
   - S13 (1 Nov): the pointer versus object confusion came back as `this != other` and `*this != other` in operator=. `this` is a pointer, so it is compared with an address: `this != &other` (compiled: both wrong forms fail).
   - Status: open.

2. Module file basics (DLL)
   - First seen S12. Interface and implementation names and first lines were guessed. The implementation must start `module Name;` (not `module Name.cpp;`, which g++ rejects) and must repeat `extern "C"` (without it g++ says "declaration conflicts with import"). Evidence: compiled, S7 amendments.
   - S13 (1 Nov, 2025-A Q4 attempt): the interface had `char arrReadings` with no `[]`, which fails when the implementation is compiled (`conflicting declaration of C function 'bool isInvalid(char*, int)'`); an `export` on the definition in the implementation file is an error (`'export' may only occur after a module interface declaration`), as read it was crossed out; the 4.1 and 4.2 labels were swapped (the top block was the implementation).
   - Status: open.

3. Batch commands for DLLs: the module compile flag
   - First seen S12 (errors across the 2025-A and 2025-B Q4.3 attempts: -L. versus -l., -shared in the program command, a missing hyphen on -fmodules-ts, a wrong -l name).
   - S13 (1 Nov): 2025-C 4.2 right (-L., -lem-calculator, `-shared` crossed out by the user), 2025-B 4.3 right (-shared -o route-generator.dll with the interface and implementation objects). Still open: 2025-A 4.3 had `-std=c++23` with no `-fmodules-ts` on the compile lines, and an extra block that creates util.dll, which the question did not ask for. Compiled on g++ 13.3: without `-fmodules-ts`, `'module' does not name a type`. The lecturer's own build.bat uses `g++ -std=c++20 -fmodules-ts -c ...` for every module. The user's g++ 15.2 was not tested.
   - Status: open for `-fmodules-ts` on every compile line. Closed for -L., -l and -shared (see section 2).

4. Dynamic array and random reals (2025-C 4.3)
   - First seen S12. double* arr[10] is ten pointers; the dynamic array is new double[10]. rand() % 100 gives whole numbers; use rand() / (double)RAND_MAX * 100 and srand(time(0)) once. A function cannot be defined inside main. Evidence: compiled, S7 amendments.
   - Status: open. Not retested cold.

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
Trailing const meaning                    | First seen S12 (quiz Q5: chose "the returned element cannot be
                                          | changed", which is the const at the FRONT). S13 (1 Nov): stated in
                                          | his own words that the trailing const protects the left object and
                                          | the const in the brackets protects the right object. Compiled errors
                                          | for each position: trailing and parameter give "assignment of member
                                          | 'Box::_v' in read-only object"; a front const return gives "passing
                                          | 'const Box' as 'this' argument discards qualifiers". The front const
                                          | only matters when the return type has & (a returned reference is the
                                          | real object; a copy cannot be damaged). a = b = c still works.
char versus string quotes                 | First seen S12 ('?' is a char, "?" is a string; comparing a char to a
                                          | string does not compile). S13: '?' used correctly in the 2025-A 3.3
                                          | and Q4 answers (!= '?', == '?').
Member vs friend by the left operand      | S12 misses are recorded in the S6 log, item "Member vs friend", which
                                          | was closed in S13 (4 of 4 on the retest).
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Three different names that look alike: the module name, the interface file name and the DLL file name. Const has three positions: front (returned value), brackets (right operand), end (the left object).

## 4. PATTERNS ACROSS SESSIONS
Recognition versus production (S7, S12): see the S7 log, item 2.
Right idea, wrong detail in command syntax (S12, S13): hyphens, dots, names, one missing flag. These are copying slips and rule slips, so practise from a blank page.

## 5. RETEST FIRST (ranked, from section 1)
1. 2025-C Q4.3: main.cpp with new double[10], srand, rand() / (double)RAND_MAX * 100.
2. The module interface and implementation files for a one function DLL from a blank page: `export module`, `extern "C"`, `module Name;`, the parameter `char arr[]` written the same in both.
3. The implicit batch file with `-fmodules-ts` on every compile line.
4. operator= self check `this != &other`.

---
*CDG v10 | written S12 | restructured S13 (v11) | 2026-11-01*
