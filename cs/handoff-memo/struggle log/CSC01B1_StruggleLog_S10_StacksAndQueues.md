Per session struggle log, restructured in S13 (1 Nov 2026). It holds only the items first seen in S10. Later evidence is added to each item as a Status line. The cumulative retest list is in the S13 log.

## 1. OPEN ITEMS (unresolved, oldest first)
None open. The one S10 item has been closed on the evidence below, but it is weak, so it is listed first in section 2.

## 2. RESOLVED (with the session that resolved it)
```
concept                                   | how it was closed
------------------------------------------|--------------------------------------------------------------
Stack versus queue from the rule          | First seen S10: over-brought real-world detail (printers)
                                          | instead of answering by LIFO or FIFO.
                                          | S13 evidence: 2025-A 1.9 correct (shuttle in arrival order is a
                                          | queue, Undo is a stack). Stack trace of push 5, 8, 2, pop, push 9,
                                          | pop, pop correct. Queue trace: the first attempt removed the
                                          | NEWEST item at every delete (stack behaviour), the second attempt
                                          | (add 4, add 7, delete, add 1, delete, delete) was correct: out 4,
                                          | 7, 1 and empty (NULL). The rule that fixed it: at each delete
                                          | ask who has been in the line the longest.
                                          | A leaderboard ranked by smallest time is neither a stack nor a
                                          | queue (ordered by value, not by arrival).
```
Weak evidence: the queue trace was right only on the second try, and the scenario question has been answered once on paper. Keep it on the light retest list.

## 3. NOTATION AND TERMINOLOGY STILL CAUSING TROUBLE
Lecture names: addQueue and deleteQueue (not enqueue and dequeue); top reads, pop removes. queueRear is a second pointer held by the queue, not a back pointer inside the nodes (see the S13 log).

## 4. PATTERNS ACROSS SESSIONS
Answer from the rule, not from a real-world story (S10). It held on 1 Nov for the written scenario questions.

## 5. RETEST FIRST (ranked, from section 1)
Nothing open. Light check: a queue trace of six operations with the oldest-leaves rule, and the two linked list snippets (push and pop on stackTop; addQueue and deleteQueue on queueFront and queueRear).

---
*CDG version not recorded | written S10 (items moved here in S13) | amended S13 (v11) | 2026-11-01*
