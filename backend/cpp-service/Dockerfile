# Stage 1: Build
FROM debian:bookworm AS builder

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        ca-certificates && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY . .

RUN cmake -S . -B build \
        -DCMAKE_BUILD_TYPE=Release && \
    cmake --build build --parallel

# Stage 2: Runtime
FROM debian:bookworm-slim

WORKDIR /app

COPY --from=builder /app/build/cpp-service /app/cpp-service

EXPOSE 9001

CMD ["/app/cpp-service"]