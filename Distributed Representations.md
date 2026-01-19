######  Table of content
[Introduction](#introduction)
[Virtues of Distributed System](#virtues-of-distributed-system)
[Efficiency of Distributed System](#efficiency-of-distributed-system)
[Difficult Issues Solved by Distributed System](#difficult-issues-solved-by-distributed-system)

# Introduction

Def Neuron, aka computing elements, as a set $V = \{V_1, \dots, V_N\}$

Def Entity , as a set $N = \{n_1,\dots, n_k\}$


Def **Local Representation**: $n_i$, $i \in \{1,\dots, k\}$, can be represented by $V_j$, for  $j\in \{1,\dots, N\}$. 

Def **Distributed Representation**: $n_i$, $i \in \{1,\dots, k\}$, can be represented by $V_o \subset V$

| | Local Representation|Distributed Representation |
|----------|----------|----------|
| Pros | Intuitive: Structure similar to knowledge  | Efficient|
| Cons | Hard to express componential structure  | Hard to store a large set of arbitary associations|

# Virtues of Distributed System
## Constructive Character(Memory as Inference)
Content-Addressable memory vs Tradition computer memory
1. Error correction | Use adress to retrieve information
2. Pattern which are not active does not exist | Patterns always exist

Other prospect to see distributed representation- Inferrence rules:

Each computing unit is 'microfeature'. The connection strength is 'microinferences'.

Def A stable pattern of acitvity is one that satisfies the microinferences less than its neighbor patterns.

Def A genuine memory/veridical recall is a pattern that is stable because the connection strength were modified before this pattern occured.

Def A confabulation/plausible reconstruction is a pattern that is stable because the connection strength have been modified by several previous patterns but not the partern itself.



## Generalization
When writing some information into distributed representation network(we call see it as small modification of a large bunches of computing units), there is only two possible way
1. For perfect related pattern, the total help for the intended pattern will be the sum of the small modifications of all previous writen patterns.
2. For unrelated patterns, all the small modifications will mainly cancle out.

Solution:
Using orthogonal pattern, but it will eliminated the most interesting properties of distributed representations - generalizations.

Let us dive into Generalization.

**EX.** C, Gi, Or, Go are all apes. C likes onion, we infer that Go likes onion as well. 

How do we implement the network? 
-> For the simplest network, the onion and C may be stored in patterns sharing the very same set of computing units-> Solution: Using separate modules for each concepts within a larger structure.

How do we express the relationship?
Use two layers of structure: Type and micro feature. Let's say C likes onion. We strengthen all the apes like onion. If later we learn some don't like onion, we modify the relationship between micro feature with onion.
In this case, we express the type apes using a set of units and a larger set of units which include types and microfeature: C, Gi, Or, Go to express it.


Local representation + spreading activation(traditional sematic network) vs distributed representation

For local representation, there is a 'handle', which is a computing unit where we assign the concept; there is no such things in distributed representation network.



## Tunability to Changing Environment(Creating New Concepts)
They make it possible to create new concepts without allocating new hardware.

# Efficiency of Distributed System

# Difficult Issues Solved by Distributed System