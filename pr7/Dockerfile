FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    apache2 ca-certificates curl \
    && rm -rf /var/lib/apt/lists/*

# Habilitar módulo headers (para cabeceras de seguridad)
RUN a2enmod headers

# Copiar web
COPY www/ /var/www/html/

# Copiar hardening y activarlo
COPY conf/hardening.conf /etc/apache2/conf-available/hardening.conf
RUN a2enconf hardening

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
