---
layout: post
title: "Getting Started với Docker - Hướng dẫn cơ bản"
subtitle: "Tìm hiểu Docker từ những khái niệm cơ bản đến thực hành"
date: 2024-01-15
author: "TechSpeaks Team"
categories: [devops, docker, container]
tags: [docker, container, virtualization, devops]
featured: true
image: "/assets/images/docker-intro.jpg"
excerpt: "Docker đã trở thành một công cụ không thể thiếu trong thế giới DevOps. Bài viết này sẽ giúp bạn hiểu rõ về Docker và cách sử dụng nó trong dự án thực tế."
---

Docker đã cách mạng hóa cách chúng ta phát triển, triển khai và quản lý ứng dụng. Trong bài viết này, chúng ta sẽ tìm hiểu về Docker từ những khái niệm cơ bản đến thực hành.

## Docker là gì?

Docker là một nền tảng để phát triển, vận chuyển và chạy ứng dụng trong các container. Container cho phép bạn đóng gói ứng dụng cùng với tất cả dependencies cần thiết vào một đơn vị chuẩn hóa.

### Lợi ích của Docker

- **Tính nhất quán**: Ứng dụng chạy giống nhau ở mọi môi trường
- **Cô lập**: Mỗi container chạy độc lập với hệ thống host
- **Hiệu quả**: Sử dụng ít tài nguyên hơn so với máy ảo
- **Di động**: Dễ dàng di chuyển giữa các môi trường

## Cài đặt Docker

### Trên Ubuntu/Debian

```bash
# Cập nhật package index
sudo apt-get update

# Cài đặt các package cần thiết
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Thêm Docker GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Thêm Docker repository
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Cài đặt Docker Engine
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Thêm user vào docker group
sudo usermod -aG docker $USER
```

### Trên macOS

```bash
# Sử dụng Homebrew
brew install --cask docker

# Hoặc tải từ trang chủ Docker
# https://www.docker.com/products/docker-desktop
```

## Các khái niệm cơ bản

### 1. Image (Hình ảnh)

Image là một template chỉ đọc chứa mã nguồn, runtime, libraries, dependencies và các file cấu hình cần thiết để chạy ứng dụng.

```bash
# Tải image từ Docker Hub
docker pull nginx:latest

# Xem danh sách images
docker images

# Xóa image
docker rmi nginx:latest
```

### 2. Container

Container là một instance có thể chạy của image. Nó là một môi trường cô lập chứa ứng dụng và tất cả dependencies.

```bash
# Chạy container từ image
docker run -d -p 8080:80 --name my-nginx nginx

# Xem danh sách containers đang chạy
docker ps

# Xem tất cả containers
docker ps -a

# Dừng container
docker stop my-nginx

# Xóa container
docker rm my-nginx
```

### 3. Dockerfile

Dockerfile là một file text chứa các instructions để build image.

```dockerfile
# Sử dụng image base
FROM node:18-alpine

# Thiết lập working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Cài đặt dependencies
RUN npm install

# Copy source code
COPY . .

# Expose port
EXPOSE 3000

# Command để chạy ứng dụng
CMD ["npm", "start"]
```

## Thực hành: Tạo ứng dụng Node.js với Docker

### Bước 1: Tạo ứng dụng Node.js đơn giản

```javascript
// app.js
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.json({
    message: 'Hello from Docker!',
    timestamp: new Date().toISOString()
  });
});

app.listen(port, () => {
  console.log(`App running on port ${port}`);
});
```

```json
// package.json
{
  "name": "docker-demo",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

### Bước 2: Tạo Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

### Bước 3: Build và chạy

```bash
# Build image
docker build -t my-node-app .

# Chạy container
docker run -d -p 3000:3000 --name my-app my-node-app

# Kiểm tra ứng dụng
curl http://localhost:3000
```

## Docker Compose

Docker Compose cho phép bạn định nghĩa và chạy multi-container applications.

```yaml
# docker-compose.yml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgresql://user:password@db:5432/myapp

  db:
    image: postgres:13
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

```bash
# Chạy với Docker Compose
docker-compose up -d

# Dừng services
docker-compose down
```

## Best Practices

### 1. Sử dụng Multi-stage builds

```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### 2. Tối ưu hóa image size

- Sử dụng base images nhỏ (alpine)
- Kết hợp RUN commands
- Sử dụng .dockerignore
- Xóa cache và temporary files

### 3. Security

- Không chạy container với root user
- Sử dụng specific versions thay vì latest
- Scan images cho vulnerabilities
- Sử dụng secrets management

## Kết luận

Docker là một công cụ mạnh mẽ giúp đơn giản hóa việc phát triển và triển khai ứng dụng. Trong bài viết tiếp theo, chúng ta sẽ tìm hiểu về Docker networking, volumes và advanced features.

### Tài liệu tham khảo

- [Docker Official Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)

### Series liên quan

- [DevOps từ A đến Z](/series/devops-complete)
- [Container Orchestration với Kubernetes](/series/kubernetes-guide)
- [CI/CD Pipeline với Docker](/series/cicd-docker)

---

**Tags**: #docker #container #devops #virtualization #deployment
