---
module: CSC01B1
topic: Stacks and Queues
session: 10
tags: [definition, worked-example, common-mistake, exam-flagged, struggle, added]
---

# CSC01B1 S10: Stacks and Queues (Lecture 9)

Lecture 9 has 108 slides. The part taught was the idea of each structure and the linked list versions. Slide code is quoted as printed, with printed slide numbers. Anything beyond the slides is marked (added). #exam-flagged

**Partial coverage, said plainly:** array stacks (slides 11 to 29, enrichment), postfix evaluation (46 to 58), printing a list backward with a stack (59 to 65), array queues (69 to 89) and the queue simulation (97 to 105) were NOT taught. Slides 31 to 45 (linked stack) and 90 to 96 (linked queue) were covered by idea and by the exam-style code below.

## Stack (slides 5 to 9)
A stack is a structure where items are added and removed at one end only, the top. The last item in is the first item out: LIFO. #definition

Operations named in the lecture: `initializeStack`, `isEmptyStack`, `isFullStack`, `push`, `top`, `pop`.
- `push` adds an item at the top.
- `top` reads the top item without removing it.
- `pop` removes the top item.

(added) Real examples: the browser back button (the last page you visited is the first you go back to), undo, a stack of plates.

## Queue (slides 67 to 68)
A queue adds items at the rear and removes them from the front. The first item in is the first item out: FIFO. #definition

Operations named in the lecture: `addQueue`, `deleteQueue`, `front`, `back`, plus the same kind of initialize and is-empty checks.

⚠️ The lecture says `addQueue` and `deleteQueue`. Many books say `enqueue` and `dequeue`. They mean the same thing. Use the lecture names, mention the others if unsure which the paper wants.

(added) Real examples: a printer job line, a ticket line. Answer the exam question with the general rule (who leaves first), not with real-world exceptions. Overthinking the printer ("it depends on the printer") cost time in the drill.

<span style="color:#e8590c">Open: stack versus queue decided by the rule (LIFO or FIFO), not by trying to imagine every real-world exception.</span>

## Stack versus queue, side by side
- Stack: one end (top), LIFO, push and pop at the same end.
- Queue: two ends (rear to add, front to remove), FIFO.
These come up in Q1 (stack versus queue) in 2025-B Q1.8, 2025-C Q1.9 and 2024-C Q1.9.

## The linked stack (slides 31 to 45)
A linked stack keeps one pointer, `stackTop`, to the first node. Slide 33, the constructor:
```cpp
template <class Type>
linkedStackType<Type>::linkedStackType()
{
    stackTop = NULL;
}
```
Slide 38, `top`:
```cpp
template <class Type>
Type linkedStackType<Type>::top() const
{
    assert(stackTop != NULL);
    return stackTop->info;
}
```
Slide 43, the overloaded assignment operator:
```cpp
if (this != &otherStack)
    copyStack(otherStack);
return *this;
```
(`this != &otherStack` stops a stack being copied onto itself.)

(added) In terms of the S9 list code:
- `push` is insert at start (new node's next = head, head = new node).
- `pop` is delete first (save in temp, head = head->next, delete temp).
- `top` is `head->data`.
Both fast operations happen at the front, so no walking is needed.

<span style="color:#e8590c">Open: this stack is linked list code with different names. If push and pop cannot be written from a blank page, go back to insert at start and delete first in the S9 notes.</span>

## The linked queue (slides 90 to 96)
(added) A queue on a linked list adds at the REAR and deletes from the FRONT. Add at rear is insert at end, delete from front is delete first. A second pointer to the last node (a tail pointer, `last`) avoids walking the whole list to add. Slides 90 to 96 carry the real code. Code for those slides was not captured in the notes.

## Recursion link (added)
Recursion uses the call stack: each call is pushed, and each return pops. This is why a stack can print a list backward (slides 59 to 65, not taught).

## Lecture recap
- Stack: LIFO, push, top, pop, all at the top.
- Queue: FIFO, add at rear, delete from front.
- A linked stack and a linked queue are linked lists restricted to certain operations.
- A tail pointer makes queue insertion fast.
- Array versions exist (slides 11 to 29 and 69 to 89), enrichment, not taught.

## Do not forget
- ⚠️ LIFO is stack, FIFO is queue.
- ⚠️ Lecture names: addQueue and deleteQueue (not enqueue and dequeue).
- ⚠️ top reads, pop removes.
- Stack on a linked list: push is insert at start, pop is delete first.
- Queue on a linked list: add at rear, delete from front, tail pointer avoids walking.
- Answer stack versus queue questions from the rule, not from a real-world detail.

## See also
- [[CSC01B1_Notes_S9_LinkedLists]]
- [[CSC01B1_Notes_S11_ComplexityAnalysis]]
