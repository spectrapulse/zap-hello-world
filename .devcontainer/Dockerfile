FROM mcr.microsoft.com/devcontainers/base:ubuntu-20.04

ARG ZIG_VERSION="0.13.0"

RUN apt-get update \
    && apt-get -y install software-properties-common wget xz-utils \
    && add-apt-repository -y ppa:savoury1/minisign \
    && apt-get update \
    && apt-get -y install minisign 

# Install Zig
RUN ARCH=$(uname -m) \
    && cd /tmp \
    && wget https://ziglang.org/download/${ZIG_VERSION}/zig-linux-${ARCH}-${ZIG_VERSION}.tar.xz -O zig-linux.tar.xz \
    && wget https://ziglang.org/download/${ZIG_VERSION}/zig-linux-${ARCH}-${ZIG_VERSION}.tar.xz.minisig -O zig-linux.tar.xz.minisig \
    && minisign -Vm zig-linux.tar.xz -P "RWSGOq2NVecA2UPNdBUZykf1CCb147pkmdtYxgb3Ti+JO/wCYvhbAb/U" \
    && tar -xvf zig-linux.tar.xz -C /usr/local \
    && rm -vf zig-linux.tar.xz* \
    && mv -v /usr/local/zig-linux-${ARCH}-${ZIG_VERSION} /usr/local/zig \
    && ln -sv /usr/local/zig/zig /usr/local/bin/zig

# Install ZLS
RUN ARCH=$(uname -m) \
    && cd /tmp \
    && wget https://builds.zigtools.org/zls-linux-${ARCH}-${ZIG_VERSION}.tar.xz -O zls-linux.tar.xz \
    && wget https://builds.zigtools.org/zls-linux-${ARCH}-${ZIG_VERSION}.tar.xz.minisig -O zls-linux.tar.xz.minisig \
    && minisign -Vm zls-linux.tar.xz -P "RWR+9B91GBZ0zOjh6Lr17+zKf5BoSuFvrx2xSeDE57uIYvnKBGmMjOex" \
    && tar -xvf zls-linux.tar.xz -C /usr/local/bin/ zls \
    && rm -vf zls-linux.tar.xz* \
    && chmod +x /usr/local/bin/zls
