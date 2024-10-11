# --------------------
# 第一阶段：下载
# --------------------
FROM alpine AS downloader

WORKDIR /app

# 下载 前端构建产物 dist.zip
RUN wget -O dist.zip https://github.com/sub-store-org/Sub-Store-Front-End/releases/latest/download/dist.zip && \
    unzip dist.zip && \
    rm dist.zip

# --------------------
# 第二阶段：构建运行镜像
# --------------------
FROM nginx:alpine AS runner

WORKDIR /app

# 复制前端构建产物到 Nginx 的默认网站目录
COPY --from=downloader /app/dist ./www

# 复制自定义的 nginx.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 暴露端口
EXPOSE 80

# 启动 Nginx，保持前台运行
CMD ["nginx", "-g", "daemon off;"]
