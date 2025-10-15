# -----------------------------
# Stage 1: Base image
# -----------------------------
FROM node:20-alpine AS base

WORKDIR /app
ENV NODE_ENV=production

# -----------------------------
# Stage 2: Install dependencies
# -----------------------------
FROM base AS deps

# Copy only package files first
COPY package.json package-lock.json ./

# Install all dependencies including dev (needed for TS build)
RUN npm ci

# -----------------------------
# Stage 3: Build
# -----------------------------
FROM deps AS build

# Copy all source files
COPY . .

# Install Nest CLI globally (if needed)
RUN npm install -g @nestjs/cli

# Build the app
RUN npm run build

# -----------------------------
# Stage 4: Final image
# -----------------------------
FROM node:20-alpine AS final

WORKDIR /app
ENV NODE_ENV=production

# Use non-root user for safety

# Copy only production dependencies
COPY --from=deps /app/node_modules ./node_modules

# Copy built files
COPY --from=build /app/dist ./dist

# Copy package.json (optional, sometimes needed for npm scripts)
COPY --from=build /app/package.json ./
RUN mkdir  /app/uploads 
RUN chmod a+x /app/
  
# Expose app port
EXPOSE 3000
USER node

# Run the app
CMD ["node", "dist/main"]

