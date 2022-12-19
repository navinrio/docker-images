FROM alpine:3.17

RUN apk update && apk upgrade 
RUN apk add --no-cache nginx nginx-mod-http-headers-more nginx-mod-http-geoip nginx-mod-http-cache-purge bash -q \
  && apk add --no-cache php81 php81-fpm php81-opcache php81-pdo_mysql php81-pdo php81-gd php81-zlib php81-mysqli php81-curl php81-xml -q \
  && mkdir /var/run/php
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log
COPY server/etc/nginx /etc/nginx
COPY server/etc/php /etc/php81
COPY src /usr/share/nginx/html
EXPOSE 80
EXPOSE 443
CMD ["/bin/bash", "-c", "php-fpm81 && chmod 777 /var/run/php/php81-fpm.sock && chmod 755 /usr/share/nginx/html/* && nginx -g 'daemon off;'"]
