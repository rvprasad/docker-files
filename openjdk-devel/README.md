# Docker Image to Build Open JDK

The image is available on [Docker Hub](https://hub.docker.com/r/rvprasad/openjdk-devel/).


## Usage

It does not include Open JDK source.  So, when you start a container based on 
this image, make sure you mount a host folder as `/open-jdk` folder in the 
container, e.g., 
`docker run -i -t -v /tmp/open-jdk/:/open-jdk rvprasad/openjdk-devel:v1 /bin/bash`.


## OpenJDK Build Instructions

In the container's shell, follow the instructions under bullet **2** under 
**a Forest** in **Cloning** section of the [Repositories]
(http://openjdk.java.net/guide/repositories.html) document to clone the source
repository of OpenJDK.  

For example, to clone the source for OpenJDK 8u and build it, use the 
following commands in the container's shell.

```
cd /open-jdk
hg clone http://hg.openjdk.java.net/jdk8u/jdk8u  

cd jdk8u
find . -exec touch '{}' \; # protection against possible clock skews
bash ./configure --with-freetype-include=/usr/include/freetype2/ --with-freetype-lib=/usr/lib/x86_64-linux-gnu
make all

cd test
make PRODUCT_HOME=/open-jdk/jdk8u/build/linux-x86_64-normal-server-release/images/j2sdk-image JT_HOME=$JT_HOME 

# to execute tests related to hotspot engine
cd ../hotspot/test
jtreg -jdk:/open-jdk/jdk8u/build/linux-x86_64-normal-server-release/images/j2sdk-image -v1 :jdk
```

If you want to execute regression tests in any repository, then look at the 
entries in _TEST.groups_ files to provide as targets to `jtreg` command.


## Status of Various Tags
- _v1 has been used to successfully build jdk8u.  However, regression testing
  has been elusive following the instructions provided by OpenJDK._
