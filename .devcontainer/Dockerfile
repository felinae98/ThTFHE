# FROM debian as runtime
FROM ubuntu as runtime

WORKDIR /work
RUN rm -f /etc/apt/apt.conf.d/docker-clean; echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' > /etc/apt/apt.conf.d/keep-cache
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    --mount=type=cache,target=/var/lib/apt,sharing=locked \
    apt-get update && apt-get install -y build-essential git cmake libboost-dev curl
ADD . .

RUN cd tfhe && \
    make && make install && cd ..
RUN cd OpenBLAS && \
    make && make PREFIX=/usr/local install && cd ..

# FROM runtime as dev
# RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
#     --mount=type=cache,target=/var/lib/apt,sharing=locked \
#     apt-get update && apt-get install -y nodejs python3
# RUN cd /tmp && \
#     curl -LO https://github.com/neovim/neovim/releases/download/stable/nvim.appimage && \
#     chmod +x ./nvim.appimage && \
#     ./nvim.appimage --appimage-extract && \
#     mv squashfs-root / && \
#     ln -s /squashfs-root/AppRun /usr/bin/nvim

# FROM runtime as dev-container
# RUN curl -sSL "https://update.code.visualstudio.com/stable/server-linux-x64/stable" -o vscode-server-linux-x64.tar.gz && \
#     mkdir -p ~/.vscode-server/bin/stable

