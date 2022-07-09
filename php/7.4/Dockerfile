FROM php:7.4-fpm

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# COPY ../../work/php74/config/php.ini /usr/local/etc/php/php.ini
# COPY ../../work/php74/config/www.conf /usr/local/etc/php-fpm.d/www.conf
# COPY ../../work/php74/config/php-fpm.conf /usr/local/etc/php-fpm.conf

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
	&& docker-php-ext-install -j$(nproc) gd pdo pdo_mysql bcmath

RUN pecl install /home/resources/redis-5.3.7.tgz \
	&& docker-php-ext-enable redis

# RUN pecl install /home/resources/mcrypt-1.0.5.tgz \
# 	&& docker-php-ext-enable mcrypt

# composer
RUN php /home/resources/installer.php
RUN php -r "unlink('/home/resources/installer.php');"


RUN mv composer.phar /usr/local/bin/composer
#全局切换阿里源
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

RUN composer config -g github-oauth.github.com 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s