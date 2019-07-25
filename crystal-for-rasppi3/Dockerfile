FROM raspbian/stretch

Maintainer Venkatesh-Prasad Ranganath "http://github.com/rvprasad"

RUN echo "deb http://deb.debian.org/debian stretch-backports main" \
        >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y g++ gcc git libpcre3-dev libevent-dev libgc-dev libyaml-dev \
      libssl-dev llvm-6.0 make pkg-config zlib1g-dev 
