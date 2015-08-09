strace (ARMEB)
==============

* Download and extract the latest strace (v4.0.1 on 08/09/2015):

```
wget https://downloads.sourceforge.net/project/strace/strace/4.10/strace-4.10.tar.xz
tar xf strace-4.10.tar.xz
cd strace-4.10/
```

* Edit v4l2.c to include an htole32() replacement before line 70 (print_pixelformat):

```c
uint32_t htole32(uint32_t i)
{
   uint32_t result;
   result = (i & 0x000000ff) << 24
          | (i & 0x0000ff00) << 8
          | (i & 0x00ff0000) >> 8
          | (i & 0xff000000) >> 24;
   return result;
}
```

* Setup the build environment variables:

```bash
export PATH=${PATH}:/opt/armeb-linux/ti-puma5/usr/bin
export TARGETMACH=armeb-linux
export BUILDMACH=i686-pc-linux-gnu
export CROSS=armeb-linux
export CC=${CROSS}-gcc
export LD=${CROSS}-ld
export AS=${CROSS}-as
export AR=${CROSS}-ar
export CXX=${CROSS}-g++
export LDFLAGS="-static"
```

* Configure and cross compile strace

```
./configure --host=$TARGETMACH
make
```

* Strip the binary:

```
armeb-linux-strip strace
```
