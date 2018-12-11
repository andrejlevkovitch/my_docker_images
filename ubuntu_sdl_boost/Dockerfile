FROM gcc:latest
FROM ubuntu:xenial

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:janisozaur/cmake-update && \
    apt-get update

RUN apt-get install -y mingw-w64 && \
    apt-get install -y mingw-w64-x86-64-dev && \
    apt-get install -y cmake g++ clang python

RUN apt-get install -y libtinyxml-dev && \
    apt-get install -y libpng12-dev && \
    apt-get install -y zlib1g-dev && \
    apt-get install -y git

RUN apt-get install -y libboost-all-dev

RUN apt-get install -y libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev && \
    apt-get install -y libsdl2-net-dev libsdl2-ttf-dev libsdl2-gfx-dev

RUN git clone https://github.com/tonymagro/sdl2-mingw.git && \
    cd sdl2-mingw && \
    sed -i 's/CROSS_PATH := \/usr\/local\/cross-tools/CROSS_PATH := \/usr/g' Makefile && \
    make cross && \
    cd ..
