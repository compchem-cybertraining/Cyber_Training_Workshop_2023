---
title: "6. NWChem"
---

<a name="toc"></a>
# Table of Content
1. [Generalities](#1) **June 20, morning**

    1.1. [Installation using a Package Manager](#1.1)

    1.2. [Building from Source](#1.2)

2. [Introduction to NWChem](#2) **June 20, morning**

3. [DFT in NWChem](#3) **June 20, morning**

4. [TDDFT in NWChem](#4) **June 20, afternoon**

5. [The GW approximation](#5) **June 21, morning**

6. [Correlated methods in NWChem](#6) **June 21, afternoon**

7. [Gaussian-basis MD (QMD) in NWChem](#7) **June 21, afternoon**

8. [Video Recordings](#8)
  
    8.1. [Morning Session, June 20](#8.1)

    8.2. [Afternoon Session, June 20](#8.2)

    8.3. [Morning Session, June 21](#8.3)

    8.4. [Afternoon Session, June 21](#8.4)




<a name="1"></a>[Back to TOC](#toc)
## 1. Generalities


<a name="1.1"></a>
### 1.1. Installation Using a Package Manager
An NWChem installation is available to all participants with access to UB CCR. 
The appropriate environment can be initialized by executing
```bash
eval "$(/projects/academic/cyberwksp21/Software/nwchem_conda0/bin/conda shell.bash hook)"
```
in a bash shell. In order to verify that the environment has been properly loaded,
check the output of the `which nwchem` command which should be :
```bash
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

<a name="1.2"></a>
### 1.2 Building from Source
The following set of instructions will result in an optimized NWChem binary
suitable for multi-node runs in UB CCR. Keep in mind that compiling NWChem from source 
can be a lengthy process.

*Note: the modules listed below are available using the new software infrastructure,
i.e. ~/.ccr_new_modules should exist.*

#### 1.2.1 Downloading NWChem source
The first step is to download the NWChem source. Here, we will download the
`master` branch into the user's home directory
```bash
cd ~
git clone --depth=1 https://github.com/nwchemgit/nwchem.git
```

#### 1.2.2 Setting Environment
We will start by setting the **mandatory** variables
```bash
export NWCHEM_TOP=$HOME/nwchem
export NWCHEM_TARGET=LINUX64
export NWCHEM_MODULES="all xtb"
export ARMCI_NETWORK=MPI-PR
export USE_MPI=1
```
The use of `ARMCI_NETWORK=MPI-PR` is recommended for best performance
as it reserves one MPI task per node for communication purposes.
`NWCHEM_MODULES="all xtb"` will compile all modules available in NWChem plus
an interface to the [TBlite](https://tblite.readthedocs.io/) library that 
enables xTB GFN1 and GFN2 calculations.

Next, we will define the **optional** variables
```bash
export USE_TBLITE=1
export USE_HWOPT=1
export USE_OPENMP=1
export USE_LIBXC=1
export USE_SIMINT=1
export SIMINT_MAXAM=5
export BUILD_PLUMED=1
export BUILD_SCALAPACK=1
export BUILD_ELPA=1
```
The variable `USE_TBLITE` must be set if `xtb` is present in `NWCHEM_MODULES`. 
Setting `USE_HWOPT=1` enables the use of hardware-specific optimizations.
Setting `USE_OPENMP=1` enables the use of OpenMP multithreading in some
modules.
Setting `USE_LIBXC=1` instructs NWChem to download and compile the
latest release version of LibXC.
Setting `USE_SIMINT=1` instructs NWChem to download and compile the 
[SIMINT](https://www.bennyp.org/research/simint/) library
supporting up to `h`-type functions (`SIMINT_MAXAM=5`).
Setting `BUILD_PLUMED=1` instructs NWChem to download and compile the
[PLUMED](https://www.plumed.org/) library to use enhanced-sampling 
algorithms in the Gaussian-basis AIMD module of NWChem.
Setting `BUILD_SCALAPACK=1` instructs NWChem to download and compile the
reference [ScaLAPACK](https://github.com/Reference-ScaLAPACK/scalapack) library.
Setting `BUILD_ELPA=1` instructs NWChem to download en compile the 
[ELPA](https://gitlab.mpcdf.mpg.de/elpa/elpa) eigensolver.

Finally, we need to load the desired compiler, MPI, and BLAS/LAPACK libraries. A common 
choice is the use the GNU compilers in combination with OpenMPI and Intel MKL
```bash
module load gcc/11.2.0
module load openmpi/4.1.1
module load imkl/2022.0.1
module load cmake/3.22.1
export LD_LIBRARY_PATH=${LIBRARY_PATH}:${CMAKE_LIBRARY_PATH}

export FC=gfortran
export CC=gcc
export CXX=g++
export BLAS_SIZE=8
export SCALAPACK_SIZE=${BLAS_SIZE}
export BLASOPT="-L${MKLROOT}/lib/intel64 -lmkl_gf_ilp64 -lmkl_gnu_thread -lmkl_core -lgomp -lpthread -lm -ldl"
export LAPACK_LIB=${BLASOPT}
```

If Intel compilers are chosen, then one can load the OneAPI components instead
```bash
module load intel/2022.00
module load cmake/3.22.1
export LD_LIBRARY_PATH=${LIBRARY_PATH}:${CMAKE_LIBRARY_PATH}

export FC=ifort
export CC=icc
export CXX=icpc
export BLAS_SIZE=8
export SCALAPACK_SIZE=${BLAS_SIZE}
export BLASOPT="-L${MKLROOT}/lib/intel64 -lmkl_intel_ilp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread -lm -ldl"
export LAPACK_LIB=${BLASOPT}
```

#### 1.2.3 Compiling
There were some issues while compiling the ELPA library due to 
a faulty `configure` script. If `USE_ELPA=1` is set, then
apply execute the following command
```bash
cd ${NWCHEM_TOP}/src/libext/elpa
patch <<'EOF'
--- original/build_elpa.sh      2023-06-19 01:14:12.659994922 -0400
+++ build_elpa.sh       2023-06-19 01:03:32.458119095 -0400
@@ -14,10 +14,11 @@
 else
     rm -rf elpa*
 echo    curl -L https://gitlab.mpcdf.mpg.de/elpa/elpa/-/archive/${VERSION}/elpa-${VERSION}.tar.gz -o elpa-${VERSION}.tar.gz
-    curl -L https://gitlab.mpcdf.mpg.de/elpa/elpa/-/archive/${VERSION}/elpa-${VERSION}.tar.gz -o elpa-${VERSION}.tar.gz
+#    curl -L https://gitlab.mpcdf.mpg.de/elpa/elpa/-/archive/${VERSION}/elpa-${VERSION}.tar.gz -o elpa-${VERSION}.tar.gz
+    curl -L https://elpa.mpcdf.mpg.de/software/tarball-archive/Releases/${SHORTVERSION}/elpa-${SHORTVERSION}.tar.gz -o elpa-${SHORTVERSION}.tar.gz
 fi
-tar xzf elpa-${VERSION}.tar.gz
-ln -sf elpa-${VERSION} elpa
+tar xzf elpa-${SHORTVERSION}.tar.gz
+ln -sf elpa-${SHORTVERSION} elpa
 cd elpa
 UNAME_S=$(uname -s)
 if [[ ${UNAME_S} == Linux ]]; then
@@ -112,7 +113,7 @@
 if [[  -z "${FORCETARGET}" ]]; then
 FORCETARGET="-disable-sse -disable-sse-assembly --disable-avx --disable-avx2  --disable-avx512  "
 fi #FORCETARGET
-if [[ "${USE_HWOPT}" == "1" ]] && [[ "${USE_HWOPT}" == "y" ]] &&[[ "${USE_HWOPT}" != "Y" ]] && [[ ${UNAME_S} == Linux ]]; then
+if [[ "${USE_HWOPT}" == "1" ]] || [[ "${USE_HWOPT}" == "y" ]] ||[[ "${USE_HWOPT}" == "Y" ]] && [[ ${UNAME_S} == Linux ]]; then
 if [[ ${UNAME_S} == Linux ]]; then
     CPU_FLAGS=$(cat /proc/cpuinfo | grep flags |tail -n 1)
     CPU_FLAGS_2=$(cat /proc/cpuinfo | grep flags |tail -n 1)
EOF
```

All the environment should now be ready to begin the NWChem compilation
```bash
cd ${NWCHEM_TOP}/src
make nwchem_config
make -j12 &> make.log &
```

More information about how to obtain and compile NWChem can be found on 
the [NWChem website](https://nwchemgit.github.io/Download). 


### 1.3 Running NWChem @ UB CCR

#### 1.3.1 Running conda binary
```bash
#!/bin/bash
#SBATCH --account=cyberwksp21
#SBATCH --partition=valhalla  --qos=valhalla
#SBATCH --clusters=faculty
#SBATCH -N 1
#SBATCH --ntasks-per-node=24
#SBATCH -C CPU-E5-2650v4
eval "$(/projects/academic/cyberwksp21/Software/nwchem_conda0/bin/conda shell.bash hook)"
mpirun -n ${SLURM_NTASKS} nwchem [input]
```

#### 1.3.2 Running native build
```bash
#!/bin/bash
#SBATCH --account=cyberwksp21
#SBATCH --partition=valhalla  --qos=valhalla
#SBATCH --clusters=faculty
#SBATCH -N 1
#SBATCH --ntasks-per-node=24
#SBATCH --cpus-per-task=1
#SBATCH -C CPU-E5-2650v4
module load gcc/11.2.0
module load openmpi/4.1.1
module load imkl/2022.0.1
export LD_LIBRARY_PATH=${LIBRARY_PATH}:${CMAKE_LIBRARY_PATH}

export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK}

srun --mpi=pmix_v4 --cpu-bind core \
       ${NWCHEM_TOP}/bin/LINUX64/nwchem [input]
```

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


<a name="8"></a>[Back to TOC](#toc)
## 8. Videorecordings

<a name="8.1"></a>
### 8.1. Morning Session, June 20
Zoom Recording

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=8c239f96-973c-48ce-b99c-b0270115c4c2
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

UB Recording
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=27d514b5-8293-4730-9efe-b01f012ccfa8
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="8.2"></a>
### 8.2. Afternoon Session, June 20
Zoom Recording 

<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=bf009b53-6245-4904-94a1-b0270154c966
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

UB Recording
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=b8f55f5e-9cd4-440b-8eef-b01f012db4b8
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="8.3"></a>
### 8.3. Morning Session, June 21

Zoom Recording
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=6a8f9f68-103b-40bf-829e-b0280110c612
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

UB Recording
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=726b72a8-e547-4246-a4bc-b01f012ccfc4
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>


<a name="8.4"></a>
### 8.4. Afternoon Session, June 21
Zoom Recording
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=f2ad3537-51ef-4b26-b14b-b02801402adb
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

UB Recording
<iframe src="https://ub.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=4d75e596-0ba2-4b9b-9998-b01f012db4d4
&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=false&interactivity=all" height="900" width="800" 
style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

