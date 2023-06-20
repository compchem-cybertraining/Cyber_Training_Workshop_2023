---
title: "7. TT-SOFT and TT-Chebyshev"
---

<a name="toc"></a>
# Table of Content


##1. Theory of Quantum Dynamics with TT-SOFT and TT-Chebyshev, IPA Optimization

###1.1 Introduction

Quantum dynamics faces the "curse of dimensionality," in which computational cost grows exponentially as the dimensionality increases. 
This problem makes standard grid-based quantum dynamics and global optimization untenable for all but the smallest molecular systems. 
Data-compression techniques based on tensor networks significantly reduce the cost of such computations, which brings a wider range of molecular 
simulations within reach of existing computational resources and enables their simulation on individual personal computers.
The low computational cost of these methods allows the codes presented in this session to be run either on personal computers or on a 
single core on clusters/cloud-based resource. We will run codes today on Google Colaboratory. Slides will include information on how to run 
programs on CCR/clusters/personal computers.

[Google Colaboratory](https://colab.research.google.com/?utm_source=scs-index#)
[Colab Python Tutorial](https://colab.research.google.com/github/cs231n/cs231n.github.io/blob/master/python-colab.ipynb)
To save a personal copy of Colab files: File -> Save a copy in drive -> Open in new tab

###1.2 Tensor Trains in Chemistry
Slides - Tensor networks and their applications to molecular systems

###1.3 Tensor-Train Multilinear Algebra
Slides - Brief overview of tensor network operations

###1.4 Tensor-Train Quantum Dynamics
Slides - Mathematics of TT-SOFT and TT-Chebyshev

###1.5 Tensor-Train Global Optimization
Slides - Mathematics of IPA

##2. Hands On with TT-SOFT and TT-Chebyshev, IPA Optimization

###2.1 Practical Computation with Tensor Trains
[TT Tutorial](https://colab.research.google.com/drive/1gFecN0WpGaKtUCQl3-xjIl5csqoe5K37?usp=sharing)
[TT Image](https://colab.research.google.com/drive/15gpyKuY9mp9t1PhIwRmxB4MgpFqQF17u?usp=sharing)
Exercise: Image compression (texture, file size, color range)

###2.2 TT-SOFT
[Complete Code](https://github.com/michelinesoley/HBT)
[Tutorial Code](https://colab.research.google.com/drive/1PbPXJUbH5Vusrwrxyc63MZ18KdpfUd-K?usp=sharing)
Exercises: (1) Calculations for varying initial position and dimensionality, (2) Energy and norm-based benchmarking, alternate potential energy surfaces

###2.2 TT-Chebyshev
[Complete Code](https://github.com/michelinesoley/FTTC)
[Tutorial Code](https://colab.research.google.com/drive/1-JOG0owjM21JUebFWLqS6H3Kk56ej4pF?usp=sharing)
Exercises: (1) Calculation for varying dimensionality, determination of wavepacket dynamics, (2) Dependence on the number of Chebyshev polynomials, time-step dependence, alternate potential energy surfaces

###2.3 IPA
[Code](https://colab.research.google.com/drive/1u2HM49BzVcN7O9xSMjLFkzmqT1TcQPn7?usp=sharing)
Exercises: (1) Global optimization, free potential choice, (2) Quantics tensor trains, prime factorization
