# Usar una imagen base de PHP oficial para Laravel
FROM php:8.1-cli

# Establecer el directorio de trabajo
WORKDIR /app/

# Copiar los archivos del proyecto
COPY . /app/

# Instalar las dependencias necesarias
RUN apt-get update && apt-get install -y \
    curl \
    php-mbstring \
    unzip \
    git \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Instalar las dependencias de Composer y NPM
RUN composer install \
    && npm install \
    && npm run build \
    && php artisan migrate --force \
    && php artisan optimize \
    && chmod 777 -R storage/ \
    && chmod 777 -R bootstrap/cache \
    && php artisan storage:link

# Exponer el puerto si es necesario
EXPOSE 8000

# Iniciar el servidor Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]


