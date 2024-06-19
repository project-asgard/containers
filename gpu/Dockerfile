FROM nvidia/cuda:11.8.0-devel-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ="America/New_York"

# build tools
RUN apt-get update -y && \
    apt-get install -y apt-utils

RUN   apt-get install -y cmake \
   && apt-get install -y g++ \
   && apt-get install -y git \
   && apt-get install -y libblis-serial-dev \
   && apt-get install -y libflame-dev

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser

