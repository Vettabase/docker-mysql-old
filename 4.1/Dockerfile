# MySQL 4.1 on Ubuntu

# Build and create a container:
# docker build --no-cache --tag vettadock/mysql-old:4.1 .
# docker rm -f mysql41
# docker run --detach --name mysql41 vettadock/mysql-old:4.1
# docker start mysql41
#
# Connect to MySQL:
# docker exec -ti mysql41 mysql

ARG ubuntu_version=20.04
FROM ubuntu:$ubuntu_version

ARG mysql_tarball=https://vettabase.com/old-sw/mysql/4.1/mysql-max-4.1.22-unknown-linux-gnu-x86_64-glibc23.tar.gz

RUN  \
    groupadd mysql \
    && useradd -r -g mysql -s /bin/false mysql

ADD $mysql_tarball /usr/local/mysql.tar.gz
WORKDIR /usr/local

RUN \
    apt-get update \
    && apt-get install -y \
        libncursesw5 \
        libncurses5 \
    && tar zxvf /usr/local/mysql.tar.gz \
    && rm -rf /usr/local/mysql.tar.gz \
    && mv mysql-max-4.1.22-unknown-linux-gnu-x86_64-glibc23 mysql \
    && cd /usr/local/mysql \
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
    description="MySQL 4.1 on recent Ubuntu" \
	com.vettabase.maturity="alpha" \
	version="1.1"


