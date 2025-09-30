# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

# Copia package files
COPY package*.json ./

# Installa tutte le dipendenze (serve anche devDependencies per build)
RUN npm ci --legacy-peer-deps

# Copia codice sorgente
COPY . .

# Build dell'applicazione React
RUN npm run build

# Stage 2: Serve con nginx
FROM nginx:alpine

# Copia build files
COPY --from=builder /app/build /usr/share/nginx/html

# Copia configurazione nginx personalizzata
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Esponi porta 80
EXPOSE 80

# Nginx parte automaticamente
CMD ["nginx", "-g", "daemon off;"]