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

By John Hopfield
<!-- slide -->
# Who is John Hopfield?

<!-- slide -->
![alt text](Image/John%20Hopfield.png)

<!-- slide -->
- Winner of the 2024 Nobel Prize in Physics
- Poineer of Associate Neuron Network
- Yue's Alumni
<!-- slide -->
What is associate memory at high level?

![alt text](Image/Associate%20Memory.png)

<!-- slide -->


#### table of contents

1. [(Write)Store information](#write-function)

2. [(Read)Retrieve Information](#read-function)

3. [Capacity of HN](#capacity)




<!-- slide -->
### writing-Storage Information
<!-- slide -->
#### Some Definitions

Def The ==instaneous state== is a Vector $\sigma = (\sigma_1, \sigma_2, \sigma_3, ...\sigma_N)$, for $i \in \{1, ...N\}$, $\sigma_i$ is a neuron with 2 states $\sigma_i \in \{0, 1\}$.

Def ==message== $\mathcal M =\{\xi^1, \xi^2, \dots, \xi^n\}$$ \subseteq \{\pm 1\}^N$, for $i \in \{1,\dots, n\}$, $\xi^i \in \{\pm 1\}^N$
<!-- slide -->


Def ==connection strength== $W$ be a $N \times N$ matrice.

$$ W = \sum_{s=1}^n (2\xi^s - 1)(2\xi^s - 1)^{\top} \tag{1}$$
<!-- slide -->

$$\scriptstyle W = \sum_{s=1}^n (2\xi^s - 1)(2\xi^s - 1)^{\top} \tag{1}$$
- Distributed Representation
- Set up a landscape where message become a statble points

Assign $W_{ii}=0$, for $i\in \{1,\dots,N\}$, we denote $W $as $\overset {\sim}{W}$
<!-- slide -->

After that we define ==single-step update function== $T(\sigma)$ to update the state Vector $\sigma$:

$$T (\sigma;W):=sign(\overset \sim W\sigma) \tag{2}$$
<!-- slide -->
Let $T_j(\sigma)$, where $j\in \{1,\dots,N\}$, be a function to update per neuron mapping from $R^N \rightarrow R$, defined by 

$$
{\scriptstyle
T_j(\sigma)=
\begin{cases}
1, & \text{if }\ W_j\sigma -W_{jj}\sigma_j> U,\\[4pt]
0, & \text{if }\ W_j\sigma -W_{jj}\sigma_j\le U.
\end{cases}}
$$
- Unless otherwise stated, we choose $U =0$

<!-- slide -->
$${\scriptstyle
T_j(\sigma)=
\begin{cases}
1, & \text{if }\ W_j\sigma -W_{jj}\sigma_i> U,\\[4pt]
0, & \text{if }\ W_j\sigma -W_{jj}\sigma_i\le U.
\end{cases}}
$$
- $W_j$ is the $j$ th row of $W$
$$W_j = \sum_{s=1}^N (2\xi_j^s-1)(2\xi^s -1)^{\top}$$
- $T_j$ is parametrized only by $W_j$
- $T$ is parametrized only by $W$
<!-- slide -->
 $W_j$ is the $j$ th row of $W$, if $W_{jj} =0$, we get

 $$T_j(\sigma) = sign(\overset \sim W_j \sigma)$$
<!-- slide -->
Def ==multi-step update function==

$$T^n: \{-1,1\}^N \rightarrow\{-1,1\}^N $$

$$T^n(\sigma;W) = \underbrace {T(T(\dots  T(\sigma))\dots)} _{\text{n times}} \tag{3}$$
> When $n=\infty$ ,  
$T ^{\infty}(\sigma)= \lim _{n\rightarrow \infty} T^n(\sigma)$

<!-- slide -->
Define ==energy function== $E: R^N \rightarrow R^+$ as follow:

$$E(\sigma;W) = \frac 1 2 \sigma^\top \overset \sim W\sigma \qquad\forall V\in R^N\tag{4}$$
- $\xi^i$, $i\in \{1,\dots,n\}$ is local minima of energy function(under certain condition it could hold)
<!-- slide -->
**Thm** ==Energy decreasing Theorem==

for any $\sigma \in R^N$, let $\sigma^{'} \in R^N$, such that 
$$
\sigma ' = T(\sigma)
$$

$E(\sigma^{'}) - E(\sigma)\leq 0$ always hold


<!-- slide -->

#### All in ALl

$\mathcal M$ specifies Hopfield Network, because $\{E, T\}$ are parametrized by $\mathcal M$


<!-- slide -->
### Read-Retrieve Information

<!-- slide -->
Initialize a state Vector $\sigma^{(0)}$, idealy $T^\infty (\sigma^{(0)}) = \xi_i$, where $i \in \{1,\dots, n\}$

<!-- slide -->
![Energy Minimization](Image/Energy%20Minimization.png)

<!-- slide -->
### Capacity

<!-- slide -->
- $\xi^i \in \mathcal M=\{\xi^1,\dots,\xi^K\}$ is a random vector with N dimensions. For $j\in \{1,\dots,N\}$, $\{\xi_j^i \sim Ber(0.5)\}$ which are independent.

- Capacity is the maximum number $K$ of messages a Hopfield Network can store, s.t. for $i\in \{1,\dots, K\}, j\in \{1,\dots, N\}$, $Pr\{T_j(\xi^i)\ne \xi^i_j\}\le \alpha$. Denoted by $C_\alpha$

<!-- slide -->
#### TL;DR
Content-addressable information storage systems capable of error correction
<!-- slide -->
# Thank you!