---
layout: post
title: Linked Lists
meta: A Linked List is a basic computer programming data structure. It is comprised of nodes with each node containing data and an reference to the next node. A Linked list may also have a reference to the previous node if applicable. A Linked List with nodes that have a previous and next reference pointer is called a doubly Linked List...
source: ''
category: Article
tags: ['Data Structures', 'Algorithms', 'Linked Lists']
---
## What is a Linked List?
A Linked List is a linear data structure. It is comprised of nodes with each node containing data and an reference to the next node. A Linked List may also have a reference to the previous node if applicable. If the nodes have both a previous and next reference pointer then it is called a Doubly Linked List.

This article will focus on Singular Linked Lists, so a List with only a next reference pointer. The head is the starting point of a Linked List, a reference to the head will be stored. The last node in a Linked List is called the tail. The next pointer of the tail will be null. This shows that there is no more nodes in the List.  

## Why Use a Linked List?
Linked Lists excel at insertions and deletions, with an average O(1) runtime for these operations. But struggle with instant access operations, with an average O(n) runtime. Linked Lists also have potential storage advantages when the size of the input is not predefined. Since nodes in a Linked List store the reference to the next node this means they do not need to be stored contiguously. This is unlike arrays, if the input expands past the array size then the array will need to be relocated which can be expensive.

When the input has a predefined size it may be cheaper to use an array. This is because Linked List nodes need to store the reference to the next node, where as items in an array do not. A good use case for a Linked List would be a task which involves a lot of insertions and deletions and doesn't require instant access. Also an expanding input instead of a set input size.

## Implementing a Linked List
In the example below I will cover a basic implementation of a Linked List. The code examples will be written in Python:
```Python
class LinkedList:
  def __init__(self, data):
    self.head = Node(data)
```
The Linked List class has one method used to initialize the head. When I set the heads data I create a new Node instance. This class will be used for each node in the Linked List.
```Python
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None
```
The Node class also uses the initializer method. It sets two properties data and next. Data is set to the data input and next will be set to None. The next property will contain the next nodes reference.
```Python
list = LinkedList('1')
list.head.next =  Node('2')
list.head.next.next = Node('3')
```
The Linked List created above would resemble this *'1->2->3->None'*. Currently the Linked List class has no methods to add nodes, so I have had to set the next references manually. This would get tedious quickly if I continously set the next references like this.

## Adding Nodes
In this section I will be expanding on the current Linked List class and implementing methods to add nodes. I will be adding three methods to the current class, addToTail, addToHead, and addToIndex.
```Python
def addToTail(self, data):
	node = self.head
	while node.next is not None:
		node = node.next
	node.next = Node(data)
```
The addToTail method traverses the Linked List until the tail is reached. Once the tail is reached a new node is added creating a new tail.
```Python
def addToHead(self, data):
	node = Node(data)
	node.next = self.head
	self.head = node
```
In this method the head is set to a new node and the old head is set to the next node in the Linked List.
```Python
def addToIndex(self, data, index):
	if index == 0:
		self.addToHead(data)
		return True

	node = Node(data)
	currentNode = self.head
	for i in range(index-1):
		currentNode = currentNode.next
		if currentNode is None:
			return False

	node.next = currentNode.next
	currentNode.next = node
	return True
```
The final method adds a node to a specific index. If the index is set to 0 then the new node will become the head node. If the index is greater than 0 then the Linked List will be traversed until the node before the index is reached. Once reached the new node can be added to the index. If the index can not be reached because the List is to short then False will be returned, indicating to the user the node was not added. If the node is added True will be returned.
```
list = LinkedList('1')
list.addToTail('2')
list.addToTail('3')
list.addToHead('4')
list.addToIndex('5', 3)
```
The List above would look like this  '4 -> 1 -> 2 -> 5 -> 3 -> None'.
## Removing Nodes
Removing nodes in a Linked List is not to dissimilar to adding nodes. In this section I will implement three more methods to the Linked List class, removeTail,  removeHead and removeIndex.
```Python
def removeTail(self):
	node = self.head

	if node.next is None:
		self.head = None
	else:
		while node.next.next is not None:
			node = node.next

		node.next = None
```
The first method removes the tail node in the Linked List. This method traverses the List until the node before the tail is found. Once found the next property is set to None making this node the new tail.
```Python
def removeHead(self):
	self.head = self.head.next
```
The second method removes the head node. In this method the head is simply set to heads next node.
```Python
  def removeIndex(self, index):
    if index == 0:
      self.removeHead()
      return True

    node = self.head
    for i in range(index-1):
      node = node.next
      if node is None:
        return False

    if node.next is None:
      return False

    node.next = node.next.next
    return True
```
The final method removes a node at a selected index in the List. If the index does not exist because the List is to short, False will be returned since a node wasn't removed. If the index does exist, True will be returned since the node was removed. This will indicate to the user if the call was successful or not.
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
	while node is not none:
		if node.data == data:
			return node
		node = node.next

	return None
```
The find method traverses the Linked List and checks if the node data is equal to the input data. If it is the matching node is returned. If it does not match then None will be returned, indicating this data is not in the Linked List.

## Summary
Linked Lists can be a powerful data structure when used in the correct circumstances. Check out these [interview questions](http://) based around Linked List so you can implement a List of your own.
