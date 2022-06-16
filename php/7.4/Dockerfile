FROM php:7.4-fpm

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}

COPY config/php.ini /usr/local/etc/php/php.ini
COPY config/www.conf /usr/local/etc/php-fpm.d/www.conf
COPY config/php-fpm.conf /usr/local/etc/php-fpm.conf

COPY resources /home/resources


RUN pecl install /home/resources/redis-5.3.7.tgz \
	&& docker-php-ext-enable redis
