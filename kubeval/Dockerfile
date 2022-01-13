# Prepared special for Jenkins docker agent
# Official Docker Hub image - garethr/kubeval

FROM golang:1.12-alpine as builder

ARG KUBEVAL_RELEASE=0.15.0

RUN set -ex && \
    apk --no-cache add make git

WORKDIR /

RUN set -ex && \
    git clone https://github.com/instrumenta/kubeval && \
    cd /kubeval && \
    git checkout tags/${KUBEVAL_RELEASE} && \
    make build

FROM alpine:latest

RUN set -ex && \
    apk --no-cache add ca-certificates

COPY --from=builder /kubeval/bin/kubeval .

RUN set -ex && \
    ln -s /kubeval /usr/local/bin/kubeval

CMD ["sh"]
