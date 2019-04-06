FROM ubuntu:xenial

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget software-properties-common git && \
    apt-get install -y build-essential mesa-common-dev libgl1-mesa-dev libgles2-mesa-dev freeglut3-dev  xvfb && \
    apt-get install -y libasound2-dev libpulse-dev

RUN add-apt-repository ppa:ubuntu-toolchain-r/test -y && \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    add-apt-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-8 main" && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y gcc-8 g++-8 clang-8 clang-format-8 && \
    apt-get install -y libboost-all-dev && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8  60 --slave /usr/bin/g++ g++ /usr/bin/g++-8 && \
    update-alternatives --install /usr/bin/clang clang /usr/bin/clang-8 50 --slave /usr/bin/clang++ clang++ /usr/bin/clang++-8 --slave /usr/bin/clang-format clang-format /usr/bin/clang-format-8

RUN mkdir /cmake && \
    git clone https://github.com/Kitware/cmake.git /cmake && \
    cd /cmake && \
    ./bootstrap && \
    make && \
    make install && \
    cd / && \
    rm cmake -rf

RUN mkdir /gl && \
    git clone https://github.com/skaslev/gl3w.git /gl && \
    mkdir /gl/build && \
    cd /gl/build && \
    cmake .. && \
    make && \
    make install && \
    cd / && \
    rm /gl -rf

RUN mkdir /sdl && \
    git clone https://github.com/SDL-mirror/SDL.git /sdl && \
    mkdir /sdl/build && \
    cd /sdl/build && \
    cmake .. && \
    make && \
    make install && \
    cd / && \
    rm /sdl -rf


RUN useradd -ms /home/user user
USER user
WORKDIR /home/user

ENV PATH="/opt/qt512/bin:${PATH}"
