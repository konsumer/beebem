This is a patched version of [beebem-unix](http://beebem-unix.bbcmicro.com/) that will compile with sdl-compat (for use with SDL2.)

## installing

You should be able to install on a debian/ubuntu system like this:

```
# system setup

apt update
apt install -y git cmake automake autoconf build-essential libsdl2-2.0-0 libsdl2-dev libgl-dev libgtk2.0-dev

# sdl12-compat, so you can link it to SDL2 instead of SDL1

git clone --depth 1 https://github.com/libsdl-org/sdl12-compat.git
cd sdl12-compat
mkdir build
cd build
cmake ..
make
make install
ldconfig
cd ../..

git clone https://github.com/konsumer/beebem.git
cd beebem

# for arm64, you will need to adjust to your arch
touch aclocal.m4 configure
./reconf
./configure --prefix=/opt/beebem --enable-econet --build=aarch64-unknown-linux-gnu
make
```


## What is patched


To get the base-repo setup I originally  did this:

```sh
wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13.tar.gz
tar zxvf beebem-0.0.13.tar.gz

# patches that were recommended in original docs

wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13_64bit.patch
wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13-keys.patch
wget http://beebem-unix.bbcmicro.com/download/beebem-0.0.13_menu_crash.patch

patch -p0 < beebem-0.0.13_64bit.patch
patch -p0 < beebem-0.0.13-keys.patch
patch -p0 < beebem-0.0.13_menu_crash.patch
```

It would not build at this point, so I made a few typedefs and moved the `includes` around a bit, and now it will build with `make`.
