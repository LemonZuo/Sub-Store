# --------------------
# 第一阶段：下载
# --------------------
FROM alpine AS downloader

WORKDIR /app

# 安装curl、下载sub-store.bundle.js
RUN wget -O sub-store.bundle.js https://github.com/sub-store-org/Sub-Store/releases/latest/download/sub-store.bundle.js

# --------------------
# 第二阶段：构建运行镜像
# --------------------
FROM node:18-alpine AS runner

WORKDIR /app

# 复制构建产物
COPY --from=downloader /app/sub-store.bundle.js .

# 创建 config 目录
RUN mkdir -p config

# 设置环境变量
ENV SUB_STORE_DATA_BASE_PATH=/app/config

# 暴露端口
EXPOSE 3000

# 使用 JSON 格式的 CMD 指令
CMD ["node", "sub-store.bundle.js"]
