FROM ubuntu:xenial

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget software-properties-common git && \
    apt-get install -y build-essential mesa-common-dev libgl1-mesa-dev libgles2-mesa-dev freeglut3-dev  xvfb && \
    apt-get install -y libasound2-dev libpulse-dev && \
    apt-get install -y autoconf automake autopoint bash bison bzip2 flex g++ g++-multilib gettext git gperf intltool libc6-dev-i386 libgdk-pixbuf2.0-dev libltdl-dev libssl-dev libtool-bin libxml-parser-perl lzip make openssl p7zip-full patch perl pkg-config python ruby sed unzip wget xz-utils


RUN mkdir /opt/mxe && \
    git clone https://github.com/andrejlevkovitch/mxe.git /opt/mxe && \
    cd /opt/mxe && \
    make MXE_TARGETS="x86_64-w64-mingw32.shared" MXE_PLUGIN_DIRS="plugins/gcc8" gcc cmake && \
    cd / && \
    ln -s /opt/mxe/usr/bin/x86_64-w64-mingw32.shared-cmake /usr/bin/cmake

RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install --no-install-recommends --assume-yes wine wine-development


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
ENV WINEPATH="/opt/mxe/usr/x86_64-w64-mingw32.shared/bin"
