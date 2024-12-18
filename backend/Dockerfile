# Usar la imagen base de Nixpacks
FROM ghcr.io/railwayapp/nixpacks:ubuntu-1731369831

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar los archivos del proyecto al contenedor
COPY . /app/

# Instalar dependencias de Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Verificar que Composer esté instalado correctamente
RUN composer --version

# Instalar dependencias de PHP y Node
RUN composer install && npm install && npm run build

# Ejecutar migraciones, optimizar el proyecto y darle permisos a las carpetas necesarias
RUN php artisan migrate --force && php artisan optimize && chmod 777 -R storage/ && chmod 777 -R bootstrap/cache && php artisan storage:link

# Exponer el puerto 8080
EXPOSE 8080

# Ejecutar el servidor de Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]

