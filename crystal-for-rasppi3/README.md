# Docker image to build [Crystal language](https://crystal-lang.org/) compiler for Raspberry Pi 3

The image is available on [Docker Hub](https://hub.docker.com/r/rvprasad/crystal-for-rasppi3/).

## Usage

1. Checkout Crystal sources by executing `git clone https://github.com/crystal-lang/crystal.git` in *$SRC* folder on a x86 Ubuntu host system.

2. Install development packages required to cross-compile to arm-linux-gnueabihf target on the host system.

4. Install crystal compiler on the host system.

5. In a shell, execute
   1. `cd $SRC/crystal`
   2. `git checkout 0.29.0`
   3. `make clean deps`
   4. `./bin/crystal build -D preview_overflow -D compiler_rt --cross-compile --target "armv6-linux-gnueabihf" src/compiler/crystal.cr -D without_openssl -D without_zlib`.

6. Make sure *qemu-user-static* package is installed on the host system.  This is required to execute an arm container on the host system.

7. Start a container based on this image by executing `docker run -it -v $SRC/crystal/:/crystal rvprasad/crystal-for-rasppi3:v1 /bin/bash`.

8. In a shell, execute
   1. `cd /crystal`
   2. `mkdir .build`
   3. `make clean deps`
   4. ``cc crystal.o -o .build/crystal -rdynamic /crystal/src/llvm/ext/llvm_ext.o `/usr/bin/llvm-config-6.0 --libs --system-libs --ldflags 2> /dev/null` -lstdc++ -lpcre -lm -lgc -lpthread /crystal/src/ext/libcrystal.a -levent -lrt -ldl -L/usr/bin/../lib/crystal/lib -L/usr/lib -L/usr/local/lib``

If all goes well, the crystal compiler for Raspberry Pi 3 (target: arm-linux-gnueabihf) will be available in */crystal/.build* folder in the container.
