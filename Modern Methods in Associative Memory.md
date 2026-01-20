

---
## Basic notion of Dense AM
Our goal is to define a DenseAM with discrete state vector, dicrest asunchronous updates.

The instaneous state of the AM is a colum vector $\sigma = (\sigma _1, \sigma_2,\dots, \sigma _N)$, for  $i =1,\dots, N$

Let $\xi^\mu$ be colum vectors in $\{-1,1\}^N \subset R^N$  with $ \mu = 1 \dots , K $. We call $\xi ^\mu$ a memory state.

$\mathcal M := \{\xi^1,\xi^2,\dots, \xi^k\} \subseteq \{-1,+1\}^N$
> we rewrite $\mathcal M$ as matrix ${\mathcal {\bar M}}\in \{-1,1\}^{N\times K}$

We define the energy function

$$E(\sigma; \mathcal {\bar M}) = -\sum _{\mu=1}^K F(\xi^\mu \cdot\sigma) \tag{1}$$
> $F$ is a function defining energy function

### Update function

Def a single-step update function $T:R^N\rightarrow R^N$

$$\sigma^{(t+1)} = T(\sigma^t;{\mathcal {\bar M}})\tag 2$$

For each element in $\sigma$, we have
$$ \sigma_i^{(t+1)} = \text{Sign}[\sum_{\mu =1}^K \xi_i^\mu f(\xi^\mu \cdot \sigma^{(t)}-\xi_i^\mu \sigma_i^{(t)})]
\tag 3$$
>Activation function $f(\cdot) = F'(\cdot)$, which is a derivatice of the function $F(\cdot)$ defining the energy function

Def $T^n: R^N\rightarrow R^N$, $\underbrace {T^n(\sigma)=T(T(\dots T(\sigma)))))))}_{\text{n times}}$

When n =$ +\infty$, $T^{\infty}(\sigma) = \lim_{n \to \infty} T^n(\sigma)$

All in all, $(\mathcal M,E,T)$ specifies an DAM with $\mathcal M$


### Information Storage Capacity
Here we want to use a strict math language to define capacity:
def given $\sigma ^{(0)}=f(\xi_i, \bar Z)$, there exist a maxmimal $K$, naming $K^{max}$, satisfying $Pr(\xi_i=T^\infty (\sigma^{(0)})) \ge \beta$. We call $K^{max}$, capacity $\alpha - \beta$ capcity.

>$\bar Z$ is a random vector with N dimension, and for each dimension, think $X = \sigma^t_i$, $Y = \sigma ^{(t+1)}_i$, $Z \sim Ber(\alpha)$ indenepdnent of $X$
>$$
Y = 
\begin{cases}
X, Z = 1\\
-X, Z = 0
\end{cases}\overset {\text{depends on how } Z \text{ is defined}}{=}(-1)^Z X
$$
We can also use another way to formulate this
$$
Y = 
\begin{cases}
X, \text{with probabilty }\alpha\\
-X, \text{with probabilty }1-\alpha
\end{cases}
$$
> $f$ is a function which can add noise to the original signal. $\bar Z$ is a random vector 
> $K^{max}$ depends on the specific choices for the stored memories, how to add noise $f$ and $\bar Z$, the torerance rate $\beta$

We assume that the patterns are drawn at random following the distribution below:

$$\xi_i^\mu =
\begin{cases}
+1, & \text{with probability } \tfrac{1}{2}, \\
-1, & \text{with probability } \tfrac{1}{2}.
\end{cases} \tag 4$$

> $E(\xi_i^\mu)=0$, $E(\xi_i^\mu \cdot \xi_j^\nu) =\delta^{\mu \nu}\delta_{ij}$

here the delta function is as below:
$$
\delta_{ij}=
\begin{cases}
1, i=j \\
0, i\ne j
\end{cases}
$$

$$
\delta^{\mu \nu}=
\begin{cases}
1, \mu=\nu \\
0, \mu \ne \nu
\end{cases}
$$

We initialize the state vector $\sigma = \xi^1$, this must be stable.

$$\sigma_i^{(t+1)}=\text{Sign}[ \underbrace {\xi_i^1f(\xi ^1 \cdot \xi^1 - \xi^1_i \xi^1_i)}_{Signal} +\underbrace {\sum _{\mu =2}^K \xi_i^\mu f(\xi^\mu\xi^1 -\xi^\mu_i \xi_i^1)}_{Noise}] \tag 5 $$

> $E(Noise) = 0$, $Var(Noise)=(K-1)\langle [f(\xi^\mu \cdot 1 -\xi^\mu_i)]^2\rangle)$

Here, we restrict $F(\cdot)=\frac 1 n (\cdot)^n$, $f(\cdot) =(\cdot)^{n-1}$, $n\in Z$

$$Var(\text{Noise})=(2n-3)!!KD^{n-1}$$

We tolerate $P_{error} <\alpha$, thus we get $K < K^{max} = \frac 1 {\alpha ^2(2n=3)!!}D^{n-1}$

---

General Dense AM - HAMUX
1. discrete $\rightarrow$ continuous
2. The structure of energy function is too simple: no hierarchy and too rigid

We design a modular energy. 

HAMUX is more fundamental than its specific software implement($\text {pytorch}\leftrightarrow \text{autograd}$)

Def Node is a non-linear function( aka activation function) $\hat x = f(x)$, where activations $\hat x$ and pre-activation $x$.

Def Edge is a parameterized energy function that captures how similar or aligned the activations of its connected neuron layers are. 
> We can design different synptic energies that can determine what kind of relationship between the activations of connected nodes is enforcing: 

For a system of $L$ nodes and $S$ edges, the energy function of the system is

$$E_{total} = \sum_{l=1}^L E^{node}_l + \sum_{s=1}^SE_s^{edge} \tag 5$$

Update Rule

Let ${\mathbf {\hat x_\ell}}$ and $\mathbf x_\ell$ represent the activations and internal states of node $\ell$, and let $N(\ell)$ represents the set of edge that connect to node $\ell$. 

$$\mathcal{T}_\ell  \frac {d\mathbf{x}} 2 = - \frac  {\partial E_s^{edge}} {\partial {\mathbf {\hat x_\ell}}}= -(\sum _{s\in N(\ell)}\frac {\partial E_s^{edge}}{\partial {{\mathbf {\hat x_\ell}}}})-\frac {\partial E^{node}_\ell}{\partial {\mathbf {\hat x_\ell}}} = \mathcal I_{x_\ell}-\mathbf x_\ell $$
> Time constant for node in layer i is denoted by $\mathcal T_\ell$
>$\mathcal I_{x_\ell}= -(\sum _{s\in N(\ell)}\frac {\partial E_s^{edge}}{\partial {{\mathbf {\hat x_\ell}}}})$
> when the activations ${\mathbf {\hat x_\ell}}$ are bounded, the above system is guaranteed to converge for any choice of edge energy(???)

