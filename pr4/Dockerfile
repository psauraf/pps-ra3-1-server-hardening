FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    apache2 \
    libapache2-mod-evasive \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Activar módulos de protección
RUN a2enmod evasive reqtimeout

# Crear directorio de logs para mod_evasive
RUN mkdir -p /var/log/apache2/mod_evasive && \
    chown -R www-data:www-data /var/log/apache2/mod_evasive

# Copiar configuración
COPY conf/evasive.conf /etc/apache2/mods-available/evasive.conf

# Web
COPY www/ /var/www/html/

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
