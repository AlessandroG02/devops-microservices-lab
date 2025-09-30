# Stage 1: Build
FROM node:20-alpine AS builder

WORKDIR /app

# Copia package files
COPY package*.json ./

# Installa dipendenze
RUN npm ci --only=production

# Stage 2: Runtime
FROM node:20-alpine

WORKDIR /app

# Copia dipendenze dal builder
COPY --from=builder /app/node_modules ./node_modules

# Copia codice applicazione
COPY . .

# Crea directory per uploads
RUN mkdir -p uploads

# Esponi porta
EXPOSE 3000

# Utente non-root per sicurezza
USER node

# Comando di avvio
CMD ["node", "index.js"]