FROM nvidia/cuda:11.4.3-devel-ubuntu20.04

# git
RUN apt-get update -y \
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
RUN apt-get install -y wget \
   && apt-get install -y zlib1g-dev \
   && apt-get install -y build-essential \ 
   && apt-get install -y gcc \
   && apt-get install -y g++ \
   && apt-get install -y gfortran \
   && apt-get install -y curl \
   && apt-get install -y libssl-dev libcurl4-openssl-dev \
   && apt-get install -y cmake

# Add AMD ROCM repository
RUN apt-get update \
   && wget -q -O - https://repo.radeon.com/rocm/rocm.gpg.key 2>/dev/null | gpg --dearmor - | tee /etc/apt/trusted.gpg.d/rocm.gpg >/dev/null \
   && apt-add-repository 'deb [arch=amd64] https://repo.radeon.com/rocm/apt/4.3.1/ ubuntu main' \
   && apt-get update

# Install HIP
RUN apt-get update -y \
   && apt-get install -y hip-base \
   && ln -s /opt/rocm-4.3.1/ /opt/rocm

# Add ROCM/HIP to PATH
ENV PATH=/opt/rocm/bin:$PATH

# Compile hipBLAS for CUDA and install it
RUN git clone --depth 1 --branch rocm-4.3.1 https://github.com/ROCmSoftwarePlatform/hipBLAS.git \
   && cd hipBLAS \
   && ./install.sh --cuda -i

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
