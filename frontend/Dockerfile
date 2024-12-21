# Étape 1 : Construire l'application React avec Vite
FROM node:18-alpine AS build
WORKDIR /app

# Copier les fichiers package.json et package-lock.json pour installer les dépendances
COPY package*.json ./
RUN npm install

# Copier tout le contenu du projet dans le conteneur
COPY . .

# Construire l'application
RUN npm run build

# Debug : Vérifier que le dossier dist est créé
RUN ls /app/dist

# Étape 2 : Utiliser une image Nginx légère pour servir l'application
FROM nginx:1-alpine-slim
COPY --from=build /app/dist /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80


# Lancer Nginx
CMD ["nginx", "-g", "daemon off;"]
