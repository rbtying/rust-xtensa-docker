FROM ubuntu:20.04
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"

RUN apt-get update \
 && DEBIAN_FRONTEND="noninteractive" apt-get install -y \
       bison \
       cmake \
       curl \
       flex \
       g++ \
       gcc \
       git \
       gperf \
       libncurses-dev \
       make \
       python3 \
       ninja-build \
 && rm -rf /var/lib/apt/lists/*

# Checkout the source code from Espressif's xtensa fork
WORKDIR /tmp/clang-build
RUN git init \
  && git remote add origin https://github.com/espressif/llvm-project.git \
  && git fetch --depth 1 origin xtensa_release_9.0.1 \
  && git checkout FETCH_HEAD

# Run the build. Results of the build will be available at /tmp/clang-install/.
RUN mkdir build \
  && cd build \
  && cmake -GNinja \
    -DPYTHON_EXECUTABLE=/usr/bin/python3 \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/tmp/clang-install \
    -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=Xtensa \
    -DLLVM_ENABLE_PROJECTS=clang \
    /tmp/clang-build/llvm \
  && ninja install
