# Usar una imagen base de PHP
FROM php:8.0-cli

# Usar una imagen base de PHP
FROM php:8.0-cli

# Instalar dependencias necesarias
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    curl \
    libzip-dev

# Instalar Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Verificar la instalación de Composer (opcional)
RUN composer --version

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar los archivos del proyecto al contenedor
COPY . .

# Instalar las dependencias de PHP y NPM
RUN composer install
RUN npm install
RUN npm run build

# Ejecutar migraciones y optimizaciones
RUN php artisan migrate --force
RUN php artisan optimize
RUN chmod 777 -R storage/
RUN chmod 777 -R bootstrap/cache
RUN php artisan storage:link

# Exponer el puerto si es necesario
EXPOSE 8080

# Iniciar el servidor Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]


