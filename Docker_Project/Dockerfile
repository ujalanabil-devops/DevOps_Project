# =========================
# Stage 1 - Build Stage
# =========================
FROM node:20-alpine AS builder

# Create app directory inside container.
WORKDIR /app

# Copy package files first. build become fast. docker use layer caching.
COPY package*.json ./

# Install dependencies.preferred for docker. faster than npm install.
RUN npm ci

# Copy source code
COPY . /app

# Build application
# Remove this line if your app has no build step
# RUN npm run build


# =========================
# Stage 2 - Production Stage
# =========================
FROM node:20-alpine

# Set environment
ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password \
    NODE_ENV=production

# Create app directory
WORKDIR /app

# Copy only package files
COPY package*.json ./

# Install only production dependencies
RUN npm ci --only=production

# Copy entire app from builder 
COPY --from=builder /app ./

# If using public/static files
#COPY --from=builder /app/public ./public

# Expose application port
EXPOSE 3000

# Start application
CMD ["node", "server.js"]