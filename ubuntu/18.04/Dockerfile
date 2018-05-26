FROM ubuntu:18.04
LABEL maintainer="Sarfaraz Ali Khan (mrkhan1417@gmail.com)"

RUN apt update && apt install -y \
    apache2 \
    php \
    libapache2-mod-php \
    php-mysql \
    php-gd \
    php-curl \
    && rm -rf /var/lib/apt/lists/*

RUN sed -i "s|/var/www|/www|g" /etc/apache2/apache2.conf
RUN sed -i "s|/var/www/html|/www|g" /etc/apache2/sites-available/000-default.conf

EXPOSE 80
WORKDIR /www

COPY start.sh /opt/
RUN chmod +x /opt/start.sh
CMD apachectl -D FOREGROUND