FROM alpine
LABEL maintainer="Sarfaraz Ali Khan (mrkhan1417@gmail.com)"

RUN apk --update --no-cache add apache2 php7-apache2 && \
    mkdir /www && \
    sed -i "s|/var/www/localhost/htdocs|/www|g" /etc/apache2/httpd.conf

EXPOSE 80
WORKDIR /www

CMD httpd -D FOREGROUND