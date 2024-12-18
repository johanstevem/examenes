# Usar una imagen base de PHP
FROM php:8.0-cli

# Instalar dependencias necesarias
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    curl \
    libzip-dev

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar los archivos del proyecto al contenedor
COPY . .

# Instalar las dependencias de PHP (Composer) y NPM
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer install
RUN npm install

# Exponer el puerto si es necesario
EXPOSE 8080

# Comando para ejecutar el servidor
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]

CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]



