FROM golang:1.12-alpine as builder

RUN apk add --no-cache make gcc musl-dev linux-headers git

RUN wget https://github.com/ethereum/go-ethereum/archive/v1.8.27.tar.gz && \
    mkdir -p /opt && \
    tar xf v1.8.27.tar.gz -C /opt && \
    mv /opt/go-ethereum-1.8.27 /opt/geth && \
    ls /opt/geth

WORKDIR /opt/geth

RUN make geth

FROM alpine:3.9

RUN apk add --no-cache ca-certificates

COPY --from=builder /opt/geth/build/bin/geth /usr/local/bin/

ENTRYPOINT ["geth"]
