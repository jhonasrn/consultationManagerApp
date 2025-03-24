# Use official PHP 8.2 FPM image as base
# Usa a imagem oficial do PHP 8.2 FPM como base
FROM php:8.2-fpm

# Install system dependencies
# Instala dependências do sistema
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    postgresql-client \
    libpq-dev

# Install PHP extensions
# Instala extensões do PHP
RUN docker-php-ext-install pdo pdo_pgsql mbstring exif pcntl bcmath gd

# Copy Composer from official image
# Copia o Composer da imagem oficial
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
# Define o diretório de trabalho
WORKDIR /var/www

# Copy application files
# Copia os arquivos da aplicação
COPY . .

# Install Composer dependencies (without dev dependencies)
# Instala dependências do Composer (sem dependências de desenvolvimento)
RUN composer install --no-dev --no-scripts --no-interaction

# Fix storage permissions
# Ajusta permissões do diretório storage
RUN chown -R www-data:www-data /var/www/storage

# Default command to run PHP-FPM
# Comando padrão para executar o PHP-FPM
CMD ["php-fpm"]