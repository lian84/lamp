FROM php:8.0-apache

RUN apt-get update && \
    apt-get install -y default-mysql-server unzip && \
    docker-php-ext-install mysqli pdo pdo_mysql && \
    a2enmod rewrite && \
    rm -rf /var/lib/apt/lists/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel
RUN composer create-project --prefer-dist laravel/laravel /var/www/html/laravel

COPY ./.config/my.cnf /etc/mysql/my.cnf
COPY ./.config/config.inc.php /var/www/html/phpmyadmin/phpMyAdmin-5.1.1-all-languages/config.inc.php
COPY ./.config/grant-privileges.sql /grant-privileges.sql
COPY ./.config/000-default.conf /etc/apache2/sites-available/000-default.conf

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

