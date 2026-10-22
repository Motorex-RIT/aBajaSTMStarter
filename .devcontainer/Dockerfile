# Development image for the aBaja STM32 starter.
#
# Plain Ubuntu + distro packages: no Nix required, by design.
# Keep the package list in sync with the maintainer's local flake so both
# environments provide the same toolchain (the flake is not used to build this
# image).

FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        ninja-build \
        gcc-arm-none-eabi \
        binutils-arm-none-eabi \
        libnewlib-arm-none-eabi \
        libstdc++-arm-none-eabi-newlib \
        gdb-multiarch \
        openocd \
        minicom \
        git \
        python3 \
        python3-pip \
        pkg-config \
        automake \
        autoconf \
        texinfo \
        libtool \
        libftdi1-dev \
        libusb-1.0-0-dev \
        zsh \
        ca-certificates \
        curl \
    && rm -rf /var/lib/apt/lists/*

# ubuntu:24.04 already provides an `ubuntu` user with UID/GID 1000
# (member of sudo, video and plugdev), so reuse it instead of creating
# another user. Dev Containers rewrites the UID at runtime when the host
# user differs.
USER ubuntu

WORKDIR /workspaces

CMD [ "bash" ]
