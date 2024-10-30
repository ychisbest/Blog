---
title: 使用Caddy进行反向代理
external: false
date: 2024-10-30
---
Caddy是一个现代化的Web服务器，具有自动HTTPS功能和简单的配置语法。本文将介绍如何使用Docker部署Caddy并实现自动HTTPS配置。

### 准备工作

1. 确保服务器已安装Docker
2. 准备好域名(ych.show)并完成DNS解析
3. 确保80和443端口可用

### 创建Caddyfile

首先创建Caddy的配置文件`Caddyfile`:

```
ych.show {
    reverse_proxy http://127.0.0.1:8080
}
```

### 部署Caddy
使用docker部署Caddy:
```
docker run -d --name caddy -p 80:80 -p 8080:8080 -p 443:443 -v ./Caddyfile:/etc/caddy/Caddyfile --restart=always caddy/caddy:2.9.4-builder-alpine
```

### 测试

在浏览器中访问`ych.show`，应该能够看到网站内容，并且是自动HTTPS的，不需要手动配置SSL证书，非常方便。
