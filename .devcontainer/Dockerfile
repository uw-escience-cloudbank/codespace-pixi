FROM mcr.microsoft.com/devcontainers/base:ubuntu26.04

ARG PIXI_VERSION=v0.71.2

RUN curl -L -o /usr/local/bin/pixi -fsSL --compressed "https://github.com/prefix-dev/pixi/releases/download/${PIXI_VERSION}/pixi-$(uname -m)-unknown-linux-musl" \
    && chmod +x /usr/local/bin/pixi \
    && pixi info

ENV VSCODE_HOME=/home/vscode \
    VSCODE_USER=vscode \
    SHELL=/bin/bash

# set some user and workdir settings to work nicely with vscode
USER ${VSCODE_USER}
WORKDIR /home/vscode

RUN echo 'eval "$(pixi completion -s bash)"' >> ${VSCODE_HOME}/.bashrc

# Pre-populate the pixi package cache so that onCreateCommand's `pixi install`
# resolves packages from disk instead of downloading from conda-forge.
# The .pixi env directory is removed afterwards because it will be created
# inside the Docker volume mount at container-create time.
COPY --chown=${VSCODE_USER}:${VSCODE_USER} pixi.toml pixi.lock /tmp/pixi-warmup/
RUN cd /tmp/pixi-warmup \
    && pixi install --locked \
    && rm -rf /tmp/pixi-warmup/.pixi \
    && rm -rf /tmp/pixi-warmup
