FROM golang:1.22.7-alpine AS builder

RUN apk add --no-cache git

RUN adduser -D -g '' appuser

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -ldflags="-w -s" -o momo-store ./cmd/api

FROM alpine:3.18

RUN apk add --no-cache ca-certificates tzdata && \
    update-ca-certificates

RUN addgroup -g 1001 -S appgroup && \
    adduser -u 1001 -S appuser -G appgroup

WORKDIR /app

COPY --from=builder /app/momo-store .

USER appuser

EXPOSE 8081

# healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -q --spider http://localhost:8081/health || exit 1

CMD ["./momo-store"]
