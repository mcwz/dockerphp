FROM php:7.0-fpm

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
    sed -i 's/snapshot.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
    sed -i 's/security-cdn.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd


ARG RUN_USER_UID=83
ARG RUN_USER_GID=83

RUN userdel www-data && \
#    groupdel www-data && \
    groupadd -g ${RUN_USER_GID} www-data && \
    useradd -g www-data -u ${RUN_USER_UID} www-data && \
    usermod -s /sbin/nologin www-data
