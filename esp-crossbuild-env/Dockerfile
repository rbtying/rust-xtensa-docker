FROM rbtying/rust-xtensa
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"

RUN apt-get update \
 && apt-get install -y curl gcc \
 && rm -rf /var/lib/apt/lists/*

RUN useradd -u 8000 -d /home/esp_dev_env esp_dev_env
RUN mkdir /home/esp_dev_env
RUN chown -R esp_dev_env /home/esp_dev_env

USER esp_dev_env

ENV PATH "/home/esp_dev_env/.cargo/bin:${PATH}"

RUN curl \
        --proto '=https' \
        --tlsv1.2 \
        -sSf \
        https://sh.rustup.rs \
    | sh -s -- -y --default-toolchain stable \
 && rustup component add rustfmt \
 && cargo install cargo-xbuild bindgen

ENV XARGO_RUST_SRC="/opt/rustc-xtensa-src/"
ENV XTENSA_LLVM_PATH="/opt/llvm-xtensa/"
ENV XTENSA_RUST_PATH="/opt/rustc-xtensa/"
ENV LIBCLANG_PATH="${XTENSA_LLVM_PATH}/lib"

RUN rustup toolchain link xtensa "${XTENSA_RUST_PATH}"

WORKDIR /project
