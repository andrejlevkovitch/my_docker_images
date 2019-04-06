FROM ubuntu:bionic

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update
RUN apt-get install software-properties-common git -y

ADD . /MySettings
WORKDIR /MySettings

RUN git clone https://github.com/andrejlevkovitch/MySettings.git
WORKDIR /MySettings/MySettings/scripts
RUN ./install_packages --qt
RUN rm -rf /MySettings

RUN useradd -ms /home/user user
USER user
WORKDIR home/user

ENV PATH="/opt/qt512/bin:${PATH}"
