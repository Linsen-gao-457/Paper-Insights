# Hopfield Network

📕 [paper link](https://pmc.ncbi.nlm.nih.gov/articles/PMC346238/)

Hopfield Network is a information storage system which have 3 functions:
1. [(Write)Store information](#write-function)

2. [(Read)Retrieve Information](#read-function)

3. [(State evolution)](#stable-evolution)


The instaneous state of the system is a Vector $V = (V_1, V_2, V_3, ...)$, for each $V_i \in V$ is a neuron with 2 states $V_i \in \{0, 1\}$. The neuron i adjust its state follow the rule below: 

$$
V_i \to 
\begin{cases}
1, & \text{if } \displaystyle\sum_{j \ne i} T_{ij} V_j > U_i, \\\\[8pt]
0, & \text{if } \displaystyle\sum_{j \ne i} T_{ij} V_j < U_i.
\end{cases}\tag{1}
$$
## Write Function

We are not directly writing the stored pattern into neurons - we are setting up a landscape in which that pattern become a statble points.

We build the storaged patterns $V^s: s \in {1,2,...,n}$. We build the strength of connection $T_{ij}$, following this prescription $T_{ij} = \sum _s (2 V_i ^s -1)(2 V_j ^s  - 1)$ with $T_{ii} = 0$ st $s' \in s$, $V_i ^{s'}$ is stable and correspond to $V_i ^{s'}$.

Learning Algorithm to learn matrice $T_{ij}$. 

$$
\Delta T_{ij} = [V_i(t) V_j(t)]_{\text{average}} \tag{2}
$$

Let's discuss how does the initial stored synaptic strength envolve to the final stroed synaptic strength.

We have $\Delta T_{ij} = [V_i(t) V_j(t)]_{average}$, so $T_{ij}$ is not fixed - it's gradually built by summing many small updates over time, thus we get $T_{ij} = \sum _t \Delta T_{ij} (t)$


When the network is exposed to a specific pattern $V^s$, we get $\Delta T_{ij}^{(s)} = [V^s_iV^s_j]_{average}$. Finally we get $T_{ij} = \sum _{s=1} ^n \Delta T_{ij} ^s = \sum _{s=1} ^n [V_i^s V_j^s]_{average}$

For the last step, we change the voltage from 0, 1 to -1 and 1. Then we get $$T_{ij} = \sum _s (2 V_i ^s -1)(2 V_j ^s  - 1)\tag{3}$$


Standard of encoding:
In biology, a nervous system preprocessed signals for efficient storage, the preprocessed inforamtion would appear random. So in our example, we'd like to decorrelate and make the stroed pattern "look random"

**How to wrtie memory into our netwrok?**

The system was started at each assigned nominal memory state(initialize all the neurons to the values of one stored pattern), and the state was allowed to evolve until stationary.

After inplement this coding, we can make other stored patter don't interface our current stored pattern.

$$H^{s'}_j = \sum _j T_{ij} V_j^{s'} = \sum_s (2V_i^s -1)[\sum_jV_j ^{s'}(2V_j^s -1)]$$

If $V^s == V^{s'}$, $H_i^{s'} \approx (2V_i ^{s'} * \frac N 2)$. else 0

## Stable Evolution

**Consider the special case $T_{ij} = T_{ji}$**, we define the energy function $$E = \frac 1 2 \sum \sum _ {i\neq j} T_{ij} V_i V_j\tag{4}$$

When $V_i$ changes by $\Delta V_i$, the corresponding change in energy is $$\Delta E = - \Delta V_i \sum _{j \neq i }T_{ij}V_j\tag{5}$$

Let $h_i = \sum _{j \neq i }T_{ij}V_j$,

If $h_i > 0$, $\Delta V_i = +1$; If $h_i <0$, $\Delta V_i = -1$. Thus $\Delta E < 0$ holds for every formula.

**Consider the case where $T_{ij}$ is not symetric**. There are 3 results

1. settle into a stable state
2. The experiement would result in a cycle consequence
3. An chaotic wandering


**Robustness**. We can ensur that whether or not $T_{ij} \neq T_{ji}$ there are only stable limit points persist. We want to prove the stable points theory:

$$
\Delta E 
= -\frac{1}{2} \Delta V_i 
\left( 
\sum_{j \ne i} T_{ij} V_j 
+ 
\sum_{j \ne i} T_{ji} V_j 
\right)
$$

This can also be written as(we let $A +B = -A + \frac 1 2 (A-B)$):

$$
\Delta E 
= \underbrace{-\Delta V_i h_i}_{\text{always } \le 0}
+ 
\underbrace{\frac{1}{2}\Delta V_i \sum_{j \ne i} (T_{ij} - T_{ji}) V_j}_{\text{"stochastic" term}}\tag{6}
$$

How do we get that the network can store only about 0.15N patterns.
$$H_i^s = \sum _{j\neq i} T_{ij}V_j^s =\underbrace{ \sum _{s' =1}^n V_i^{s'}V_j^{s'}V_j^s}_{T_{ij} =V_i^{s'}V_j^{s'}} = \underbrace{V_i^s \sum _{i\neq j} V_i^s (V_j^s)^2}_{\text{signal term when s = s'}}+\underbrace {\sum_{s' \neq s} V_i^{s'}V_j^{s'}V_j^s}_{\text{noise when s}\neq \text{s'}} \tag7$$
signal term: $H_i^s = V_i^s * \frac 1 2N$

**Stochastical process**

We find the mean and standard derivation of noise term: $\sigma = \sqrt{(n-1)N/2}$, $\mu = 0$
We want $\frac N 2 > \sigma$, solve this function we get $n <0.15$.

## Read Function

The inputs should be appropriately coded.

The input is the initialize $V(0)$

A representation suitable for Hopfield input is a binary, decorrelated feature-level pattern.

It must follow the same rule as the memory writing process.
