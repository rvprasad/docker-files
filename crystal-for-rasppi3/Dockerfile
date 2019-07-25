FROM raspbian/stretch

Maintainer Venkatesh-Prasad Ranganath "http://github.com/rvprasad"

RUN echo "deb http://deb.debian.org/debian stretch-backports main" \
        >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y g++ gcc gdb git libc6-dbg libevent-dev libgc-dev \
      llvm-6.0 libpcre3-dev libssl-dev libyaml-dev make pkg-config zlib1g-dev 
