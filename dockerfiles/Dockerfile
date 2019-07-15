FROM ubuntu:latest
MAINTAINER oevans <ore2000@columbia.edu>

USER root
WORKDIR /tmp

# Install dependencies
RUN apt-get update && \
    apt-get -y install \
                       git \
                       g++ \
                       gfortran \
                       cmake \
                       openmpi-bin \
                       libopenmpi-dev \
                       flex \
                       libblas-dev \
                       liblapack-dev \
                       swig3.0 \
                       libeigen3-dev \
                       libboost-dev \
                       libboost-filesystem-dev \
                       libboost-program-options-dev \
                       libboost-iostreams-dev \
                       libboost-timer-dev \
                       libvtk5-dev \
                       libvtk-java \
                       libvtk5-qt4-dev \
                       libhdf5-openmpi-dev \
                       gmsh \
                       environment-modules \
                       python3-dev \
                       python3-pip && \

    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install python packages
RUN pip3 install \
                 sympy \
                 numpy \
                 pandas \
                 requests \
                 pytest

# Install spud
RUN git clone -b gtk3_python3_merged https://github.com/FluidityProject/spud.git && \
    cd spud && \
    ./configure --prefix=/usr/local/spud && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    make && \
    make install && \
    rm -rf /tmp/*

# Set environmental variables
ENV SPUD_DIR "/usr/local/spud"
ENV PATH "$SPUD_DIR/bin:$PATH"
ENV PYTHONPATH "$SPUD_DIR/lib/python3.6/site-packages"
ENV LD_LIBRARY_PATH "$SPUD_DIR/lib"

WORKDIR /root
