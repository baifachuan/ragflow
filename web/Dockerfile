FROM openresty/openresty:latest
COPY sources.list /etc/apt/
RUN apt-get update && apt-get install -y \
    luarocks \
    luajit \
    git \
    libpcre3 \
    libpcre3-dev \
 && rm -rf /var/lib/apt/lists/*

# 安装Lua-RESTy-Prometheus模块
RUN luarocks install nginx-lua-prometheus

# 添加 nginx 用户和用户组
RUN adduser --disabled-password --gecos '' nginx

# 拷贝nginx配置文件
COPY nginx/nginx.conf /usr/local/openresty/nginx/conf/nginx.conf
# 从构建阶段拷贝应用程序
COPY dist /usr/local/openresty/nginx/html
# 更改文件权限
RUN chown -R nginx:nginx /usr/local/openresty/nginx/html