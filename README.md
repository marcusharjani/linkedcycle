# Linked Lists: HackerRank Detect a Cycle challenge

This is my response and explanation to one of the [HackerRank challenges](https://www.hackerrank.com/challenges/ctci-linked-list-cycle).

## Overview

The prompt states:

```Complete the function provided in the editor below. It has one parameter: a pointer to a Node object named that points to the head of a linked list. Your function must return a boolean denoting whether or not there is a cycle in the list. If there is a cycle, return true; otherwise, return false.```

Further

```A linked list is said to contain a cycle if any node is visited more than once while traversing the list.```

The implication here is that the Nodes of an unordered list may lead to next Nodes in such a way that a prior Node may be visted more than once.  This makes sense if we understand the difference between unordered lists and deterministic lists. In the latter, a list order is determined and a list element is accessed by it's given index 

```a[x]```

Where a is `a` list and `x` is the index of a specific element in that list. 

## Challenge

There are a few concepts to bear in mind for this challenge. First, we should be mindful of the structure of a linked list (e.g. that a linked list is made of Nodes which have a data value and position in the list, whether head or not). Second, how we might traverse a linked list. Third, when traversing the linked list how we might compare current Nodes to past Nodes and assess whether we have detected a cycle.

## Solution

So to begin, we are given some information about Nodes: 

```
"""
Detect a cycle in a linked list. Note that the head pointer may be 'None' if the list is empty.

A Node is defined as: 
 
    class Node(object):
        def __init__(self, data = None, next_node = None):
            self.data = data
            self.next = next_node
"""
```

Our class Node contains a constructor establishign an empty Node and so an empty list (e.g. data value and next node as None). 

We know that we will be given a series of lists as tests and we are given the start of a cycle for detecting a cycle:

```
def has_cycle(head):
```

First, we can say in plain language what we want to happen then we can translate that into a completed method. So, we want to say something like....

```
Let's keep track of our Node data values,
While we are running through a list,
If the data value of the Node we are currently on exists in this 'keeping track of data values',
Retrun 1 (for True in this case)
Otherwise, let's add the current data value to our 'keeping track' and move on.
If we never return 1, return 0.
```

So one way to do this is with the following method:

```
def has_cycle(head):
    nodes = set()
    while (head != None):
        if (head in nodes):
            return 1
        nodes.add(head)
        head = head.next
    return 0
```

Here we create a set() structure to store values from our list.
We then say While head is not None, if head is in our set, return True.
Outside of this conditional statement we add the current head to our set, and make the current head equal the next head.
Of course, returning 0 if no cycle is detected (i.e. our condition is left unmet).
