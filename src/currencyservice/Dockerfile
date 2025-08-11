# Stage 1 - Build
FROM node:20-alpine AS builder

WORKDIR /app

RUN apk add --no-cache python3 make g++ 

COPY package*.json ./
RUN npm install

COPY . .

# Stage 2 - Runtime
FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app /app

EXPOSE 7000

CMD ["node", "server.js"]
