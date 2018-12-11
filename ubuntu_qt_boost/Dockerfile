FROM gcc:latest
FROM ubuntu:xenial

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:beineri/opt-qt-5.10.1-xenial && \
    apt-get update && \
    apt-get install -y cmake g++ clang python && \
    apt-get install -y libboost-all-dev && \
    apt-get install -y build-essential libgl1-mesa-dev && \
    apt-get install -y qt510-meta-full && \
    apt-get install -y qt510multimedia

ENV PATH="/opt/qt510/bin:${PATH}"
