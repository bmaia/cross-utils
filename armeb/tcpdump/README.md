tcpdump (ARMEB)
=========================

* Download and extract the latest libpcap and tcpdump (v1.7.4 and v4.7.4 on 09/13/2015):

```
wget http://www.tcpdump.org/release/libpcap-1.7.4.tar.gz
wget http://www.tcpdump.org/release/tcpdump-4.7.4.tar.gz
tar xvzf libpcap-1.7.4.tar.gz
tar xvzf tcpdump-4.7.4.tar.gz
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

* Configure and cross compile libpcap:

```
cd ./libpcap-1.7.4/
./configure --host=$TARGETMACH --with-pcap=linux ac_cv_linux_vers=2
make
mv libpcap.so.1.7.4 /opt/armeb-linux/ti-puma5/lib/
```

* Configure and cross compile tcpdump:

```
cd ../tcpdump-4.7.4/
./configure --build=$BUILDMACH --host=$TARGETMACH ac_cv_linux_vers=2
```

* Strip the binaries:

```
armeb-linux-strip tcpdump
```
