FROM ubuntu:xenial

MAINTAINER andrejlevkovitch@gmail.com

RUN apt-get update && \
    apt-get install -y wget software-properties-common git w3m build-essential

RUN add-apt-repository ppa:ubuntu-toolchain-r/test -y && \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    add-apt-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-8 main" && \
    apt-get update && \
    apt-get install -y gcc g++ gdb clang-8 clang-format-8 libclang-8-dev cppcheck && \
    update-alternatives --install \
              /usr/bin/llvm-config       llvm-config      /usr/bin/llvm-config-8  200 && \
    update-alternatives --install \
              /usr/bin/clang        clang        /usr/bin/clang-8 50 \
      --slave /usr/bin/clang++      clang++      /usr/bin/clang++-8 \
      --slave /usr/bin/clang-format clang-format /usr/bin/clang-format-8

RUN apt-get install -y \
    libncurses5-dev libncursesw5-dev \
    libbonoboui2-dev \
    libcairo2-dev \
    libatk1.0-dev \
    liblua5.3-0 liblua5.3-dev \
    libperl-dev \
    ruby-dev \
    xz-utils libpthread-workqueue-dev \
    python2.7-dev \
    libcurl4-openssl-dev \
    autoconf

RUN mkdir /usr/include/lua5.3/lib && \
    ln -sf /usr/lib/x86_64-linux-gnu/liblua5.3.so /usr/include/lua5.3/lib/liblua.so && \
    ln -sf /usr/lib/x86_64-linux-gnu/liblua5.3.a  /usr/include/lua5.3/lib/liblua.a && \
    ln -sf /usr/include/lua5.3                    /usr/include/lua5.3/include


RUN wget "https://github.com/Kitware/CMake/releases/download/v3.14.1/cmake-3.14.1.tar.gz" && \
    tar -xzvf cmake-3.14.1.tar.gz && \
    rm cmake-3.14.1.tar.gz && \
    cd cmake-3.14.1 && \
    ./bootstrap --system-curl && \
    make -j4 && \
    make install && \
    cd .. && \
    rm -rf cmake-3.14.1

RUN wget "https://github.com/universal-ctags/ctags/archive/master.zip" && \
    unzip master.zip && \
    rm master.zip && \
    cd ctags-master && \
    ./autogen.sh && \
    ./configure && \
    make -j4 && \
    make install && \
    cd .. && \
    rm -rf ctags-master

RUN wget "https://github.com/vim/vim/archive/v8.1.1140.tar.gz" && \
    tar -xzvf v8.1.1140.tar.gz && \
    rm v8.1.1140.tar.gz && \
    cd vim-8.1.1140 && \
    ./configure --with-features=huge \
                --enable-luainterp=yes \
                --with-lua-prefix=/usr/include/lua5.3 \
                --enable-pythoninterp=yes \
                --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
                --enable-rubyinterp=yes \
                --enable-perlinterp=yes \
                --enable-multibyte \
                --enable-gui=no \
                --enable-cscope \
                --enable-largefile \
                --disable-netbeans \
                --prefix=/usr/local && \
    make -j4 && \
    make install && \
    cd .. && \
    rm -rf vim-8.1.1140

RUN wget "https://github.com/vifm/vifm/archive/v0.10.tar.gz" && \
    tar -xzvf v0.10.tar.gz && \
    rm v0.10.tar.gz && \
    cd vifm-0.10 && \
    ./configure && \
    make -j4 && \
    make install && \
    cd .. && \
    rm -rf vifm-0.10

RUN git clone https://github.com/andrejlevkovitch/MySettings.git && \
    cp MySettings/git/git_diff_wrapper /usr/local/bin

RUN useradd -ms /home/user user
USER user

RUN ./MySettings/scripts/install_packages --settings

RUN echo "\nset encoding=utf-8" >> /home/user/.vimrc
    
USER root
RUN rm -rf MySettings
RUN apt-get autoremove -y gcc g++ wget software-properties-common
RUN apt-get clean

USER user
WORKDIR /home/user
CMD ["vim"]
