FROM busybox:latest as test
WORKDIR /app
RUN echo '<?php phpinfo(); ?>' > index.php

FROM alpine:3.17
RUN apk add --no-cache php81 php81-mysqlnd php81-gd php81-zip php81-xml php81-apache2 apache2 -q
COPY --from=test /app/index.php /var/www/localhost/htdocs
EXPOSE 80
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
