# Docker Image to Build Open JDK

The image is available on [Docker Hub](https://hub.docker.com/r/rvprasad/openjdk-devel/).


## Image Usage

It does not include Open JDK source.  So, when you start a container based on 
this image, make sure you mount a host folder as `/open-jdk` folder in the 
container, e.g., 
`docker run -i -t -v /tmp/open-jdk/:/open-jdk openjdk-devel /bin/bash`.


## Build Instructions

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
bash ./configure \
    --with-freetype-include=/usr/include/freetype2/ \
    --with-freetype-lib=/usr/lib/x86_64-linux-gnu
make all
```


## Tags
- v1 has been tested to build jdk8u.
