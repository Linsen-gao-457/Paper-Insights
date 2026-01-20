---
presentation:
  theme: moon.css
  width: 800
  height: 600
  margin: 0.2
  minScale: 0.2
  maxScale: 1.5
  slideNumber: true
---
<!-- slide -->

## Hopfield Network
📕 [paper link](https://pmc.ncbi.nlm.nih.gov/articles/PMC346238/)


<!-- slide -->
Goal: we aim to design a system which implements a contend-addressable memories using a large number of simple components, and exhibits some collective properties such as generalization, familiarity recognization, categorization, eror correction, and time sequence.




<!-- slide -->


Hopfield Network is a information storage system which have 2 functions:

1. [(Write)Store information](#write-function)

2. [(Read)Retrieve Information](#read-function)

3. [Capacity of HN](#capacity)




<!-- slide -->
### writing-Storage Information
<!-- slide -->
#### Some Definitions

Def The ==instaneous state== of the system is a Vector $V = (v_1, v_2, v_3, ...v_N)$, for $i \in \{1, ...N\}$, $v_i$ is a neuron with 2 states $v_i \in \{0, 1\}$.

Def ==message== $\mathcal M =\{V^1, V^2, \dots, V^n\}$ be colum vectors in $\{0,1\}^N \subset \{\pm 1\}^N$
<!-- slide -->


Def ==connection strength== $T$ be a $N \times N$ matrice. Here, $T_{ij}$(for $i,j \in \{1...N\}$) as the synaptic weight representing the strength of the connection from neuron $v_i$ to neuron $v_j$. 

$$ T = \sum_{s=1}^n (2V^s - 1)(2V^s - 1)^{\top} \tag{1}$$
<!-- slide -->

$$\scriptstyle T = \sum_{s=1}^n (2V^s - 1)(2V^s - 1)^{\top} \tag{1}$$
- Distributed Representation: every time we write a new message, we make a small modification of the connnection strength
<a id="Strength Matrice"></a>
- We are not directly writing the stored pattern into neurons - we are setting up a landscape in which that pattern become a statble points

- $T_{ii}=0$
<!-- slide -->

After that we define ==single-step update function== $\mathcal U(V)$ to update the state Vector $V^{(t)}$:

$$\mathcal U (V^{(t)};T):=sign(T V^{(t)})=V^{(t+1)} \tag{2}$$

Let $A(V)$ be a function to update per neuron mapping from $R^N \rightarrow R$, defined by 

$$
{\scriptstyle
A_i(V)=
\begin{cases}
1, & \text{if }\ \langle T_i,V\rangle-T_{ii}V_i\ge U_i,\\[4pt]
0, & \text{if }\ \langle T_i,V\rangle-T_{ii}V_i\le U_i.
\end{cases}}
$$

<!-- slide -->

$$
{\scriptstyle
A_i(V)=
\begin{cases}
1, & \text{if }\ \langle T_i,V\rangle-T_{ii}V_i\ge U_i,\\[4pt]
0, & \text{if }\ \langle T_i,V\rangle-T_{ii}V_i\le U_i.
\end{cases}}
$$
> Unless otherwise stated, we choose $U_i =0$

> $A_i : R^N \rightarrow R$ depends only on $T_i$

<!-- slide -->
Def ==multi-step update function==

$$\mathcal U^n: \{-1,1\}^N \rightarrow\{-1,1\}^N $$

$$\mathcal U^n(V;T) = \underbrace {\mathcal U(\mathcal U(\dots \mathcal U(V))\dots)} _{\text{n times}} \tag{3}$$
> When $n=\infty$ ,  
$\mathcal U ^{\infty}(V)= \lim _{n\rightarrow \infty} \mathcal U^n(V)$

<!-- slide -->
Define ==energy function== $E: R^N \rightarrow R^+$ as follow:

$$E(V;T) = \frac 1 2 V^TTV \qquad\forall V\in R^N\tag{4}$$

<!-- slide -->
**Thm** ==Energy decreasing rule==

for any $V\in R^N$, let $V^{'} \in R^N$, such that 
$$
\begin{cases}
v_j^{'} =v_j, &\text{if } j\neq i
\\\\[8pt]
v_i^{'} = A_i(V)
\end{cases}
$$

$E(V^{'}) - E(V)\leq 0$ always hold

<!-- slide -->
#### All in ALl

$\mathcal M$ specifies Hopfield Network, because $\{E, \mathcal U\}$ are parametrized by $\mathcal M$


<!-- slide -->
### Read-Retrieve Information

<!-- slide -->
Idealy, initialize a state Vector $V^{(0)} = f(V^i, Z)$, if $\mathcal U^\infty (V_0) = V^i$, we say we successfully retrive the message.
> $Z$ is a random vector in $R^N$. Think it as a noise form
> $f$ is a noise function to add noise Z to the original message $V^i$


<!-- slide -->
### Capacity

<!-- slide -->
Give $V^{(0)} = f(V^i, Z)$, there exists a maximal number $K$, satisfying $Pr(\mathcal U^\infty (V_0) = V^i) \ge \beta$, we call this capacity $Z-\beta$ capacity.
<!-- slide -->