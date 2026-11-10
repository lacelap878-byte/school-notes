Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S9. Later evidence is added to each item as a Status line. The cumulative retest list is in the S13 log.

## 1. OPEN ITEMS (unresolved, oldest first)

1. Delete a specific node
   - First seen S9. Could not use temp at first. Later wrote next->next where next->data was needed and missed the first node case.
   - S13 drill, three tries (31 Oct). Try 1: the first node block was `delete head; head = nullptr;`, which throws away the rest of the list; `current` was never set; there was no not found check; `last` and `count` were not touched. Try 3 (own previous and current style): the first node test was `head->next == nullptr`, which asks whether there is ONE node, not whether the first node holds the value; `previous` and `current` were never set before the loop; `last` and `count` were not updated. A corrected version was compiled with address and undefined checks and printed the expected 7 test lines. Try 4 was declined.
   - Status: open.

2. Delete last, stop position
   - First seen S9. Quiz answered B, correct is C. The loop stops one BEFORE the last node, to unlink it.
   - Status: open. In S13 the previous and current version (`if (current == last) last = previous;`) was shown and compiled, but the user did not rewrite it.

3. Variable name case
   - First seen S9. Typed NewNode in one line and newNode in another, twice.
   - S13 evidence: `Watercheck` for `WaterCheck`, `rec.day` for `rec.Day`, `Tap[i]` for `rec.Tap[i]`, and `strFilename` against `strFileName`. g++ reports `'Watercheck' was not declared in this scope` (compiled).
   - Status: open, recurring in every file handling and list answer.

4. Insert BEFORE and search
   - First seen S9. Never practised. Both appear in past papers (2025-C Q2.6 and 2022-B Q2.6).
   - S13: the singly linked `insertBefore` drill (with the first node, empty and not found cases) was set and not attempted. The circular version (2025-C 2.6, insert "S5" before the first "S6") was correct on the user's page (traced; run in his peek ahead style: S1 S2 S3 S4 S5 S5 S6). `search` has never been practised.
   - Status: open for the singly insertBefore and for search. The circular case is right.

5. Delete the whole list (regressed)
   - First seen S9, marked resolved then. In S13 (2025-B 2.6) the loop was right (current, temp, delete) but `_head = nullptr;` and `_tail = nullptr;` were left out. Run: both pointers stayed non-null (compiled).
   - Status: open again.

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
Insert after a node (stop ON, link order) | S13: 2025-A 2.6 correct, 5 of 5. Loop stops ON "T3" with
                                          | while (current != nullptr && current->data != "T3"), then
                                          | newNode->next = current->next first, current->next = newNode second.
Missing newNode->next = nullptr           | S13: present in the doubly linked back insert attempt.
Counting skeleton in production           | S13: 2025-C 2.5 counting logic correct (current = _head, if data
                                          | == "S6" then count++, move on). The circular end test is a
                                          | separate item in the S13 log.
Node struct with head inside              | S9 retests, then S13: the templated node struct was correct in
                                          | 2025-A, B and C 2.4 (B with the extra back pointer).
Delete first                              | S9 production and quiz, then S13: 2025-A 2.5 correct (temp, move
                                          | _head, delete temp). Add _tail = nullptr when the list becomes empty.
```
Copying addresses and where head lives was only discussed in S9 (weakest evidence). On 1 Nov the same confusion came back; the working model agreed was "head is a label on a box": `_head->x` follows the label to the node, `_head = y` moves the label. Not retested. See the S13 log.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Linked lists: `->` chains such as `current->next->next`, and `Node<string> *`. Slide names (nodeType, info, link, NULL) differ from exam names (Node<T>, data, next, nullptr, and in 2025 the pointers `_head` and `_tail`). User preference (1 Nov): previous and current, not peek ahead `current->next` and not `trailCurrent`.

## 4. PATTERNS ACROSS SESSIONS
Mixing similar patterns (S9): stop ON versus stop BEFORE, delete all versus delete specific.
Small copying slips (S9, again S13): variable names, case, missing lines.
Recognition versus production: see the S7 and S13 logs.

## 5. RETEST FIRST (ranked, from section 1)
1. Delete a specific node from a blank page with previous and current (first node case, not found, last and count).
2. Delete the whole list, ending with `_head = nullptr; _tail = nullptr;`.
3. Insert BEFORE a value in a singly linked list, and search.
4. Delete last, stopping one BEFORE the last node.

---
*CDG version not recorded | written S9 (items moved here in S13) | amended S13 (v11) | 2026-11-01*
