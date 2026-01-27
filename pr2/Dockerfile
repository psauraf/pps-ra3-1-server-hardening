FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    apache2 \
    libapache2-mod-security2 \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Activar ModSecurity
RUN a2enmod security2

# Configurar ModSecurity en modo bloqueo
RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf && \
    sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf

# AÑADIR REGLA PERSONALIZADA DIRECTAMENTE (una sola vez)
RUN cat >> /etc/modsecurity/modsecurity.conf << 'EOF'
SecRule ARGS "@rx (?i)(select|union|or|and|--)" "id:999999,phase:2,deny,status:403,msg:'SQLi detectado'"
EOF

# Web mínima
COPY www/ /var/www/html/

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
