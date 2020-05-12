# Overlay over `rbtying/esp-crossbuild-env` to ensure that the docker container
# creates files with the right permissions.
FROM rbtying/esp-crossbuild-env
LABEL maintainer "Robert Ying <rbtying@aeturnalus.com>"

ARG USER_ID
ARG GROUP_ID

# Add the group, if it doesn't exist
RUN addgroup --gid $GROUP_ID user || true
# Add the user -- ideally, it should not exist (TBD what to do if it does)
RUN adduser --disabled-password -gecos '' --uid $USER_ID --gid $GROUP_ID user || true

RUN chown -R $USER_ID:$GROUP_ID /project

WORKDIR /project

USER $USER_ID:$GROUP_ID

ENV PATH "/opt/rust/bin:${PATH}"
ENV RUSTUP_HOME=/opt/rust

# Change `CARGO_HOME` to the bind-bounded directory, so that we don't
# redownload the registry on every build
ENV CARGO_HOME=/project/.cargo-docker-cache/
ENV XARGO_RUST_SRC="/opt/rustc-xtensa-src/"
ENV XTENSA_LLVM_PATH="/opt/llvm-xtensa/"
ENV XTENSA_RUST_PATH="/opt/rustc-xtensa/"
ENV LIBCLANG_PATH="${XTENSA_LLVM_PATH}/lib"
