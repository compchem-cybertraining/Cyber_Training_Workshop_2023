---
title: "5. Spin-Restricted Ensemble-Referenced Kohn-Sham (REKS) Method: Practical Implementation of Ensemble DFT Methodology"
---

<a name="toc"></a>
# Table of Content
1. [Theory: Introduction in ensemble DFT and basic aspects of REKS method for ground electronic states](#1) - **June 16, morning**

   1.1. [The concept of electron correlation](#1.1)

   1.2. [Dynamic vs non-dynamic correlation](#1.2)

   1.3. [Examples of strong non-dynamic correlation](#1.3)

   1.4. [Density functional theory and Kohn-Sham method](#1.4)

   1.5. [Ensemble DFT](#1.5)

   1.6. [Practical implementation of eDFT in REKS(2,2) method](#1.6)

   1.7. [Extension of REKS method beyond (2,2) active space](#1.7)

   1.8. [Examples of application of REKS method to bond dissociation](#1.8)

   1.9. [Videorecordings](#1.9)

2. [Hands on: REKS implementation in GAMESS-US; Demos and practical exercises with REKS method for strongly correlated molecular ground states](#2) - **June 16, afternoon**

   2.1. [Overview of REKS implementation in GAMESS-US](#2.1)

   2.2. [Interfacing GAMESS-US with DL-FIND](#2.2)

   2.3. [Environment setup and submitting jobs in SLURM](#2.3)

   2.4. [Practical example: TME diradical](#2.4)

   2.5. [Optimization of ground state minima with DL-FIND](#2.5)

   2.6. [Optimization of NEB path with DL-FIND](#2.6)

   2.7. [Videorecordings](#2.7)

3. [Theory: Ensemble DFT for excited states and its implementation in state-averaged REKS methodology](#3) - **June 19, morning**

   3.1. [Excited states and non-adiabatic dynamics](#3.1)

   3.2. [DFT and excited states](#3.2)

   3.3. [Ensemble DFT for excited states](#3.3)

   3.4. [Practical implementation of eDFT in SA-REKS and SSR methods](#3.4)

   3.5. [Applications of SSR method](#3.5)

   3.6. [SSR method with extended active space](#3.6)

   3.7. [Videorecordings](#3.7)

4. [Hands on: Practical exercises with GAMESS-US and NAMD simulations with GAMESS/pyUNI-xMD package](#4) - **June 19, afternoon**

   4.1. [Excited state decay in PSB3](#4.1)

   4.2. [pyUNI-xMD and its interface with SSR/GAMESS-US](#4.2)

   4.3. [Optimization of S<sub>0</sub> and S<sub>1</sub> stationary points (SSR/DL-FIND)](#4.3)

   4.4. [Setting up initial conditions (Newton-X)](#4.4)

   4.5. [Preparing the input data for pyUNI-xMD](#4.5)

   4.6. [Running the simulations](#4.6)

   4.7. [Videorecordings](#4.7)


<a name="1"></a>[Back to TOC](#toc)
## 1. Theory: Introduction in ensemble DFT and basic aspects of REKS method for ground electronic states. (180 min)
[Slides](../files/Michael_Filatov/REKS-June16.pdf)

UB Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=f0575c9e-c0b9-4785-b03a-b01f012ccf55
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

Zoom Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=19949e7d-c787-409f-ac74-b023012e02d8
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="2"></a>[Back to TOC](#toc)
## 2. Hands on: REKS implementation in GAMESS-US; Demos and practical exercises with REKS method for strongly correlated molecular ground states
[Slides](../files/Michael_Filatov/HandsOn.pdf)

<a name="2.1"></a>
### 2.1. Overview of REKS implementation in GAMESS-US
[See also](../files/Michael_Filatov/note_about_reks.pdf)[ and ](../files/Michael_Filatov/reks_gamess_synopsis.pdf)
[REKS keywords](../files/Michael_Filatov/reks_gamess_input.txt)

<a name="2.3"></a>
### 2.3. For environment setup and sample files, refer to /projects/academic/cyberwksp21/Software/mfilatov
<a name="3"></a>[Back to TOC](#toc)

UB Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=b0b71fca-f1e2-4116-8da1-b01f012db483
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


Zoom Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=64b11842-467a-40d6-a18e-b024000dc741
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


## 3. Theory: Ensemble DFT for excited states and its implementation in state-averaged REKS methodology (180 min)
[Slides](../files/Michael_Filatov/REKS-June19.pdf)
<a name="4"></a>[Back to TOC](#toc)


UB Recording 

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=51abff80-5340-457b-a7d4-b01f012ccf86
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

Zoom Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=92422f4f-b427-49a5-9325-b026011ecdd9
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


## 4. Hands on: Practical exercises with GAMESS-US and NAMD simulations with GAMESS/pyUNI-xMD package
[Slides](../files/Michael_Filatov/HandsOn.pdf)

UB Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=fb726f7d-c822-469c-822f-b01f012db4a2
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

Zoom Recording 

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=c82c5523-9373-4be6-baed-b026014e0087
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>
