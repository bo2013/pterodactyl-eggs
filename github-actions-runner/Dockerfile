# syntax=docker/dockerfile:1

ARG DISTRO=ubuntu:24.04

FROM ${DISTRO}

ARG GAR_VERSION=2.336.0
ARG GAR_CHECKSUM=04cf0be1aff4c3ec3554466c39124ca250e3effd8873bb7e8d68535aa9505d5d

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN groupadd container && \
    useradd -d /home/container -m -g container container && \
    mkdir -p /home/container/actions-runner

RUN --mount=type=tmpfs,target=/tmp \
    curl -o /tmp/actions-runner-linux-x64-${GAR_VERSION}.tar.gz -L \
    https://github.com/actions/runner/releases/download/v${GAR_VERSION}/actions-runner-linux-x64-${GAR_VERSION}.tar.gz && \
    echo "${GAR_CHECKSUM}  /tmp/actions-runner-linux-x64-${GAR_VERSION}.tar.gz" | sha256sum -c - && \
    tar xzf /tmp/actions-runner-linux-x64-${GAR_VERSION}.tar.gz -C /home/container/actions-runner && \
    chown -R container:container /home/container

WORKDIR /home/container/actions-runner
USER container
ENTRYPOINT [ "/bin/bash", "-c" ]