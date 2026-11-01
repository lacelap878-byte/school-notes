Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S11. Later evidence is added to each item as a Status line. The cumulative retest list is in the S13 log.

## 1. OPEN ITEMS (unresolved, oldest first)

1. Nested loop combining
   - First seen S11. Multiplied a term that should be added. The outer loop's overhead is added once per outer pass.
   - Status: open. Not retested in S13 (the 2025-A 3.5 code has two loops one after the other, not nested). The lecturer's slides print two arithmetic slips in the nested examples, see the S11 notes.

2. Delete last in drill (28 Oct)
   - First seen S11. Loop current->next != nullptr then delete current; delete temp, so previous->next dangles. The loop must stop one BEFORE the last node, or use a trailing pointer. Persisting 2.
   - Status: open. See also the S9 log, item 2.

3. Node versus pointer, what head is
   - First seen S11. Argued that head is a node and that every node is a pointer. Not accepted. Working model then: a pointer behaves like the node it points at, except for delete, a = b (copies the address) and head = nullptr.
   - S13 (1 Nov): the same confusion returned ("head can be two things at once"). Working model agreed: head is a label on a box. `_head->x` reaches into the box the label is on; `_head = y` moves the label; `current = _head` puts a second label on the same box; `nullptr` is a label on no box. Do not argue definitions; trace code by hand and draw the label.
   - Status: open (model agreed, not retested).

4. Second-guessing a correct line
   - First seen S11. Crossed out a correct one-node case and replaced it with wrong code (delete head->next). Check against the rule before crossing out.
   - Status: open. Not observed again in S13, not retested.

5. Syntax slips in the 28 Oct drills
   - First seen S11. `int count == 0;`, `Node *<string>;`, `head = nullptr` without braces after an else, a counting loop with a data stop condition and the if outside, capital Template.
   - S13: new slips of the same kind: `Watercheck` for `WaterCheck`, `rec.day` for `rec.Day`, a bare `Tap[i]`, `this != other` for `this != &other`, `<` for `<=` in "not positive". See the S13 log.
   - Status: open, recurring.

6. Writing code from a hard to follow explanation
   - First seen S11. Could not memorise the peek two ahead delete last because it was not understood. The lecture previous pointer version (slides 58 and 71) works better for the user.
   - S13: the user chose previous and current for every list answer and rejected the peek ahead style and the `trailCurrent` name.
   - Status: open until delete is written correctly from a blank page (S9 item 1).

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
Three assumptions                         | First seen S11 (the third, N is the problem size, was a gut
                                          | feeling). S13: written correctly in his own words in 2025-A 3.5,
                                          | both attempts: the operations take the same time, the number of
                                          | operations is a fair measure of time, N is the problem size.
Copying addresses and where head lives    | S11 discussion only (weakest evidence); see item 3.
```

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Pointer versus node (item 3): do not argue definitions. Use the label on a box picture.

## 4. PATTERNS ACROSS SESSIONS
Time management (ST1): the UML wasted 45 minutes. Plan a 6 minute cap, a time budget at the top of the paper, and skip and return.
Second-guessing and small copying slips (S9, S11, S13): re-read the code once at the end.

## 5. RETEST FIRST (ranked, from section 1)
1. Delete last, stopping one BEFORE the last node.
2. Nested loop: derive T(N) for a nested loop and give the Big-O.
3. Draw the label picture for `_head = newNode;` and `current = _head;`.
4. Re-read every answer once for case and boundary slips.

---
*CDG version not recorded | written S11 (S6, S7, S9 and S10 items moved to their own logs in S13) | amended S13 (v11) | 2026-11-01*
