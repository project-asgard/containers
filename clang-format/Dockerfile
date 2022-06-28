FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get upgrade -y

# build tools
RUN apt-get install -y clang-format-12

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
