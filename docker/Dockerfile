FROM rust:1.48.0-buster AS builder

COPY ./ /app
WORKDIR /app
RUN make setup
RUN make build

FROM debian:buster
COPY --from=builder /app/target/release/datafuse-query /datafuse-query
COPY --from=builder /app/target/release/datafuse-store /datafuse-store
COPY --from=builder /app/docker/datafuse-query-docker.toml /datafuse-query.toml
COPY --from=builder /app/docker/bootstrap.sh /bootstrap.sh
ENTRYPOINT ["/bootstrap.sh"]
