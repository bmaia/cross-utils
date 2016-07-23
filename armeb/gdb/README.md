gdb and gdbserver (ARMEB)
=========================

* Download and extract the latest GDB (v7.11.1 on 07/23/2015):

```
wget https://ftp.gnu.org/gnu/gdb/gdb-7.11.1.tar.xz
tar xf gdb-7.11.1.tar.xz
```

* Comment lines 125 and 126 from /gdb-7.9.1/gdb/gnulib/import/mbrtowc.c (you can also set # define MB_CUR_MAX 1):

```c
//      if (m >= 4 || m >= MB_CUR_MAX)
//        goto invalid;
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
export LDFLAGS="-static"
```

* Download and install termcap (dependency):

```
wget https://ftp.gnu.org/gnu/termcap/termcap-1.3.1.tar.gz
tar xvzf termcap-1.3.1.tar.gz
cd termcap-1.3.1/
./configure --host=$TARGETMACH --prefix='/opt/armeb-linux/ti-puma5/usr'
make install
mv termcap.o /opt/armeb-linux/ti-puma5/lib/
```

* Configure and cross compile gdb and gdbserver:

```
cd ../gdb-7.11.1/
./configure --host=$TARGETMACH --target=$TARGETMACH
make
```

```
cd gdb
./configure --host=$TARGETMACH --target=$TARGETMACH
make
```

* Strip the binaries:

```
armeb-linux-strip gdb
armeb-linux-strip gdbserver/gdbserver
```
