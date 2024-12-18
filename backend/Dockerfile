# Usamos una imagen base compatible con Ubuntu
FROM ghcr.io/railwayapp/nixpacks:ubuntu-1731369831

# Establecemos el directorio de trabajo
WORKDIR /app/

# Copiamos los archivos del proyecto
COPY . /app/.

# Instalamos Composer
RUN apt-get update && apt-get install -y \
    curl \
    php-cli \
    php-mbstring \
    unzip \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Ahora, instalamos las dependencias
RUN composer install && npm i && npm run build && php artisan migrate --force && php artisan optimize && chmod 777 -R storage/ && chmod 777 -R bootstrap/cache && php artisan storage:link

# Expone el puerto (si es necesario)
EXPOSE 8000

# Inicia el servidor de Laravel (puedes ajustarlo según lo que necesites)
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]

# Ejecutar el servidor de Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]

