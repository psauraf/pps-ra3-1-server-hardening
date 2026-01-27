FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

# Apache + ModSecurity + OWASP CRS (paquete oficial Debian)
RUN apt-get update && apt-get install -y --no-install-recommends \
    apache2 \
    libapache2-mod-security2 \
    modsecurity-crs \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Activar ModSecurity
RUN a2enmod security2

# Activar ModSecurity en modo BLOQUEO (sin duplicar reglas)
RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf && \
    sed -i 's/^SecRuleEngine.*/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf

# Web mínima
COPY www/ /var/www/html/

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
