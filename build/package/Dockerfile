FROM golang:1.13 AS builder
WORKDIR /app

# copy resources
COPY . .

# build the server
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /build/server ./cmd/server

# second stage
FROM alpine:latest
WORKDIR /app

# install certificates
RUN apk update && apk add ca-certificates && update-ca-certificates && rm -rf /var/cache/apk/*

COPY --from=builder /build /app
ENTRYPOINT ["./server"]