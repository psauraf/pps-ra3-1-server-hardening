# RA3 – Server Hardening y Seguridad Web

Este repositorio contiene el desarrollo completo de la **RA3 – Server Hardening**, correspondiente al módulo **Puesta en Producción Segura**.

El objetivo de esta RA es aplicar distintas técnicas de **endurecimiento (hardening)** y **protección de servidores web**, utilizando contenedores Docker para aislar y validar cada práctica de forma independiente.

---

## 🧱 Estructura del repositorio

Cada práctica se ha desarrollado en un **contenedor Docker independiente**, con su propia configuración, validaciones y documentación.

- **PR1 – Apache Server Hardening (SSL, HSTS, CSP)**
- **PR2 – Protección del servidor Apache con ModSecurity (WAF)**
- **PR3 – Instalación de reglas OWASP Core Rule Set**
- **PR4 – Mitigación de ataques DoS/DDoS**
- **PR5 – Nginx Hardening (EXTRA)**
- **PR6 – Certificados digitales (Apache + SSL)**
- **PR7 – Apache Hardening Best Practices**

Cada carpeta incluye:
- `Dockerfile`
- Archivos de configuración
- Evidencias (capturas)
- `README.md` específico con explicación y validaciones

---

## 📁 Árbol del proyecto

```text

pps-ra3-1-server-hardening/
├── README.md
│
├── pr1/                                # PR1 – Apache Server Hardening (SSL, HSTS, CSP)
│   ├── conf/
│   ├── img/
│   │   ├── autoindex-disabled.png
│   │   ├── docker-running.png
│   │   ├── error-page-no-version.png
│   │   └── headers-https.png
│   ├── www/
│   ├── Dockerfile
│   └── README.md
│
├── pr2/                                # PR2 – ModSecurity (regla SQLi)
│   ├── conf/
│   ├── img/
│   │   ├── curl-http-200.png
│   │   ├── curl-sqli-403.png
│   │   └── docker-ps-pr2.png
│   ├── www/
│   ├── Dockerfile
│   └── README.md
│
├── pr3/                                # PR3 – OWASP Core Rule Set
│   ├── conf/
│   ├── img/
│   │   ├── apache-modules-security2.png
│   │   ├── curl-200-pr3.png
│   │   ├── docker-ps-pr3.png
│   │   └── dpkg-modsecurity-crs.png
│   ├── www/
│   ├── Dockerfile
│   └── README.md
│
├── pr4/                                # PR4 – Mitigación de ataques DoS/DDoS
│   ├── conf/
│   ├── img/
│   │   ├── evasive-module.png
│   │   ├── flood-sim.png
│   │   └── operative-service.png
│   ├── www/
│   ├── Dockerfile
│   └── README.md
│
├── pr5/                                # PR5 – Nginx Hardening (extra)
│   ├── conf/
│   ├── img/
│   │   ├── curl-http-200.png
│   │   ├── docker-ps-pr5.png
│   │   ├── method-not-allowed.png
│   │   ├── nginx-conf.png
│   │   ├── rate-limit-503.png
│   │   └── security-headers-nginx.png
│   ├── www/
│   ├── Dockerfile
│   └── README.md
│
├── pr6/                                # PR6 – Certificados digitales (Apache + SSL)
│   ├── conf/
│   ├── img/
│   │   ├── cert-details.png
│   │   ├── https-ok.png
│   │   ├── https-warning.png
│   │   └── redirect-http-https.png
│   ├── www/
│   ├── Dockerfile
│   └── README.md
│
└── pr7/                                # PR7 – Apache Hardening Best Practices
    ├── conf/
    ├── img/
    │   ├── autoindex-disabled.png
    │   ├── headers.png
    │   ├── no-index.png
    │   ├── put-blocked.png
    │   └── trace-blocked.png
    ├── www/
    ├── Dockerfile
    └── README.md

```

---

## 🐳 Tecnologías utilizadas
- Docker
- Apache HTTP Server
- Nginx
- OpenSSL
- ModSecurity
- OWASP Core Rule Set

---

## ℹ️ Notas
- Cada práctica puede ejecutarse de forma independiente.
- Los certificados utilizados son autofirmados, con fines educativos.
- Las validaciones se han realizado mediante curl, navegador web y logs del servidor.