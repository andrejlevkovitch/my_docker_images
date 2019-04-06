FROM ubuntu:bionic

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update
RUN apt-get install software-properties-common git -y

ADD . /MySettings
WORKDIR /MySettings

RUN git clone https://github.com/andrejlevkovitch/MySettings.git
WORKDIR /MySettings/MySettings/scripts
RUN ./install_packages --cross
RUN rm -rf /MySettings

RUN ln -s /opt/mxe/usr/bin/x86_64-w64-mingw32.shared-cmake /usr/bin/cmake

RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install --no-install-recommends --assume-yes wine-development

RUN useradd -ms /home/user user
USER user
WORKDIR home/user

ENV PATH="/opt/mxe/usr/bin:${PATH}"
ENV WINEPATH="/opt/mxe/usr/x86_64-w64-mingw32.shared/bin;/opt/mxe/usr/x86_64-w64-mingw32.shared/qt5/bin"
