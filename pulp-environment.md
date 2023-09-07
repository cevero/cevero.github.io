# Configure your machine to develop/run the PULP/Cevero Project

## Introduction:

The objective is to present a step by step tutorial to configure the environment necessary to use the PULP (Parallel Ultra Low-power) platform. The recommended operating system is Ubuntu. The whole environment will occupy about 25 GB on hard drive.

### ⚠️ ATTENTION!! ⚠️
In all of the following commands, substitute `<YOUR-PATH>` with the paths you decided to use.

In the `pulp` VM we use `/opt` as `<YOUR-PATH>`, this requires root access to the machine. If you prefer, you can install it in your home folder and install it as a regular user.

## Step 1 and Step 2

Install and configure QuestaSim.

## Step 3: Running QuestaSim

Configure the paths to the QuestaSim files. This depends completely on the paths you used in Steps 1 and 2.

``` bash
export PATH="$PATH:<YOUR-PATH>/questasim_10.7c_linux64/questasim/linux_x86_64"
export LM_LICENSE_FILE="PATH TO LICENSE"
```

Open QuestaSim 10.7c with the following command:

``` bash
vsim
```

## Step 4: Installing Prerequisites

### Requirements

``` bash
sudo apt-get install git make python3 python3-venv python3-pip autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev
```

### Python modules
``` bash
pip3 install pyelftools
pip3 install numpy
```

## Step 5: Installing the RISC-V GNU Compiler Toolchain

This is the RISC-V C and C++ cross-compiler. Download source with the following command:

``` bash
git clone --recursive https://github.com/pulp-platform/pulp-riscv-gnu-toolchain
```

Enter the folder where you cloned the toolchain repository:
``` bash
cd pulp-riscv-gnu-toolchain
```

Decide where you want to install the toolchain, and replace the `<YOUR-PATH>` with it.
In the `pulp` VM it's installed in `/opt`. This location require *root* access.
Configure then make:

``` bash
export PATH=$PATH:<YOUR-PATH>/riscv/bin

./configure --prefix=<YOUR-PATH>/riscv --with-arch=rv32imc --with-cmodel=medlow --enable-multilib

make
```

This process will take a long time, approximately 1 hour and 30 minutes.
You can use the `-j` option followed by the number of threads of your computer, for example `make -j4`, to speed up the compilation.

## Step 6: Compile and run the PULP Platform

Follow the [PULP Compile and run test](pulp-tutorial) tutorial, adjusting the paths to where you installed your tools.
