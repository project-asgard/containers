FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ="America/New_York"

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y apt-utils

# build tools
RUN apt-get install -y build-essential \
    && apt-get install -y cmake \
    && apt-get install -y gcc \
    && apt-get install -y gfortran \
    && apt-get install -y g++ \
    && apt-get install -y git \
    && apt-get install -y libmkl-dev

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
