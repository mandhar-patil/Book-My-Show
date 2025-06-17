FROM node:18-slim

WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install --legacy-peer-deps

# Copy all files
COPY . .

# Set the OpenSSL legacy provider to fix Webpack build issue
ENV NODE_OPTIONS=--openssl-legacy-provider

# Build the app
RUN npm run build

# Install serve to serve the build directory
RUN npm install -g serve

EXPOSE 3000

# Start the app
CMD ["serve", "-s", "build", "-l", "3000"]
