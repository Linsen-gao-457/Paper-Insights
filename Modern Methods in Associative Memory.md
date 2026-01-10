Questions:
1. What's novel Lagrangain formulations?
2. What's associative memories?
3. Engineer memory or general memory?
4. How to unify different non-linearities?
Why legendre Transform is Energy?

---
Our goal is to define a DenseAM with discrete state vector, dicrest asunchronous updates.

The instaneous state of the AM is a colum vector $\sigma = (\sigma _1, \sigma_2,\dots, \sigma _N)$, for  $i =1,\dots, N$

Let $\xi^\mu$ be colum vectors in $\{0,1\}^N \subset R^N$  with $ \mu = 1 \dots , K $. We call $\xi ^\mu$ a memory state.

We define the energy function

$$E(\sigma) = -\sum _{\mu=1}^K F(\xi^\mu_i\sigma) \tag{1}$$
> $F$ is a function defining energy function

==Energy or energy function?==

Update Rule

$$ \sigma_i^{(t+1)} = \text{Sign}[\sum_{\mu =1}^K f(\xi \sigma^{(t)}-\xi_i^\mu\sigma_i^{(t)})]
\tag 2$$
>Activation function $f(\cdot) = F'(\cdot)$, which is a derivatice of the function $F(\cdot)$ defining the energy function


---