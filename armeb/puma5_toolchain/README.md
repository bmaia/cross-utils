Description
===========

Quick guide to create a working buildroot to cross compile binaries and firmwares from puma5 cable modems, including Motorola SB6120/6121/6141 and Arris TG862 families.

[puma5_toolchain-2010.02.24.tgz](https://github.com/bmaia/cross-utils/blob/master/armeb/puma5_toolchain/puma5_toolchain-2010.02.24.tgz?raw=true) - ARMEB toolchain (puma5) and installation script and patches.

Installation
============

The procedure was tested on a Kali Linux 1.1.0a 64 bit Image with GCC 4.7.2.

* Download and extract the puma5 toolchain:

```
wget https://github.com/bmaia/cross-utils/raw/master/armeb/puma5_toolchain/puma5_toolchain-2010.02.24.tgz
tar xjf puma5_toolchain-2010.02.24.tgz
```

* Install dependencies:

```
sudo apt-get install kernel-package libncurses5-dev fakeroot wget bzip2 build-essential bison flex unifdef build-essential texinfo libc6-dev-i386 quilt g++-multilib
```

* Make sure you're using make 3.8.1:

```
make -version
GNU Make 3.81
```

* Install the puma5 toolchain on the /opt/armeb-linux folder:

```
cd puma5_toolchain/src/
mkdir /opt/armeb-linux
export TI_PUMA5_TOOLCHAIN_INSTALL_DIR=/opt/armeb-linux
./build-toolchain.sh
```

* Cross compile a Hello World in C:

```c
#include <stdio.h>

main(){
    printf("Hello World\n");
}

```

```
/opt/armeb-linux/ti-puma5/usr/bin/armeb-linux-cc hello.c -o hello -static
```

* Check the ELF binary

```
file hello
```
```
hello: ELF 32-bit MSB executable, ARM, version 1 (SYSV), dynamically linked (uses shared libs), not stripped
```

Installation (prebuilt toolchain)
=================================

If you don't want to compile everything and you trust the Internet, download the prebuilt puma5 toolchain for Linux 64bits (tested on Kali 1.1.0a):

```
cd /opt/
wget https://github.com/bmaia/cross-utils/raw/master/armeb/puma5_toolchain/armeb-linux.tar.xz
tar xf armeb-linux.tar.xz
```

References
==========

[1] http://www.grandrapidsdevs.com/creating-a-working-buildroot-for-sb6120-6141-komodo.html

[2] http://sourceforge.net/projects/sb6120.arris/files/SB6120%20SB6121%20SB6141%201.0.6.3-SCM03 

[3] http://sourceforge.net/projects/sb6x2x.arris/files/SBV6x2x_1_0_2_0_SCM01/1.0.2.0SCM01 

[4] http://sourceforge.net/projects/sb6141.arris/files/SB6141_1_0_6_1_SCM00 
