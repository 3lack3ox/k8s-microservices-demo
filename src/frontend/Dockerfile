# Stage 1 - Build Stage
FROM golang:1.23-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o frontend .
    
# Stage 2 - Runtime Stage
FROM alpine:latest
    
WORKDIR /app

COPY --from=builder /app/frontend .
COPY --from=builder /app/templates ./templates    

EXPOSE 3000

CMD ["./frontend"]