

---
## Basic notion of Dense AM
Our goal is to define a DenseAM with discrete state vector, dicrest asunchronous updates.

The instaneous state of the AM is a colum vector $\sigma = (\sigma _1, \sigma_2,\dots, \sigma _N)$, for  $i =1,\dots, N$

Let $\xi^\mu$ be colum vectors in $\{-1,1\}^N \subset R^N$  with $ \mu = 1 \dots , K $. We call $\xi ^\mu$ a memory state.

$\mathcal M := \{\xi^1,\xi^2,\dots, \xi^k\} \subseteq \{-1,+1\}^N$
> we rewrite $\mathcal M$ as matrix ${\mathcal {\bar M}}\in \{-1,1\}^{N\times K}$

We define the energy function

$$E(\sigma; \Xi) = -\sum _{\mu=1}^K F(\xi^\mu \cdot\sigma) = - \langle \mathbf 1, F(\Xi \sigma)\rangle \tag{1}$$
> $F: R \rightarrow R$ is a function defining energy function, $\Xi = ({\xi^1 }^\top, \dots, {\xi^K}^\top)$ is a $K \times N$ matrices

### Update function

Def a single-step update function $T:R^N\rightarrow R^N$

$$\sigma^{(t+1)} = T(\sigma^t;{\mathcal {\bar M}}) = \text{Sign}[\Xi^\top f(\overset {\sim}{\Xi} \sigma ^{(t)})]\tag 2$$

For each element in $\sigma$, we have
$$ \sigma_i^{(t+1)} = \text{Sign}[\sum_{\mu =1}^K \xi_i^\mu f(\xi^\mu \cdot \sigma^{(t)}-\xi_i^\mu \sigma_i^{(t)})]= \text{Sign}[\langle \Xi_{\cdot i}, f(\Xi\sigma^{(t)}-\sigma_i^{(t)}\Xi_{\cdot i})\rangle] = $$
$$\text{Sign}[\langle \Xi_{\cdot i}, f(\overset \sim \Xi \sigma^{(t)})\rangle]
\tag 3$$
>Activation function $f(\cdot) = F'(\cdot)$, which is a derivatice of the function $F(\cdot)$ defining the energy function
> let $\overset \sim \Xi = \Xi$ with $i_{th}$ colum set to 0 

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
#### Building Blocks of AMs with Modular Energies
We design a modular energy perspective framework(general DAM)  HAMUX Comparing with DAM
1. discrete state vectors $\rightarrow$ continuous state vectors, which allows backpropagation training.
2. No hierarchy $\rightarrow$ Hierarchical structure to capture complex representations
3. The structure of energy function is too rigid $\rightarrow$ modular energy to allow more types of patterns and relationship the network can handle. 


Def **neuron layer(Node)** is a non-linear function( aka activation function) $\hat {\mathbf x} = f(\mathbf x)$, where $\mathbf x, \hat {\mathbf x} \in R^n$ 
> activations $\hat {\mathbf x} $ and pre-activation(input) $\mathbf x$.
> $f$ is monotonically increasing function of $x$ 

Def **Energy function of neuron layers $\mathbf x$** 

$$E_n(\mathbf x) = \mathcal T(\mathcal L_\mathbf x) = \langle f({\mathbf x}) , \mathbf x\rangle - \mathcal L_\mathbf x(\mathbf x) = \langle f(\mathbf x), \mathbf x\rangle - \langle \mathcal l(\mathbf x), \mathbf{1}\rangle \tag 6$$
 $\mathcal L_\mathbf x$ is a convex Lagrangian function, s.t. activation function
 > a convex scalar-valued Lagrangian $$\mathcal L_x$$ The Legendre transform $\mathcal T$ of this Lagrangian produces the dual energy

 [Proof $\mathcal L$ is convex function](#l-is-a-convex-function)
We can derive that
$$\frac {\partial E(\mathbf x)}{\partial \hat {\mathbf x}} = \mathbf x \tag 7$$
A nice property of dual energy : gradient of dual energy equals the hidden states
$$\frac{d \mathbf x}{d t}
= - \nabla_{\hat{x}} E_x(\hat{\mathbf x})
= -\mathbf x \tag 8$$



> > Think this as regurarization, i.e. exponential decay, which make neuron layers bounded

$$\hat{\mathbf x} = \nabla \mathcal{L}_\mathbf x(\mathbf x) \tag 9$$



we let $\mathcal L_x(\mathbf x) = \mathcal l(x_1)+ \mathcal l(x_2) + \dots \mathcal l(x_n) = \langle \mathcal l (\mathbf x), \mathbf 1 \rangle$

$l(x_i) = \int _{- \infty }^{x_i} f(t) dt$ where $i\in \{1,\dots, n\}$

---

Ex.
Let $f(\mathbf x)$ be a ReLu function 

let $\mathcal l: R\rightarrow R$
$$\mathcal l(x)= 
\begin{cases}
0, x\le 0 , \\
\frac 1 2 x^2, x>0
\end{cases}$$

we can easify find that $l'(x) = \text{Relu}(x)$

$\mathcal L(\mathbf x) = \mathcal l(\mathbf x [1]) + \mathcal l(\mathbf x[2])$

$$\text{Relu}(x)=
\begin{cases}
0, & x \le 0,\\
x, & x > 0.
\end{cases}$$

$\nabla \mathcal L(\mathbf x) = (\frac {\partial \mathcal L}{\partial \mathbf x[1]}, \frac {\partial \mathcal L}{\partial \mathbf x[2]}) = (\text{Relu}(\mathcal x[1]), \text{Relu}(\mathcal x[2])) = f(\mathbf x)$

---

Def **hypersynapse(Edge)** is a parameterized energy function that captures how similar or aligned the activations of its connected neuron layers are. 
> We can design different synptic energies that can determine what kind of relationship between nodes is enforcing : Conv, Pooling, or attention. 



A hypersynapse connecting neuron layers X and Y has an interaction energy $E_{xy}(\hat {\mathbf x}, \hat {\mathbf y}, W)$ which pull the connected neron layers toward configurations encoded in $W$ via update rules.
> $W$ represents the synaptic weights or learnable parameters

Hypersynapse in HAMUX vs real bio synaptic
1. Hypersynapses can connect any number of layers simultaneously
2. Hypersynapses are undirected

Self connection synaptic energy noted by $E_{\{x\}}$

Ex. Edge function
$E_{\mathbf x \mathbf y}(\hat {\mathbf x}, \hat {\mathbf y}; W)= \hat {\mathbf x}^\top W \hat {\mathbf y}$

where $W$ is a $N \times N$ matrice.

[General Form of Energy function](#general-form-of-energy-function)

---
##### Energy function of system

For a system of $L$ neuron layers and $S$ hypersynapses, the energy function of the system is

$$E_{total} = \sum_{l=1}^L E^{neuron layer}_l + \sum_{s=1}^SE_s^{synapse} \tag {10}$$

##### Update Rule

Let ${\mathbf {\hat x_\ell}}$ and $\mathbf x_\ell$ represent the activations and internal states of node $\ell$, and let $N(\ell)$ represents the set of edge that connect to node $\ell$. 

$$\tau_\ell  \frac {d\mathbf{x}} {dt} = - \frac  {\partial E_{total}} {\partial {\mathbf {\hat x_\ell}}}= -(\sum _{s\in N(\ell)}\frac {\partial E_s^{edge}}{\partial {{\mathbf {\hat x_\ell}}}})-\frac {\partial E^{node}_\ell}{\partial {\mathbf {\hat x_\ell}}} = \mathcal I_{x_\ell}-\mathbf x_\ell \tag {11}$$
> Time constant for node in layer i is denoted by $\tau_\ell$
>neuron layer $\ell$ receive signal $\mathcal I_{x_\ell}= -(\sum _{s\in N(\ell)}\frac {\partial E_s^{edge}}{\partial {{\mathbf {\hat x_\ell}}}})$
> when the activations ${\mathbf {\hat x_\ell}}$ are bounded, the above system is guaranteed to converge for any choice of ==hypersynapse energies==.

#### Energy Descent Dynamics

**Non-increasing thm**
$$\frac{dE_{\text{total}}}{dt}=\sum_{i=1}^{L}\frac{\partial E_{\text{total}}}{\partial \hat{x}_i}\frac{\partial \hat{x}_i}{\partial x_i}\frac{dx_i}{dt}=-\sum_{i=1}^{L}\tau_i\frac{dx_i}{dt}\frac{\partial^2 \mathcal{L}_x}{\partial x_i \partial x_i}\frac{dx_i}{dt}\le 0 \tag {12} $$

> The Hessian of $\mathcal L$ is positive semi-definite

- if the energy of the system is bounded below, the energy function are guaranteed to lead the trajectories to fixed manifolds corresponding to local minima of the energy
- If the Hessian of $\mathcal L$ is positive definite, the fixed manifolds have zero-dimension; i.e. manifolds are fixed point attractors. Alternatively, if the Lagrangians have zero mode, i.e. the Hessian matrices have zero eigen value, the energy function may converge to the fixed manifolds while the gradient $\nabla E \ne 0$.

#### Implementing AMs

##### Energy Transformer Block
Attention formula
$$\text{Attention}(Q,K,V) = \text{softmax}(\frac {QK^\top}{\sqrt d_k})V$$
> $d_k$ is the dimension of each key vector

Multi-Head Attention
$$\text{MultiHead} (Q,K,V) = \text{Concat}(\text{head}_1, \dots,\text{head}_h)W^O$$
where $\text{head}_i = \text{Attention} (QW_i^Q, KW_i^K,VW_i^V)$
> $W_i^Q \in R^{d_{model} \times d_k}$, $W_i^K \in R^{d_{model}\times d_k}$, $W_i^V \in R^{d_{model} \times d_v}$ and $W^O \in R^{hd_v \times d_{model}}$

we want to capture layernorm, attn, and mlp. 

---

##### MLP

Def a transformer with L blocks: input $\{\mathbf x_1^{(0)}, \dots, \mathbf x_N^{(0)}\}$ and output $\{\mathbf x_1^{(L)}, \dots, \mathbf x_N^{(L)}\}$, for each $\mathbf x _i^{(l)} \in R^D$

In traditional transformers, the MLP can be written as a two-layer feedforward network with a ReLU on the hidden activations. The MLP is parametrized by two weight matrice $\mathbf V, \mathbf W \in R^{M \times D}$. 

$$\text{MLP}(\hat {\mathbf x})_{B} = \langle W_{\cdot i}, \text{ReLU}(\langle V, \hat {\mathbf{x_B}}\rangle)\rangle $$
> $B = 1, \dots, N$

Which is similar to [Energy function](#update-function)

We let $V =W = \Xi$, This is exactly classic Hopfield network, since $\text{ReLU} = xß$

Layer Norm and Attn, see original paper

# Appendix

## L is a convex function

Since $f$ is mononitically increasing，we can easily get $\nabla f \ge 0$. 

Thus the Hessian of $\mathcal L \succeq 0$, we can easily know that $\mathcal L$ is positive definite.

## General Form of Energy Function

energy can be decomposed into three functional layers:

$$
E(\sigma) = - Q\left(\sum_{\mu=1}^{K} F\big(S(\xi^\mu,\sigma)\big)\right)
$$

where the computation proceeds as:

1. Similarity layer $$S(\xi^\mu,\sigma)$$

Example A — Dot product (Hopfield-style)

$$
S_\mu = \xi^\mu \cdot \sigma = \sum_{i=1}^N \xi_i^\mu \sigma_i
$$

Example B — Cosine similarity

$$
S_\mu = \frac{\xi^\mu \cdot \sigma}{|\xi^\mu||\sigma|}
$$

Example C — Negative Euclidean distance

$$
S_\mu = -|\sigma - \xi^\mu|^2
$$


2. Separation layer $$F(S)$$

Amplifies strong matches and suppresses weak ones.

Example A — Power nonlinearity

$$
F(S) = S^n, \quad n>2
$$

Example B — Exponential

$$
F(S) = e^{\beta S}
$$

Example C — Rectified power

$$
F(S) = \max(0,S)^n
$$

⸻

3. Global shaping layer $$Q(z)$$

Transforms the total evidence

$$
z = \sum_{\mu=1}^{K} F(S_\mu)
$$

into energy.

Example A — Linear

$$
Q(z) = z
$$

Example B — Logarithmic

$$
Q(z) = \log z
$$

Example C — Power

$$
Q(z) = z^p, \quad p>1
$$

⸻

Concrete model instantiations

Classical Dense Hopfield

$$
S_\mu = \xi^\mu \cdot \sigma
$$
$$
F(S) = S^2
$$
$$
Q(z) = z
$$
$$
E = -\sum_\mu (\xi^\mu \cdot \sigma)^2
$$

⸻

Modern Hopfield / Attention-like

$$
S_\mu = \xi^\mu \cdot \sigma
$$
$$
F(S) = e^{\beta S}
$$
$$
Q(z) = \log z
$$
$$
E = -\log \sum_\mu e^{\beta (\xi^\mu \cdot \sigma)}
$$

