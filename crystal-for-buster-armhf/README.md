# Docker image to build [Crystal language](https://crystal-lang.org/) compiler for Raspberry Pi 3

**WARNING: Currently, these instructions are non-functional on Raspberry Pi 3B.**

## Usage

1. Checkout Crystal sources by executing `git clone https://github.com/crystal-lang/crystal.git` in *$SRC* folder on a x86 Ubuntu host system.

2. Install crystal compiler on the host system.

3. In a shell, execute
   1. `cd $SRC/crystal`
   2. `git checkout 0.34.0`
   3. `make clean deps`
   4. `LLVM_CONFIG=/usr/bin/llvm-config-8 ./bin/crystal build --cross-compile --target "armv7l-unknonw-linux-gnueabihf" src/compiler/crystal.cr -D without_openssl -D without_zlib`.

4. Make sure *qemu-user-static* and *qemu-system-arm* packages are installed on the host system.  These are required to execute an arm container on the host system.

5. Build the docker image by executing `build.sh`.

6. Start a container based on this image by executing `docker run -it --rm -v $SRC/crystal/:/crystal crystal-for-buster-armhf:v1 /bin/bash`.

6. In a shell, execute
   1. `cd /crystal`
   2. `make clean deps`
   3. `mkdir .build`
   4. ``cc crystal.o -o .build/crystal -rdynamic /crystal/src/llvm/ext/llvm_ext.o `/usr/bin/llvm-config-8 --libs --system-libs --ldflags 2> /dev/null` -lstdc++ -lpcre -lm -lgc -lpthread /crystal/src/ext/libcrystal.a -levent -lrt -ldl``

If all goes well, the crystal compiler for Raspberry Pi 3 (target: arm-linux-gnueabihf) will be available in */crystal/.build* folder in the container.
