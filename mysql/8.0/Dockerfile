FROM mysql:8.0

# 修改时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}


COPY config/my.cnf/mysql.cnf /etc/mysql/conf.d/mysql.cnf

