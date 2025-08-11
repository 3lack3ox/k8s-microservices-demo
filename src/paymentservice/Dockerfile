# 1 - Builder Stage

FROM node:20-alpine AS builder

RUN apk add --no-cache python3 make g++

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# 2 - Final Stage

FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app .

EXPOSE 3002

CMD ["node", "index.js"]
