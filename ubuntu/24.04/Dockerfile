FROM ubuntu:24.04
LABEL maintainer="Sarfaraz Ali Khan (mrkhan1417@gmail.com)"

ENV DEBIAN_FRONTEND=noninteractive

#Install Apache2 And PHP
RUN apt update && \
    apt install -y --no-install-recommends \
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
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Install Composer (with proper verification)
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Change Apache web directory to /www and enable mod_rewrite
RUN mkdir -p /www && \
    sed -i "s|/var/www|/www|g" /etc/apache2/apache2.conf && \
    sed -i "s|/var/www/html|/www|g" /etc/apache2/sites-available/000-default.conf && \
    a2enmod rewrite && \
    sed -i '/<Directory \/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

EXPOSE 80
WORKDIR /www

# Add a healthcheck to monitor Apache
HEALTHCHECK --interval=30s --timeout=10s --start-period=10s --retries=3 \
    CMD curl -f http://localhost || exit 1

# Start Apache in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
