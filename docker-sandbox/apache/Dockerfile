ARG APACHE_VERSION=""
FROM httpd:${APACHE_VERSION:+${APACHE_VERSION}-}alpine

RUN apk update; \
    apk upgrade;

COPY sandbox.apache.conf /usr/local/apache2/conf/sandbox.apache.conf
