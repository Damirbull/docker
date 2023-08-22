FROM php:php:7.4.29-fpm
RUN apt-get update && apt-get install -y zip
RUN docker-php-ext-install pdo mysqli pdo_mysql 
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Install required dependency
RUN apt-get update && apt-get install -y \
    zip \
    libxml2-dev \
    libzip-dev

# Configure and install gd extension
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd

# Install zip and zml
RUN docker-php-ext-install zip xml

# RUN apt-get update && apt-get install -y \
#     git \
#     curl \
#     zip \
#     vim \
#     unzip
RUN composer require nuovo/spreadsheet-reader
WORKDIR /var/www
RUN apt-get update && apt-get install -y git \
    && git clone https://github.com/nuovo/spreadsheet-reader.git /var/www/spreadsheet-reader \
    && rm -rf /var/www/spreadsheet-reader/.git \
    && chown -R www-data:www-data /var/www/spreadsheet-reader