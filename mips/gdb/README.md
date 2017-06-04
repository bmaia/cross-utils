gdb and gdbserver (MIPS)
=========================

* On a newer Ubuntu System (16.04+), install the MIPS toolchain:

```
sudo apt update
sudo apt install g++-mips-linux-gnu gcc-mips-linux-gnu
```

* Download and extract the latest GDB (v8.0 on 04/06/2017):

```
wget ftp://ftp.gnu.org/gnu/gdb/gdb-8.0.tar.xz
tar xvf gdb-8.0.tar.xz
```

* Setup the build environment variables:

```bash
export TARGETMACH=mips-linux-gnu
export CROSS=mips-linux-gnu
export CC=${CROSS}-gcc
export LD=${CROSS}-ld
export AS=${CROSS}-as
export AR=${CROSS}-ar
export CXX=${CROSS}-g++
export LDFLAGS="-static"
```

* Configure and cross compile gdb and gdbserver:

```
cd gdb-8.0/
./configure --host=$TARGETMACH --target=$TARGETMACH
make
```

* Strip the binaries:

```
mips-linux-gnu-strip gdb
mips-linux-gnu-strip gdbserver/gdbserver
```

