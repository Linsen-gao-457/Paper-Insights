# Writing to the Hopfield Memory via Training a Recurrent Network

TL;DR
We want to design an algorithm to design $W$ in classic hopfield via RNN named TRN.

Pros
1. Better noise revocer ability comparing with other existing writing protocols
2. The capacity of TRN is also SOTA

Cons
1. Complexity $\sim O(\exp ^N)$
## some basis concepts:

**Def** $\mathbf x \in \{\pm 1\}^N$ is the state vector.

**Def** Update function: $$x^{new}=f_W(x^{old})$$

**Def** message we want to store $\mathcal M = \{\xi^1,\dots, \xi^M\}\subseteq \{\pm 1\}^N$

---

## Different Writing protocols

### HOP
$$W := \sum _{m=1}^M [\xi^m](\xi^m)^\top - I_N$$

### PSE(pesudo-inverse protocol)
$$W_{ij} := \frac 1 N \sum_{m = 1}^M \sum _{m' = 1}^M \xi_i^m (Q^{-1})_{mm'}\xi ^{m'}_j \tag 2$$
>$Q_{mm'} = \frac 1 N \sum _{k=1}^N \xi_{k=1}^m \xi_{k'}^m$ and $(Q^{-1})_{mm'} = Q_{mm'}^{-1}$

pros:
1. Increase the capacity camparing with HOP protocol

cons:
1. Lose all appealing properties of classic hopfield network

### MPF(Minimun probability flow)
$$\min K(W)= \sum_{m=1}^M\sum_{x'\in \mathcal N(x^m)}\exp (\frac {E(\mathbf x^m)-E(\mathbf x')}{2})$$
> $\mathcal N(x)$ is the set of state vectors within Hamming distance one from $\mathbf x$ and $E$

Pros:
1. Keep the appealing properties of HN
2. Shape the region around such local minima so that no state within Hamming distance one from a message attains the same energy level as the message(Assuming the distance between any two message in $\mathcal M$ is larger than two)

