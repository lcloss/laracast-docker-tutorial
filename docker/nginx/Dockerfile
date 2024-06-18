FROM nginx:stable-alpine

ENV NGINXUSER=www-data
ENV NGINXGROUP=www-data

RUN mkdir -p /var/www/public_html/public

ADD ./default.conf /etc/nginx/conf.d/default.conf

RUN sed -i "s/user www-data/user ${NGINXUSER}/g" /etc/nginx/conf.d/default.conf

# RUN adduser -g ${NGINXGROUP} -s /bin/sh -D ${NGINXUSER}

