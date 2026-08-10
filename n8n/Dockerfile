ARG N8N_VERSION=latest

FROM docker.n8n.io/n8nio/n8n:${N8N_VERSION}

RUN addgroup -S container && \
    adduser -S -G container -h /home/container container && \
    mkdir -p /home/container && \
    chown -R container:container /home/container

WORKDIR /home/container
USER node