FROM ubuntu:20.04

# git & apt-utils
RUN apt-get update \
   && apt-get upgrade -y \
   && apt-get install -y git \
   && apt-get install -y apt-utils

# Use Kitware APT Repository for newer CMake
# https://apt.kitware.com/
RUN apt-get update \
   && apt-get install -y apt-transport-https \
   && apt-get install -y ca-certificates \
   && apt-get install -y gnupg \
   && DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common \
   && apt-get install -y wget \
   && wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null \
   && apt-add-repository 'deb https://apt.kitware.com/ubuntu/ focal main' \
   && apt-get update

# build tools
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends tzdata \
   && dpkg-reconfigure --frontend noninteractive tzdata \
   && apt-get install -y wget \
   && apt-get install -y zlib1g-dev \
   && apt-get install -y clang-format \
   && apt-get install -y build-essential \ 
   && apt-get install -y gcc \
   && apt-get install -y g++ \
   && apt-get install -y gfortran \
   && apt-get install -y libopenmpi-dev \
   && apt-get install -y clang-format-6.0 \
   && apt-get install -y clang-7 \
   && apt-get install -y curl \
   && apt-get install -y libssl-dev libcurl4-openssl-dev \
   && apt-get install -y cmake \
   && apt-get install -y libblas-dev \
   && apt-get install -y liblapack-dev \
   && apt-get install -y libscalapack-openmpi-dev

#https://bugs.launchpad.net/ubuntu/+source/scalapack/+bug/1917534
RUN sed -i 's/${_IMPORT_PREFIX}\/lib/${_IMPORT_PREFIX}\/lib\/x86_64-linux-gnu/g' /usr/lib/cmake/scalapack-2.1.0.openmpi/scalapack-targets-none.cmake

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
