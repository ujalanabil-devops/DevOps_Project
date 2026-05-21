# Multi-Stage Docker Setup for Node.js App

This project demonstrates how to create a **production-ready Docker image** for a Node.js application using a **multi-stage Docker build**.

---

# 📦 Project Architecture

```text
Local Machine
     │
     ▼
┌──────────────────────┐
│   Docker Builder     │
│ Install dependencies │
│ Build application    │
└─────────┬────────────┘
          │
          ▼
┌──────────────────────┐
│ Production Container │
│ Lightweight Image    │
│ Runs Node.js App     │
└─────────┬────────────┘
          │
          ▼
     Browser :3000
```

---

# 📁 Dockerfile

```dockerfile
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
```

---

# 🚀 Step-by-Step Explanation

---

# 🟢 Stage 1 — Builder Stage

```dockerfile
FROM node:20-alpine AS builder
```

## What it does

- Uses lightweight Alpine Linux image
- Installs Node.js v20
- Names this stage as `builder`

## Why use builder stage?

This stage is used to:

- Install dependencies
- Compile/build app
- Prepare files

The final production image will stay smaller because build tools are not included.

---

```dockerfile
WORKDIR /app
```

## What it does

Creates `/app` directory inside container.

All commands after this run inside `/app`.

Equivalent to:

```bash
mkdir /app
cd /app
```

---

```dockerfile
COPY package*.json ./
```

## What it does

Copies:

- package.json
- package-lock.json

into container.

---

## Why copy package files first?

This is very important for **Docker Layer Caching**.

If source code changes but package.json stays same:

✅ Docker reuses dependency layer  
✅ Build becomes much faster

---

# Docker Cache Example

## First Build

```bash
docker build -t myapp .
```

Docker installs dependencies.

---

## Second Build (only code changed)

```bash
docker build -t myapp .
```

Docker skips:

```dockerfile
RUN npm ci
```

because package.json did not change.

This saves a lot of time.

---

```dockerfile
RUN npm ci
```

## What it does

Installs dependencies exactly from package-lock.json.

---

## Why use npm ci instead of npm install?

| npm ci | npm install |
|---|---|
| Faster | Slower |
| Clean install | Can modify lock file |
| Best for Docker/CI | Better for local development |
| Reproducible builds | Can vary |

---

```dockerfile
COPY . /app
```

## What it does

Copies complete project into container.

Example:

```text
server.js
routes/
controllers/
public/
views/
```

Everything gets copied into `/app`.

---

## Why not copy everything first?

Because if you copy everything before:

```dockerfile
RUN npm ci
```

then every code change invalidates cache.

Build becomes slower.

---

```dockerfile
# RUN npm run build
```

## Optional Step

Used for:

- React
- Angular
- Vue
- TypeScript
- Next.js

This generates production build files.

If your app is simple Node.js backend:

❌ Not needed

---

# 🟢 Stage 2 — Production Stage

This is the final lightweight container users will run.

---

```dockerfile
FROM node:20-alpine
```

Starts fresh clean image.

Builder tools from previous stage are not included.

Result:

✅ Smaller image  
✅ Better security  
✅ Faster deployment

---

```dockerfile
ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password \
    NODE_ENV=production
```

## What it does

Creates environment variables.

Application can access them using:

```javascript
process.env.MONGO_DB_USERNAME
process.env.MONGO_DB_PWD
process.env.NODE_ENV
```

---

# Example in Node.js

```javascript
console.log(process.env.NODE_ENV)
```

Output:

```text
production
```

---

```dockerfile
WORKDIR /app
```

Sets working directory again for production image.

---

```dockerfile
COPY package*.json ./
```

Copies package files again.

Why again?

Because production image is completely new and separate from builder stage.

---

```dockerfile
RUN npm ci --only=production
```

## What it does

Installs only production dependencies.

---

# Example

Installed:

✅ express  
✅ mongoose  

Not installed:

❌ nodemon  
❌ eslint  
❌ jest  

This reduces image size.

---

```dockerfile
COPY --from=builder /app ./
```

## MOST IMPORTANT LINE

Copies application from builder stage into production image.

---

# What happens internally?

Docker copies:

```text
/app
```

from:

```dockerfile
AS builder
```

into current container.

---

# Why use this?

Because:

✅ Build files already prepared  
✅ Reuse installed files  
✅ Final image smaller  
✅ Cleaner architecture

---

# Visual Flow

```text
Builder Stage
┌────────────────────┐
│ Install dependencies
│ Build application
│ Prepare files
└─────────┬──────────┘
          │ COPY --from=builder
          ▼
Production Stage
┌────────────────────┐
│ Lightweight image
│ Only runtime files
└────────────────────┘
```

---

```dockerfile
EXPOSE 3000
```

## What it does

Documents application port.

Application runs on:

```text
localhost:3000
```

---

```dockerfile
CMD ["node", "server.js"]
```

## What it does

Starts Node.js application when container starts.

Equivalent to:

```bash
node server.js
```

---

# ▶️ Build Docker Image

```bash
docker build -t my-node-app .
```

---

# ▶️ Run Container

```bash
docker run -p 3000:3000 my-node-app
```

---

# 🌐 Access Application

Open browser:

```text
http://localhost:3000
```

---

# 📌 Why Multi-Stage Build is Important

| Benefit | Explanation |
|---|---|
| Smaller Image | Removes unnecessary build tools |
| Faster Deployment | Lightweight containers |
| Better Security | Fewer packages |
| Cleaner Architecture | Separate build/runtime |
| Production Ready | Industry standard |

---

# 📌 Recommended .dockerignore

Create `.dockerignore`

```text
node_modules
npm-debug.log
Dockerfile
.git
.gitignore
README.md
```

---

# 📌 Check Running Containers

```bash
docker ps
```

---

# 📌 Stop Container

```bash
docker stop <container-id>
```

---

# 📌 Remove Container

```bash
docker rm <container-id>
```

---

# 📌 Remove Image

```bash
docker rmi my-node-app
```

---

# 📌 Open Shell Inside Container

```bash
docker exec -it <container-id> sh
```

---

# 📌 Check Files Inside Container

```bash
ls -la
```

---

# 📌 Check Environment Variables

```bash
printenv
```

---

# 📌 Production Best Practices

✅ Use `.dockerignore`  
✅ Use `npm ci`  
✅ Use multi-stage builds  
✅ Keep image lightweight  
✅ Use environment variables  
✅ Never hardcode secrets in Dockerfile  

---

# 📌 Better Security Recommendation

Instead of hardcoding:

```dockerfile
ENV MONGO_DB_USERNAME=admin
```

use:

```bash
docker run -e MONGO_DB_USERNAME=myuser \
           -e MONGO_DB_PWD=mypassword \
           my-node-app
```

---

# 🎯 Final Summary

This Dockerfile:

✅ Uses multi-stage builds  
✅ Optimizes Docker caching  
✅ Installs production dependencies only  
✅ Creates smaller production image  
✅ Follows modern Docker best practices  
✅ Is suitable for deployment

---

# 👨‍💻 Author

Created for learning Docker + Node.js production deployment.
