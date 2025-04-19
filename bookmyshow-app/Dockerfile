# === Stage 1: Build Stage ===
FROM node:18 AS builder

# Set working directory
WORKDIR /app

# Copy dependency files first (for better caching)
COPY package.json package-lock.json ./

# Force install compatible PostCSS version and dependencies
RUN npm install postcss@8.4.21 postcss-safe-parser@6.0.0 --legacy-peer-deps
RUN npm install

# Copy full source code
COPY . .

# Build your project (uncomment if you use a build step)
# RUN npm run build


# === Stage 2: Production Stage ===
FROM node:18-slim AS production

# Set working directory
WORKDIR /app

# Copy only what's needed from the builder
COPY --from=builder /app ./

# Set environment variables
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV PORT=3000

# Expose the port
EXPOSE 3000

# Start the app
CMD ["npm", "start"]

