FROM php:8.2-fpm-alpine

# Set working directory
WORKDIR /var/www/html

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set up non-root user
RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel
USER laravel

# Install Laravel framework
RUN composer require laravel/framework

# Copy existing application directory contents (if applicable)
COPY --chown=laravel:laravel . .

# Install application dependencies
RUN composer install --no-interaction --no-plugins --no-scripts

# Generate Laravel application key
RUN php artisan key:generate

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
