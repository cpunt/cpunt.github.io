---
layout: post
title: Linked Lists
meta: A Linked List is a data structure that consists of nodes with each node containing data and a reference to the next node. It may also have a reference to the previous node if applicable...
posted: 20/08/2020
source: ''
category: Article
tags: ['Data Structures', 'Algorithms', 'Linked Lists']
---
## What is a Linked List?
A Linked List is a data structure that consists of nodes with each node containing data and a reference to the next node. It may also have a reference to the previous node if applicable. If the nodes have both a previous and next reference pointer then it is called a Doubly Linked List.

This article will focus on Singular Linked Lists, so a List with only a next reference pointer. The head is the starting point of a Linked List, a reference to the head will be stored. The last node in a Linked List is called the tail. The next pointer of the tail will be null. This shows that there are no more nodes in the List.  

## Why Use a Linked List?
Linked Lists excel at insertions and deletions, with an average O(1) runtime for these operations. But struggle with instant access operations, with an average O(n) runtime. Linked Lists also have potential storage advantages when the size of the input is not predefined. Since nodes in a Linked List store the reference to the next node this means they do not need to be stored contiguously. So a good use case for a Linked List would be a task which involves a lot of insertions and deletions and doesn't require instant access. Also an expanding input instead of a set input size.

## Implementing a Linked List
In the example below I will cover a basic implementation of a Linked List and its Nodes. The code examples will be written in Python:
```Python
class LinkedList:
  def __init__(self):
    self.head = None
    self.tail = None
    self.listLen = 0
```
The Linked List class has one method used to initialize the head. The class has three properties head and tail which are both set to None and listLen which is set to 0.
```Python
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None
```
The Node class also uses the initializer method. It sets two properties, data and next. Data is set to the data input and next will be set to None. The next property will contain the next nodes reference.
```Python
list = LinkedList('1')
list.head.next =  Node('2')
list.head.next.next = Node('3')
list.tail = list.head.next.next
```
The Linked List created above would resemble this *'1->2->3->None'*. Currently the Linked List class has no methods to add nodes, so I have had to set the next references manually. This would get tedious quickly if I continuously set the next references like this.

## Adding Nodes
In this section I will be expanding on the current Linked List class and implementing methods to add nodes. I will be adding three methods to the current class, addToTail, addToHead, and addToIndex.
```Python
def addToTail(self, data):
  self.listLen += 1
  if self.head is None:
    self.head = Node(data)
    self.tail = self.head
  else:
    self.tail.next = Node(data)
    self.tail = self.tail.next

  return True
```
The addToTail method sets the current tails next property to the node being added. Then sets the tail equal to this node.
```Python
def addToHead(self, data):
  self.listLen += 1
  node = Node(data)
  if self.head is not None:
    node.next = self.head
  else:
    self.tail = node

  self.head = node
  return True
```
In this method the head is set to a new node and the old head is set to the next node in the Linked List.
```Python
def addToIndex(self, data, index):
  if index < 0 or index > self.listLen:
    return False

  if index == 0:
    return self.addToHead(data)

  if index == self.listLen:
    return self.addToTail(data)

  self.listLen += 1
  node = Node(data)
  currentNode = self.head
  for i in range(index-1):
    currentNode = currentNode.next

  node.next = currentNode.next
  currentNode.next = node
  return True
```
The final method adds a node to a specific index. If the index is invalid then False will be returned indicating to the user that no node was added. If the index is set to the first or last element in the List then the node will be added to the head or tail. If the index is somewhere in the middle of the List, then the List will be traversed until the index is reached and the node is added. If the node is added True will be returned so the user knows the operation has been successful.
```
list = LinkedList('1')
list.addToTail('2')
list.addToTail('3')
list.addToHead('4')
list.addToIndex('5', 3)
```
The List above would look like this  '4 -> 1 -> 2 -> 5 -> 3 -> None'.
## Removing Nodes
Removing nodes in a Linked List is not too dissimilar to adding nodes. In this section I will implement three more methods to the Linked List class, removeTail,  removeHead and removeIndex.
```Python
  def removeTail(self):
    node = self.head

    if node is None:
      return False

    self.listLen -= 1

    if node.next is None:
    	self.head = None
      self.tail = None
      return True

    while node.next.next is not None:
    	node = node.next

    self.tail = node
    node.next = None
    return True
```
The first method removes the tail node in the Linked List. This method traverses the List until the node before the tail is found. Once found the next property is set to None making this node the new tail.
```Python
def removeHead(self):
  if self.head is None:
    return False

  self.listLen -= 1
	self.head = self.head.next

  if self.head is None:
    self.tail = None

  return True
```
The second method removes the head node. In this method the head is simply set to the head’s next node. If the head is already None then False is returned since a node wasn’t removed.
```Python
  def removeIndex(self, index):
    if index < 0 or index > self.listLen:
      return False

    if index == 0:
      return self.removeHead()

    if index == self.listLen:
      return self.removeTail()

    node = self.head
    for i in range(index-1):
      node = node.next

    node.next = node.next.next
    return True
```
The final method removes a node at a selected index in the List. If the input is invalid then False will be returned. If the index does exist, True will be returned since the node was removed. This will indicate to the user if the call was successful or not.
```Python
list = LinkedList('1')
list.addToTail('2')
list.addToTail('3')
list.addToTail('4')
list.addToTail('5')
list.addToTail('6')
list.addToTail('17')
list.removeTail()
list.removeHead()
list.removeIndex(3)
```
The Linked List above would look like this  '2 -> 3 -> 4 -> 6 -> None'.
## Finding Nodes
The final method I'm going to implement is a find method.
```Python
def find(self, data):
  node = self.head
  while node is not None:
    if node.data == data:
      return node
    node = node.next

  return None
```
The find method traverses the Linked List and checks if the node data is equal to the input data. If it is, the matching node is returned. If it does not match then None will be returned, indicating this data is not in the Linked List.

## Runtimes
In this section I will cover the runtime of each of the methods above. The addToTail and addToHead methods both have a O(1) runtime. Without tracking the tail the addToTail method would have been O(n), since the Linked List would've needed to have been traversed to reach the tail. The addToIndex method is O(n) for a valid input and O(1) for an erroneous input. This is made possible by tracking the Lists length to filter out invalid inputs.

The removeTail and removeIndex methods are both O(n) runtime. If this was a Doubly Linked List the removeTail method would be O(1). The removeIndex method like the addIndex method also has a O(1) runtime for any erroneous inputs. The removeHead method has an O(1) runtime and the find method has an O(n) runtime.

## Summary
Linked Lists can be a powerful data structure when used in the correct circumstances. If you want to do some interview prep on Linked Lists, [hackerrank](https://www.hackerrank.com/domains/data-structures?filters%5Bsubdomains%5D%5B%5D=linked-lists) and [leetcode](https://leetcode.com/tag/linked-list/) have some good questions.
