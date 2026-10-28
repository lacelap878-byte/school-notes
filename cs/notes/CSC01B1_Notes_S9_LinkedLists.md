---
module: CSC01B1
topic: Linked Lists
session: 9
tags: [definition, worked-example, common-mistake, exam-flagged, struggle, added]
---

# CSC01B1 S9: Linked Lists (Lecture 8)

These notes cover the part of Lecture 8 that was taught in drill format, plus the exam-style version of the same code. Slide code is quoted as printed (slide numbers are the printed ones). Anything beyond the slides is marked (added). The slides use `nodeType`, `info`, `link` and `NULL`. The exam papers use a templated `Node<T>` with `data`, `next` and `nullptr`. Learn the exam style, recognise the slide style. #exam-flagged

**Partial coverage, said plainly:** slides 29 to 50 (the linkedListType class, iterators, destroy, copy, the big three), 51 to 71 (unordered and ordered lists), 72 (print in reverse), 74 to 85 (doubly linked) and 87 to 88 (circular) were NOT taught in the drill. Amended S11: slides 42 to 61 and 71 have since been read as images and are summarised below (the earlier note that several of these were code slides that did not read cleanly was wrong; they contain no code). Slides 29 to 41, 62 to 70, 72 and 74 to 88 have not yet been re-checked. Doubly linked and circular lists appear only in the 2018 and 2019 papers, not in 2021 to 2025.

## What a linked list is
A linked list is a collection of nodes. Each node holds data and a pointer to the next node. The last node points to nothing. #definition

`head` is a separate pointer variable that holds the address of the first node. It is not inside any node. If you lose `head`, you lose the whole list. (added) Think of head as the address on the front door of the first house, and each house has a note with the next address.

## The node (slide 8)
```cpp
struct nodeType
{
    int info;
    nodeType *link;
};
nodeType *head;
```

Templated node (slide 33):
```cpp
template <class Type>
struct nodeType
{
    Type info;
    nodeType<Type> *link;
};
```

(added) Exam style, the one you write in the paper:
```cpp
template <typename T>
struct Node { T data; Node<T> *next; };

Node<string> *head = nullptr;
```

- `<>` after the name fills in the type for the template, so `Node<string>` is a node holding a string.
- `Node<T> *next` inside the struct: the node points to another node of the same kind.
- ⚠️ `head` is NEVER declared inside the node.
- ⚠️ `Node<string> *head;` on its own is garbage, not empty. Empty is `= nullptr`. #common-mistake

<span style="color:#e8590c">Open: the "empty list is nullptr, not garbage" point was only discussed, never produced under test.</span>

## Pointers copy addresses, not nodes
(added) `current = head;` copies the address. There is still one list. `current` is like a mailman: he carries an address and visits the houses, the houses do not move. You never need the names of the nodes, because every node is reached through the `next` of the one before it.

Never walk with `head` itself. If you move `head`, the front of the list is lost. Copy it into `current` and walk with that.

### Pointer or node (added, Amended S11)
This is the point that caused the most argument in the S11 drill, so it is stated plainly. #struggle
- A node is the whole struct: `data` plus a pointer `next`. It is created with `new`.
- A pointer is a variable that holds an address. `head`, `current`, `previous`, `newNode` and every node's `next` are pointers. Test: the declaration has a `*`.
- Having a pointer inside a node does not make the node a pointer, in the same way a business card that holds an address is not itself an address.
- `Node<string> *head = n1;` creates no node. Only a line with `new` (or a declared `Node<string> x;`) makes a node. With five `new`s there are five nodes, however many pointers point at them.
- `delete current;` destroys the node that `current` points at. The variable `current` stays, still holding the old address, which is why we write `current = nullptr;` or fix the node before it.
- Every pointer that held the freed node's address needs fixing separately (`head` for the first node, the earlier node's `next` for a later one).
- A node cannot hold a real node of its own type inside itself. g++ gives `field 'next' has incomplete type 'Node'`, because the size would be infinite. A pointer has a fixed size, and can also be `nullptr` to end the list.
- Value nodes (`Node<string> n1, n2;`) work only for a fixed, known number of items; they disappear at the closing brace and cannot be deleted from the middle. The list uses `new` because its size changes while the program runs.
- Working model that gives correct code: a pointer behaves like the node it points at, except in three places: `delete` (the node dies, the pointer stays), assignment of pointers (`a = b` copies the address, not the node), and `head = nullptr` (changes only the pointer).

<span style="color:#f08c00">Open: node versus pointer. The user's own picture treated `head` as a node. The practical model above gives correct code, but the distinction has not been accepted yet.</span>

## Traversal (slides 13 and 14)
```cpp
current = head;
while (current != NULL)
{
    //Process the current node
    current = current->link;
}
```
(the slide example prints `current->info << " "`)

(added) Exam style, counting:
```cpp
int count = 0;
Node<string> *current = head;
while (current != nullptr)
{
    if (current->data == "S6") count++;
    current = current->next;
}
cout << count << endl;
```

Skeleton: set `current = head`, loop while `current != nullptr`, process, step with `current = current->next`. Declare `current` ONCE. #worked-example

<span style="color:#e8590c">Open: counting skeleton in production. In the timed drill current was declared twice and a peek-ahead loop was used that never moved forward.</span>

## Which loop test stops where
(added) This is the most useful table in the topic. Say it out loud with a three node list A to B to C.

- `current != nullptr`: walks off the end. current is nullptr when it stops. Use for count, print, search, delete whole list.
- `current->next != nullptr`: stops ON the last node (C). Use for insert at end.
- `current->next->next != nullptr`: stops one BEFORE the last node (B). Use for delete last.
- `next->next` is two separate hops: first `current->next`, then `->next` of that. `current` itself still moves ONE node per pass.
- Insert after X stops ON X: `current != nullptr && current->data != "X"`.
- Delete X stops BEFORE X: `current->next->data != "X"`.

⚠️ Stop ON the node to insert after it. Stop BEFORE the node to delete it. Mixing these two is the most repeated slip. #common-mistake #struggle

<span style="color:#e8590c">Open: delete last stop position (in the session quiz the answer chosen was B, correct is C: the loop is `while (current->next->next != nullptr)`).</span>

## Insertion (slides 15 to 19)
Slide 16, insert after the node p points to:
```cpp
newNode = new nodeType;
newNode->info = 50;
newNode->link = p->link;
p->link = newNode;
```
Slide 18, with two pointers (p and q, q is the node after p):
```cpp
newNode->link = q;
p->link = newNode;
```

Order matters: the new node grabs what comes after it FIRST, then the earlier node is re-pointed. Reverse the two lines and the new node points at itself and the rest of the list is lost. #common-mistake

(added) Exam style, insert at start:
```cpp
Node<string> *newNode = new Node<string>;
newNode->data = "N0";
newNode->next = head;
head = newNode;
```
Line 3 says where to look after the new node. Line 4 makes head know the address of the new node. `head` is the one pointer variable outside the nodes, so overwriting it is how the new node becomes first.

(added) Insert at end:
```cpp
newNode->next = nullptr;
if (head == nullptr) { head = newNode; }
else {
    Node<string> *current = head;
    while (current->next != nullptr) current = current->next;
    current->next = newNode;
}
```
The empty list case comes first because `head->next` on nullptr crashes. ⚠️ Do not forget `newNode->next = nullptr;`. Garbage in `next` makes the traversal run off into nonsense.

(added) Insert after "T3":
```cpp
Node<string> *current = head;
while (current != nullptr && current->data != "T3") current = current->next;
if (current != nullptr) {
    newNode->next = current->next;
    current->next = newNode;
}
```

<span style="color:#e8590c">Open: insert after in production (stop ON the node; link order). In the drill the loop stopped before the node and the two linking lines were reversed.</span>
<span style="color:#e8590c">Open: variable name copied wrongly (NewNode vs newNode). It happened twice. C++ is case sensitive, so copy the name exactly.</span>
<span style="color:#e8590c">Open: missing `newNode->next = nullptr;` in insert at end.</span>

(added) Insert BEFORE a node and search are in the exam papers (insert before: 2025-C Q2.6, search: 2022-B Q2.6) but were never practised. See the frequency table below.

## Deletion (slides 20 to 22)
Slide 20, bypass the node:
```cpp
p->link = p->link->link;
```
Slide 21, the version that frees memory:
```cpp
q = p->link;
p->link = q->link;
delete q;
```
Pattern: save the node in `temp`, move or bypass, THEN delete. If you delete first you lose the address.

(added) Delete first:
```cpp
if (head != nullptr) {
    Node<string> *temp = head;
    head = head->next;
    delete temp;
}
```

(added) Delete last. One node and empty cases first:
```cpp
if (head == nullptr) return;
else if (head->next == nullptr) { delete head; head = nullptr; }
else {
    Node<string> *current = head;
    while (current->next->next != nullptr) current = current->next;
    Node<string> *toDelete = current->next;
    current->next = nullptr;
    delete toDelete;
}
```
Why two ahead: to unlink the last node you need the node BEFORE it, because that node's `next` must become nullptr. A singly linked list cannot go backwards.

(added) Delete a specific node "T3":
```cpp
if (head == nullptr) return;
if (head->data == "T3") { Node<string> *temp = head; head = head->next; delete temp; }
else {
    Node<string> *current = head;
    while (current->next != nullptr && current->next->data != "T3") current = current->next;
    if (current->next != nullptr) {
        Node<string> *temp = current->next;
        current->next = temp->next;
        delete temp;
    }
}
```
The first node is a special case, because no node comes before it.

(added, Amended S11) Delete last, the lecture's way: two pointers, `current` on the node to delete and a trailing pointer on the node before it. Slide 58 says: "update link field of the previous node to NULL". Slide 71 (the ordered list version) names the trailing pointer `trailCurrent`. The slides give this in words and pictures, not code. Compiled and run on lists of 0 to 5 nodes with no leaks:
```cpp
if (head == nullptr) return;
else if (head->next == nullptr) { delete head; head = nullptr; }
else {
    Node<string> *previous = nullptr;
    Node<string> *current = head;
    while (current->next != nullptr)
    {
        previous = current;
        current = current->next;
    }
    previous->next = nullptr;
    delete current;
}
```
`previous->next` and `current` hold the same address. Cut the earlier node loose first, then free the node. Setting `current = nullptr` instead would not fix `previous->next`, which would still hold the freed address. This does the same job as the `next->next` version above; use whichever you can hold in your head.

(added) Delete the whole list:
```cpp
Node<string> *current = head;
while (current != nullptr)
{
    Node<string> *temp = current;
    current = current->next;
    delete temp;
}
head = nullptr;
```
Save, move on, then delete. ⚠️ `head = nullptr;` at the end, or head points at freed memory.

<span style="color:#e8590c">Open: delete a specific node (temp, bypass lines, first-node case). In the drill `next->next` was written where `next->data` was needed and the first-node case was missing.</span>

## Resolved (weakest evidence)
- Node struct with no head inside: correct in two later retests.
- Delete first: correct once under production, and once in the quiz.
- Delete whole list: correct under production.
- Copying addresses and where head lives: discussion only.

## The class version (slides 30 to 41), not taught in drill
Slide 34, the data members of the list class:
```cpp
protected:
    int count;
    nodeType<Type> *first;
    nodeType<Type> *last;
```
Slide 41, the default constructor:
```cpp
first = NULL;
last = NULL;
count = 0;
```
Here `first` is what the drill called head, and `last` is a tail pointer so adding at the end needs no walk. The slides continue with iterators (36 to 39), the list operations (41 to 50), unordered lists (51 to 61) and ordered lists (62 to 71).

Amended S11: slides 41 to 50 read as images. They are words only, no code (source, slides as numbered):
- 41 default constructor: initialises the list to the empty state.
- 42 destroyList: traverses the list deallocating each node, then sets `first` and `last` to NULL and `count` to 0.
- 43 initializeList: reinitialises an existing list to empty (the constructor already did this once).
- 44 print: prints the data in each node, traversing with another pointer.
- 45 length: returns the node count, using the `count` variable.
- 46 front and back: return the info in the first or last node; the program terminates if the list is empty.
- 47 begin and end: iterators; `end` is one past the last node.
- 48 copyList: create a node called newNode, copy the info into it, insert newNode at the end of the list being created.
- 49 the destructor calls destroyList; the copy constructor calls copyList.
- 50 the overloaded assignment operator is similar to the copy constructor.

## Unordered list operations (slides 51 to 61)
(Amended S11, read as images. Words and diagrams, no code. Not taught in the drill.)
- 51 and 52: the class unorderedLinkedList is derived from the abstract class linkedListType. It implements search, insertFirst, insertLast and deleteNode (UML diagram on slide 52: `+search(const Type&) const: bool`, `+insertFirst(const Type&): void`, `+insertLast(const Type&): void`, `+deleteNode(const Type&): void`, with an inheritance arrow to linkedListType).
- 53 search: compare the search item with the current node; if its info is the same, stop; otherwise make the next node the current node; repeat until found or no data is left.
- 54 insertFirst: create a new node, store the new item in it, insert it before `first`, increment `count`.
- 55 insertLast: inserts a new node after `last`, similar to insertFirst.
- 56 to 61 deleteNode, the cases: case 1 the list is empty (output an error message); case 2 the node to delete is the first (adjust `first` and `count`; if there are no other nodes set `first` and `last` to NULL); case 3 the node is not the first: 3a not the last (update the link field of the previous node), 3b the last node (update the link field of the previous node to NULL and update `last` to point to the previous node); case 4 the node is not in the list (no adjustment, output an error message). Slides 57 to 60 are diagrams of a list 28, 17, 37, 24, 54 before and after deleting 28, 37 and 54.
The "previous node" in cases 3a and 3b is the trailing pointer described under Deletion. The exam list has only `head`, so there is no `last` to update.


## Doubly linked and circular (slides 74 to 88), not taught
A doubly linked node has two pointers, and the lecture calls the backward one `back`, not `prev`. A circular list has the last node pointing at the first. Read slides 74 to 88 once if time allows. They are not in the 2021 to 2025 papers.

## Exam frequency (verified, 2021 to 2025, Q2.4 to Q2.6)
Q2 is worth 30 and holds the linked list part (templated node 5, then two operations of 5 each). Operations seen:
- Count or traverse and print.
- Insert at start, insert at end, insert after a value.
- Insert BEFORE a value (2025-C Q2.6).
- Search (2022-B Q2.6).
- Delete first, delete last, delete a specific node, delete the whole list.
Insert before and search are the two never practised.

## Lecture recap
- A linked list is nodes joined by pointers, with head holding the first address.
- Traverse with a copy of head, never head itself.
- Insert: new node grabs the next first, then re-point the earlier node.
- Delete: save in temp, bypass, then delete.
- Slide style `nodeType/info/link/NULL` is the same thing as exam style `Node<T>/data/next/nullptr`.

## Do not forget
- ⚠️ Stop ON the node to insert after it, stop BEFORE the node to delete it.
- ⚠️ Link order on insert: `newNode->next = ...` first, then the earlier node.
- ⚠️ `newNode->next = nullptr;` on insert at end, and handle the empty list.
- ⚠️ Copy variable names exactly (case sensitive).
- ⚠️ Declare `current` once, and set it to `head` before the loop.
- Empty list is `= nullptr`, never garbage.
- Delete last: handle empty and one node first.
- Delete everything: temp, move, delete, then head = nullptr.
- Practise insert BEFORE and search.

## See also
- [[CSC01B1_Notes_S10_StacksAndQueues]]
- [[CSC01B1_Notes_S6_OperatorOverloadingTemplates]]

## Amendments
S11: corrected the claim that slides 42 to 50 and 54 to 55 were code slides that did not read cleanly. They contain no code. Added summaries of slides 41 to 61 and 71, the lecture's previous-node method for delete last (compiled and run), and the Pointer or node section after the user's questions in the S11 drill.
