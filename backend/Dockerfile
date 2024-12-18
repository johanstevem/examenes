# Usar la imagen base de PHP
FROM php:8.2-cli

# Instalar dependencias del sistema y Composer
RUN apt-get update && apt-get install -y \
    unzip \
    git \
    curl \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    libzip-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql gd zip \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar el proyecto al contenedor
COPY . /app

# Instalar las dependencias de Composer y Node.js
RUN composer install \
    && npm install \
    && npm run build \
    && php artisan migrate --force \
    && php artisan optimize \
    && chmod -R 777 storage bootstrap/cache \
    && php artisan storage:link

# Exponer el puerto
EXPOSE 8080

# Comando para ejecutar la aplicación
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]

