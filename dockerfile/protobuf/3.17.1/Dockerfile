FROM golang:1.16-alpine AS go-builder

RUN apk add upx \
    && go get -u google.golang.org/protobuf/cmd/protoc-gen-go@v1.26.0 \
    && go get -u google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.1.0 \
    && go get -u github.com/envoyproxy/protoc-gen-validate@v0.6.1 \
    && go get -u github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@v1.4.1 \
    && go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger@v1.16.0 \
    && go get -u github.com/gogo/protobuf/protoc-gen-gogo@v1.3.2 \
    && upx --lzma $GOPATH/bin/*

FROM memominsk/protobuf-alpine:3.17.1

COPY --from=go-builder /go/bin/* /usr/local/bin/