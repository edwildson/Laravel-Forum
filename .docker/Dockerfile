FROM php:8.1.3-fpm

LABEL author="Edwildson C. Rodrigues <edwildson.coelho@sysvale.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ADD default.conf /tmp/default

RUN apt-get update \
    && apt-get install -y \
    && apt-get install -y --no-install-recommends\
      build-essential \
      nginx\
      git\
      libpng-dev \
      zip \
      unzip

# Install extensions
RUN docker-php-ext-install pdo_mysql exif pcntl
RUN docker-php-ext-configure gd 
RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    &&  usermod --non-unique --uid 1000 www-data \
    &&  groupmod --non-unique --gid 1000 www-data \
    &&  chown -R www-data:www-data /var/www \
    &&  mv /tmp/default /etc/nginx/sites-available/ \
    &&  ln -sf /etc/nginx/sites-available/default /etc/nginx/sites-enabled/

