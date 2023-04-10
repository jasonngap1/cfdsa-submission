FROM golang:1.20-alpine3.17 AS builder

WORKDIR /app

COPY main.go .
COPY go.mod .
COPY go.sum .

RUN go build -o main .

# this is call multi-container stage builds
FROM alpine:3.17

WORKDIR /app

COPY public public
COPY templates templates
COPY --from=builder /app/main .

ENV PORT=3000
ENV INSTANCE_NAME="my dov-bear"

EXPOSE ${PORT}

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl localhost:${PORT}/healthz || exit 1

ENTRYPOINT /app/main