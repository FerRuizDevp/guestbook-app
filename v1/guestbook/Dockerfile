# Use Go 1.18 on Alpine for building
FROM golang:1.18-alpine AS builder

WORKDIR /app

# Copy all files into the container
COPY . .

# Build the Go application
# Build the app WITHOUT go.mod by specifying the file directly
RUN go build -o guestbook main.go

# Use a lightweight Alpine image for the final container
FROM alpine:latest
WORKDIR /app

# Copy the built executable
COPY --from=builder /app/guestbook .

# Copy the public folder with static files
COPY --from=builder /app/public ./public

# Expose port 3000
EXPOSE 3000

# Run the Go application

# Make the guestbook binary executable
RUN chmod +x ./guestbook

# Set the default command
CMD ["./guestbook"]


