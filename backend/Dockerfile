# Usar una imagen de Ubuntu como base
FROM ubuntu:20.04

# Actualizar el sistema e instalar dependencias necesarias
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    libzip-dev \
    && apt-get clean

# Instalar PHP y las extensiones necesarias
RUN apt-get update && apt-get install -y \
    php8.2-cli \
    php8.2-fpm \
    php8.2-mbstring \
    php8.2-xml \
    php8.2-zip \
    php8.2-mysql

# Descargar e instalar Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Verificar que Composer esté instalado correctamente
RUN composer --version

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar el proyecto al contenedor
COPY . /app

# Instalar las dependencias de Composer, Node y ejecutar las migraciones
RUN composer install \
    && npm install \
    && npm run build \
    && php artisan migrate --force \
    && php artisan optimize \
    && chmod -R 777 storage bootstrap/cache \
    && php artisan storage:link

# Exponer el puerto 8080
EXPOSE 8080

# Ejecutar el servidor de Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]
