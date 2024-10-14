---
title: AdaptiveBandit, Methods, MD Simulations
---

# MD Simulations

- The Configurational space of a Molecular System for MD Simulations is given by $\chi=\{ x=(r_1,...r_n)\in \mathbb{R}^{3N}\}$, where $N$ is the number of atoms of the system
- Experimental observables $O$ are measured as equilibrium expectations $<O>=\int O(x)\mu(x)dx$, where $\mu(x)$ is the equilibrium distribution
- the form of this distribution is known
  - for instancem the Boltzmann distribution in the canonical ensemble at temperature $T$ is

$$
\mu(x)=\frac{1}{Z}\exp{-\frac{U(x)}{k_B T}} \qquad Eq.1
$$

> [!INFO] $Eq.1$ Parameters
> where
> - $U(x)$ is the molecular potential energy
> - $k_B T$ is the Boltzmann constant multiplied by the Temperature,
> - and $Z$ is the normalization factor

- MD Numerically solves Newton's eq. over the potential $U(x)$ for the variable $x$, plus a Langevin stochastic term accounting for thermal fluctuations
- Now consider the state $x(t)\in \chi$ as a specific conformation inside the configurational space $\chi$ at time $t$
- the probability of finding the molecule in configuration $x_{t+\tau}$ at a later time can be expressed by the conditional transition density function $p_\tau$, $x_{t+\tau} \sim p_\tau(x_{t+\tau}|x_t)$, which describes the probability of finding state $x_{t+\tau}$ given state $x_t$ at time $t$ after a time increment $\tau$

When performing an MD simulation,
- the dynamics of the molecular system propagates the state $x_t$ across time
- Therefore, MD samples from the transition density $p_\tau$ given discrete time steps $\tau$ to obtain the next state $x_{t+\tau}$
- this process is repeated for many steps, generating a trajectory of conformations

The main goal of performing MD simulations
- is to obtain a good representation of the system's equilibrium distribution $\mu(x)$, i.e., the probability to find conformation $x$ under equilibtrium conditions, to measure the average of observable $<O>$
- if an MD trajectory $\tau$ is long enough, sampling from $p_\tau$ is equivalent to sampling from $\mu(x)$

$$
\lim_{\tau \to \infty} p_\tau(x_{t+\tau}|x_t)=\mu(x) \qquad Eq.2
$$

- generating long enough trajectories is computationally expensive, and often practically impossible when trying to sample slow events
- However, long trajectories can be substituted by short parallel trajectories
- while in principle one could model directly the conditional probability in $E1.2$, in practice this is not possible due to the very high dimensional space
- fortunately, it can be shown that the dynamics can be separated into a slow and fast set of variables, and b/c the contributions of fast variables decay exponentially in $\tau$, a reliable MSM can be constructed in terms of the slow variables to compute the thermodynamic averages
- usually, time-independent component analysis (tICA) and clustering methods are used to study this set of variable during sampling, which is necessary to build the MSM
- one we obtain the MSM, computed by estimating the transition probabilities from discrete conformational states, one can derive the thermodynamics and kinetic properties, just assuming local, not global, equilibrium (i.e., $\tau$ is much shorter than what is necessary to satisfy $Eq.2$)
