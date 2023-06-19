---
title: "6. NWChem"
---

<a name="toc"></a>
# Table of Content
1. [Generalities](#1) **June 20, morning**

    1.1 [Installation](#1.1)

2. [Introduction to NWChem](#2) **June 20, morning**

3. [DFT in NWChem](#3) **June 20, morning**

4. [TDDFT in NWChem](#4) **June 20, afternoon**

5. [The GW approximation](#5) **June 21, morning**

6. [Correlated methods in NWChem](#6) **June 21, afternoon**

7. [Gaussian-basis MD (QMD) in NWChem](#7) **June 21, afternoon**


<a name="1"></a>[Back to TOC](#toc)
## 1. Generalities


<a name="1.1"></a>
### 1.1. Installation
An NWChem installation is available to all participants with access to UB CCR. 
The appropriate environment can be initialized by executing
```bash
eval "$(/projects/academic/cyberwksp21/Software/nwchem_conda0/bin/conda shell.bash hook)"
```
in a bash shell. In order to verify that the environment has been properly loaded,
the following output should be obtained by the `which nwchem` command:
```bash
$ which nwchem
/projects/academic/cyberwksp21/Software/nwchem_conda0/bin/nwchem
```

Please note that the conda-based installation is suitable for 
single-node calculations but *there is* a performance impact as 
compared to native builds or containers with other
optimizations enabled.


For those who want to install NWChem in their local machines,
the following code snippet will download the miniconda package
and install NWChem in a clean environment. We strongly suggest
to avoid installing NWChem in a pre-existing conda environment,
as it could lead to some incompatibilities with `mpi` libraries.
```bash
mkdir -p ~/conda 
cd ~/conda 
wget https://repo.anaconda.com/miniconda/Miniconda3-py38_23.1.0-1-Linux-x86_64.sh 
bash Miniconda3-py38_23.1.0-1-Linux-x86_64.sh -b -p ~/conda/miniconda3 
eval "$(~/conda/miniconda3/bin/conda shell.bash hook)" 
conda install -c conda-forge -y micromamba  
micromamba activate ~/conda/miniconda3   
eval "$(micromamba shell hook --shell=bash)" 
micromamba install -c conda-forge -y nwchem=7.2.0
```

Alternatively, NWChem can be installed using `homebrew` using the 
following commands
```bash
bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew install nwchem
```

More information about how to obtain NWChem can be found on 
the [NWChem website](https://nwchemgit.github.io/Download). 

<a name="2"></a>[Back to TOC](#toc)
## 2. Introduction to NWChem

[Slides](../files/NWChem/1_NWChem_intro_2023.pdf)


<a name="3"></a>[Back to TOC](#toc)
## 3. DFT in NWChem

[Slides](../files/NWChem/2_NWChem_DFT_2023.pdf)


<a name="4"></a>[Back to TOC](#toc)
## 4. TDDFT in NWChem

[Slides](../files/NWChem/3_NWChem-TDDFT-2023.pdf)


<a name="5"></a>[Back to TOC](#toc)
## 5. The GW approximation: Theory and hands-on

[Slides](../files/NWChem/4_NWChem_GW.pdf)


<a name="6"></a>[Back to TOC](#toc)
## 6. Correlated methods in NWChem

[Slides](../files/NWChem/5_CorrelatedMethods_2023.pdf)


<a name="7"></a>[Back to TOC](#toc)
## 7. Gaussian-basis MD (QMD) in NWChem

[Slides](../files/NWChem/6_NWChem_QMD_2023.pdf)


