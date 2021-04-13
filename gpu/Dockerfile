FROM nvidia/cuda:10.2-devel

# git
RUN apt-get update -y \
   && apt-get upgrade -y \
   && apt-get install -y git

# build tools
RUN apt-get install -y wget \
   && apt-get install -y zlib1g-dev \
   && apt-get install -y clang-format \
   && apt-get install -y build-essential \ 
   && apt-get install -y gcc \
   && apt-get install -y g++ \
   && apt-get install -y gfortran \
   && apt-get install -y clang-7 \
   && apt-get install -y curl \
   && apt-get install -y libssl-dev libcurl4-openssl-dev

# cmake
RUN wget wget https://github.com/Kitware/CMake/releases/download/v3.20.1/cmake-3.20.1.tar.gz || true
RUN tar -zxvf cmake-3.20.1.tar.gz \
    && cd cmake-3.20.1 \
    && ./bootstrap --system-curl \
    && make -j 2 \
    && make install

# openmpi isn't happy with running su
RUN useradd -ms /bin/bash mpiuser
USER mpiuser
WORKDIR /home/mpiuser
