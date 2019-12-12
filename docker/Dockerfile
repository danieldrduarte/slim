FROM php:7.3-apache
RUN apt-get update && apt-get install -y \
	apt-transport-https \
	libpq-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
    libmcrypt-dev \
    git \
    zip \
    && docker-php-ext-install pdo pdo_pgsql pgsql calendar \
	&& docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN usermod -u 1000 www-data

RUN a2enmod headers rewrite
COPY apache_default /etc/apache2/sites-enabled/000-default.conf
WORKDIR /var/www