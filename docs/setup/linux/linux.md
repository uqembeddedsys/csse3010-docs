# Native Linux Setup Guide

## Overview
Linux Installation - Install CSSE3010 source and tools directly on Ubuntu (Not using a VM). You can install the CSSE3010 source and toolchain onto Ubuntu, directly. NOTE: You must first have your git account setup BEFORE attempting this.

**NOTE: ONLY USE THIS GUIDE IF YOU ARE NOT USING A VIRTUAL MACHINE**

## Ubuntu Automatic Script installation
The automatic script will download and install the required packages, add the sourcelib_env.sh script to your .bashrc startup script and add your user name to the “dialout” group.

1. Clone the sourcelib repository into your csse3010 directory using `git clone`
2. Go to the sourcelib/tools folder
3. Run the script sourcelib_install.sh as root – i.e. `sudo ./sourcelib_install.sh`
4. The script will download and install part of the toolchain
5. Once the script has finished, close and re-open your terminal 
6. Type `echo $SOURCELIB_ROOT` into your terminal. This command should return a path variable, i.e ~/csse3010/sourcelib


## Installing the GNU Arm Embedded Toolchain and STLink programming software

The GNU Arm Embedded Toolchain contains a compatible compiler for our MCU, while the utilities provided by STLink allows us to flash the Nucleo via the on-board STLinkV2 programmer.

1. Download the latest version of GNU Arm Embedded Toolchain for your OS via [https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)
2. Run the following commands in your terminal:
    1. change into the home directory and make a new folder called tools `cd ~; mkdir tools`
    2. change into the directory where the file was downloaded into, Downloads is used here as an example, it could be called something different on your machine `cd ~/Downloads`
    3. extract the tar file into the tools folder that we created earlier `tar -xjf <NAME_OF_DOWNLOADED_FILE> -C ~/tools`
        * NOTE: Normally you'd need to add the executable folder to PATH but that had already been taken care of by the install script in step 3 of the previous section.

3. Run the following commands to install the stlink utilities (including st-flash, which is used by `make flash` to program the Nucleo).


4. change into the tools folder we created earlier `cd ~/tools`
    1. clone the latest version of the stlink repository: `git clone https://github.com/texane/stlink.git`
    2. change into the stlink directory: `cd stlink`
    3. install required dependencies: `sudo apt-get install cmake build-essentials libusb-1.0`
    4. build stlink:` make release`
    5. `cd build/Release` 
    6. install stlink system-wide: `sudo make install`
    7. update the dynamic library cache: `sudo ldconfig`
    8. change into stlink's udev rules folder: `cd ~/tools/stlink/etc/udev/rules.d`
    9. copy the rules to /etc/udev/rules.d to allow stlink utilities to access USB devices: `sudo cp *.rules /etc/udev/rules.d`


## Manual Installation
This section applies to non-Ubuntu OS's (OSX for example).

1. Clone the sourcelib repository into your csse3010 directory using \texttt{git clone}
2. Go to the sourcelib/tools folder
3. Look in the sourcelib\_install.sh script for the packages that you will have to install.
4. You will also have to modify your `.bashrc` script with the following line: `export SOURCELIB_ROOT=$HOME/csse3010/sourcelib`, to initalise the environment variables.
5. Follow the instructions in the previous section to install the GNU Arm Embedded Toolchain and STLink programming software.
6. You should also add your user to the dialout group, so that the flash programmer can access the Nucleo via USB. Use the following command: `sudo adduser $USER dialout`
