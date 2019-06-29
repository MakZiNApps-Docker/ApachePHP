FROM ubuntu:18.04
LABEL maintainer="Sarfaraz Ali Khan (mrkhan1417@gmail.com)"

#Install Apache2 And PHP
RUN apt update && \
    DEBIAN_FRONTEND=noninteractive \
    apt install -y \
    apache2 \
    php \
    libapache2-mod-php \
    php-mysql \
    php-gd \
    php-curl \
    php-mbstring \
    && rm -rf /var/lib/apt/lists/*

#Change apache web directory to /www
RUN mkdir /www && \
    sed -i "s|/var/www|/www|g" /etc/apache2/apache2.conf && \
    sed -i "s|/var/www/html|/www|g" /etc/apache2/sites-available/000-default.conf

EXPOSE 80
WORKDIR /www

CMD apachectl -D FOREGROUND