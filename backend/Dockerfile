FROM php:8.2-fpm

# Instalar extensiones necesarias para PostgreSQL y otros paquetes necesarios
RUN apt-get update && apt-get install -y \
    libpq-dev \
    unzip \
    git \
    zip \
    curl \
    nodejs \
    npm \
    && docker-php-ext-install pdo_pgsql

# Instalar Composer desde la imagen oficial de Composer
COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

# Configuración del directorio de trabajo
WORKDIR /var/www

# Copiar todos los archivos del proyecto
COPY . .

# Instalar dependencias de PHP
RUN composer install --no-dev --optimize-autoloader

# Instalar dependencias de Node.js y compilar assets
RUN npm install
RUN npm run build

# Ajustar permisos
RUN chmod -R 775 storage bootstrap/cache
RUN chown -R www-data:www-data /var/www

# Exponer el puerto de PHP-FPM
EXPOSE 8000

# Iniciar PHP-FPM
CMD ["php-fpm"]

# Iniciar PHP-FPM
CMD ["php-fpm"]
