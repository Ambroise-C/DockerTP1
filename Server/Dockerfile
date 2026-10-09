# --- Étape 1 : Build du Front (Vue.js) ---
FROM node:18-alpine AS frontend-builder
WORKDIR /app
# On copie les fichiers de configuration du front depuis la racine du projet
COPY ../front/package.json ../front/yarn.lock ./
RUN yarn config set strict-ssl false && yarn install
COPY ../front/ ./
RUN NODE_OPTIONS=--openssl-legacy-provider yarn build

# --- Étape 2 : Image finale Apache (httpd) ---
FROM httpd:2.4

# On copie directement le dossier dist généré par l'étape précédente vers le dossier d'Apache
COPY --from=frontend-builder /app/dist /usr/local/apache2/htdocs/

# On copie votre configuration Apache personnalisée
COPY ./conf/httpd.conf /usr/local/apache2/conf/httpd.conf

# Installation de curl pour le healthcheck (tel que vous l'aviez fait)
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*