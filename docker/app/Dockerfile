FROM php:8.1-fpm-alpine
WORKDIR /var/www/html

# Download the latest version of OpenCart


# Copy bin files
COPY ./bin/wait-for-it /usr/local/bin/wait-for-it
RUN chmod -R +x /usr/local/bin/wait-for-it

COPY ./bin/init /usr/local/bin/init
RUN chmod -R +x /usr/local/bin/init

# Install packages
#RUN apk add --no-cache --virtual .build-deps \
#	$PHPIZE_DEPS \
#	bash \
#	libxml2-dev \
#	libpng \
#	libpng-dev \
#	libmcrypt-dev \
#	jpeg-dev \
#	libjpeg-turbo-dev \
#	freetype-dev \
#	mysql-client \
#	ncurses \
#	nano \
#	imagemagick-dev \
#	rsync

# Install GD
# RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Install PHP Ext
RUN docker-php-ext-install soap \
	pdo_mysql \
	mbstring \
	gd \
	iconv \
	pcntl \
	posix \
	bcmath \
	zip \
	sockets

# Install imagick
RUN pecl install imagick && docker-php-ext-enable imagick

# Install xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN { \
        echo 'xdebug.mode=off'; \
        echo 'xdebug.start_with_request=trigger'; \
        echo 'xdebug.client_host=host.docker.internal'; \
        echo 'xdebug.idekey=PHPSTORM'; \
	} | tee -a "/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini"

# Download the latest version of modman
RUN curl -SL https://raw.githubusercontent.com/colinmollenhour/modman/master/modman -o modman \
    && chmod +x ./modman \
    && mv ./modman /usr/local/bin/

# Download and place magerun

# Download and place mkcert
RUN curl -SL https://dl.filippo.io/mkcert/latest?for=linux/amd64 -o mkcert \
    && chmod +x ./mkcert \
    && mv ./mkcert /usr/local/bin/mkcert

#Expose port ¿xdebug? Is this need it ? Better in docker-compose-yml?
EXPOSE 9003

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD ["/usr/local/bin/wait-for-it db:3306 --timeout=15 -- /usr/local/bin/init"]
