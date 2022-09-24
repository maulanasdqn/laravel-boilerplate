FROM php:8.1-fpm
ENV USER=www
ENV GROUP=www
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd
RUN apt-get update && apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
WORKDIR /var/www/
RUN groupadd -g 1000 ${GROUP} && useradd -u 1000 -ms /bin/bash -g ${GROUP} ${USER}
RUN chown -R ${USER} /var/www
USER ${USER}
COPY --chown=${USER}:${GROUP} . .
EXPOSE 9000
CMD ["php-fpm"]