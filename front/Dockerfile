# --------------------
# 第一阶段：下载
# --------------------
FROM alpine AS downloader

WORKDIR /app

# 更新包列表并安装curl
RUN apk update && apk add curl

# 下载 nginx.conf 和前端构建产物 dist.zip
RUN curl -LJOk https://sub-store-org.github.io/resource/ssm/nginx.conf && \
    curl -LJOk https://github.com/sub-store-org/Sub-Store-Front-End/releases/latest/download/dist.zip && \
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
COPY --from=downloader /app/nginx.conf /etc/nginx/conf.d/default.conf

# 暴露端口
EXPOSE 80

# 启动 Nginx，保持前台运行
CMD ["nginx", "-g", "daemon off;"]
