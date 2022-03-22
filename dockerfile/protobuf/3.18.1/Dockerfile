FROM --platform=$TARGETPLATFORM golang:1.17-alpine AS go-builder

ENV GOPROXY="https://goproxy.cn,direct"

RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.27.1 \
    && go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2.0 \
    && go install github.com/envoyproxy/protoc-gen-validate@v0.6.7 \
    && go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway@v2.8.0 \
    && go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2@v2.8.0 \
    && go install github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@v1.5.1

FROM alpine:3

COPY --from=go-builder /go/bin/* /usr/local/bin

COPY ./google/api  /usr/include/google/api
COPY ./protoc-gen-openapiv2  /usr/include/protoc-gen-openapiv2

RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories \
    && apk add --no-cache protobuf=3.18.1-r1 protobuf-dev=3.18.1-r1

ENTRYPOINT ["/usr/bin/protoc"]
