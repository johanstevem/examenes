# Usar una imagen base de PHP con Composer preinstalado
FROM composer:2.2 AS build

# Establecer el directorio de trabajo
WORKDIR /app/

# Copiar los archivos del proyecto
COPY . /app/

# Instalar las dependencias de Composer y NPM
RUN composer install
RUN npm install
RUN npm run build
RUN php artisan migrate --force
RUN php artisan optimize
RUN chmod 777 -R storage/ bootstrap/cache
RUN php artisan storage:link

# Exponer el puerto si es necesario
EXPOSE 8000

# Iniciar el servidor Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]


