# Stage 1 - Builder
FROM python:3.12-alpine AS builder

WORKDIR /app

RUN apk add --no-cache gcc musl-dev libffi-dev g++ make linux-headers

COPY requirements.txt .
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# Stage 2 - Runtime
FROM python:3.12-alpine

ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN apk add --no-cache libffi libstdc++

COPY --from=builder /install /usr/local

COPY . .

EXPOSE 8080

CMD ["python", "recommendation_server.py"]

