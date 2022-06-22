FROM php:7.0-fpm

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY config/php.ini /usr/local/etc/php/php.ini
COPY config/www.conf /usr/local/etc/php-fpm.d/www.conf
COPY config/php-fpm.conf /usr/local/etc/php-fpm.conf

COPY resources /home/resources
# 替换源
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's|security.debian.org/debian-security|mirrors.ustc.edu.cn/debian-security|g' /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
		git \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install pdo_mysql gd
RUN docker-php-ext-install -j$(nproc) bcmath


RUN pecl install /home/resources/redis-5.3.7.tgz \
	&& docker-php-ext-enable redis

