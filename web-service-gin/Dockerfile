# Stage 1: Build
FROM golang:1.23 AS builder
WORKDIR /app
COPY . .
RUN go mod tidy
RUN CGO_ENABLED=0 GOOS=linux go build -o main

# Stage 2: Production
FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/main .
# Make sure binary is executable
RUN chmod +x main
CMD ["./main"]
EXPOSE 8085
