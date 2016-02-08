FROM alpine

RUN apk add --no-cache php-cli php-mysqli php-ctype php-xml php-gd php-zlib php-openssl php-curl php-opcache php-json curl

RUN curl --location https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz | tar xzf - \
 && mv phpMyAdmin* /www \
 && rm -rf /www/js/jquery/src/ /www/examples /www/po/

COPY config.inc.php /www/
COPY run.sh /run.sh
RUN chmod u+rwx /run.sh

RUN sed -i \
    -e "s/^upload_max_filesize\s*=\s*2M/upload_max_filesize = 64M/" \
    -e "s/^post_max_size\s*=\s*8M/post_max_size = 64M/" \
    -e "s/^;\s*max_input_vars\s*=\s*1000/max_input_vars = 2000/" \
    /etc/php/php.ini

EXPOSE 80

ENTRYPOINT [ "/run.sh" ]
