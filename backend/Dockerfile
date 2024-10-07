# 构建阶段
FROM node:18 AS web_builder

WORKDIR /build

# 复制依赖文件并安装 pnpm 和项目依赖
COPY package.json .
COPY pnpm-lock.yaml .
RUN npm install -g pnpm && pnpm install

# 复制项目文件
COPY . ./

# 创建 dist 目录
RUN mkdir -p dist

# 设置环境变量
ENV NODE_OPTIONS=--max_old_space_size=4096

# 运行构建命令
RUN pnpm run build && pnpm run bundle

# 运行阶段
FROM node:18-alpine

WORKDIR /app

# 复制构建产物
COPY --from=web_builder /build/dist/sub-store.bundle.js .

# 创建 config 目录
RUN mkdir -p config

# 设置环境变量
ENV SUB_STORE_DATA_BASE_PATH=/app/config

# 暴露端口
EXPOSE 3000

# 使用 JSON 格式的 CMD 指令
CMD ["node", "sub-store.bundle.js"]
