FROM nginx
COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/conf.d/default.conf /etc/nginx/conf.d/default.conf

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}
