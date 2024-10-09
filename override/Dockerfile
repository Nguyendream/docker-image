FROM golang:alpine AS builder

WORKDIR /app
RUN apk update && apk add --no-cache git bash && go mod download 

RUN git clone https://github.com/linux-do/override.git .

RUN CGO_ENABLED=0 go build -ldflags="-w -s" -o override

FROM alpine:latest

RUN apk --no-cache add ca-certificates

COPY --from=builder /app/override /usr/local/bin/
COPY --from=builder /app/config.json.example /app/config.json

WORKDIR /app

EXPOSE 8181
CMD ["override"]