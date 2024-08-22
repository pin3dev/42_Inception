FROM debian:bullseye
RUN apt update && apt upgrade -y && apt install -y \
php7.4-fpm \
php7.4-mysqli \
curl 
RUN mkdir -p /run/php && chown -R www-data:www-data /run/php
COPY conf/www.conf /etc/php/7.4/fpm/pool.d/.
COPY ./tools/wp-install.sh .
RUN chmod +x ./wp-install.sh
ENTRYPOINT ["sh", "./wp-install.sh"]