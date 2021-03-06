# MySQL 5.6 on Ubuntu

# Build and create a container:
# docker build --no-cache --tag vettadock/mysql-old:5.6 .
# docker rm -f mysql56
# docker run --detach --name mysql56 vettadock/mysql-old:5.6
# docker start mysql56
#
# Connect to MySQL:
# docker exec -ti mysql56 mysql

ARG ubuntu_version=20.04
FROM ubuntu:$ubuntu_version

ARG mysql_tarball=https://vettabase.com/old-sw/mysql/5.6/mysql-5.6.51-linux-glibc2.12-x86_64.tar.gz

RUN  \
    groupadd mysql \
    && useradd -r -g mysql -s /bin/false mysql

ADD $mysql_tarball /usr/local/mysql.tar.gz
WORKDIR /usr/local

RUN \
    apt-get update \
    && apt-get install -y \
        libncursesw5 \
        libaio1 \
        libncurses5 \
        numactl \
        libfile-copy-recursive-perl \
    && tar zxvf /usr/local/mysql.tar.gz \
    && rm /usr/local/mysql.tar.gz \
    && mv mysql-5.6.51-linux-glibc2.12-x86_64 mysql
RUN cd /usr/local/mysql \
    && /usr/local/mysql/scripts/mysql_install_db --user=mysql

EXPOSE 3306
ENV PATH="/usr/local/mysql/bin:${PATH}"
ENTRYPOINT ["mysqld_safe"]
USER root:root

# metadata
LABEL \
    com.vettabase.vendor="Vettabase" \
    maintainer="federico.razzoli@vettabase.com" \
    com.vettabase.license="GNU GPL 2.0" \
    description="MySQL 5.6 on recent Ubuntu" \
    com.vettabase.maturity="alpha" \
    version="1.1"


