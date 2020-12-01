---
layout: post
title: Stacks and Queues
meta: This article will cover the data structures Stacks and Queues. This article will contain what a Stack and Queue is and also how to implement the data structures.
posted: 01/09/2020
source: ''
category: Article
tags: ['Data Structures', 'Algorithms', 'Stacks', 'Queues']
---
## What are Stacks and Queues?
This article will cover Stacks and Queues. Stacks and Queues are very similar, they are both data structures with an average O(1) insert / delete and O(n) access / search. Stacks and Queues differ when it comes to how inserts and deletes are handled. Stacks operate in a first in last out manner, whereas Queues are first in first out.

Here's a real world example of a Stack being used: *Imagine there is a pile of plates. When a plate is removed it is removed from the top of the pile. When a plate is added, it is added to the top of the pile*. This example follows a Stacks first in last out pattern. Stacks are a commonly used data structure in computer programming. One example of where a Stack is used in the computing world would be the [Call Stack](https://en.wikipedia.org/wiki/Call_stack).

A real world example of a Queue would be: *There is a single line at a supermarket of people waiting to pay for their items. The first person in the line would get to see the cashier first and be the first person to leave the line. If somebody wanted to join the line they would have to go to the back*. This example follows the Queue pattern of first in first out. Queues are also a commonly used data structure. An example of a Queue being used in programming would be the [Keyboard Buffer](https://en.wikipedia.org/wiki/Keyboard_buffer).

## Stack Example
In the example below, I will implement a basic Stack class which will have the ability to push (add) and pop (delete) items. For the code examples in this article, I will be using Python. Python does already have built-in Stacks and Queues data structures such as queue and deque. In these examples, I will not be using built-in data structures for the purpose of clearly demonstrating the inner workings of Stacks and Queues.
```Python
class Stack:
    def __init__ (self):
        self.top = None;

    def push (self, data):
        node = Node(data)

        if self.top is None:
            self.top = node
        else:
            node.next = self.top
            self.top = node

    def pop (self):
        if self.top is not None:
            popped = self.top
            self.top = self.top.next
            return popped
```
The Stack class implemented has three methods. The first method initializes the top of the Stack to None. This property will keep track of the node at the top of the Stack. The second method pushes the new node to the top of the Stack. The final method pops the top node off the Stack. Notice when adding a new node the Node class is used. Below is an example of this class.
```Python
class Node:
    def __init__ (self, data):
        self.data = data
        self.next = None
```
The Node class creates a Linked Lists structure, keeping reference to the next element. Using a Linked List structure will ensure that delete / insert times will be O(1).
```Python
myStack = Stack()
myStack.push(8)
myStack.push(3)
myStack.push(2)
myStack.push(7)
myStack.pop()
```
The Stack example above would look like this '2 -> 3 -> 8 -> None'.
## Queue Example
In the example below I will be implementing a basic Queue class with the same methods as the Stack class featured above, push and pop.
```Python
class Queue:
    def __init__ (self):
        self.head = None
        self.tail = None

    def push (self, data):
        node = Node(data)

        if self.tail is None:
            self.tail = node
            self.head = node
        else:
            self.tail.next = node
            self.tail = node

    def shift (self):
        if self.head is not None:
            self.head = self.head.next

        if self.head is None:
            self.tail = None
```
The Queue class has three methods. The first method initializes the head and tail properties to None. These properties will store the first and last nodes in the Queue. The second method adds the new Node to the end of the Queue, updating the tail. The final method removes the first item in the Queue, updating the head.
```Python
myQueue = Queue()
myQueue.push(9)
myQueue.push(3)
myQueue.push(5)
myQueue.push(12)
myQueue.push(4)
myQueue.pop()
```
The Queue example above would look like this '3 -> 5 -> 12 -> 4 -> None'.
## Summary
Stacks and Queues are a core data structure in computer programming which will frequently be seen, so it's best to be familiar with what they are and how they work. If you want to test your knowledge, [hackerrank](https://www.hackerrank.com/domains/data-structures?filters%5Bsubdomains%5D%5B%5D=queues&filters%5Bsubdomains%5D%5B%5D=stacks) and [leetcode](https://leetcode.com/problemset/all/) have some good questions on Stacks and Queues.
