FROM redis

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}

RUN mkdir /usr/local/etc/redis
RUN mkdir /usr/local/etc/redis/data

COPY config/redis.conf /usr/local/etc/redis/redis.conf
CMD [ "redis-server","/usr/local/etc/redis/redis.conf" ]
