FROM golang:1.26-alpine AS builder

WORKDIR /app

COPY . .

RUN CGO_ENABLED=0 GOOS=linux \
    go build -trimpath -o /go-service .

FROM alpine:3.22

WORKDIR /app

COPY --from=builder /go-service /app/go-service

EXPOSE 8081

CMD ["/app/go-service"]