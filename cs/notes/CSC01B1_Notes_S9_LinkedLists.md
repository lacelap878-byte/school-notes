---
module: CSC01B1
topic: Linked Lists
session: 9
tags: [definition, worked-example, common-mistake, exam-flagged, struggle, added]
---

# CSC01B1 S9: Linked Lists (Lecture 8)

These notes cover the part of Lecture 8 that was taught in drill format, plus the exam-style version of the same code. Slide code is quoted as printed (slide numbers are the printed ones). Anything beyond the slides is marked (added). The slides use `nodeType`, `info`, `link` and `NULL`. The exam papers use a templated `Node<T>` with `data`, `next` and `nullptr`. Learn the exam style, recognise the slide style. #exam-flagged

**Partial coverage, said plainly:** slides 29 to 50 (the linkedListType class, iterators, destroy, copy, the big three), 51 to 71 (unordered and ordered lists), 72 (print in reverse), 74 to 85 (doubly linked) and 87 to 88 (circular) were NOT taught in the drill. Amended S11: slides 42 to 61 and 71 have since been read as images and are summarised below (the earlier note that several of these were code slides that did not read cleanly was wrong; they contain no code). Slides 23 to 40, 62 to 70, 72 and 74 to 92 have since been read as images too (Amended S11, 28 Oct) and are written below as presented. Doubly linked and circular lists appear only in the 2018 and 2019 papers, not in 2021 to 2025.

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
(Amended S11: the slide by slide detail is in the sections "Doubly linked lists, slide by slide" and "Circular linked lists" below.)

A doubly linked node has two pointers, and the lecture calls the backward one `back`, not `prev`. A circular list has the last node pointing at the first. Read slides 74 to 88 once if time allows. They are not in the 2021 to 2025 papers.

## Exam frequency (verified, 2021 to 2025, Q2.4 to Q2.6)
Q2 is worth 30 and holds the linked list part (templated node 5, then two operations of 5 each). Operations seen:
- Count or traverse and print.
- Insert at start, insert at end, insert after a value.
- Insert BEFORE a value (2025-C Q2.6).
- Search (2022-B Q2.6).
- Delete first, delete last, delete a specific node, delete the whole list.
Insert before and search are the two never practised.

## Building a linked list forward and backward (slides 23 to 28, Amended S11)
- Slide 23: if the data is unsorted, the list will be unsorted. A list can be built forward or backward. Forward: a new node is always inserted at the END of the list. Backward: a new node is always inserted at the BEGINNING.
- Slide 24: three pointers are needed to build the list forward: one to the first node, which cannot be moved; one to the last node; one to create the new node. Example data: 2, 15, 8, 24, 34.
- Slide 25: figure 16-12 is the empty list (`first` and `last` both NULL). Figure 16-14, after inserting the first `newNode`: `first`, `last` and `newNode` all point at the node holding 2.
- Slide 26: figure 16-15 shows the list and a separate `newNode` holding 15. Figure 16-16, after inserting `newNode` at the end: the node holding 2 links to the node holding 15, and `last` and `newNode` both point at 15.
- Slide 27: repeat the process three more times. Figure 16-17, the list after inserting 8, 24 and 34: 2, 15, 8, 24, 34, with `last` and `newNode` at 34.
- Slide 28: the algorithm to build a list backward: initialise `first` to NULL; for each item in the list, create the new node `newNode`, store the data in `newNode`, insert `newNode` before `first`, and update the value of the pointer `first`.

## The class version, slide by slide (slides 29 to 40, Amended S11)

> N.B. Low frequency in past papers. The recorded Q2.4 to Q2.6 items (2021 to 2025) are operations on a given node structure (count, insert, delete, search), not the class, the iterators or the UML diagrams. Do not focus too much on this section.

- Slide 30, a linked list as an ADT, the basic operations: initialise the list, determine whether it is empty, print it, find its length, destroy it, retrieve the info in the first or last node, search for a given item, insert an item, delete an item, make a copy.
- Slide 31: there are two general types of linked list, sorted and unsorted. The algorithms for search, insert and remove differ slightly between them. The abstract class `linkedListType` implements the basic operations, with derived classes `unorderedLinkedList` and `orderedLinkedList`.
- Slide 32: for an unordered list a new item can go at either end. `buildListForward` inserts at the end and `buildListBackward` inserts at the beginning. Two functions are needed, `insertFirst` and `insertLast`, and the list uses two pointers, `first` and `last`.
- Slide 33: each node has two member variables, and the node is implemented as a struct. The slide names the members `info` and `link` (our drill code names them `data` and `next`):
```cpp
//Definition of the node

template <class Type>
struct nodeType
{
    Type info;
    nodeType<Type> *link;
};
```
- Slide 34: `linkedListType` has three member variables: two pointers, `first` and `last`, and `count`, the number of nodes in the list:
```cpp
protected:
    int count;       //variable to store the number of
                     //elements in the list
    nodeType<Type> *first; //pointer to the first node
                           //of the list
    nodeType<Type> *last;  //pointer to the last node
                           //of the list
```
- Slide 36, iterators: to process each node the list must be traversed, starting at the first node. An iterator is an object that produces each element of a container, one element at a time. The two most common iterator operations are `++` (increment) and `*` (dereference).
- Slide 37: an iterator is an object, so a class (`linkedListIterator`) is defined to create iterators for objects of `linkedListType`. It has one member variable that refers to the current node.
- Slide 38, figure 16-19, UML of `linkedListIterator<Type>`: private `*current: nodeType<Type>`; public `linkedListIterator()`, `linkedListIterator(nodeType<Type>)`, `operator*(): Type`, `operator++(): linkedListIterator<Type>`, `operator==(const linkedListIterator<Type>&) const: bool`, `operator!=(const linkedListIterator<Type>&) const: bool`.
- Slide 39, figure 16-20, UML of `linkedListType<Type>`: protected `count: int`, `*first: nodeType<Type>`, `*last: nodeType<Type>`; public `operator=`, `initializeList(): void`, `isEmptyList() const: bool`, `print() const: void`, `length() const: int`, `destroyList(): void`, `front() const: Type`, `back() const: Type`, the abstract (in italics, `= 0`) `search(const Type&) const: bool`, `insertFirst(const Type&): void`, `insertLast(const Type&): void`, `deleteNode(const Type&): void`, then `begin()` and `end()` returning `linkedListIterator<Type>`, the constructors `linkedListType()` and `linkedListType(const linkedListType<Type>&)`, `~linkedListType()`, and private `copyList(const linkedListType<Type>&): void`.

## Ordered linked lists (slides 62 to 71, Amended S11)

> N.B. Low frequency in past papers. Do not focus too much on this section.

- Slide 62: `orderedLinkedList` is derived from `linkedListType` and provides the definitions of the abstract functions `insertFirst`, `insertLast`, `search` and `deleteNode`. The elements are assumed to be in ascending order. It adds a function `insert` to put an element in its proper place.
- Slide 63, figure 16-29, UML of `orderedLinkedList<Type>`: `search(const Type&) const: bool`, `insert(const Type&): void`, `insertFirst(const Type&): void`, `insertLast(const Type&): void`, `deleteNode(const Type&): void`; it inherits from `linkedListType`.
- Slide 64, search: compare the search item with the current node. If the info of the current node is greater than or equal to the search item, stop the search. Otherwise make the next node the current node. Repeat until an item greater than or equal to the search item is found, or no data is left.
- Slides 65 to 67, insert cases: case 1, the list is empty, so the new node becomes the first node. Case 2, the list is not empty and the new item is smaller than the smallest item, so the new node goes at the beginning. Case 3, the new item goes somewhere in the list: 3a, it is larger than the largest item, so it goes at the end; 3b, it goes somewhere in the middle.
- Slide 68, figures 16-33 and 16-34: the list 17, 27, 38, 54 (count 4) before inserting 65, then 17, 27, 38, 54, 65 (count 5) after.
- Slide 69, figures 16-35 and 16-36: the list 17, 38, 45, 54 (count 4) before inserting 27, then 17, 27, 38, 45, 54 (count 5) after.
- Slide 70: `insertFirst` and `insertLast` must insert at the proper place so the list stays sorted. They are not actually used, but definitions must be provided because they are declared abstract in the parent class. The slide names `insertNode` as the function used to insert at the proper place (slides 62 and 63 call it `insert`).
- Slide 71, delete: case 1, the list is empty, which is an error. Case 2, the item is the first node, so adjust the head (`first`) pointer. Case 3, the item is somewhere in the list: `current` points at the node with the item to delete and `trailCurrent` points at the node before it. Case 4, the item is not in the list, which is an error.

## Printing a list in reverse with recursion (slide 72, Amended S11)

> N.B. Low frequency in past papers. Do not focus too much on this section.

- The links only go forward, so the list cannot be traversed backward using the links. Recursion can be used. The list is printed only if the pointer to the list is not null. The recursive call is on the tail of the list. When the tail is empty, the recursion stops.
- (added) As code, compiled and run (prints C, B, A for a list A, B, C). The slide has no code:
```cpp
void printReverse(Node<string> *current)
{
    if (current != nullptr)
    {
        printReverse(current->next);    // the tail first
        cout << current->data << endl;  // then this node
    }
}
```

## Doubly linked lists, slide by slide (slides 74 to 85, Amended S11)

> N.B. Low frequency in past papers: doubly linked lists appear only in the 2018 and 2019 papers. Do not focus too much on this section.

- Slide 74: in a doubly linked list every node has `next` and `back` pointers, so it can be traversed in either direction (figure 16-39).
- Slide 75, the operations: initialise or destroy the list, determine whether it is empty, search for a given item, retrieve the first or last element, insert or delete an item, find the length, print, make a copy.
- Slide 76: the default constructor initialises the list to empty, setting `first` and `last` to NULL and `count` to 0. `isEmptyList` returns true if the list is empty, false otherwise.
- Slide 77: `destroy` deletes all the nodes, leaving the list empty, and sets `count` to 0. `initializeList` reinitialises the list to empty, using `destroy`.
- Slide 78: `length` returns the count of nodes. `print` traverses the list and outputs the info in each node. `reversePrint` traverses the list in reverse order using the back links and outputs the info in each node.
- Slide 79: `search` returns true if the item is found, otherwise false. The algorithm is the same as for an ordered linked list.
- Slide 80: `front` returns the first element and `back` the last. If the list is empty, both terminate the program.
- Slide 81, insert, four cases: 1, insertion in an empty list; 2, at the beginning of a nonempty list; 3, at the end of a nonempty list; 4, somewhere in a nonempty list. Cases 1 and 2 require an update to the pointer `first`. Cases 3 and 4 are similar. After inserting, increment `count` by 1.
- Slide 82, figures 16-40 and 16-41: the list 8, 15, 24, 40 (count 4) before inserting 20, then 8, 15, 20, 24, 40 (count 5) after.
- Slide 83, delete: case 1, the list is empty; case 2, the item is the first node, so update the pointer `first`; case 3, the item is somewhere in the list; case 4, the item is not in the list. After deleting a node, `count` is decremented by 1.
- Slide 84, figures 16-42 and 16-43: the list 5, 17, 44, 52 (count 4) before deleting 17. Then the list after adjusting the links of the nodes before and after the node with info 17, with `trailCurrent` at 5 and `current` at 17.
- Slide 85, figure 16-44: the list 5, 44, 52 (count 3) after deleting 17.

## Circular linked lists (slides 87 and 88, Amended S11)

> N.B. Low frequency in past papers: circular lists appear only in the 2018 and 2019 papers. Do not focus too much on this section.

- Slide 87: a circular linked list is a linked list in which the last node points to the first node. Figure 16-45: (a) an empty circular list (`first` is NULL); (b) a circular list with one node (the node points to itself); (c) a circular list with more than one node (the last node points back to the first, and `first` points into the ring).
- Slide 88, the operations: initialise the list (to an empty state), determine if it is empty, destroy it, print it, find its length, search for a given item, insert or delete an item, copy the list.

## Lecture summary slides (slides 90 to 92, Amended S11)
- A linked list is a list of items (nodes). The order of the nodes is determined by the address (link) stored in each node. The pointer to a linked list is called `head` or `first`. A linked list is a dynamic data structure. The list length is the number of nodes.
- Insertion and deletion do not require data movement, only the pointers are adjusted. A (single) linked list is traversed in only one direction. Search of a linked list is sequential. The head pointer is fixed on the first node. To traverse, use a pointer other than head.
- A doubly linked list has two links in every node, next and previous, and can be traversed in either direction. Insertion and deletion require the adjustment of two pointers in a node. A linked list in which the last node points to the first node is a circular linked list.

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
- 28 Oct (Amend S11, second pass): read slides 23 to 40, 62 to 72 and 74 to 92 as images and added them as presented: building a list forward and backward, the class version slide by slide (slides 33, 34 and 36 to 39 add the node struct, data members and UML diagrams), ordered lists, print in reverse with recursion, doubly linked and circular lists, and the summary slides. Added N.B. lines: low frequency, do not focus too much on these. (added) the `printReverse` code (compiled and run).
