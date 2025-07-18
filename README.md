# TechSpeaks - Chia sẻ kiến thức công nghệ

[![TechSpeaks](https://img.shields.io/badge/TechSpeaks-Landing%20Page-blue?style=for-the-badge&logo=github)](https://techspeaks.github.io)
[![Jekyll](https://img.shields.io/badge/Jekyll-4.3.0-red?style=flat-square&logo=jekyll)](https://jekyllrb.com/)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3.0-purple?style=flat-square&logo=bootstrap)](https://getbootstrap.com/)

> Landing page chính thức của TechSpeaks - Nơi chia sẻ kiến thức công nghệ chất lượng đến cộng đồng lập trình viên Việt Nam.

## 🌟 Tính năng

- **Trang chủ hiện đại** với hero section và featured content
- **Blog system** với Jekyll - dễ viết và quản lý bài viết
- **Series management** - tổ chức bài viết theo chuỗi
- **Responsive design** - tối ưu cho mọi thiết bị
- **SEO friendly** - tích hợp meta tags và sitemap
- **Search & Filter** - tìm kiếm bài viết theo chủ đề
- **Newsletter signup** - đăng ký nhận bài viết mới
- **Social integration** - liên kết với GitHub, Twitter, LinkedIn

## 🚀 Công nghệ sử dụng

- **Jekyll 4.3.0** - Static site generator
- **Bootstrap 5.3.0** - CSS framework
- **Font Awesome 6.4.0** - Icons
- **Google Fonts (Inter)** - Typography
- **JavaScript ES6+** - Interactive features

## 📁 Cấu trúc dự án

```
techspeaks.github.io/
├── _config.yml              # Cấu hình Jekyll
├── _layouts/                # Layout templates
│   ├── default.html         # Layout chính
│   ├── page.html           # Layout cho trang tĩnh
│   └── post.html           # Layout cho bài viết
├── _posts/                 # Bài viết blog
│   └── 2024-01-15-getting-started-with-docker.md
├── _series/                # Series bài viết
├── assets/                 # Static assets
│   ├── css/
│   │   └── style.css       # Custom CSS
│   ├── js/
│   │   └── main.js         # Custom JavaScript
│   └── images/             # Images
├── blog/                   # Trang danh sách bài viết
│   └── index.html
├── series/                 # Trang danh sách series
│   └── index.html
├── about.html              # Trang About
├── index.html              # Trang chủ
├── Gemfile                 # Ruby dependencies
└── README.md               # Documentation
```

## 🛠️ Cài đặt và chạy locally

### Yêu cầu hệ thống

- Ruby 2.7.0 hoặc cao hơn
- RubyGems
- GCC và Make

### Bước 1: Clone repository

```bash
git clone https://github.com/techspeaks/techspeaks.github.io.git
cd techspeaks.github.io
```

### Bước 2: Cài đặt dependencies

```bash
# Cài đặt Bundler nếu chưa có
gem install bundler

# Cài đặt Jekyll và các plugins
bundle install
```

### Bước 3: Chạy development server

```bash
# Chạy Jekyll server
bundle exec jekyll serve

# Hoặc với live reload
bundle exec jekyll serve --livereload
```

Website sẽ chạy tại: `http://localhost:4000`

## ✍️ Viết bài viết mới

### Tạo bài viết

```bash
# Tạo file markdown mới trong _posts/
# Format: YYYY-MM-DD-title.md
```

### Front matter cho bài viết

```yaml
---
layout: post
title: "Tiêu đề bài viết"
subtitle: "Phụ đề (tùy chọn)"
date: 2024-01-15
author: "TechSpeaks Team"
categories: [devops, docker, container]
tags: [docker, container, virtualization, devops]
featured: true  # Hiển thị ở trang chủ
image: "/assets/images/featured-image.jpg"
excerpt: "Mô tả ngắn gọn về bài viết..."
---
```

### Tạo series mới

```bash
# Tạo file markdown trong _series/
# Ví dụ: _series/docker-complete-guide.md
```

### Front matter cho series

```yaml
---
layout: series
title: "Docker Complete Guide"
description: "Hướng dẫn toàn diện về Docker từ cơ bản đến nâng cao"
featured: true
duration: "4-5"
level: "Trung cấp"
topics: [docker, container, devops, kubernetes]
posts:
  - title: "Getting Started với Docker"
    url: "/blog/getting-started-with-docker"
  - title: "Docker Networking"
    url: "/blog/docker-networking"
---
```

## 🎨 Tùy chỉnh giao diện

### Thay đổi màu sắc

Chỉnh sửa CSS variables trong `assets/css/style.css`:

```css
:root {
    --primary-color: #0d6efd;
    --secondary-color: #6c757d;
    --success-color: #198754;
    --warning-color: #ffc107;
    --info-color: #0dcaf0;
    --dark-color: #212529;
    --light-color: #f8f9fa;
}
```

### Thay đổi thông tin website

Cập nhật `_config.yml`:

```yaml
title: TechSpeaks
description: Chia sẻ kiến thức công nghệ, bài viết và series về lập trình, DevOps, và các công nghệ mới
author: TechSpeaks Team
email: contact@techspeaks.dev
url: "https://techspeaks.github.io"

# Social media
social:
  github: techspeaks
  twitter: techspeaks_dev
  linkedin: techspeaks
```

## 📝 Quản lý nội dung

### Categories và Tags

- **Categories**: Phân loại chính (devops, programming, cloud, database, security, ai-ml)
- **Tags**: Từ khóa chi tiết hơn

### Images

- Đặt images trong `assets/images/`
- Sử dụng format: `YYYY-MM-DD-title.jpg`
- Tối ưu hóa kích thước (khuyến nghị < 500KB)

### External Series

Để liên kết đến series trong repo khác, thêm vào trang series:

```html
<div class="card border-success">
  <div class="card-header bg-success text-white">
    <i class="fab fa-github me-2"></i>
    Tên Series
  </div>
  <div class="card-body">
    <p class="card-text">Mô tả series...</p>
    <a href="https://github.com/techspeaks/repo-name" class="btn btn-success btn-sm">
      Xem trên GitHub
    </a>
  </div>
</div>
```

## 🚀 Deploy

### GitHub Pages (Tự động)

1. Push code lên repository `techspeaks/techspeaks.github.io`
2. GitHub Pages sẽ tự động build và deploy
3. Website sẽ có sẵn tại `https://techspeaks.github.io`

### Manual Deploy

```bash
# Build static files
bundle exec jekyll build

# Deploy lên server
# Copy _site/ lên web server
```

## 🤝 Đóng góp

Chúng tôi rất hoan nghênh mọi đóng góp! Hãy:

1. Fork repository
2. Tạo feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Tạo Pull Request

### Guidelines cho bài viết

- Viết bằng tiếng Việt hoặc tiếng Anh
- Sử dụng Markdown format
- Thêm code examples khi có thể
- Kiểm tra grammar và spelling
- Thêm images minh họa nếu cần

## 📞 Liên hệ

- **Email**: <contact@techspeaks.dev>
- **GitHub**: [@techspeaks](https://github.com/techspeaks)
- **Twitter**: [@techspeaks_dev](https://twitter.com/techspeaks_dev)
- **LinkedIn**: [TechSpeaks](https://linkedin.com/company/techspeaks)

## 📄 License

Dự án này được phân phối dưới giấy phép MIT. Xem file `LICENSE` để biết thêm chi tiết.

---

***Made with ❤️ by TechSpeaks Team***
