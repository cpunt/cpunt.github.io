---
layout: post
title: Linked Lists
meta: A Linked List is a basic computer programming data structure. It is comprised of nodes with each node containing data and an reference to the next node. A Linked list may also have a reference to the previous node if applicable. A Linked List with nodes that have a previous and next reference pointer is called a doubly Linked List...
source: ''
category: Article
tags: ['Data Structures', 'Algorithms', 'Linked Lists']
---
## What Is A Linked List?
A Linked List is a basic computer programming data structure. It is comprised of nodes with each node containing data and an reference to the next node. A Linked list may also have a reference to the previous node if applicable. A Linked List with nodes that have a previous and next reference pointer is called a doubly Linked List. In this article we will be focusing on an singular Linked List, which only has a next reference pointer. The head is the starting point of our Linked List, we will store the reference to this node. The tail is the last node in our Linked List, we know we have reached the tail when the next node is equal to null.

## Why Use A Linked List?
Linked Lists excel with insertions and deletions, with an average O(1) runtime for these operations. But struggle with instant access operations, with an average O(n) runtime. Linked Lists can also be cheaper to store if we do not know the size of the list. Since nodes in a Linked List store the reference to the next node this means they do not need to be stored contiguously. This is unlike arrays which do need to be stored contiguously. So if we have an expanding list, an array may need to relocate it's memory which can be an expensive operation. But if we know the size of the list it is cheaper to store it in an array. This is because Linked List nodes need to store the reference to the next node, where as items in an array do not. A good use case for a Linked List would be a task which involves a lot of insertions and deletions and doesn't require instant access. Also an expanding list instead of a set list.

## Implementing A Linked List
Now we have a basic understanding of what a Linked List is lets implement one. In our code example below we will be using Python:
```Python
class LinkedList:
  def __init__(self, data):
    self.head = Node(data)

  def __repr__(self):
        node = self.head
        nodes = []
        while node is not None:
            nodes.append(node.data)
            node = node.next
        nodes.append("None")
        return " -> ".join(nodes)
```
First we implement our Linked List class. This class currently has two methods. This init method will initialize the head of our Linked List. We set our head equal to a Node instance passing in our data argument. The repr method is the representation we want our class to display when printed. Now let's take a look at the Node class.
```Python
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

  def __repr__(self):
    return self.data
```
This class takes the same two methods as our Linked List class. We initialize the Node class by setting our data property equal to our data and the next property equal to None. Next will be our reference to the next node. Now we have the very basics of our Linked List implemented let's use it.
```Python
list = LinkedList('1')
node2 = Node('2')
node3 = Node('3')

list.head.next = node2
node2.next = node3
print(list)
```
In the code above we create a new Linked List, we then create two other nodes and finally we set the Linked List next references. When we print out list we should get the output *'1->2->3->None'*. This would get very tedious if we had to do this every time we wanted to add an item to our Linked List. In the next section we will look at methods which will add nodes to our Linked Lists.
## Adding Nodes
In this section we will look at methods we can use to add nodes to our Linked List. We will cover three methods, the first will be adding a node to the tail of our list, the second will be adding a node to the middle of our list and the third method will be adding nodes to the head of our list.
```Python
def addToTail(self, data):
	node = self.head
	while node.next is not None:
		node = node.next
	node.next = Node(data)
```
In this method we traverse our Linked List until we get to the tail of the tree and then add our new node to our tail nodes next property.
```Python
def addToHead(self, data):
	node = Node(data)
	node.next = self.head
	self.head = node
```
In this method we create a new node and then set the next property to our current head. We then set the head to our new node.
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
In our final method we first check for the edge case if the node is 0. We do this because our function will not work for this case, if our index is 0 we call our addToHead method. If our index is not 0 we traverse our Linked List until we reach the node before where we want our new node. If we can't traverse the node to this index we will return False so the user knows this has failed. Once we have reached our desired node we set our new node next property to currentNode next property. We then set our currentNode next property to our new node. We then finally return True. This is so the user knows the add was successful.
```
list = LinkedList('1')
list.addToTail('2')
list.addToTail('3')
list.addToHead('4')
list.addToIndex('5', 3)

print(list)
```
Now we have all our add functions let's take a look at them in action. In the example above we would expect the output '4 -> 1 -> 2 -> 5 -> 3 -> None'.
## Removing Nodes
Now we can add nodes it would be nice to be able to remove nodes which are no longer needed. In this section we will cover the counter parts of adding nodes. So we will cover removing nodes from the tail, head and middle.
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
In our first method we remove the tail node. We do this by finding the node before the tail node and setting this nodes next property to None.
```Python
def removeHead(self):
	self.head = self.head.next
```
Our second method removes the head node. In this method we simply set the head to the next node.
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
In our final method we remove a select index from our Linked List. If we can not remove the node because it doesn't exist we return False and if the index is removed successfully we return True. This is so the user is aware if the method call was successful or not.
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

print(list)
```
Let's take a look at our methods in action. When we print our Linked List after using all the methods it would look like this '2 -> 3 -> 4 -> 6 -> None'.
## Finding Nodes
Now we can remove and add nodes what if we want to find if an node exists in our list and return it? This is will be our final method we implement for our Linked List class.
```Python
def find(self, data):
	node = self.head
	while node is not none:
		if node.data == data:
			return node
		node = node.next

	return None
```
In our find method we traverse the Linked List checking if each node data is equal to our input data. If we get a match we return the node. If there is no matches we return None.
## Notes
Methods should have check to see if Linked List is empty.
Removing Nodes should return node.data removed.
Refer to as linear
