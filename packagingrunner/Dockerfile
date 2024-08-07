# Use an ARM-compatible Ubuntu base image
FROM runbase:0.0.1
ENV https_proxy http://10.0.0.214:7890
ENV http_proxy http://10.0.0.214:7890
# Install rbenv and required Ruby version (similar to what quay.io/dennybaa/droneruby does)
# Use an ARM-compatible Ubuntu base image

# 使用ARM架构的Ubuntu基础镜像

# 安装必要的包
RUN apt-get update && apt-get install -y \
    git \
    curl \
    autoconf \
    bison \
    build-essential \
    libssl-dev \
    libyaml-dev \
    libreadline-dev \
    zlib1g-dev \
    libncurses5-dev \
    libffi-dev \
    libgdbm-dev \
    netcat \
    && apt-get clean

# 克隆rbenv和ruby-build
ADD Gemfile /root/Gemfile

RUN ~/.rbenv/bin/rbenv exec bundle --gemfile=/root/Gemfile
# 复制入口点脚本
COPY busybee /root/.ssh/busybee
COPY busybee.pub /root/.ssh/busybee.pub
COPY busybee /root/.ssh/authorized_keys
COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]

