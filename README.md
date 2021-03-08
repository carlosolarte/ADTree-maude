# Attack-Defence Trees in Maude

An Attack-Defense Trees (ADTree) is a tree-like representation of a security
scenario. Nodes in the tree represent attacks and defensive measures [1]. 

This repository contains a rewriting logic specification of ADTree. Some
examples from [2] are used to illustrate the approach. 

## Getting Started 

The project was tested in [Maude 3.0](http://maude.cs.illinois.edu/). No extra
libraries are needed for execution.

The specification includes the following files:

- *syntax.maude*: We have used the object-like notation in the Maude's module
  `CONFIGURATION`. This file defines the identifiers for classes (sort `Cid`)
  for the different nodes of the tree with their respective attributes (cost,
  duration, children, state, etc). 

- *semantics.maude*: This file gives meaning to the different nodes. There is
  an alternative semantics for `AND` nodes where it is possible to accumulate
  the cost using the function `max`. This is an initial attempt to represent
  the situation where several agents may perform, in parallel, the attack. 

### Examples

- *steal-jewels.maude*: This is a simple example that illustrates the syntax
  used for defining the ADTree and the queries that can be performed. 

- *forestall.maude* (Forestalling a software release): Models an attack to the
  intellectual property of a company. 

- *gain-admin.maude*: Models the attack for obtaining root privileges on a
  server. 

Further details and motivations for these systems can be found in [2]. 

## Execution and Queries

Here an example showing how to execute the queries: 

```
$> maude forestall
Maude> search System =>* {C} .
...
Solution 3 (state 35)
states: 36  rewrites: 1366 in 8ms cpu (8ms real) (162968 rewrites/second)
C --> < 'FS : SAND | time: 10,cost: 0,acctime: 43,acccost: 13000,lchd: nil,stat: Succeed >
...
```

The following notation is used:

- `'FS: SAND` denotes a sequential `AND` node with label `'FS`
- `time: 10, cost: 0` are the time and cost attributes of the node
- `acctime: 43, acccost: 13000` are the accumulated time and cost for the
  attack
- `lchd: nil` is the list of remaining children of the node to be explored
- `state:Succeed` is the (final) state of the node

More details about the syntax for specifying ADTrees can be found in
`syntax.maude`. 


This package is free software; you can redistribute it and/or modify it under
the terms of GNU Lesser General Public License (see the COPYING file).


## Refences

[1] _Sjouke Mauw, Martijn Oostdijk_: Foundations of Attack Trees. ICISC 2005:
186-198

[2] _Jaime Arias, Carlos E. Budde, Wojciech Penczek, Laure Petrucci, Teofil
Sidoruk, Mariëlle Stoelinga_: Hackers vs. Security: Attack-Defence Trees as
Asynchronous Multi-agent Systems. ICFEM 2020: 3-19

