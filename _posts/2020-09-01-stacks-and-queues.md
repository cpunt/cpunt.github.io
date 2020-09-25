---
layout: post
title: Stacks and Queues
meta: In this article we will be covering the data structures stacks and queues. We will learn how to implement both a stack and a queue written in Python. But before we look at code examples let's talk about what a stack and a queue actually is...
posted: 01/09/2020
source: ''
category: Article
tags: ['Data Structures', 'Algorithms', 'Stacks', 'Queues']
---
## What are Stacks and Queues?
In this article we will be covering the data structures stacks and queues. We will learn how to implement both a stack and a queue written in Python. But before we look at code examples let's talk about what a stack and a queue actually is.
<br><br>
A stack is something we regularly encounter in our day to day lives. An example of a stack would be a pile of plates. When we want a new plate we grab the plate from the top of the stack. When we want to put a plate back this also goes to the top of the stack. This real world example is exactly how stacks work in the computer programming world. When we want to add an item onto our stack, it will be added to the top of our stack. When we want to remove an item from our stack, it will be removed from the top of our stack. We will be referring to these stack methods as push and pop. It is important to remember that stacks work on a last in first out basis.
<br><br>
A queue is something we also encounter frequently in real life. An example of a queue would be waiting in line at a supermarket. If you are the first person in the line, you will be the first person to see the cashier and first person to leave. If you join the line you will join at the back. This is how queues are used when we use them in our code. Where queues differ from stacks is that they work on a first in first out basis. So when we push at item onto our queue it will be added to the back of the queue. When we pop at item from our queue the first item will be removed from the queue. Now we have a rough understanding on how queues and stacks work let's look at some code examples.

## Stacks
In this example we will implement a very basic stack class which has the ability to push and pop. You could of course extend on this stack class by adding methods which can return the size of the stack, the top item in the stack, weather of not the stack is empty, etc. Python has built in data structures like queue and deque which can be used as a stack but in this example we will be implementing our own stack class so we understand clearly the inner workings.
```Python
class Stack:
  def __init__ (self):
    self.top = None;

  def push (self, data):
    node = StackNode(data)

    if self.top is None:
      self.top = node
    else:
      node.next = self.top
      self.top = node

  def pop (self):
    if self.top is not None:
      self.top = self.top.next
```
The example above is an example of how to implement a stack. When we initiate our class we set the top property equal to None. This property will keep track of the last node added to our stack. When pushing an item onto our stack this will become our the new value for our top property. When removing an item from our stack the next node will become our new top property. Now let's take a look at StackNode so we know how our stack nodes are formed.
```Python
class StackNode:
  def __init__ (self, data):
    self.data = data
    self.next = None
```
Our StackNode is the same as a linked list node. Linked lists are perfect to implement a stack because when we push or pop a node from our stack the runtime will always be O(1). If we used an array instead of a linked list our runtime would be O(n). This is because arrays need to be stored contiguously and Linked Lists do not. Let's take a look at our stack in action.
```Python
myStack = Stack()
myStack.push(8)
myStack.push(3)
myStack.push(2)
myStack.push(7)
myStack.pop()
```
In this example we used our push and pop methods to form our stack. Our end stack would look like this '2 -> 3 -> 8 -> None'.

## Queues
In this example we are also going to keep our queue class basic with the same methods as our stack class, push and pop. This is a very basic implementation of a queue but it lays the crucial foundations and can easily be built on once implemented.
```Python
class Queue:
  def __init__ (self):
    self.head = None
    self.tail = None

  def push (self, data):
    node = QueueNode(data)

    if self.tail is None:
      self.tail = node
      self.head = node
    else:
      self.tail.next = node
      self.tail = node

  def pop (self):
    if self.head is not None:
      self.head = self.head.next

    if self.head is None:
      self.tail = None
```
In our queue class we initialize two properties, head and tail. The head property will keep track of the start of our queue and the tail property will keep track of the end of our queue. When we push at item onto our queue we update the tail with the new node. When we pop an item from our queue we change the head to the next item in our queue. The QueueNode class is the exact same as our StackNode class in the last example. Now let's take a look at our queue in action.
```Python
myQueue = Queue()
myQueue.push(9)
myQueue.push(3)
myQueue.push(5)
myQueue.push(12)
myQueue.push(4)
myQueue.pop()
```
In our example our queue would look like this '3 -> 5 -> 12 -> 4 -> None'. Each time we call the pop method it removes the item at the top of the queue. So the next item to be removed would be 5 and so on until None is reached.

## Notes
Refer to as linear
