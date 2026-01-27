FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    apache2 openssl ca-certificates curl \
    && rm -rf /var/lib/apt/lists/*

RUN a2enmod ssl headers && \
    a2dismod -f autoindex && \
    a2ensite default-ssl

RUN mkdir -p /etc/apache2/ssl && \
    openssl req -x509 -nodes -days 3650 -newkey rsa:2048 \
      -keyout /etc/apache2/ssl/apache.key \
      -out /etc/apache2/ssl/apache.crt \
      -subj "/C=ES/ST=Valencia/L=Valencia/O=PPS/OU=RA3.1/CN=localhost"

COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY conf/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
COPY conf/z-security-hardening.conf /etc/apache2/conf-available/z-security-hardening.conf

RUN a2enconf z-security-hardening

COPY www/ /var/www/html/

EXPOSE 80 443

CMD ["apachectl", "-D", "FOREGROUND"]
