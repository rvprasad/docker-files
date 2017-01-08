FROM ubuntu:xenial

Maintainer Venkatesh-Prasad Ranganath "http://github.com/rvprasad"

COPY .bashrc_local /root/

RUN apt-get update && \
      apt-get install -y software-properties-common && \
      add-apt-repository -y ppa:openjdk-r/ppa && \
      apt-get update && \
      apt-get install -y \
        ccache \
        cpio \
        g++ \
        gcc \
        libasound2-dev \
        libcups2-dev \
        libfreetype6-dev \
        libx11-dev \
        libxext-dev \
        libxrender-dev \
        libxtst-dev \
        libxt-dev \
        make \
        mercurial \
        openjdk-7-jdk \
        unzip \
        zip && \
     echo ". /root/.bashrc_local" >> /root/.bashrc


VOLUME ["/open-jdk"]
