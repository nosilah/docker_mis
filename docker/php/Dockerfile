FROM php:7.2-fpm

# Copy composer.lock and composer.json
COPY composer.lock composer.json /var/www/

# Set working directory
WORKDIR /var/www

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    zlib1g-dev \
    exiftool \
    libmcrypt-dev \
    libicu-dev \
    libxpm-dev \
    libvpx-dev \
    libxml2-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo_mysql mysqli mbstring zip exif pcntl iconv pdo soap intl bcmath opcache
RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-install gd

#my settiing "install imagick"
# RUN apt-get update && apt-get install -y \
#     libmagickwand-dev --no-install-recommends \
#     && pecl install imagick \
#     && docker-php-ext-enable imagick

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer



# Copy existing application directory contents
COPY --chown=www-data:www-data . /var/www

RUN chmod -R 755 /var/www
# Copy existing application directory permissions
# RUN chmod -R 775 /var/www/storage /var/www/bootstrap/cache \
#     chmod 777 -R /var/www/storage /var/www/bootstrap/cache
# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]