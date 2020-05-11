FROM rbtying/llvm-xtensa-build as builder
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"

RUN apt-get update \
 && DEBIAN_FRONTEND="noninteractive" apt-get install -y \
       cmake \
       g++ \
       curl \
       git \
       libssl-dev \
       pkg-config \
       make \
       python2.7 \
 && rm -rf /var/lib/apt/lists/*

# Checkout the source code from Espressif's xtensa fork
WORKDIR /tmp/rustc-build
RUN git init \
  && git remote add origin https://github.com/MabezDev/rust-xtensa.git \
  && git fetch --depth 1 origin xtensa-target \
  && git checkout FETCH_HEAD

# Run the build. 
RUN ./configure --experimental-targets=Xtensa --llvm-root=/tmp/clang-build/build \
  && python2.7 x.py build

# Stage 2. Produce a minimal release image with build results.
FROM ubuntu:20.04
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"

RUN mkdir /opt/rustc-xtensa/
# Copy build results of stage 1 to /usr/local.
COPY --from=builder /tmp/rustc-build/build/x86_64-unknown-linux-gnu/stage2/ /opt/rustc-xtensa/
COPY --from=rbtying/llvm-xtensa-build /tmp/clang-install/ /opt/llvm-xtensa/

RUN mkdir /opt/rustc-xtensa-src/
COPY --from=builder /tmp/rustc-build/src/ /opt/rustc-xtensa-src/
