FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

COPY .env.production ./.env.production

RUN npm run build


