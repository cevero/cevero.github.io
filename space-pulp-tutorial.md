 # Space Pulp Tutorial
  ## Questasim setup
  1.  Unpack questa.tar.gz:
  `tar xf questa.tar.gz`
  2. Execute and install as "All platforms":
  `sudo ./install.linux64`
  3. Execute the magical stuff using wine:
  `wine MentorKG.exe -patch <install_path> -pkg <path_to_lib/mgc.pkginfo>  -o license.dat`
  Instal path is where you can find the vsim executable. On linux, it should be inside /questasim/linux_x86_64. The mgc.pkginfo is in the install_path/mgls/lib.
  Example install path: `/opt/questa/`
  `wine MentorKG.exe -patch /opt/questa/questasim/linux_x86_64/ -pkg /opt/questa/questasim/linux_x86_64/mgls/lib/mgc.pkginfo -o license.dat` 
  4. Run the command to export the LM_LICENSE_FILE. This is the location of the license.dat generated in the last command:
  `export LM_LICENSE_FILE=<license_location>`
  5. Then run the sfk command. SFK is a linux utilitary called Swiss File Knife.
  `./sfk rep -yes -pat -bin /5589E557565381ECD00000008B5508/31C0C357565381ECD00000008B5508/ -bin /5589E557565381ECD8000000E8000000005B81C3/33C0C357565381ECD8000000E8000000005B81C3/ -bin /41574989FF415641554154554889CD534489C3/33C0C389FF415641554154554889CD534489C3/ -dir <path_to_mgls/lib>`

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