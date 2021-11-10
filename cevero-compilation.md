---
layout: default
---

# [](#header-1)CEVERO

The CEVERO comprises of a few forked repositories from the PULP Platform.
This tutorial assumes you are using a version of Modelsim or Questa for simulation.

You must install the PULP gcc in your system. Download the release from [pulp-riscv-gnu-toolchain](https://github.com/pulp-platform/pulp-riscv-gnu-toolchain) and add the folder to your PATH enviroment variable, so that the binaries are accessible in the terminal.

## [](#header-2)Configuring Environment

Clone the following repositories
```
git clone https://github.com/cevero/pulpissimo
git clone https://github.com/cevero/pulp-sdk 
git clone https://github.com/cevero/pulp-rt-examples
```

Read the README.md from the repositories and install any dependencies that are needed.

Run the following comands to configure the repositories to compile the PULP Platform with the CEVERO core.

```
cd pulpissimo/
source setup/vsim.sh
cd ..
# sourcing the sourceme.sh might result in error if the SDK has not been compiled yet.
# if so, just ignore this error, and compile the SDK
source pulp-sdk/pkg/sdk/dev/sourceme.sh
source pulp-sdk/configs/cevero.sh
source pulp-sdk/configs/platform-rtl.sh
```

You'll have to execute the comands above every time you restart your terminal and tries to compile the CEVERO. It's advisable to copy the comands to a script for ease of execution. If you copy these commands to a file, config.sh, for example, you should source it.

```
source config.sh
```

## [](#header-2)Compiling Hardware

In order to compile the project, first compile the SDK.

```
cd pulp-sdk
make all
```
Then compile the SoC
```
cd pulpissimo
./update-ips
cd sim/
make clean lib build opt
```


## [](#header-2)Simulating Hardware

Then, to simulate, first source the config.sh file, in order to execute the `source pkg/sdk/dev/sourceme.sh`
```
source config.sh
```
```
cd pulp-rt-examples
cd error-recovery
make clean all run
```

To use the Graphic Interface of the simulator, use
```
make clean all run gui=1
```

[back](./)



