FROM ubuntu:22.04

# git & apt-utils
RUN apt-get update \
   && apt-get upgrade -y \
   && apt-get install -y git \
   && apt-get install -y apt-utils

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ="America/New_York"

# build tools
RUN apt-get install -y tzdata \
   && apt-get install -y build-essential \ 
   && apt-get install -y gcc \
   && apt-get install -y g++ \
   && apt-get install -y gfortran \
   && apt-get install -y libopenmpi-dev \
   && apt-get install -y clang-format-12 \
   && apt-get install -y clang-12 \
   && apt-get install -y libomp-12-dev \
   && apt-get install -y cmake \
   && apt-get install -y liblapack-dev \
   && apt-get install -y libopenmpi-dev \
   && apt-get install -y libscalapack-openmpi-dev \
   && apt-get install -y doxygen \
   && apt-get install -y graphviz

#https://bugs.launchpad.net/ubuntu/+source/scalapack/+bug/1917534
RUN sed -i 's/${_IMPORT_PREFIX}\/lib/${_IMPORT_PREFIX}\/lib\/x86_64-linux-gnu/g' /usr/lib/cmake/scalapack-2.1.0.openmpi/scalapack-targets-none.cmake

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
