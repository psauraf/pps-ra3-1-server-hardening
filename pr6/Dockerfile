FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

# Instalación de Apache y OpenSSL
RUN apt-get update && apt-get install -y --no-install-recommends \
    apache2 \
    openssl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Evitar warning de ServerName
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Habilitar módulo SSL
RUN a2enmod ssl

# Crear directorio para certificados
RUN mkdir -p /etc/apache2/ssl

# Generar certificado autofirmado
RUN openssl req -x509 -nodes -days 365 \
    -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/server.key \
    -out /etc/apache2/ssl/server.crt \
    -subj "/C=ES/ST=Valencia/L=Valencia/O=PPS/OU=PR6/CN=localhost"

# VirtualHost HTTPS
RUN printf "<IfModule mod_ssl.c>\n\
<VirtualHost *:443>\n\
    ServerName localhost\n\
    DocumentRoot /var/www/html\n\
\n\
    SSLEngine on\n\
    SSLCertificateFile /etc/apache2/ssl/server.crt\n\
    SSLCertificateKeyFile /etc/apache2/ssl/server.key\n\
\n\
    <Directory /var/www/html>\n\
        AllowOverride None\n\
        Require all granted\n\
    </Directory>\n\
\n\
    ErrorLog \${APACHE_LOG_DIR}/error.log\n\
    CustomLog \${APACHE_LOG_DIR}/access.log combined\n\
</VirtualHost>\n\
</IfModule>\n" > /etc/apache2/sites-available/default-ssl.conf

# Redirección HTTP -> HTTPS
RUN printf "<VirtualHost *:80>\n\
    ServerName localhost\n\
    Redirect permanent / https://localhost/\n\
</VirtualHost>\n" > /etc/apache2/sites-available/000-default.conf

# Activar sitios
RUN a2ensite default-ssl && a2ensite 000-default

# Web de prueba
COPY www/ /var/www/html/

EXPOSE 80 443

CMD ["apachectl", "-D", "FOREGROUND"]
