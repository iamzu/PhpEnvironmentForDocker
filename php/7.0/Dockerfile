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
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
    mv /home/resources/sources.list /etc/apt/sources.list


RUN pecl install /home/resources/redis-5.3.7.tgz \
	&& docker-php-ext-enable redis