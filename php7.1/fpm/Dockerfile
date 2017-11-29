FROM php:7.1-fpm
MAINTAINER Kane Valentine <kane@cute.im>

RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y --no-install-suggests --no-install-recommends \
		libjpeg-dev \
		libpng-dev \
		libpq-dev \
	; \
        apt-get clean; \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd pgsql mysqli opcache

RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

VOLUME /var/www/html

ENV MYBB_VERSION 1814
ENV MYBB_SHA1 d3cd88bfbdbeb8ac44bba44020a3d84efd6a3163

RUN set -ex; \
	curl -o mybb.tar.gz -fSL "https://github.com/mybb/mybb/archive/mybb_${MYBB_VERSION}.tar.gz"; \
	echo "$MYBB_SHA1 *mybb.tar.gz" | sha1sum -c -; \
	tar -xzf mybb.tar.gz -C /usr/src/; \
	rm mybb.tar.gz; \
	chown -R www-data:www-data /usr/src/mybb-mybb_${MYBB_VERSION}

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["php-fpm"]
