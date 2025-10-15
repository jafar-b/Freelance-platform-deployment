# Stage 1: Base image
FROM node:20-alpine AS base

WORKDIR /app
ENV NODE_ENV=production

# Stage 2: Installing dependencies
FROM base AS deps

COPY package.json package-lock.json ./

RUN npm ci

# Stage 3: Build
FROM deps AS build

COPY . .

RUN npm install -g @nestjs/cli

RUN npm run build

# Stage 4: Final image
FROM node:20-alpine AS final

WORKDIR /app
ENV NODE_ENV=production


COPY --from=deps /app/node_modules ./node_modules

COPY --from=build /app/dist ./dist

COPY --from=build /app/package.json ./
RUN mkdir  /app/uploads 
RUN chmod a+x /app/
  
EXPOSE 3000
USER node

CMD ["node", "dist/main"]

