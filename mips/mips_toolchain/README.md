Download OpenWRT/LEDE SDK for a device that has the same arch/SOC as your target. On our case, let's use

```bash
wget https://downloads.lede-project.org/releases/17.01.1/targets/ar71xx/generic/lede-sdk-17.01.1-ar71xx-generic_gcc-5.4.0_musl-1.1.16.Linux-x86_64.tar.xz
tar xvf lede-sdk-17.01.1-ar71xx-generic_gcc-5.4.0_musl-1.1.16.Linux-x86_64.tar.xz
cd lede-sdk-17.01.1-ar71xx-generic_gcc-5.4.0_musl-1.1.16.Linux-x86_64/
```

Follow the instructions from the OpenWRT/LEDE docs to compile packages using the SDK:

- [https://lede-project.org/docs/guide-developer/compile_packages_for_lede_with_the_sdk](https://lede-project.org/docs/guide-developer/compile_packages_for_lede_with_the_sdk)

Go to the SDK folder and then open the SDK's menu:

```bash
make menuconfig
```

Select Global Build Settings and press enter, in the submenu deselect/exclude the following options:

```
“Select all target specific packages by default”
“Select all kernel module packages by default”
“Select all userspace packages by default”
```

Save the configuration and then update the package lists

```
./scripts/feeds update -a
```

Select the packages you want to compile:

```bash
./scripts/feeds install <packagename>
```

Type ```make menuconfig``` again, find the package you want to build and select it using "m", save the config and compile the package using:

```bash
make
```

Now go to the **bin/packages/mips_24kc/base/** directory and check the newly created .ipk package. If you want to 

```bash
$ cd bin/packages/mips_24kc/base/
$ tar xvf strace_4.15-1_mips_24kc.ipk
$ tar xvf data.tar.gz
./
./usr/
./usr/bin/
./usr/bin/strace
$ file ./usr/bin/strace
./usr/bin/strace: ELF 32-bit MSB executable, MIPS, MIPS32 rel2 version 1 (SYSV), dynamically linked, interpreter /lib/ld-musl-mips-sf.so.1, corrupted section header size
```

If you want to statically compile the binary, you can change the package Makefile and include **LDFLAGS+="-static"** to the MAKE_FLAGS entry.

```
vim package/feeds/base/strace/Makefile
```

```bash
MAKE_FLAGS := \
        CCOPT="$(TARGET_CFLAGS)" LDFLAGS+="-static"
```

```bash
make
```

Extract the .ipk package again and get the statically compiled binary:

```bash
$ file bin/packages/mips_24kc/base/usr/bin/strace 
bin/packages/mips_24kc/base/usr/bin/strace: ELF 32-bit MSB executable, MIPS, MIPS32 rel2 version 1 (SYSV), statically linked, corrupted section header size
```
