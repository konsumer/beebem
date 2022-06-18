This is a patched version of [beebem-unnix](http://beebem-unix.bbcmicro.com/) that will compile with sdl-compat (for use with SDL2.)

To get teh base-repo setup I did this:

```sh
apt update
apt install -y git wget autoconf cmake  build-essential cmake libsdl2-2.0-0 libsdl2-dev libgl-dev libgtk2.0-dev

git clone --depth 1 https://github.com/libsdl-org/sdl12-compat.git
cd sdl12-compat
mkdir build
cd build
cmake ..
make
make install
cd ../..

wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13.tar.gz
tar zxvf beebem-0.0.13.tar.gz

wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13_64bit.patch
wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13-keys.patch
wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13_menu_crash.patch

patch -p0 < beebem-0.0.13_64bit.patch
patch -p0 < beebem-0.0.13-keys.patch
patch -p0 < beebem-0.0.13_menu_crash.patch

cd beebem-0.0.13
./configure --prefix=/opt/beebem --enable-econet --build=aarch64-unknown-linux-gnu
```

It would not build at this point, so I made a few typedefs and moved the `includes` around a bit, and it will build with `make`.