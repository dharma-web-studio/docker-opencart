ARG PHP_VERSION=8.1
FROM php:${PHP_VERSION}-fpm-alpine

# Switch directory
WORKDIR /var/www/html

# Copy bin files
COPY ./bin/wait-for-it /usr/local/bin/wait-for-it
RUN chmod -R +x /usr/local/bin/wait-for-it

COPY ./bin/init /usr/local/bin/init
RUN chmod -R +x /usr/local/bin/init

# Install packages
RUN apk add --no-cache --virtual .build-deps \
	$PHPIZE_DEPS \
	bash \
	libpng \
	libzip-dev \
	zip \
	libpng-dev \
	jpeg-dev \
	freetype-dev \
	libjpeg-turbo \
	libwebp \
	mysql-client \
	php-mysqli \
	nano \
	zlib-dev \
	git \
	rsync

# Install PHP Extensions
RUN docker-php-ext-install gd \
	zip \
	mysqli

# Install xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN { \
        echo 'xdebug.mode=off'; \
        echo 'xdebug.start_with_request=trigger'; \
        echo 'xdebug.client_host=host.docker.internal'; \
        echo 'xdebug.idekey=PHPSTORM'; \
    } | tee -a "/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini"

# Configure and enable gd
RUN docker-php-ext-configure gd --with-freetype --with-jpeg && docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) gd

# Download and place mkcert
RUN curl -SL https://dl.filippo.io/mkcert/latest?for=linux/amd64 -o mkcert \
    && chmod +x ./mkcert \
    && mv ./mkcert /usr/local/bin/mkcert

# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Download the latest version of OpenCart
ARG OPENCART_VERSION

RUN git clone -b ${OPENCART_VERSION} --single-branch https://github.com/opencart/opencart.git  ./opencart
RUN mv /var/www/html/opencart/upload/* /var/www/html/ \
    && mv /var/www/html/opencart/upload/.htaccess.txt /var/www/html/.htaccess \
    && mv /var/www/html/config-dist.php /var/www/html/config.php \
    && mv /var/www/html/admin/config-dist.php /var/www/html/admin/config.php \
    && rm -rf /var/www/html/opencart

# Fix permissions
RUN chown -R www-data:www-data /var/www/html/

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD ["/usr/local/bin/wait-for-it db:3306 --timeout=60 -- /usr/local/bin/init"]
