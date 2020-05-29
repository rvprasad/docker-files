FROM arm32v7/debian:buster-backports

Maintainer Venkatesh-Prasad Ranganath "http://github.com/rvprasad"

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y apt-utils && \
    apt-get install -y \
      build-essential \
      libbsd-dev \
      libedit-dev \
      libevent-dev \
      libgc-dev \
      libgmp-dev \
      libgmpxx4ldbl \
      libssl-dev \
      libxml2-dev \
      libyaml-dev \
      automake \
      libtool \
      git \
      llvm-8 \
      llvm-8-dev \
      lld-8 \
      libpcre3-dev 
