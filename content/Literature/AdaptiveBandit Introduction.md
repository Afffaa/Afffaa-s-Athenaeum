---
title: AdaptiveBandit Introduction
---

# AdaptiveBandit Introduction

- on why to use Computer Molecular Simulations
    - In computational biology, macroscopic measurements by computer simulations are obtained by simulating microscopic molecular systems made of the order of a hundred thousand DOF
    - Statistical mechanics tells us the analytical form of the equilibrium distribution given the macroscopic constraint of the environment, e.g., constant T, P, N
    - Therefore, the problem consists in generating samples from such a distribution

- Sampling in Molecular Simulations
    - Molecular Simulation methods have always been hampered by sampling limitations over the equilibrium distribution due to their computational cost
    - 2 Main Methods used to obtain samples are
        1. Molecular Dynamics (MD) - a numerical scheme where the propagator of the dynamical system is discretized in time and iterated for billions of steps, and
        2. Monte Carlo Sampling (MC) - where the Monte Carlo rule is used to draw samples from the distribution
    - These sampling methods are also commonly used in other fields to sample for arbitrary probability distributions, and many of the methods developed for molecular simulations have been exploited in such contexts later, for instance, _Umbrella Sampling_, _biased Monte Carlo Methods_, or _biased Molecular Dynamics like Replica Exchange_, _Steered MD_, _Metadynamics_, etc.
    - Progress in molecular simulation sampling has therefore shown its relevance to a broader field of problems
    - Recentlym a new generative method based on normalizing flows has proposed to sample from _Boltzmann Distribution

- Sampling Problems and Difficulties, Introducing MSMs
    - due to difficulties in determining the bias a priori, practically equivalent to having a good prior, _Unbiased Methods such as Adapative Sampling_ have been recently developed and used successfully
    - Similarly, due to the difficulty in generating good Monte Carlo moves, MD is almost always preferred to MC methods, largely due to the current efficiency of generating trajectories rooted in the capability of modern hardware
    - Specialized computer chips like _Anton_ have made it possible to run ling simulations of the order of hundreds of microseconds, sampling reversibly fast processes and exploring longer timescales
    - The Advent of GPUs and GPU Molecular Dynamics software was a notable improvement, greatly increasing the computational efficiency of simulations
    - This, combined with Markov State Models (MSMs), allowed us to reconstruct a complete statistical description of the full dynamical system from many shorter trajectories, obtaining a description that is equivalent to reversible sampling, once at convergence

- MSMs
    - Running not one but hundreds or thousands of simulation trajectories created a new opportunity to decide the starting conditions of the simulations to obtain the best equilibrium characterization at the minimal computational cost, i.e., _Adaptive Sampling_
    - Initially, Adaptive Sampling Algorithms were used to reduce the statistical uncertainty by choosing conformations that contributed the most to the error in the mean first passage of time of an MSM, eigenvalues, and eigenvectors, or by choosing low state populations
    - MSMs were also used to detect those conformations that were kinetically farthest to the starting point to the increase sampling of high-barrier transitions
    - Furthermore, similar algorithms appeared recently, which introduced prior knowledge to the selection criteria, seeking to further speed up the sampling toward equilibrium
    - One notable ex. is where contact information is used for _Protein Floding_ or _Bound state contacts in Protein-Ligand or Protein-Protein binding_
    - Other applications have used alternative geometric features, such as RMSD or pocket volume, to improve conformational exploration and to find cryptic pockets
    - It is also worth mentioning the _weighted-ensemble algorithms_, which distribute sampling across regions in a collective variable
    - In General, the adaptive sampling policy was always empirical, not based on any mathematical decision process, even though similarities have been recognized with the multi-armed bandit problem and Reinforcement Learning before

- Here,
    - we frame adaptive sampling in terms of a multi-armed bandit problem and propose _AdaptiveBandit_, and algorithm that uses an action-value function and an upper confidence bound selection algorithm, improving adaptive sampling's performance and increasing its versatility when faced against different free-energy landscapes
    - Our main goal is to provide strong fundamentals when facing exploration-exploitation dilemma by redefining it in terms of reinforcement learning, creating a solid framework from where to easily develop novel algorithms
    - _AdaptiveBandit_ is available in _HTMD_
