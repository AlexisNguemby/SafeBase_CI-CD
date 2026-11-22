FROM node:22-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

# Génère le client Prisma dans le conteneur
RUN npx prisma generate

EXPOSE 3000

CMD ["npm", "run", "dev"]