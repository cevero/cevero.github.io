# PULP Compile and run test

## Step 1: Configuring Questa's environment variables:

If you are using the `pulp` VM, QuestaSim and the PULP RISCV Toolchain are already installed. The paths in this tutorial are based on the VM.

If you are following this tutorial on your own machine, adjust the paths to where you installed the tools!

To configure the access to these tools in your user, run the following commands:

```bash
# PULP Toolchain
export PULP_RISCV_GCC_TOOLCHAIN=/opt/riscv
export PATH="$PATH:/opt/riscv/bin"

# Mentor Questa
export LM_LICENSE_FILE=/opt/mentor/license.dat
export PATH=$PATH:/opt/mentor/questasim/linux_x86_64/
```

You should add these commands to the end of your `.bashrc` file, otherwise you'll have to run it every time you log in to the machine.

## Step 2: Downloading and compiling PULP

For this tutorial, create a `pulp-tutorial` folder in your home folder:
```bash
mkdir pulp-tutorial
```

Enter in the folder:
```bash
cd pulp-tutorial
```

Clone the PULP Project
``` bash
git clone https://github.com/pulp-platform/pulp.git
```

Enter the folder
``` bash
cd pulp
```

Source the tools configurations
``` bash
source setup/vsim.sh
```

Download the project's files
``` bash
make checkout
```

Generate scripts
``` bash
make scripts
```

>*BUG CORRECTION*
Comment line 57 in `pulp/sim/Makefile`, as it looks for a `modelsim.ini` file which does not exist (yet):

```bash
# @chmod +w modelsim.ini
```

Compile the project, you should get no errors.
``` bash
make build
```

## Step 3: Running the Hello World regression test on the PULP platform

In your `pulp-tutorial` folder clone the `regression_tests` and `pulp-runtime` repositories:

``` bash
git clone https://github.com/pulp-platform/regression_tests.git
```

``` bash
git clone https://github.com/pulp-platform/pulp-runtime.git
```

Source `pulp-runtime` configurations:
``` bash
source pulp-runtime/configs/pulp.sh
```

Set up the toolchain paths (unnecessary if you have followed Step 1!):
``` bash
export PATH="$PATH:/opt/riscv/bin"
export PULP_RISCV_GCC_TOOLCHAIN="/opt/riscv"
```

Enter the test source folder:
``` bash
cd regression_tests/hello
```

Compile and run (in Questa)!

``` bash
make clean all run
```
## Step 4: Done!

After some errors, warnings and debug output a `[STDOUT-CL31_PE0] Hello !` message must appear on the screen.

You can use the `regression_tests/hello` folder as a template to develop your own PULP applications. The code is run in the complete hardware simulation in Questa.
