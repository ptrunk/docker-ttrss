# Based on Alpine Linux
FROM alpine:3.7

LABEL description="Tiny Tiny RSS + httpd + mod_php" \
      maintainer="Paul Trunk <mail@p7k.org>"

# Install necessary packages
RUN apk add --no-cache \
    git \
    php7-apache2 \
    php7-curl \
    php7-dom \
    php7-fileinfo \
    php7-gd \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-mysqli \
    php7-mysqlnd \
    php7-pgsql \
    php7-pdo_mysql \
    php7-pdo_pgsql \
    php7-posix \
    php7-xml

# Fix Pid file error
RUN sed -i 's/\/run\/apache2\/httpd.pid/\/run\/httpd.pid/g' /etc/apache2/conf.d/mpm.conf

# Change DocumentRoot
RUN sed -i 's/\/var\/www\/localhost\/htdocs/\/var\/www\/html/g' /etc/apache2/httpd.conf

# Install ttrss
RUN git clone https://git.tt-rss.org/git/tt-rss.git /var/www/html
RUN chown -R apache:apache /var/www/html

# Clean up
RUN rm -rf /var/cache/*

EXPOSE 80

VOLUME ["/var/www/html"]

ENTRYPOINT ["httpd"]
CMD ["-D", "FOREGROUND", "-k", "start"]

