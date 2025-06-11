# Iris Photo Gallery Docker 部署

一个基于 Docker 的 [Iris Photo Gallery](https://github.com/Iris-Photo-Gallery/iris) 部署方案，让您能够快速部署现代化的照片画廊网站。

## 🚀 快速开始

### 环境要求

- Docker
- Docker Compose (可选)

### 1. 修改配置文件

**`config.json`**

```json
{
  "name": "Your Photo Gallery", // 网站名称
  "title": "Your Photo Gallery", // 页面标题
  "description": "Capturing beautiful moments in life", // 网站描述
  "url": "https://", // 个人 URL
  "accentColor": "#fb7185", // 主题色
  "author": {
    "name": "Your Name",
    "url": "https://your-website.com",
    "avatar": "https://your-avatar-url.com/avatar.png"
  },
  "social": {
    "twitter": "@yourusername"
  },
  "extra": {
    "accessRepo": true
  }
}
```

**`builder.config.json`**

```json
{
  "repo": { // 使用远端仓库作为 manifest 和 thumbnail 缓存
    "enable": false,
    "url": "https://github.com/username/gallery-public"
  },
  "storage": { // 存储配置
    "provider": "s3",
    "bucket": "your-photos-bucket",
    "region": "us-east-1",
    "prefix": "photos/",
    "customDomain": "cdn.yourdomain.com"
  }
}
```

### 2. 构建 Docker 镜像

```bash
docker build -t iris-gallery .
```

### 3. 运行容器

```bash
docker run -p 3000:3000 iris-gallery
```

或者使用 Docker Compose:

```yaml
version: '3.8'
services:
  iris-gallery:
    build: .
    ports:
      - '3000:3000'
    environment:
      - NODE_ENV=production
    volumes:
      - ./config.json:/app/config.json
      - ./builder.config.json:/app/builder.config.json
      - ./.env:/app/.env
```

## ⚙️ 环境变量配置

### S3 存储配置

```bash
S3_REGION=us-east-1 # 非敏感参数可以在 builder.config.json 中设置
S3_ACCESS_KEY_ID=your_access_key_id
S3_SECRET_ACCESS_KEY=your_secret_access_key
S3_ENDPOINT=https://s3.amazonaws.com
S3_BUCKET_NAME=your_bucket_name
S3_PREFIX=photos/
S3_CUSTOM_DOMAIN=cdn.yourdomain.com  # 可选
```

## 🔧 自定义配置

### 修改配置文件

1. 编辑 `config.json` 设置网站基本信息
2. 编辑 `builder.config.json` 配置存储和构建选项
3. 重新构建 Docker 镜像

### 添加环境变量文件

创建 `.env` 文件：

```env
S3_REGION=us-east-1
S3_ACCESS_KEY_ID=your_key
S3_SECRET_ACCESS_KEY=your_secret
S3_BUCKET_NAME=your_bucket
```

## 📦 部署选项

### 本地部署

```bash
docker run -d \
  --name iris-gallery \
  -p 3000:3000 \
  --env-file .env \
  iris-gallery
```

### 云平台部署

支持部署到：

- Railway
- Render
- DigitalOcean App Platform
- AWS ECS
- Google Cloud Run

### 日志查看

```bash
docker logs iris-gallery
```

### 进入容器调试

```bash
docker exec -it iris-gallery sh
```

## 📄 许可证

MIT License © 2025

## 🔗 相关链接

- [Iris Photo Gallery 源码](https://github.com/Iris-Photo-Gallery/iris)
- [在线演示](https://gallery.innei.in)
- [作者主页](https://innei.in)

## 🤝 贡献

欢迎提交 Issues 和 Pull Requests 来改进这个 Docker 部署方案。
