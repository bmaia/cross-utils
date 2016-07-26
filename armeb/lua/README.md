lua 5.3.0 (ARMEB)
=================

* Download and extract lua 5.3.0:

```
wget https://www.lua.org/ftp/lua-5.3.0.tar.gz
tar xvzf lua-5.3.0.tar.gz
cd lua-5.3.0/
```

* Edit src/Makefile and change line 98 from CC="gcc -std=c89" to CC="armeb-linux-gcc -std=c89".

* Cross compile lua:

```
export PATH=${PATH}:/opt/armeb-linux/ti-puma5/usr/bin
make CC=armeb-linux-gcc c89
```