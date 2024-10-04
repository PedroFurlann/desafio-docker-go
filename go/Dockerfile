FROM golang:1.23-alpine3.20 AS builder

RUN apk add --no-cache upx

WORKDIR /app

COPY . .

RUN go mod init fullcycle-go

RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -o fullcycle-go .

RUN upx --best fullcycle-go

FROM scratch

COPY --from=builder /app/fullcycle-go /fullcycle-go

ENTRYPOINT ["/fullcycle-go"]
