FROM debian:buster-slim as builder

RUN apt-get update && \
    apt-get install -y curl xz-utils

RUN mkdir -p /deps
WORKDIR /deps
RUN curl https://ziglang.org/download/0.8.0/zig-linux-"$(uname -m)"-0.8.0.tar.xz  -O && \
    tar xf zig-linux-"$(uname -m)"-0.8.0.tar.xz && \
    mv zig-linux-"$(uname -m)"-0.8.0 local/

FROM debian:buster-slim
COPY --from=builder /deps/local/ /deps/local/
RUN ln -s /deps/local/zig /usr/bin/zig

RUN mkdir -p /opt/app
WORKDIR /opt/app
COPY . .
RUN zig build -Drelease-fast

ENTRYPOINT [ "./zig-out/bin/PrimeZig" ]
