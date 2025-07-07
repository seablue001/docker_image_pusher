FROM php:8.1-fpm

# 设置时区，保证日志和应用时间一致
ENV TZ=Asia/Shanghai

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libonig-dev \
        gcc g++ make autoconf libc-dev pkg-config libssl-dev \
        libpng-dev libjpeg-dev libfreetype6-dev libzip-dev zip unzip \
        libcurl4-openssl-dev \
    # 安装 PHP 常用扩展
    && docker-php-ext-install pdo_mysql mysqli gd mbstring sockets curl opcache fileinfo zip \
    # 安装 igbinary 和 redis 扩展（如需指定版本可写 pecl install redis-5.3.7）
    && pecl install igbinary redis \
    && docker-php-ext-enable igbinary redis \
    # SQL Server 驱动及扩展（如需支持，建议基础镜像用 bullseye，否则注释以下内容）
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 \
    && pecl install pdo_sqlsrv sqlsrv \
    && docker-php-ext-enable pdo_sqlsrv sqlsrv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www/html