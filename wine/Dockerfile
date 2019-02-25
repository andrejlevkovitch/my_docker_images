FROM debian:wheezy
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install --no-install-recommends --assume-yes wine
RUN useradd -ms /home/user user
USER user
WORKDIR home/user
ENV DISPLAY :0
