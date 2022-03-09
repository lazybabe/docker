FROM --platform=$BUILDPLATFORM pratikimprowise/upx AS upx

FROM golang:1.17-alpine AS go-builder

COPY --from=upx / /

ENV GOPROXY="https://goproxy.io"

RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.27.1 \
    && go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2.0 \
    && go install github.com/envoyproxy/protoc-gen-validate@v0.6.7 \
    && go install github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway@v1.16.0 \
    && go install github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger@v1.16.0 \
    && go install github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@v1.5.1 \
    && go install github.com/gogo/protobuf/protoc-gen-gogo@v1.3.2 \
    && upx --lzma /go/bin/*

FROM alpine:3

COPY --from=go-builder /go/bin/* /usr/local/bin/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --no-cache protobuf=3.18.1-r1 protobuf-dev=3.18.1-r1

ENTRYPOINT ["/usr/bin/protoc"]
