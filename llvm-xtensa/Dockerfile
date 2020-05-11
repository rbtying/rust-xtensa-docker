FROM ubuntu:20.04
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"
RUN apt-get update && \
    DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends libstdc++-10-dev binutils && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /opt/llvm-xtemsa/
COPY --from=rbtying/llvm-xtensa-build /tmp/clang-install/ /opt/llvm-xtensa/
