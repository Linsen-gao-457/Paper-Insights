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
Use two layers of structure: Type and micro feature. And another model to express relationship. Let's say C likes onion. We strengthen all the apes like onion. If later we learn some don't like onion, we modify the relationship between micro feature with onion.
In this case, we express the type apes using a set of units and a larger set of units which include types and microfeature: C, Gi, Or, Go to express it.


Local representation + spreading activation(traditional sematic network) vs distributed representation

For local representation, there is a 'handle', which is a computing unit where we assign the concept; there is no such things in distributed representation network.



## Tunability to Changing Environment(Creating New Concepts)
They make it possible to create new concepts without allocating new hardware.

For local representation, a scheme must first make a discrete decision about when to form a new concept and assign the new concept to a spare unit. But it's really inefficient to find a spare unit connecting to a specific set. For Example in a collection of million units each connected at random to ten thousand others, the chance of there being connected to a particular set of 6 others is only $\frac 1 {1,000,000}$.

Solution: 
We divide the units into two group: concept nodes and intermediate nodes. If there are $k$ layers of units, each of whihc has a fan-out of $n$ connections to randomly selected units in the following layer. There are $n^k$ potential pathway. But all but one of the actual connection emanating from each intermediate unit are wasted. So this method is only suitable for a relatively small fan-out.

We don't need to allocate new units to a new concept if we use distributed representations.

We only need to write the connection strength. If this is done by modifying a large number of connections very slightly, the creation of a new pattern need not disrupt the existing representations. 

When introduing a new concept into a distributed representation system. We want to find the pattern being ordered from least to most desirable:
1. Random pattern where major changes would be needed in the weights.
2. Find a pattern that already produce roughly the correct effects
3. Find a pattern that requires the least modification of weights to make the new pattern stable and to make it have the required effects on other representations.

> Note we don't need to find a pattern in one step. We can also find pattern to emerge as a result of modifications on many separate steps. 

The central problem is to specify the exact procedures where distributed representations are to be learned to optimize a system yielding stable. generalizable properties.

# Efficiency of Distributed System

# Difficult Issues Solved by Distributed System