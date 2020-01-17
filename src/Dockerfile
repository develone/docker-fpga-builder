FROM ubuntu:xenial

RUN apt-get update && apt-get install -y build-essential clang bison flex libreadline-dev \
                                         gawk tcl-dev libffi-dev git mercurial \
                                         pkg-config python python3 libftdi-dev \
                                         python3-dev libboost-all-dev cmake libeigen3-dev \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/develone/icestorm.git icestorm \
    && cd icestorm \
    && make -j$(nproc) \
    && make install \
    && cd .. && rm -rf icestorm

RUN git clone https://github.com/develone/nextpnr nextpnr \
    && cd nextpnr \
    && cmake -DARCH=ice40 -DBUILD_GUI=OFF -DCMAKE_INSTALL_PREFIX=/usr/local . \
    && make -j$(nproc) \
    && make install \
    && cd .. && rm -rf nextpnr

RUN git clone https://github.com/develone/yosys.git yosys \
    && cd yosys \
    && make -j$(nproc) \
    && make install \
    && cd .. && rm -rf yosys

# /module is used for releases when we check out code in the toolbelt container
# It is passed on to the builder with --volumes-from
# Make sure it is accessible for all users
RUN mkdir /module && chmod 777 /module

WORKDIR /module
