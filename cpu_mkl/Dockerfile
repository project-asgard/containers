FROM ubuntu:20.04

# git & apt-utils
RUN apt-get update \
   && apt-get upgrade -y \
   && apt-get install -y git \
   && apt-get install -y apt-utils

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
   && apt-get install -y clang-7 \
   && apt-get install -y curl \
   && apt-get install -y libssl-dev libcurl4-openssl-dev \
   && apt-get install -y cmake \
   && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libmkl-full-dev

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
