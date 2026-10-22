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

# Match the usual WSL user so files created in the bind-mounted workspace
# stay owned by the host user instead of root.
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

RUN groupadd --gid "${USER_GID}" "${USERNAME}" \
    && useradd --uid "${USER_UID}" --gid "${USER_GID}" \
               --create-home --shell /bin/bash "${USERNAME}"

USER ${USERNAME}
WORKDIR /workspaces

CMD [ "bash" ]
