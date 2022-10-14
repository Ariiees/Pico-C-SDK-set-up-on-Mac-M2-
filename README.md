# Pico C SDK set up on Mac

## Machine Details
**OS:** macOS Monterey (version 12.6)

**Chip:** Aoole M1 Pro

**Memory:** 16GB

**Serial Number** TNXP7CF44H

## Installed Software
1.Terminalx86

2.`homebrew`

3.`cmake`

4.`ArmMbed/homebrew-formulae`

5.`arm-none-eabi-gcc`

## Step by Step Guide

### Sept 1: Creat Terminalx86
Right click `Terminal` in **Finder/Applications/Utilities**, select **Duplicate**

<img width="600" alt="image" src="https://user-images.githubusercontent.com/87698138/194957529-d6d67b12-ae6c-4c20-9ce2-97e7d075d4bc.png">

Rename the new duplicated Terminal to `Terminalx86`

Right click on `Terminalx86` and select **Get Info**

<img width="350" alt="image" src="https://user-images.githubusercontent.com/87698138/194957912-a154ad56-1924-47a3-9c20-95860d546b86.png">

Click on **Open using Rosetta** in **General**

<img width="267" alt="image" src="https://user-images.githubusercontent.com/87698138/194958076-de599e45-2fad-46c4-9d88-8dba3c80c816.png">

### Step 2: Install related software through Terminalx86

Install `homebrew` in `Terminalx86`

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

Then install the toolchain.

```
$ brew install cmake
$ brew tap ArmMbed/homebrew-formulae
$ brew install arm-none-eabi-gcc
```

### Step 3: Get the SDK and examples

Create a pico directory at **/howe/pi/pico**, run the following command in `Terminalx86`

```
$ cd ~/
$ mkdir pico
$ cd pico
```

You can verify it in Finder, follow the path **Macintosh HD/Users/(Your user name)**

<img width="600" alt="image" src="https://user-images.githubusercontent.com/87698138/194960268-b214ccdc-e74c-4601-9481-c423bb335475.png">

Then clone the **pico-sdk** and **pico-examples** git repositories.

```
$ git clone -b master https://github.com/raspberrypi/pico-sdk.git
$ cd pico-sdk
$ git submodule update --init
$ cd ..
$ git clone -b master https://github.com/raspberrypi/pico-examples.git
```

You can verify it in Finder, follow the path **Macintosh HD/Users/(Your user name)/pico**

<img width="600" alt="image" src="https://user-images.githubusercontent.com/87698138/194960417-6e7fc3ab-e4b5-4dd7-b888-050feb570dbe.png">

### Step 4: Building with CMake Tools

Run following command through `Terminalx86` to create a new folder called `build` under the folder `pico-examples`

```
$ cd pico examples
$ mkdir build
$ cd build
```

Then set the **PICO_SDK_PATH** environment variable.

`$ export PICO_SDK_PATH=../../pico-sdk`

### Step 5: Build "Hello World"

Change directory into the **hellow_world** directory inside the **pico-examples/build** tree and run make.

```
$ cmake ..
$ cd hello_world
$ make -j4
```

Connect RP2040 to your laptop using a micro-USB cabel. **Hold down `BOOTSEL` button and then hold `RESET` button and then releas `RESET` button, when you find the Mass Storage Device shown on your screen, release `BOOTSEL`**

<img width="160" alt="image" src="https://user-images.githubusercontent.com/87698138/194962292-9a9785c9-c12a-4c56-8ffa-89fa7b5bb9f8.png">

<img width="600" alt="image" src="https://user-images.githubusercontent.com/87698138/194962600-1d762083-5c36-40e1-a757-48fd362642d4.png">

Drag and drop `hello_usb.uf2` onto the `RPI-RP2` and `RPI-RP2` will eject automatically.

### Step 6: Check the results in Serial Console
Run following command in your Terminal

```
$ ls /dev/tty.*
$ screen /dev/tty.board_name 115200
```

Then you will see the **hello world** in the console

<img width="473" alt="image" src="https://user-images.githubusercontent.com/87698138/194963273-e2ee0a4f-a65e-4baa-b64d-c1b2824299ee.png">

