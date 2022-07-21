FROM php:5.4-fpm

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY resources /home/resources
# 替换源
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's|security.debian.org/debian-security|mirrors.ustc.edu.cn/debian-security|g' /etc/apt/sources.list


# RUN apt-get update && apt-get install -y \
# 	libfreetype6-dev \
# 	libjpeg62-turbo-dev \
# 	libpng-dev \
# 	git \
# 	&& docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql bcmath

#	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
#	&& docker-php-ext-install -j$(nproc) gd pdo pdo_mysql bcmath

RUN docker-php-ext-install mysqli mysql mbstring


# composer
# RUN php /home/resources/installer.php
# RUN php -r "unlink('/home/resources/installer.php');"


# RUN mv composer.phar /usr/local/bin/composer
# #全局切换阿里源
# RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# RUN composer config -g github-oauth.github.com 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s