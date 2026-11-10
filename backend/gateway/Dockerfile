# Stage 1: Build
FROM golang:1.26-alpine AS builder

WORKDIR /app

COPY . .

RUN CGO_ENABLED=0 GOOS=linux \
    go build -trimpath -o /gateway .

# Stage 2: Runtime
FROM alpine:3.22

WORKDIR /app

COPY --from=builder /gateway /app/gateway

EXPOSE 8080

CMD ["/app/gateway"]