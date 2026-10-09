# --- Étape 1 : Build du Front (Vue.js) ---
FROM node:18-alpine AS frontend-builder
WORKDIR /app

# On copie les fichiers de configuration depuis le dossier front/ (situé un niveau au-dessus du contexte Server)
COPY ../front/package.json ../front/yarn.lock ./
RUN yarn config set strict-ssl false && yarn install

# On copie tout le code du front
COPY ../front/ ./
RUN NODE_OPTIONS=--openssl-legacy-pattern yarn build 
# (ou --openssl-legacy-provider selon ce qui fonctionnait pour vous)

# --- Étape 2 : Image finale Apache (httpd) ---
FROM httpd:2.4

# On récupère le dossier dist généré à l'étape précédente et on le place dans le dossier web d'Apache
COPY --from=frontend-builder /app/dist /usr/local/apache2/htdocs/

# On copie votre configuration Apache personnalisée depuis le dossier Server/conf/
COPY ./conf/httpd.conf /usr/local/apache2/conf/httpd.conf

# Installation de curl pour les healthchecks
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*