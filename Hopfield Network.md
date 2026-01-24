---
toc:
  depth_from: 1     # include from H1
  depth_to: 2      
  ordered: true     # numbered list instead of bullets
---
[TOC]



# Hopfield Network
📕 [paper link](https://pmc.ncbi.nlm.nih.gov/articles/PMC346238/)

**Goal**: we aim to design a system which implements a contend-addressable memories using a large number of simple components, and exhibits some collective properties such as generalization, familiarity recognization, categorization, eror correction, and time sequence.

Hopfield Network is a information storage system which have 2 functions:

1. [(Write)Store information](#write-function)

2. [(Read)Retrieve Information](#read-function)



# Write Function

Def The ==instaneous state== of the system is a Vector $\sigma = (\sigma_1, \sigma_2, \sigma_3, ...\sigma_N)$, for $i \in \{1, ...N\}$, $\sigma_i$ is a neuron with 2 states $\sigma_i \in \{0, 1\}$.

Def ==message== $\mathcal M =\{\xi^1, \xi^2, \dots, \xi^n\}$$ \subseteq \{\pm 1\}^N$, for $i \in \{1,\dots, n\}$, $\xi^i \in \{\pm 1\}^N$

Def ==connection strength== $W$ be a $N \times N$ matrice.

$$ W = \sum_{s=1}^n (2\xi^s - 1)(2\xi^s - 1)^{\top} \tag{1}$$


<a id="Strength Matrice"></a>

> We are not directly writing the stored pattern into neurons - we are setting up a landscape in which that pattern become a statble points.

Assign $W_{ii}=0$, for $i\in \{1,\dots,N\}$, we denote $W $as $\overset {\sim}{W}$

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
- $W_j$ is the $j$ th row of $W$
$$W_j = \sum_{s=1}^N (2\xi_j^s-1)(2\xi^s -1)^{\top}$$

 $W_j$ is the $j$ th row of $W$, we get

 $$T_j(\sigma) = sign(\overset \sim W_j \sigma)$$

- $T_j$ is parametrized only by $W_j$
- $T$ is parametrized only by $W$

---
After that we define ==single-step update function== $T(\sigma)$ to update the state Vector $\sigma$:

$$T (\sigma;W):=sign(\overset \sim W\sigma) \tag{2}$$

Def ==multi-step update function==

$$T^n: \{-1,1\}^N \rightarrow\{-1,1\}^N $$

$$T^n(\sigma;W) = \underbrace {T(T(\dots  T(\sigma))\dots)} _{\text{n times}} \tag{3}$$
> When $n=\infty$ ,  
$T ^{\infty}(\sigma)= \lim _{n\rightarrow \infty} T^n(\sigma)$


---

Define ==energy function== $E: R^N \rightarrow R^+$ as follow:

$$E(\sigma;W) = \frac 1 2 \sigma^\top \overset \sim W\sigma \qquad\forall V\in R^N\tag{4}$$
- $\xi^i$, $i\in \{1,\dots,n\}$ is local minima of energy function(under certain condition it could hold)



---
**Thm** ==Energy decreasing Theorem==

for any $\sigma \in R^N$, let $\sigma^{'} \in R^N$, such that 
$$
\sigma ' = T(\sigma)
$$

$E(\sigma^{'}) - E(\sigma)\leq 0$ always hold

---
##### Proof:

When $v_i$ changes by $\Delta v_i$, the corresponding change in energy is $$\Delta E = - \Delta v_i \sum _{j \neq i }T_{ij}v_j\tag{5}$$

Let $h_i = \sum _{j \neq i }T_{ij}v_j$,

If $h_i > 0$, $\Delta v_i = +1$; If $h_i <0$, $\Delta v_i = -1$. Thus $\Delta E < 0$ holds for every formula.

We give an input $V_0$, the energy will converge to a minima(a stored pattern $V^s$)

From this definition, we can know that $s' = s$, $v_i ^{s'}$ is stable and correspond to $V_i ^{s}$(we don't consider the noise from $s\neq s'$ terms), otherwise $v_i = 0$

---

#### All in All
$\mathcal M$ specifies Hopfield Network, because $\{E, T\}$ are parametrized by $\mathcal M$

# Read Function
Initialize a state Vector $\sigma^{(0)}$, idealy $T^\infty (\sigma^{(0)}) = \xi_i$, where $i \in \{1,\dots, n\}$

# Capacity

- $\xi^i \in \mathcal M=\{\xi^1,\dots,\xi^K\}$ is a random vector with N dimensions. For $j\in \{1,\dots,N\}$, $\{\xi_j^i \sim Ber(0.5)\}$ which are independent.

- Capacity is the maximum number $K$ of messages a Hopfield Network can store, s.t. for $i\in \{1,\dots, K\}, j\in \{1,\dots, N\}$, $Pr\{T_j(\xi^i)\ne \xi^i_j\}\le \alpha$. Denoted by $C_\alpha$

## Proof
>Given $i\in \{1,\dots, K\}, j\in \{1,\dots, N\}$, $Pr\{T_j(\xi^i)\ne \xi^i_j\}\le \alpha$. Denoted by $C_\alpha$

>Goal: $K$ or $C_\alpha$
From above we know:

$$T_j(\xi) = sign (\overset \sim W_j\xi) \tag 5$$

$$ W _j = \sum _{s=1} ^N (2 \xi _j^s -1)(2\xi^s -1)^\top \tag 6$$


$T_j (\xi ^i)= sign (\overset \sim W_j \xi^i) $

$W_j \xi^i \overset {\text{plug in (6)}}{=} \sum _{s=1}^K (2\xi^s_j-1)(2\xi^s -1)^\top $
$=\underbrace {(2\xi^i_j -1)(2\xi^i-1)^\top\xi^i} _{Signal - \text{1 item}} + \underbrace {\sum_{s\ne i}(2\xi^s_j-1)(2\xi^s-1)^\top \xi^i}_{Noise -\text{K-1 items}}$

$\text{Signal} = (2\xi^i_j -1)(2\xi^i-1)^\top\xi^i $
$(2\xi^i-1)^\top\xi^i = \sum_{n=1}^N(2(\xi_n^i)^2-\xi_n^i)=\sum_{n=1}^N\xi_n^i := m_i$
$\text{Signal} = (2\xi_j^i -1)m_i$

$\text{Noise} = \underbrace {\sum_{s \ne i}(2\xi_j^s-1)(2\xi^s -1)^\top\xi^i}_{\text{K-1 items}}$

$(2\xi^s -1)^\top\xi^i = \sum_{n=1}^N(2\xi^s_n -1)\xi_n^i = \underbrace {\sum_{n:\xi_n^i =1}(2\xi^s_n -1)}_{m_i \text{ items}}$

CLT, $(2\xi_n^s -1)$ does not affect the distribution.
$E(2\xi_n^s -1 ) = 0$, $Var(2\xi_n^s -1) = 1 $
$Noise \sim \mathcal N(0, (K-1)m_i)$

Now we want to substitude $W$ with $\overset \sim W$.
$Signal + Noise - W_{jj} \xi ^i$

$W_{jj}\xi^i =\sum_{s=1}^N(2\xi^s_j -1)(2\xi^s_j-1) \xi^i = N\xi^i$

plug this into signal term

$\text{Signal} = (2\xi _j^i -1)m_i - N\xi^i$
$\text{Noise} \sim \mathcal N (0, (K-1)m_i)$

$\text {P}(\text{sign}(\overset \sim W_j \xi^i))= \text{P}(\xi_j^i =1 )\text P (T_j(\xi _i =-1)|\xi_j^i =1) + 
\text{P}(\xi_j^i =-1 )\text P (T_j(\xi _i =1)|\xi_j^i =-1)$
# Other properties

**Consider the case where $T_{ij}$ is not symetric**. There are 3 results

1. settle into a stable state
1. The experiement would result in a cycle consequence
3. An chaotic wandering


**Robustness**. We can ensur that whether or not $T_{ij} \neq T_{ji}$ there are only stable limit points persist. We want to prove the stable points theory:

$$
\Delta E 
= -\frac{1}{2} \Delta v_i 
\left( 
\sum_{j \ne i} T_{ij} v_j 
+ 
\sum_{j \ne i} T_{ji} v_j 
\right)
$$

This can also be written as(we let $A +B = -A + \frac 1 2 (A-B)$):

$$
\Delta E 
= \underbrace{-\Delta V_i h_i}_{\text{always } \le 0}
+ 
\underbrace{\frac{1}{2}\Delta v_i \sum_{j \ne i} (T_{ij} - T_{ji}) v_j}_{\text{"stochastic" term}}\tag{6}
$$




### Genelization, Familiarity Recognition

Genelization happens when the memory is overloaded. 

- Familiar patterns cause slower neuron readjustments.
- Unfamiliar patterns cause faster readjustments 

### Categorization

close hamming distance? when talk about asymetric $T_{ij}$

### Error Correction

If we store a memory with length k less than N. we can determine the rest of neuron based on correlations


### Time sequence in nonsymmetric weight

Sequences longer than four states proved impossible to generate, and even these were not faithfully followed.