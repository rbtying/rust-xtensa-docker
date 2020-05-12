FROM rbtying/rust-xtensa
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"
RUN apt-get update \
 && apt-get install -y curl gcc \
 && rm -rf /var/lib/apt/lists/*

# Install Rust system-wide
WORKDIR /opt/rust
ENV RUSTUP_HOME=/opt/rust
ENV CARGO_HOME=/opt/rust
ENV PATH "${CARGO_HOME}/bin:${PATH}"
ENV XTENSA_RUST_PATH="/opt/rustc-xtensa/"

RUN curl \
        --proto '=https' \
        --tlsv1.2 \
        -sSf \
        https://sh.rustup.rs \
    | sh -s -- -y --default-toolchain stable --profile minimal \
 && cargo install cargo-xbuild bindgen

RUN rustup toolchain link xtensa "${XTENSA_RUST_PATH}"
RUN chmod o+w -R /opt/rust

# Set environment variables, in case somebody wants to use this directly
ENV PATH "/opt/rust/bin:${PATH}"
ENV XARGO_RUST_SRC="/opt/rustc-xtensa-src/"
ENV XTENSA_LLVM_PATH="/opt/llvm-xtensa/"
ENV XTENSA_RUST_PATH="/opt/rustc-xtensa/"
ENV LIBCLANG_PATH="${XTENSA_LLVM_PATH}/lib"
ENV RUSTUP_HOME=/opt/rust

WORKDIR /project
