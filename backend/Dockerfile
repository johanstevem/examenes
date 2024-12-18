FROM php:8.1-cli

# Establecemos el directorio de trabajo
WORKDIR /app/

# Copiamos los archivos del proyecto
COPY . /app/.

# Instalamos dependencias necesarias
RUN apt-get update && apt-get install -y \
    curl \
    php-mbstring \
    unzip \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Instalamos las dependencias de Composer
RUN composer install && npm i && npm run build && php artisan migrate --force && php artisan optimize && chmod 777 -R storage/ && chmod 777 -R bootstrap/cache && php artisan storage:link

# Expone el puerto (si es necesario)
EXPOSE 8000

# Inicia el servidor de Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]


# Ejecutar el servidor de Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]

