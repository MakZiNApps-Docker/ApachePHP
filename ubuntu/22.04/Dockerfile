FROM ubuntu:22.04
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
    php-xml \
    php-bcmath \
    php-intl \
    php-soap \
    php-zip \
    unzip \
    && rm -rf /var/lib/apt/lists/*

#Install PHP Composer
RUN cd /tmp && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === file_get_contents('https://composer.github.io/installer.sig')) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

#Change apache web directory to /www and enable mod_rewrite
RUN mkdir /www && \
    sed -i "s|/var/www|/www|g" /etc/apache2/apache2.conf && \
    sed -i "s|/var/www/html|/www|g" /etc/apache2/sites-available/000-default.conf && \
    a2enmod rewrite && \
    sed -i '/<Directory \/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

EXPOSE 80
WORKDIR /www

CMD apachectl -D FOREGROUND
