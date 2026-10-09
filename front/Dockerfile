# --- Build du Front ---
FROM node:18-alpine AS build
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn config set strict-ssl false && yarn install
COPY . .
RUN NODE_OPTIONS=--openssl-legacy-provider yarn build

# --- Serveur Nginx pour le Front ---
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80