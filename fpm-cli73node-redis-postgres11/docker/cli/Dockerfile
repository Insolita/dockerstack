FROM php:7.3-cli
# Prepare Debian environment
ENV DEBIAN_FRONTEND noninteractive

# Performance optimization - see https://gist.github.com/jpetazzo/6127116
# this forces dpkg not to call sync() after package extraction and speeds up install
RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup
# we don't need and apt cache in a container
RUN echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache

RUN  apt-get update && \
     apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libicu-dev \
        libzip-dev \
        libpq-dev \
        && pecl install xdebug-2.7.0beta1 \
        && pecl install redis \
            && docker-php-ext-enable xdebug \
            && docker-php-ext-enable redis \
            && docker-php-ext-install -j$(nproc) gd \
            && docker-php-ext-install -j$(nproc) pcntl \
            && docker-php-ext-install -j$(nproc) bcmath \
            && docker-php-ext-install -j$(nproc) intl \
            && docker-php-ext-install -j$(nproc) zip \
            && docker-php-ext-install -j$(nproc) pgsql \
            && docker-php-ext-install -j$(nproc) pdo_pgsql \
            && docker-php-ext-install -j$(nproc) exif \
            && docker-php-ext-configure gd \
                --with-freetype-dir=/usr/include/ \
                --with-jpeg-dir=/usr/include/ \
            && apt-get clean \
            &&  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Initialize application
WORKDIR /app
ENV COMPOSER_HOME /root/.composer
ENV PATH /root/.composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
&& curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
# Make sure we're installing what we think we're installing!
&& php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
&& php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot \
&& rm -f /tmp/composer-setup.*

ENV XDEBUGINI_PATH=/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# Enable Remote xdebug
RUN echo "xdebug.idekey = PHPSTORM" >> $XDEBUGINI_PATH && \
    echo "xdebug.default_enable = 1" >> $XDEBUGINI_PATH && \
    echo "xdebug.remote_enable = 1" >> $XDEBUGINI_PATH && \
    echo "xdebug.remote_autostart = 0" >> $XDEBUGINI_PATH && \
    echo "xdebug.remote_connect_back = 1" >> $XDEBUGINI_PATH && \
    echo "xdebug.profiler_enable = 0" >> $XDEBUGINI_PATH
