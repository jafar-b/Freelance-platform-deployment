# Use a standard Node.js image
FROM node:20-alpine

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY package*.json ./

# Install ALL dependencies, including devDependencies
RUN npm install

# Copy the rest of your application source code
COPY . .

# Vite needs to bind to 0.0.0.0 to be accessible from outside the container
# The --host 0.0.0.0 flag is crucial for Docker
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]