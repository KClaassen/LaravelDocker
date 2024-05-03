# Use the official PHP 8.0 Alpine image as base
FROM php:8.0-alpine

# Set working directory
WORKDIR /var/www/html

# Install system dependencies
RUN apk --no-cache add \
    bash \
    git \
    openssh \
    openssl \
    libzip-dev \
    oniguruma-dev \
    php8 \
    php8-common \
    php8-fpm \
    php8-json \
    php8-dom \
    php8-pdo \
    php8-pdo_mysql \
    php8-tokenizer \
    php8-xml \
    php8-mbstring \
    php8-openssl \
    php8-fileinfo \
    php8-pecl-redis \
    php8-phar \
    php8-zip \
    php8-simplexml \
    php8-xmlwriter \
    php8-gd \
    php8-curl \
    php8-session \
    && docker-php-ext-install pdo_mysql zip mbstring

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set up non-root user
RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel
USER laravel

# Copy existing application directory contents
COPY --chown=laravel:laravel . .

# Install application dependencies
RUN composer install --no-interaction --no-plugins --no-scripts

# Generate Laravel application key
RUN php artisan key:generate

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
