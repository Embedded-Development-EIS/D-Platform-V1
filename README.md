# D-Platform-V1
EIS developed new BSP for the CCC unit (EIS Product) on top of mainline linux distribution, based on open embedded project and Bitbake tool. This BSP is basically a lightweight OpenEmbedded based Linux Distribution.

# Initial setup

```
git clone https://github.com/Embedded-Development-EIS/D-Platform-V1.git
cd D-Platform-V1/
git submodule update --init
meta-ccc/scripts/init-oe.sh

cd build/
# In D-Platform-V1/meta-ccc/recipes-bsp/fpga/
# Edit fpga-image-wizard.bb to upload the desired bitstream labelled "static.bit" and export location for hardware design.
gedit ../meta-ccc/recipes-bsp/fpga/fpga-image-wizard.bb

# Then build your first image:
source profile
nice bitbake my-image
````

Note that "my-image" was designed to be used with DISTRO=tiny. It
expects to run with busybox-mdev instead of udev.

# Copying to SD-card

The simplest way to boot the resulting image is to copy it onto an SD card. In case you have not yet formatted and partitioned your SD-card yet, execute the following script first or use an application (e.g. G-Parted) to do the same. This script partitions and formats an SD card so it can be used directly. This is only required once.

#In build directory,

```
cd ~/D-Platform-V1/build/
sudo ../meta-ccc/scripts/partition_sd_card.sh
```

The meta-ccc/scripts/install-to-sdcard.sh script copy the required files to your SD card. You'll have to run these scripts as root, as they require low-level access to the SD card.

```
cd ~/D-Platform-V1/build/
sudo ../meta-ccc/scripts/install_to_sdcard.sh
```

# Update
This repository contains links to other repositories.
To bring your local copy of the repository up-to-date and fetch
all the sub-repositories along with it, run the following commands:

```
git pull
git submodule update
```
