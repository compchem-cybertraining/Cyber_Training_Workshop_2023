---
title: "3. Nonadiabatic Dynamics and More with Libra"
---

<a name="toc"></a>
# Table of Content
1. [General overview of Libra](#1) - **June 12, morning**

    1.1. [Overview and Installation](#1.1)

    1.2. [Demonstrations](#1.2)

    1.3. [Videorecording of the session](#1.3)

2. [Theory and Practice of NA-MD with Libra](#2)  **June 12, afternoon**

    2.1. [Theoretical Introduction](#2.1)

    2.2. [NA-MD (TSH and Ehrenfest dynamics) for model Hamiltonians](#2.2)

    2.3. [Videorecording of the session](#2.3)

3. [NA-MD for atomistic systems](#3) **June 13, morning**

    3.1. [Overview of the NBRA workflow. step4 (dynamics) within the NBRA settings](#3.1)

    3.2. [Computing NACs in the MO basis with DFTB+](#3.2)

    3.3. [Mapping single-particle properties to the Slater-determinants picture](#3.3)

    3.4. [Complete example with DFTB+](#3.4)

    3.5. [Interfacing Libra with external codes](#3.5)

    3.6. [Videorecording of the session](#3.6)

4. [NA-MD for atomistic systems](#4) **June 13, afternoon**

5. [Additional material, in case we'll have extra time]

    5.1. [Exact dynamics via SOFT-DVR](#5.1)
  
    5.2. [Hierarchical Equations of Motion (HEOM)](#5.2)

    5.3. [Wavepackets and Quantum Trajectories with Adaptive Gaussians (QTAG)](#5.3)

    5.4. [Getting started with developing and testing NAMD methods in Libra](#5.4)



<a name="1"></a>[Back to TOC](#toc)
## 1. General overview of Libra. 


<a name="1.1"></a>
### 1.1. Overview and Installation (30 min)

[Slides](../files/Alexey_Akimov/Libra-June12.pdf)

This workshop will involve experience with Python-based software and packages. One that will be used extensively throughut 
the event is the [Libra](https://github.com/Quantum-Dynamics-Hub/libra-code/tree/devel) package developed by the 
[Akimov group](https://akimovlab.github.io/). 

Although Libra and some of its strong and weak dependencies are already installed on UB CCR and will be directly accessible via
the Jupyter notebooks on OnDemand, you may want/need to install them locally. Since most of the calculations we'll be doing 
are not too intensive computationally, runnig most of them on your laptop shall not be a problem. 

You may want to use this option, if you want to follow the hands-on exercises with Libra, but you have not been accepted as a fully-fledged 
participant (the participant without full access to UB CCR resources, which may be because of your geographic location at the moment).

Please follow the [installation instructions](https://github.com/Quantum-Dynamics-Hub/libra-code/tree/devel) to build the corresponding 
environment, install all needed dependencies and packages, and build and install the Libra code itself. **Make sure to use the "devel" branch**. 

<a name="1.2"></a>
### 1.2. Demonstrations (60 min)

  To start - clone thetutorials repository into your working directory

      git clone https://github.com/compchem-cybertraining/Tutorials_Libra.git

  Then let's explore these tutorials

  * [Basic algebra](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/3_linear_algebra/1_vector_matrix_cmatrix_basics/tutorial.ipynb)
  * [Matrix decompositions](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/3_linear_algebra/2_matrix_functions/tutorial.ipynb)
  * [Metropolis](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/7_special_functions/4_random_numbers/2_metropolis/tutorial.ipynb)
  * [Gaussian Kernel Algorithm](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/7_special_functions/2_gaussian_kernel_algorithm/tutorial.ipynb)
  * [Runge-Kutta for classical MD](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/2_integrators/1_runge_kutta_4th_order/tutorial.ipynb)
  * [Runge-Kutta for Liouville Eq](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/2_integrators/2_runge_kutta_4_for_Liouville/tutorial.ipynb)
  * [ML Basics](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/9_machine_learning/1_basics_of_mlp/tutorial.ipynb)
  * [ML Derivatives](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/9_machine_learning/2_ann_derivatives/tutorial.ipynb)
  * [CP2K input preparation](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/11_program_specific_methods/3_cp2k_methods/1_input_generator/tutorial.ipynb)
  * [QE: pdos, statistics, normal modes](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/11_program_specific_methods/2_qe_methods)
  * [Extended Huckel Theory: electronic structure, orbitals, and pDOS](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/5_electronic_structure/1_eht/1_compact/tutorial.ipynb)


<a name="1.3"></a>
### 1.3. Videorecording of the session

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=f3181766-b927-4cae-9bd4-b01f0121de1c
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="2"></a>[Back to TOC](#toc)
## 2. Theory and Practice of NA-MD with Libra

<a name="2.1"></a>
### 2.1. Theoretical Introduction  (120 min)

[Slides](../files/Alexey_Akimov/NAMD_theory-June12.pdf)

<a name="2.2"></a>
### 2.2. NA-MD (TSH and Ehrenfest dynamics) for model Hamiltonians (50 min + 50 min)

We will be working with these examples:

 * [Model Hamiltonians in Libra](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/8_model_hamiltonians/3_models/tutorial.ipynb)
 * [Running NA-MD with model Hamiltonians](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/6_dynamics/1_trajectory_based/9_model_revised/tutorial.ipynb)
 * [Various methods in Libra](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/1_trajectory_based/10_model_many_methods)
 

<a name="2.3"></a>
### 2.3. Videorecording of the session

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=5ef94ff1-b952-432e-967a-b01f016d9b71
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=c4805c09-e38a-4d95-87a2-b01f011d9684
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="3"></a>[Back to TOC](#toc)
## 3. NA-MD for atomistic systems, June 13, morning (Alexey Akimov)

<a name="3.1"></a>
### 3.1. Overview of the NBRA workflow. step4 (dynamics) within the NBRA settings (30 min)

 * [Slides](../files/Alexey_Akimov/NBRA_workflows-June13.pdf)

 * [Example](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/2_nbra_workflows/10_generic_step3_4)

<a name="3.2"></a>
### 3.2. Computing NACs in the MO basis with DFTB+  (30 min)

 * [Computing NACs](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/2_nbra_workflows/11_step2_dftb)

<a name="3.3"></a>
### 3.3. Mapping single-particle properties to the Slater-determinants picture (30 min)

 * [Mapping example](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/2_nbra_workflows/12_generic_mapping)

<a name="3.4"></a>
### 3.4. Complete example with DFTB+ (60 min)

 * [Complete example](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/2_nbra_workflows/13_complete_example)

<a name="3.5"></a>
### 3.5. Interfacing Libra with external codes (30 min)

 * [Interfaces with other codes](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/8_model_hamiltonians/2_interfaces_with_qchem_codes/tutorial.ipynb)

<a name="3.6"></a>
### 3.6. Videorecording of the session

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=4036db20-1374-4890-aeb2-b02001241b95
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=08d5b3a2-7729-49ce-8bb9-b01f012ccea9
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=67c70549-f7af-42df-a9e6-b02001640b57
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>




<a name="4"></a>[Back to TOC](#toc)
## 4. NA-MD for atomistic systems, June 13, afternoon (Mohammad Shakiba)


<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=59a812ef-0352-4743-a204-b02001645022
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="5"></a>
## 5. Additional material, in case we'll have extra time
[Back to TOC](#toc)

<a name="5.1"></a>
### 5.1. Exact dynamics via SOFT-DVR

  * [3_soft_propagation/tutorial](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/3_soft_propagation/tutorial.ipynb)

   the wrapped up SOFT simulation and cool visualization

<a name="5.2"></a>
### 5.2. Hierarchical Equations of Motion (HEOM)

  * [HEOM tutorial](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/3_heom/1_dynamics_and_lineshapes/tutorial.ipynb)


<a name="5.3"></a>
### 5.3 Wavepackets and Quantum Trajectories with Adaptive Gaussians (QTAG)

  * [1_gaussian/1_matrix_elements](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/1_gaussian/1_matrix_elements/tutorial.ipynb)
   
   computing matrix elements, exercises
 
  * [2_dvr_basics/tutorial](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/2_dvr_basics/tutorial.ipynb) 
   and [4_more/Tutorial1](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/4_more)

  * [QTAG basics](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/6_dynamics/5_qtag/1_basics/tutorial.ipynb)


<a name="5.4"></a>
### 5.4. Getting started with developing and testing NAMD methods in Libra
   
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=c147e6dd-9a88-475c-a6f9-b0270154cf88
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


