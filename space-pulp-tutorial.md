 ---
 layout: default
 ---

 # Space Pulp Tutorial

  ## Install pulp-riscv-gnu-toolchain
  - Clone the repositories and submodules:
  `git clone --recursive https://github.com/pulp-platform/pulp-riscv-gnu-toolchain.git`
  - Install dependencies (Ubuntu 20.04):
  `sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk
  build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev`
  - Add install path to PATH:
  `export PATH=$PATH:/opt/riscv/bin`
  `./configure --prefix=/opt/riscv --with-arch=rv32imc --with-cmodel=medlow --enable-multilib`
  - Compile and install to `--prefix`:
  `sudo make`
  - Install `pyelftools`
  `sudo apt install python3-pip`
  `sudo pip3 install pyelftools`
 
  ## Michael's Space Pulp instructions
  - Clone my fork of the `pulp` repository (https://github.com/micprog/pulp) and check out the `space_pulp_tmp` branch.
  - There's also the cevero fork, just clone (https://github.com/cevero/pulp) and check out the `cevero-space-pulp-tmp` branch. This was created by:
      - Adding Michael's fork as a remote: `git remote add micprog https://github.com/micprog/pulp.git`
      - Creating a local branch named `cevero-space-pulp-tmp` and switching to it.
      - Pulling `micprog/space_pulp_tmp` into `cevero-space-pulp-tmp` with `git pull micprog space_pulp_tmp`
  - Here, run the following make targets to get the corresponding software with changes:
  `make pulp-runtime test-checkout-gitlab`
  - As I did all my development using bender for dependency management, before collecting
  dependencies first run `export BENDER=1`
  - Make sure your git is configured with github ssh keys;
  - To collect all dependencies and generate the corresponding scripts, run `make checkout`
  - To build, first set the correct paths by running `source setup/vsim.sh` and then run `make build`
  - To run a simulation, first source the correct runtime config by running
  `source pulp-runtime/configs/tcls_pulp_ibex.sh`
  - I currently set up one SW test to enable TCLS, to test this run `make -C regression_tests/parallel_bare_tests/parMatrixMul/ clean all run`
  - If you would like to inject faults into the simulation, the rather crude script can be enabled by
  running `export INJECT_FAULT=1` and disabled by running `unset INJECT_FAULT`
