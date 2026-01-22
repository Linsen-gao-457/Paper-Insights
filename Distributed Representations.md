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
> Componential structure means that a concept, object, or piece of knowledge is systematically composed of reusable parts, and that meaning depends on how those parts are combined.

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
2. For unrelated patterns, all the small modifications will mainly cancel out.

Solution:
Using orthogonal pattern, but it will eliminated the most interesting properties of distributed representations - generalizations. So that's the reason we use distributed representation.

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
1. Certain distributed representation schemes can fail to provide a sufficient basis for differentiating different concepts and its solution.
2. A way of using distributed representations to get the most information possible out of a simple network of connected units.

Coarse coding is a form of distributed representation: a feature can be represented by several units. And each unit is activated by many features.

The question of interest is that how many units it takes to encode feature with a given accuracy. (The accuracy here need to be defined)

We start by defining a feature by two things:
1. Discrete Type - e.g. line-segment, corner, dot
2. Continuous Parameters - e.g. position, orientation, size

EX1
dot in a plane, specified by coordinate (x,y), 2 dimensinos

EX2
Stopped, orientex edge-segments, specified by (x,y,z), 2 angle parameters and 1 length. In total, 6 dimensions.

Suppose we use coarse encodign to represent the position of a single dot in a plane. Divide the units into two group X and Y, dedicate each unit to encoding a particular X or Y interval.

Def accuracy of an encoing scheme to be the number of different encodings that are generated as the dot is moved a standard distance through the space. 

EX 3
0.0 -> 0.5 -> 1
A -> A -> B 
low accuracy = 2
0.0 -> 0.25 -> 0.50 -> 0.75 -> 1.00
A -> B -> C -> D -> E
high accuracy = 5

There are two problems in this encoding systems.
1. If two dots have to be encoded at the same time. We cannot tell $(x_1. y_1), (x_2,y_2), (x_1, y_2), (x_2,y_1)$. We call this binding problem.
2. Suppose we want certain representations to be associated with an overt response. This is another aspect of binding pronblem; The x1 and x2 would both activate the response smae as y1 and y2. 

## Conjunctive Encoding

Solution to the binding problem: use a unit to express the pair(x1,y1). It's a local representation.

The accuracy is porportional to the $k^{th}$ root of the number of units. 

It would be more efficient to use an encoding where a larger fraction of the units were activate at any moment. Otherwise, we use coarse coding.

## Coarse Coding

Def coarse coding, we divide the sapce into overlaping zones and assign unit ot each zone. We assume that zones are circular, which their centers have a uniform random distribution throughout the space, and all the zones used by a given encoding scheme have the radius. 

Accuracy: the accuracy is a number which is proportional to the number of different encodings that are generated as we move a feature point along a straight line from one side to the other.

Improve the efficiency comparing with local representation.

accuracy $\sim n r^{k-1}$
> $n$ is the number of zones the line penetrates
> $r$ is the radius of the zones


Limitation of coarse coding
1. Coarse coding is useful when the features that must be represented are relatively sparse.
2. Coarse coding is useful if the required effect of a feature is the average of the required effects of its neighbors.
3. When coarse-coded representations interact, there is a tendency for the coarseness to increase.


# Difficult Issues Solved by Distributed System( Structured Representations and process)