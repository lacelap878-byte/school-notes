---
module: CSC01B1
topic: Stacks and Queues
session: 10
tags: [definition, worked-example, common-mistake, exam-flagged, struggle, added]
---

# CSC01B1 S10: Stacks and Queues (Lecture 9)

Lecture 9 has 108 slides. The part taught was the idea of each structure and the linked list versions. Slide code is quoted as printed, with printed slide numbers. Anything beyond the slides is marked (added). #exam-flagged

**Coverage, said plainly (Amended S11, 28 Oct):** array stacks (slides 10 to 29, marked "for enrichment" on the slides), postfix evaluation (46 to 58), printing a list backward with a stack (59 to 65), array queues (69 to 89) and the queue simulation (97 to 105) were NOT taught in a session. Slides 31 to 45 (linked stack) and 90 to 96 (linked queue) were covered by idea and by the exam-style code below. Every slide of Lecture 9 has now been read, text and figures, and is written below as presented. Slides 90 to 96 are words only, with no code.

> N.B. Frequency check. The recorded exam items for this lecture are the short Q1 ones (stack versus queue, 2025-B Q1.8, 2025-C Q1.9, 2024-C Q1.9) and the stack on a linked list (2 marks in Q1). The array versions, postfix, printing a list backward and the queue simulation are not among the recorded items, so do not focus too much on them. Read them once. The linked stack and the stack versus queue rule are the part to know.

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
    assert(stackTop != NULL); //if stack is empty,
                              //terminate the program
    return stackTop->info;    //return the top element
}//end top
```
Slide 43, the overloaded assignment operator:
```cpp
template <class Type>
const linkedStackType<Type>& linkedStackType<Type>::operator=
                      (const linkedStackType<Type>& otherStack)
{
    if (this != &otherStack) //avoid self-copy
        copyStack(otherStack);

    return *this;
}//end operator=
```
(`this != &otherStack` stops a stack being copied onto itself.)

(added) In terms of the S9 list code:
- `push` is insert at start (new node's next = head, head = new node).
- `pop` is delete first (save in temp, head = head->next, delete temp).
- `top` is `head->data`.
Both fast operations happen at the front, so no walking is needed.

<span style="color:#e8590c">Open: this stack is linked list code with different names. If push and pop cannot be written from a blank page, go back to insert at start and delete first in the S9 notes.</span>

## The linked queue (slides 90 to 96)
(added) A queue on a linked list adds at the REAR and deletes from the FRONT. Add at rear is insert at end, delete from front is delete first. A second pointer to the last node (a tail pointer, `last`) avoids walking the whole list to add. Slides 90 to 96 carry words only, no code (see "Linked queue, slide by slide" below).

## Stack slides, the figures (slides 5 to 8, Amended S11)
- Slide 5: a stack is a data structure in which elements are added and removed from one end only. Addition and deletion occur only at the top. LIFO. Push adds an element onto the stack, pop removes one.
- Slide 6, figure 17-1: various types of stacks (coins, trays, boxes, books).
- Slide 7, figure 17-2: an empty stack, with boxes A to E lying beside it.
- Slide 8, figure 17-3, stack operations: (a) push box A, (b) push box B, (c) push box C, (d) peek at the top element (C), (e) push box D, (f) pop stack (D is removed, C is the top again).

## The linked stack, slide by slide (slides 31 to 45, Amended S11)
- Slide 31: an array only allows a fixed number of elements. If the number of elements pushed exceeds the array size the program may terminate. Linked lists organise data dynamically. In a linked stack, `stackTop` is a pointer to the memory address of the top element.
- Slide 32, figure 17-12: (a) an empty stack, `stackTop` is NULL; (b) a nonempty stack, `stackTop` points to C, which points to B, which points to A, which points to NULL.
- Slide 33: the default constructor initialises the stack to empty when a stack object is declared. It sets `stackTop` to NULL (code above).
- Slide 34: in a linked stack `isFullStack` does not apply, because logically the stack is never full. The stack is empty if `stackTop` is NULL.
- Slide 35: `initializeStack` reinitialises the stack to empty. It must deallocate the memory occupied by the current elements, then set `stackTop` to NULL.
- Slides 36 and 37: push. `newNode` is added at the beginning of the linked list pointed to by `stackTop` (figure 17-13 shows C, B, A before the push). Figure 17-14: (a) create `newNode` and store D; (b) put `newNode` on the top of the stack (its link points at C); (c) make `stackTop` point to the top element (D).
- Slide 38: `top` returns the top element (code above).
- Slides 39 and 40: pop. The node pointed to by `stackTop` is removed, and the second element becomes the top (figure 17-15 shows C, B, A before the pop). Figure 17-16: (a) make `temp` point to the top element; (b) make `stackTop` point to the next element; (c) delete `temp`.
- Slide 41: `copyStack` makes an identical copy of a stack. The definition is similar to `copyList` for linked lists.
- Slide 42, the copy constructor and destructor (similar to those for linked lists):
```cpp
    //copy constructor
template <class Type>
linkedStackType<Type>::linkedStackType(
                      const linkedStackType<Type>& otherStack)
{
    stackTop = NULL;
    copyStack(otherStack);
}//end copy constructor

    //destructor
template <class Type>
linkedStackType<Type>::~linkedStackType()
{
    initializeStack();
}//end destructor
```
- Slide 43: the overloaded assignment operator (code above).
- Slide 44: a stack as derived from the class `unorderedLinkedList`. The implementation of push is similar to `insertFirst` for general lists. Other similar functions: `initializeStack` and `initializeList`, `isEmptyList` and `isEmptyStack`. `linkedStackType` can be derived from `linkedListType`, which is an abstract class.
- Slide 45: `unorderedLinkedListType` is derived from `linkedListType` and provides the definitions of its abstract functions. Then derive `linkedStackType` from `unorderedLinkedListType`.
- (added) The slides give push and pop as figures and words only; the code is not on them. The S9 list code in the (added) paragraph above is the way to write it.

## Array stack (slides 10 to 29, for enrichment, Amended S11)

> N.B. The slides mark all of these "for enrichment". Low frequency, do not focus on this section.

- Slide 11: the first element goes in the first array position, the second in the second, and so on. The top of the stack is the index of the last element added. The elements are stored in an array, a random access data structure, but a stack element is accessed only through the top. A variable called `stackTop` tracks the top position.
- Slide 12: the array can be dynamically allocated, so the user can specify its size. `class stackType` implements the functions of the abstract class `stackADT`.
- Slide 13, figure 17-5, UML class diagram of `stackType<Type>`:
  - private: `maxStackSize: int`, `stackTop: int`, `*list: Type`
  - public: `operator=(const stackType<Type>&): const stackType<Type>&`, `initializeStack(): void`, `isEmptyStack() const: bool`, `isFullStack() const: bool`, `push(const Type&): void`, `top() const: Type`, `pop(): void`
  - private: `copyStack(const stackType<Type>&): void`
  - public: `stackType(int = 100)`, `stackType(const stackType<Type>&)`, `~stackType()`
- Slide 14: C++ arrays begin at index 0, so the value of `stackTop` and the array position it indicates are different things. If `stackTop` is 0 the stack is empty; if it is nonzero the stack is not empty. The top element is given by `stackTop - 1`.
- Slide 15, figure 17-6: an example stack with `maxStackSize` 100, `stackTop` 4 and `list` pointing at an array holding A, B, C, D in positions 0 to 3.
- Slide 16, figure 17-7: initialising the stack gives an empty stack, `stackTop` 0, and the array slots become unused stack.
- Slide 17: the stack is empty if `stackTop` = 0 and full if `stackTop` = `maxStackSize`.
- Slides 18 to 20: push stores the new item in the array component indicated by `stackTop`, then increments `stackTop`. Overflow occurs if you try to add a new item to a full stack. Figure 17-9: the stack after pushing y has `stackTop` 5 and holds S, u, n, n, y in positions 0 to 4.
- Slide 21: the `top` operation returns the top element of the stack.
- Slides 22 to 24: to remove an element, decrement `stackTop` by 1. Underflow is trying to remove an item from an empty stack. Figures 17-10 and 17-11: before popping D, `stackTop` is 4 (B, O, L, D); after, `stackTop` is 3. (added) The figure still draws D in slot 3 after the pop: pop only lowers `stackTop`, it does not erase the slot.
- Slide 25: the `copyStack` function copies a stack.
- Slide 26: the constructor sets the stack size to the parameter value (or the default if none is given), sets `stackTop` to 0 and creates the array. The destructor deallocates the array and sets `stackTop` to 0.
- Slide 27: the copy constructor is called when a stack object is passed as a value parameter to a function. It copies the member variables from the actual parameter to the formal parameter.
- Slide 28: the assignment operator must be explicitly overloaded because of the pointer member variables.
- Slide 29: put the class and function definitions (the stack operations) together in a file called `myStack.h`.

## Postfix expressions (slides 46 to 58, Amended S11)

> N.B. Low frequency, not taught. Do not focus too much on this section.

- Slide 46, infix: the usual notation. The operator is written between the operands (a + b). It evaluates left to right, operators have precedence, and parentheses override precedence.
- Slide 47, prefix (Polish): operators are written before the operands, for example `+ a b`. Introduced by the Polish mathematician Jan Lukasiewicz in the early 1920s. Parentheses can be omitted.
- Slide 48, reverse Polish (postfix): operators follow the operands. Proposed by the Australian philosopher and early computer scientist Charles L. Hamblin in the late 1950s. Advantage: the operators appear in the order required for computation. Example: a + b * c becomes `a b c * +`.
- Slide 49, example 17-4, infix to postfix:
  - a + b gives `a b +`
  - a + b * c gives `a b c * +`
  - a * b + c gives `a b * c +`
  - (a + b) * c gives `a b + c *`
  - (a - b) * (c + d) gives `a b - c d + *`
  - (a + b) * (c - d / e) + f gives `a b + c d e / - * f +`
- Slide 50: postfix has important applications. Many compilers first translate arithmetic expressions into postfix and then translate that into machine code. Evaluation algorithm: scan the expression from left to right; when an operator is found, back up to get the operands, perform the operation and continue.
- Slide 51, figure 17-17, evaluating `6 3 + 2 * =`: (a) push 6; (b) push 3; (c) `+`: pop the stack twice, op2 = 3, op1 = 6; (d) op1 + op2 = 9, push 9; (e) push 2; (f) `*`: pop twice, op2 = 2, op1 = 9; (g) op1 * op2 = 18, push 18; (h) `=`: pop the stack and print 18.
- Slide 52, symbols: `+`, `-`, `*` and `/` are operators and need two operands, so pop the stack twice and evaluate; if the stack has fewer than two elements it is an error. If the symbol is `=` the expression ends: pop and print the answer; if the stack has more than one element it is an error. Any other symbol means the expression contains an illegal operator.
- Slide 53: the expressions are assumed to be in the form `#6 #3 + #2 * =`. If the symbol scanned is `#`, the next input is a number. If it is not `#`, it is an operator (which may be illegal) or an equal sign (end of expression). Only `+`, `-`, `*` and `/` are assumed.
- Slide 54, main algorithm pseudocode:
```
Read the first character
while not the end of input data
{
    a. initialize the stack
    b. process the expression
    c. output result
    d. get the next expression
}
```
  Four functions are needed: `evaluateExpression`, `evaluateOpr`, `discardExp` and `printResult`.
- Slide 55: `evaluateExpression` evaluates each postfix expression, and each expression ends with the `=` symbol. The slide shows its header:
```cpp
void evaluateExpression(ifstream& inpF, ofstream& outF,
                        stackType<double>& stack,
                        char& ch, bool& isExpOk)
```
- Slide 56: `evaluateOpr` evaluates an expression. It needs two operands saved in the stack (fewer than two is an error) and also checks for illegal operations.
- Slide 57: `discardExp` is called when an error is discovered in the expression. It reads and writes the input data until the `=`.
- Slide 58: `printResult` prints the result if the postfix expression has no errors, otherwise it outputs an appropriate message. The result of the expression is in the stack and the output is sent to a file.

## Printing a linked list backward with a stack (slides 59 to 65, Amended S11)

> N.B. Low frequency, not taught. Do not focus too much on this section.

- Slide 59: to print a list backward without recursion, first get to the last node. Problem: the links go in only one direction. Solution: save a pointer to each node in a stack (the LIFO principle). The number of nodes is usually not known, so use the linked implementation of a stack.
- The figures on slides 60 to 65 trace a list `first` pointing to 5, 10, 15 and a stack with `stackTop` (the slides call the next pointer `link`; in our code it is `next`):
  - Slide 60, figures 17-18 and 17-19: the list, then the list after `current = first;` executes. `current` points at 5 and the stack is empty.
  - Slide 61, figure 17-20: after `stack.push(current);` and `current = current->link;` the stack holds 5 and `current` points at 10.
  - Slide 62, figure 17-21: the same two statements again. The stack holds 10 on top of 5 and `current` points at 15.
  - Slide 63, figure 17-22: the same two statements again. The stack holds 15, 10, 5 and `current` is NULL.
  - Slide 64, figure 17-23: after `current = stack.top();` and `stack.pop();` `current` points at 15 and the stack holds 10, 5.
  - Slide 65, figures 17-24 and 17-25: the same two statements again, so `current` points at 10 and the stack holds 5, then `current` points at 5 and the stack is empty.
- (added) The slides show the figures only. The loops they stand for: push every node's pointer while `current != nullptr`, then while the stack is not empty set `current` to the top, pop, and print `current->data`.

## Queue slides, the extra detail (slides 67 and 68, Amended S11)
- Slide 67: a queue is a set of elements of the same type. Elements are added at one end (the back or rear) and deleted from the other (the front). FIFO. The middle elements are inaccessible. Example: a waiting line in a bank.
- Slide 68: the queue operations are `initializeQueue`, `isEmptyQueue`, `isFullQueue`, `front`, `back`, `addQueue` and `deleteQueue`. The abstract class `queueADT` defines them.

## Array queue (slides 69 to 89, Amended S11)

> N.B. Low frequency, not taught. Do not focus too much on this section.

- Slide 69: at least four member variables are needed: an array to store the queue elements, `queueFront` and `queueRear` to track the first and last elements, and `maxQueueSize`.
- Slides 70 and 71: to add, advance `queueRear` to the next array position and add the element at the position `queueRear` points to. Figure 17-27: after two more `addQueue` operations the array holds A, B, C in positions 0 to 2, `queueFront` is 0 and `queueRear` is 2.
- Slide 72: to delete, retrieve the element `queueFront` points to, then advance `queueFront` to the next queue element.
- Slides 73 and 74: will this design work? Let A be an add and D a delete, and consider `AAADADADADADADADA...`. This eventually sets `queueRear` to the last array position and gives the impression that the queue is full.
- Slide 75: Solution 1: when the queue overflows at the rear, check `queueFront`. If it shows room at the front, slide all the queue elements toward the first array position. Problem: too slow for large queues. Solution 2: assume the array is circular.
- Slide 76, figure 17-30: a circular queue (a ring of slots).
- Slide 77, figure 17-31: before `addQueue(Queue, 'Z');` `queueFront` is 98 and `queueRear` is 99 (X and Y). After it, Z is in position 0 and `queueRear` is 0.
- Slide 78, deletion case 1, figure 17-32: before `deleteQueue();` `queueFront` and `queueRear` are both 98 (X). After it, `queueFront` is 99 and `queueRear` is 98.
- Slide 79, labelled deletion case 2, figure 17-33 (the caption says "before and after the add operation"): before `addQueue(Queue, 'Z');` `queueFront` is 99 and `queueRear` is 97. After it, Z is in position 98 and `queueRear` is 98.
- Slide 80, the problem: figures 18-32b and 18-33b have identical values of `queueFront` and `queueRear` (99 and 98). Yet 18-32b is an empty queue and 18-33b is a full queue. How do you tell them apart?
- Slide 81, solution 1: keep a count. Increment it when an element is added, decrement it when one is removed, start it at 0. Very useful if the user often needs the number of elements in the queue.
- Slide 82, solution 2: let `queueFront` indicate the index of the array position before the first element, while `queueRear` still indicates the last. The queue is empty if `queueFront == queueRear`. The slot `queueFront` indicates is reserved, and the queue is full if the next available space is that reserved slot.
- Slide 83, figure 17-34: an array with a reserved slot, `queueFront` 1, `queueRear` 97, reserved slot at position 1.
- Slide 84: with the count version, the queue is empty if `count == 0` and full if `count == maxQueueSize`.
- Slide 85: `initializeQueue` makes the queue empty. The first element is added at the first array position, `queueFront` is set to 0, `queueRear` to `maxQueueSize - 1` and `count` to 0.
- Slide 86: `front` returns the first element and `back` returns the last. If the queue is empty the program terminates.
- Slide 87: `addQueue` advances `queueRear` to the next array position, adds the new element at the position `queueRear` indicates, and increments `count` by 1.
- Slide 88: `deleteQueue` decrements `count` by 1 and advances `queueFront` to the next queue element.
- Slide 89: the constructor sets `maxQueueSize` to the user's specification, creates an array of that size (or a default size) and initialises `queueFront` and `queueRear` to indicate an empty queue. The destructor deallocates the array.
- (added) "Advance" in a circular array means wrap round at the end, for example `(index + 1) % maxQueueSize`. The slides show the wrap in figure 17-31 but do not print this formula.

## Linked queue, slide by slide (slides 90 to 96, Amended S11)
- Slide 90: the array version has issues: its size is fixed so only a finite number of elements can be stored, and the array must be treated in a special way together with `queueFront` and `queueRear`. The linked version simplifies many of these issues, and the queue is never full because memory is allocated dynamically.
- Slide 91: elements are added at one end and removed from the other. Only two pointers are needed to maintain the queue: `queueFront` and `queueRear`.
- Slide 92: the queue is empty if `queueFront` is NULL. It is never full unless the system runs out of memory. Note: you must still provide an `isFullQueue` definition, because it is an abstract function in the parent class `queueADT`.
- Slide 93: `initializeQueue` makes the queue empty. It must remove all existing elements, if any, and deallocate the memory they occupy.
- Slide 94: `addQueue` adds a new element to the end of the queue, `front` returns the first element, `back` returns the last, and `deleteQueue` removes the first element.
- Slide 95: the constructor accesses `maxQueueSize`, `queueFront` and `queueRear`. The destructor destroys the queue and deallocates the memory the elements occupy. The copy constructor and overloaded assignment operator are similar to the corresponding functions for the stack.
- Slide 96: a queue derived from `unorderedLinkedListType`. The linked queue is similar to a linked list created in a forward manner: `addQueue` is similar to `insertFirst`, `initializeQueue` is like `initializeList`, `isEmptyQueue` is similar to `isEmptyList`, `deleteQueue` can be implemented as before, `queueFront` is the same as `first` and `queueRear` is the same as `last`.
- (added) Slide 94 says `addQueue` adds at the END of the queue, while slide 96 compares it with `insertFirst`. For an exam answer trust slide 94: add at the rear, delete from the front.

## Queue simulation (slides 97 to 105, Amended S11)

> N.B. Low frequency, not taught. Do not focus too much on this section.

- Slide 97: a simulation is a technique in which one system models the behaviour of another. Computer models are used to study the behaviour of real systems. Queuing systems are computer simulations that use queues as the data structure, with queues of objects waiting to be served.
- Slide 98: the server is the object that provides the service, the customer is the object receiving it, and the transaction time is the service time (the time to serve a customer). The model is a system of a list of servers and a waiting queue holding the customers to be served. The customer at the front of the queue waits for the next available server.
- Slide 99: you need to know the number of servers, the expected arrival time of a customer, the time between arrivals and the number of events affecting the system. Performance depends on how many servers there are, how long it takes to serve a customer and how often a customer arrives.
- Slide 100: if serving takes too long and customers arrive frequently, more servers are needed. The system can be modelled as a time-driven simulation, where the clock is a counter and one unit of time passing is the counter incrementing by 1. The simulation is run for a fixed amount of time.
- Slide 101, figure 17-36, UML of `customerType`: private `customerNumber`, `arrivalTime`, `waitingTime`, `transactionTime` (all `int`); public `setCustomerInfo(int = 0, int = 0, int = 0, int = 0): void`, `getWaitingTime() const: int`, `setWaitingTime(int): void`, `incrementWaitingTime(): void`, `getArrivalTime() const: int`, `getTransactionTime() const: int`, `getCustomerNumber() const: int` and the constructor `customerType(int = 0, int = 0, int = 0, int = 0)`.
- Slide 102, figure 17-37, UML of `serverType`: private `currentCustomer: customerType` (the slide spells it "currentCustoner"), `status: string`, `transactionTime: int`; public `isFree() const: bool`, `setBusy(): void`, `setFree(): void`, `setTransactionTime(int): void`, `setTransactionTime(): void`, `getRemainingTransactionTime() const: int`, `decreaseTransactionTime(): void`, `setCurrentCustomer(customerType): void`, `getCurrentCustomerNumber() const: int`, `getCurrentCustomerArrivalTime() const: int`, `getCurrentCustomerWaitingTime() const: int`, `getCurrentCustomerTransactionTime() const: int` and the constructor `serverType()`.
- Slide 103: the server list is a set of servers. At any given time a server is either free or busy.
- Slide 104: when a customer arrives they go to the end of the queue. When a server becomes available, the customer at the front leaves to conduct the transaction. After each time unit the waiting time of every customer in the queue is incremented by 1. You can use `queueType` but must add an operation to increment the waiting time.
- Slide 105, the main loop:
```
for (clock = 1; clock <= simulationTime; clock++)
{
  2.1 Update the server list to decrement the transaction time of each busy server by one time unit.
  2.2 If the customer's queue is nonempty, increment the waiting time of each customer by one time unit.
  2.3 If a customer arrives, increment the number of customers by 1 and add the new customer to the queue.
  2.4 If a server is free and the customer's queue is nonempty, remove a customer from the front of the queue and send the customer to the free server.
}
```

## Lecture summary slides (slides 107 and 108, Amended S11)
- Stack: items are added and deleted from one end. LIFO. Operations: push, pop, initialize, destroy, check for an empty or full stack. It can be implemented as an array or a linked list. Middle elements should not be accessed directly. Postfix notation: operators are written after the operands (no parentheses needed).
- Queue: items are added at one end and removed from the other. FIFO. Operations: add, remove, initialize, destroy, check if the queue is empty or full. It can be implemented as an array or a linked list. Middle elements should not be accessed directly. A queue is a restricted version of an array and a linked list.

## Recursion link (added)
Recursion uses the call stack: each call is pushed, and each return pops. This is why a stack can print a list backward (slides 59 to 65, written below). Slide 3 lists "use a stack to remove recursion" as an objective.

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

## Amendments
- 28 Oct (Amend S11): read every slide of Lecture 9 as an image and added them as presented: stack figures, the linked stack slide by slide, array stack (10 to 29), postfix (46 to 58), print backward (59 to 65), extra queue detail (67 and 68), array queue (69 to 89), linked queue (90 to 96), simulation (97 to 105) and the summary (107 and 108). Corrected the coverage paragraph and the wrong claim that slides 90 to 96 held code (they are words only). Replaced the `top` and assignment operator snippets with the full slide code. Added N.B. lines: low frequency, do not focus too much on the array versions, postfix, print backward and simulation.
- (added) in this amendment: the array wrap formula, the print backward loops, the slide 94 versus slide 96 note, the pop figure remark.
