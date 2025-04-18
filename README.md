# LicheeRV-Nano-Build

# download source

```
git clone https://github.com/sipeed/LicheeRV-Nano-Build --depth=1
cd LicheeRV-Nano-Build
git clone https://github.com/sophgo/host-tools --depth=1
```

## host environment

you can use container:

```
cd host/ubuntu
docker build -t licheervnano-build-ubuntu .
docker run --name licheervnano-build-ubuntu licheervnano-build-ubuntu
docker export licheervnano-build-ubuntu | sqfstar licheervnano-build-ubuntu.sqfs
singularity shell -e licheervnano-build-ubuntu.sqfs
```

# build it

```
source build/cvisetup.sh
# C906:
defconfig sg2002_licheervnano_sd
# A53:
# defconfig sg2002_licheea53nano_sd
build_all
```

# build fail

on some system, qt5svg or qt5base will build failed on first build, please retry command:

```
build_all
```

# how to modify image after build:

```
# first partition
touch wifi.sta
mcopy -i install/xxx/xxx.img@@1s wifi.sta ::/

# second partition
./host/mount_ext4.sh install/xxx/xxx.img mountpoint
cd mountpoint
touch xxx
```

# logo

```
./host/make_logo.sh input.jpeg logo.jpeg
mcopy -i install/xxx/xxx.img@@1s logo.jpeg ::/
```
