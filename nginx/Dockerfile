FROM nginx:alpine

COPY nginx.conf /etc/nginx/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories 

RUN apk update \
    && apk upgrade \
    && apk --update add logrotate \
    && apk add --no-cache openssl \
    && apk add --no-cache bash

RUN apk add --no-cache curl

ARG RUN_USER_UID=83
ARG RUN_USER_GID=83

RUN set -x ; \
    delgroup www-data ; \
    addgroup -g ${RUN_USER_GID} -S www-data ; \
    adduser -u ${RUN_USER_UID} -D -S -G www-data www-data && exit 0 ; exit 1


ARG PHP_UPSTREAM_CONTAINER=phpfpm
ARG PHP_UPSTREAM_PORT=9000

ARG PHP70_UPSTREAM_CONTAINER=php70fpm

# Create 'messages' file used from 'logrotate'
RUN touch /var/log/messages

# Copy 'logrotate' config file
COPY logrotate/nginx /etc/logrotate.d/

# Set upstream conf and remove the default conf
RUN echo "upstream php-upstream { server ${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; } upstream php70-upstream { server ${PHP70_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; }" > /etc/nginx/conf.d/upstream.conf \
    && rm /etc/nginx/conf.d/default.conf

ADD ./startup.sh /opt/startup.sh
RUN sed -i 's/\r//g' /opt/startup.sh
CMD ["/bin/bash", "/opt/startup.sh"]

EXPOSE 80 81 443
