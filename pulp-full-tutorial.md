# Tutorial to run the PULP platform from scratch

## Introduction:

The objective is to present a step by step tutorial to configure the environment necessary to use the PULP (Parallel Ultra Low-power) platform. The recommended operating system is Ubuntu. The whole environment will occupy about 25 GB on hard drive.

## Step 1 and Step 2

Install and configure QuestaSim.

## Step 3: Running QuestaSim

``` bash
export PATH="$PATH:/proj/questasim_10.7c_linux64/questasim/linux_x86_64"
```

``` bash
export LM_LICENSE_FILE="/proj/questasim_10.7c_linux64/license.dat"
```

Open QuestaSim 10.7c with the following command:

``` bash
vsim
```

## Step 4: Installing Prerequisites

> One-line command: {

``` bash
sudo apt-get install git make python3 python3-venv python3-pip autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev
```
> }

Don't forget to run the bug correction.

> Detailed commands:

GIT:

``` bash
sudo apt-get install git
```

GNU Make:

``` bash
sudo apt-get install make
```

Python 3:

``` bash
sudo apt-get install python3
```

``` bash
sudo apt-get install python3-venv
```

``` bash
sudo apt-get install python3-pip
```

> BUG CORRECTION {

``` bash
pip3 install pyelftools
pip3 install numpy
```
> }

Other Packages:

``` bash
sudo apt-get install autoconf
```

``` bash
sudo apt-get install automake
```

``` bash
sudo apt-get install autotools-dev
```

``` bash
sudo apt-get install curl
```

``` bash
sudo apt-get install libmpc-dev
```

``` bash
sudo apt-get install libmpfr-dev
```

``` bash
sudo apt-get install libgmp-dev
```

``` bash
sudo apt-get install gawk
```

``` bash
sudo apt-get install build-essential
```

``` bash
sudo apt-get install bison
```

``` bash
sudo apt-get install flex
```

``` bash
sudo apt-get install texinfo
```

``` bash
sudo apt-get install gperf
```

``` bash
sudo apt-get install libtool
```

``` bash
sudo apt-get install patchutils
```

``` bash
sudo apt-get install bc
```

``` bash
sudo apt-get install zlib1g-dev
```

## Step 5: Installing the RISC-V GNU Compiler Toolchain

This is the RISC-V C and C++ cross-compiler. Download source with the following command:

``` bash
git clone --recursive https://github.com/pulp-platform/pulp-riscv-gnu-toolchain
```

``` bash
export PATH="$PATH:/proj/riscv/bin"
```

``` bash
cd pulp-riscv-gnu-toolchain
```

``` bash
./configure --prefix=/proj/riscv --with-arch=rv32imc --with-cmodel=medlow --enable-multilib
```

``` bash
make
```

This process will take a long time, approximately 1 hour and 30 minutes.

## Step 6: Downloading PULP

``` bash
cd /proj
```

``` bash
git clone https://github.com/pulp-platform/pulp.git
```

``` bash
cd pulp
```

``` bash
source setup/vsim.sh
```

``` bash
make checkout
```

``` bash
make scripts
```

> BUG CORRECTION {

``` bash
gedit /proj/pulp/sim/Makefile
Comment line 57
```
> }

``` bash
make build
```

## Step 7: Running the Hello World regression test on the PULP platform

``` bash
cd /proj
```

``` bash
git clone https://github.com/pulp-platform/regression_tests.git
```

``` bash
git clone https://github.com/pulp-platform/pulp-runtime.git
```

``` bash
source pulp-runtime/configs/pulp.sh
```

``` bash
export PATH="$PATH:/proj/riscv/bin"
```

``` bash
export PULP_RISCV_GCC_TOOLCHAIN="/proj/riscv"
```

``` bash
cd regression_tests/hello
```

``` bash
make clean all run
```
