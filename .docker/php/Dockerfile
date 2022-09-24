FROM php:8.1-fpm-alpine3.16

RUN docker-php-ext-install pdo pdo_mysql sockets
RUN curl -sS https://getcomposer.org/installer​ | php -- \
     --install-dir=/usr/local/bin --filename=composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
WORKDIR /var/www/
ENV USER=docker
ENV UID=12345
ENV GID=23456
RUN addgroup -g ${GID} ${USER} && adduser \
    --disabled-password \
    --gecos "" \
    --home "$(pwd)" \
    --ingroup "$USER" \
    --no-create-home \
    --uid "$UID" \
    "$USER"
ADD . /var/www
RUN chown -R ${USER}:${USER} /var/www
USER ${USER}
COPY --chown=${USER}:${USER} . .
EXPOSE 9000
CMD ["php-fpm"]