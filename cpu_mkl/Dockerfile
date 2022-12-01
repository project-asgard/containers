FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ="America/New_York"

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y apt-utils

RUN apt-get install -y wget \
    && apt-get install -y gpg

# download the key to system keyring
RUN wget -O- https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB | gpg --dearmor | tee /usr/share/keyrings/oneapi-archive-keyring.gpg > /dev/null

# add signed entry to apt sources and configure the APT client to use Intel repository:
RUN echo "deb [signed-by=/usr/share/keyrings/oneapi-archive-keyring.gpg] https://apt.repos.intel.com/oneapi all main" | tee /etc/apt/sources.list.d/oneAPI.list

RUN apt-get update

# build tools
RUN apt-get install -y build-essential \
    && apt-get install -y cmake \
    && apt-get install -y gcc \
    && apt-get install -y gfortran \
    && apt-get install -y g++ \
    && apt-get install -y git \
    && apt-get install -y intel-oneapi-mkl-devel

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
