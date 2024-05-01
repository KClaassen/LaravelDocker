FROM php:8.0-fpm-alpine

# Install dependencies
RUN docker-php-ext-install pdo pdo_mysql

WORKDIR /var/www/html

# Copy application files
COPY . .

# Run migrations and seeds (optional)
# RUN php artisan migrate --seed

CMD ["php-fpm"]