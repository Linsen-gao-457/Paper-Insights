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

The instaneous state of the system is a Vector $V = (v_1, v_2, v_3, ...v_N)$, for $i \in \{1, ...N\}$, $v_i$ is a neuron with 2 states $v_i \in \{0, 1\}$.

Let $V^1, V^2, \dots, V^n$ be colum vectors in $\{0,1\}^N \subset R^N$

Let $T$ be a $N \times N$ matrice. Here, $T_{ij}$(for $i,j \in \{1...N\}$) as the synaptic weight representing the strength of the connection from neuron $v_i$ to neuron $v_j$. 

$$T = \sum_{s=1}^n (2V^s - 1)(2V^s - 1)^{\top} \tag{1}$$


<a id="Strength Matrice"></a>

> We are not directly writing the stored pattern into neurons - we are setting up a landscape in which that pattern become a statble points.

> $T_{ii}=0$
---
After that we define the function $A_i(V)$ to update the state of neuron $v_i$:

Let $A_i(V)$ be a function mapping from $R^N \rightarrow R$, defined by 

$$
A_i(V) = 
\begin{cases}
1, & \text{if } \displaystyle\sum_{j \ne i} T_{ij} v_j > U_i \quad \text{or} \ <T_i,V>-T_{ii}V_i \geq U_i, 
\\\\[8pt]
0, & \text{if } \displaystyle\sum_{j \ne i} T_{ij} v_j < U_i \quad \text{or} \ <T_i,V>-T_{ii}V_i \leq U_i.
\end{cases}\tag{2}
$$
> Unless otherwise stated, we choose $U_i =0$

> $A_i : R^N \rightarrow R$ depends only on $T_i$

---

**Thm** Update neurons rules

For any $S = 1,2, \dots n$, any $i = 1,2,\dots N$

$$V_i^s = A_i(V^s) \tag{3}$$

Define energy function $E: R^N \rightarrow R^+$ as follow:

$$E(V) = \frac 1 2 V^TTV \qquad\forall V\in R^N\tag{4}$$

==new idea==: 
Define energy function $E: (R^N; R^{N\times N}) \rightarrow R^+$ also we can write it as fellow, $V \mapsto E(V;T)$:

$$E(V;T) = \frac 1 2 V^TTV \qquad\forall V\in R^N$$

Capacity Thm

Input to a neuron

 $Z = <T_{i}, V^{s'}> \overset {T_{ii} =0 }= \sum_s(2V_i^{s} - 1)[\sum_j V_j^{s'}(2V_j^s-1)]$ 
 
$ = \underbrace {(2V_i^{s'} - 1)[\sum_j V_j^{s'}(2V_j^{s'}-1)]}_{Siganl} + \sum_{s\neq s'}\underbrace {(2V_i^{s} - 1)[\sum_j V_j^{s'}(2V_j^s-1)]}_{Noise}$

Based on Central limit theorem, we can get 

$Z \sim N(0,\frac {nN}2)$

The amplitude of Signal is $|\frac N 2|$
So probability of the bit error in memory $P_{bit} = P[Z > \frac N 2]$

Errors happen in one state $E[Errors] = N\times P_{bit}=1 $
Thus we found that $n = 0.15N$
Proof:
Consider $V_j^{s'}\in \{0,1\}$ and $x_j^s \in \{-1,1\}$
$E(V_j^{s'}x_j^s)=0$, $Var(V_j^{s'}x_j^s)=0.5$
$\sum_j V_j^{s'}x_j^s \underbrace {\sim}_{i.i.d}\mathcal N(0,\frac n 2)$

We times $(2V_i^s -1)$ before $\mathcal N(0,\frac n 2)$, which does not change the distribution, thus we get $Z \sim N(0,\frac {nN} 2)$

---
**Thm** Energy decreasing rule

for any $V\in R^N$, let $V^{'} \in R^N$, such that 
$$
\begin{cases}
v_j^{'} =v_j, &\text{if } j\neq i
\\\\[8pt]
v_i^{'} = A_i(V)
\end{cases}
$$

$E(V^{'}) - E(V)\leq 0$ always hold

---
##### Proof:

When $v_i$ changes by $\Delta v_i$, the corresponding change in energy is $$\Delta E = - \Delta v_i \sum _{j \neq i }T_{ij}v_j\tag{5}$$

Let $h_i = \sum _{j \neq i }T_{ij}v_j$,

If $h_i > 0$, $\Delta v_i = +1$; If $h_i <0$, $\Delta v_i = -1$. Thus $\Delta E < 0$ holds for every formula.

We give an input $V_0$, the energy will converge to a minima(a stored pattern $V^s$)

From this definition, we can know that $s' = s$, $v_i ^{s'}$ is stable and correspond to $V_i ^{s}$(we don't consider the noise from $s\neq s'$ terms), otherwise $v_i = 0$

---
#### From biology perspectives to prove our math setting is correct
$$v_i =\sum _s T_{ij}v_j^{s} \thickapprox (2 v_i^{s} -1) \frac N 2$$

Learning Algorithm to learn matrice $T_{ij}$. 

$$
\Delta T_{ij} = [v_i(t) v_j(t)]_{\text{average}} \tag{6}
$$

Let's discuss how does the initial stored synaptic strength envolve to the final stroed synaptic strength.

We have $\Delta T_{ij} = [v_i(t) v_j(t)]_{average}$, so $T_{ij}$ is not fixed - it's gradually built by summing many small updates over time, thus we get $T_{ij} = \sum _t \Delta T_{ij} (t)$


When the network is exposed to a specific pattern $V^s$, we get $\Delta T_{ij}^{(s)} = [v^s_iv^s_j]_{average}$. Finally we get $T_{ij} = \sum _{s=1} ^n \Delta T_{ij} ^s = \sum _{s=1} ^n [v_i^s v_j^s]_{average}$

For the last step, we change the voltage from 0, 1 to -1 and 1. Then we get $$T_{ij} = \sum _s (2 v_i ^s -1)(2 v_j ^s  - 1)\tag{7}$$


Thus, from a biological perspective, we recover [Strength Matrice](#hopfield-network).

 
# Read Function

1. Capacity
2. Guranteed we can fech the right pattern(distance to define)





# Other properties

**Consider the case where $T_{ij}$ is not symetric**. There are 3 results

1. settle into a stable state
2. The experiement would result in a cycle consequence
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

### Capacity

How do we get that the network can store about 0.15N patterns befroe error in retrival process is severe.

$$H_i^s = \sum _{j\neq i} T_{ij}V_j^s =\underbrace{ \sum _{s' =1}^n V_i^{s'}V_j^{s'}V_j^s}_{T_{ij} =V_i^{s'}V_j^{s'}} = \underbrace{V_i^s \sum _{i\neq j} (V_j^s)^2}_{\text{signal term when s = s'}}+\underbrace {\sum_{s' \neq s} V_i^{s'}V_j^{s'}V_j^s}_{\text{noise when s}\neq \text{s'}} \tag7$$

signal term: $H_i^s = V_i^s * \frac 1 2N$


We find the mean and standard derivation of noise term: $\sigma = \sqrt{(n-1)N/2}$, $\mu = 0$

$H_i^s = signal + noise$

We want $signal =\frac N 2 > noise =\sigma$, solve this function we get $n <0.15N$.

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