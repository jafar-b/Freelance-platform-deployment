#STAGE 1: Creating and extracting the static images 
# Use a standard Node.js image
FROM node:20-alpine AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY package*.json ./

# Install ALL dependencies, including devDependencies
RUN npm install

# Copy the rest of your application source code
COPY . .

COPY .env.production ./.env.production


#CREATING THE BUILD FILES
RUN npm run build


