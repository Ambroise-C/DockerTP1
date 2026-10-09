FROM httpd:2.4

# Copier la configuration Apache personnalisée
COPY ./conf/httpd.conf /usr/local/apache2/conf/httpd.conf

# Installer curl pour le healthcheck si nécessaire
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*