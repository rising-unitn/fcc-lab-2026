# The final image contains only the statically-compiled binary - nothing else.
FROM ubuntu:24.04 AS builder
RUN apt-get update && apt-get install -y golang-go
WORKDIR /app
COPY main.go .
# CGO_ENABLED=0 produces a fully static binary with no libc dependency,
# which is required when using 'scratch' as the base image.
RUN CGO_ENABLED=0 go build -o hello main.go

FROM scratch
COPY --from=builder /app/hello /hello
CMD ["/hello"]
