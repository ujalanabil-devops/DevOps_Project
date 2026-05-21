# Docker Compose Setup for MongoDB + Mongo Express

This project demonstrates how to use **Docker Compose** to run:

- MongoDB database
- Mongo Express web UI

using a single `docker-compose.yml` file.

---

# 📦 Architecture

```text
Browser
   │
   ▼
localhost:8081
   │
   ▼
┌────────────────────┐
│   Mongo Express    │
│  Database Web UI   │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│      MongoDB       │
│   Database Server  │
└────────────────────┘
```

---

# 📁 docker-compose.yml

```yaml
version: '3'

services:
  mongodb:
    image: mongo
    ports:
      - 27017:27017

    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password

  mongo-express:
    image: mongo-express
    ports:
      - 8081:8081

    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
```

---

# 🚀 Step-by-Step Explanation

---

# 🟢 version: '3'

```yaml
version: '3'
```

## What it does

Defines Docker Compose file version.

Version 3 is commonly used and supported by modern Docker.

---

# 🟢 services

```yaml
services:
```

## What it does

Defines containers/services to run.

In this project:

- mongodb
- mongo-express

Each service becomes its own container.

---

# 🟢 MongoDB Service

```yaml
mongodb:
```

Creates MongoDB container.

Service name:

```text
mongodb
```

This name becomes internal Docker hostname.

Other containers can connect using:

```text
mongodb
```

instead of IP address.

---

# 🟢 image: mongo

```yaml
image: mongo
```

## What it does

Pulls official MongoDB image from Docker Hub.

Equivalent to:

```bash
docker pull mongo
```

---

# 🟢 ports

```yaml
ports:
  - 27017:27017
```

## Port Mapping Format

```text
HOST_PORT:CONTAINER_PORT
```

---

# What it means

| Host Machine | Docker Container |
|---|---|
| 27017 | 27017 |

---

# Access MongoDB

From local machine:

```text
localhost:27017
```

---

# 🟢 environment

```yaml
environment:
```

Used to define environment variables inside container.

---

# MongoDB Username

```yaml
- MONGO_INITDB_ROOT_USERNAME=admin
```

Creates root username:

```text
admin
```

---

# MongoDB Password

```yaml
- MONGO_INITDB_ROOT_PASSWORD=password
```

Creates root password:

```text
password
```

---

# MongoDB Login Credentials

| Username | Password |
|---|---|
| admin | password |

---

# 🟢 Mongo Express Service

```yaml
mongo-express:
```

Creates Mongo Express container.

Mongo Express is web-based MongoDB admin panel.

Similar to:

- phpMyAdmin for MySQL
- pgAdmin for PostgreSQL

---

# 🟢 image: mongo-express

```yaml
image: mongo-express
```

Downloads official Mongo Express image.

---

# 🟢 Mongo Express Port

```yaml
ports:
  - 8081:8081
```

Access browser UI on:

```text
http://localhost:8081
```

---

# 🟢 Mongo Express Environment Variables

---

## MongoDB Username

```yaml
- ME_CONFIG_MONGODB_ADMINUSERNAME=admin
```

Mongo Express uses this username to connect to MongoDB.

---

## MongoDB Password

```yaml
- ME_CONFIG_MONGODB_ADMINPASSWORD=password
```

Mongo Express uses this password to connect.

---

## MongoDB Server Name

```yaml
- ME_CONFIG_MONGODB_SERVER=mongodb
```

MOST IMPORTANT LINE.

---

# Why mongodb?

Because Docker Compose creates internal network automatically.

Service name:

```yaml
mongodb:
```

becomes hostname:

```text
mongodb
```

Mongo Express connects internally using:

```text
mongodb:27017
```

---

# 🔥 Internal Docker Networking

Docker Compose automatically creates:

✅ Network  
✅ DNS resolution  
✅ Container communication  

---

# Visual Networking Flow

```text
mongo-express container
        │
        ▼
   mongodb:27017
        │
        ▼
   mongodb container
```

No manual IP configuration needed.

---

# ▶️ Start Containers

Run:

```bash
docker-compose up
```

or modern command:

```bash
docker compose up
```

---

# ▶️ Run in Background

```bash
docker compose up -d
```

---

# ▶️ Check Running Containers

```bash
docker ps
```

---

# ▶️ Stop Containers

```bash
docker compose down
```

---

# 🌐 Access Mongo Express

Open browser:

```text
http://localhost:8081
```

---

# 🔐 Mongo Express Login

Depending on image version, it may ask:

| Username | Password |
|---|---|
| admin | pass |

OR sometimes directly opens dashboard.

---

# 📌 Common Issue

## Error:

```text
MongoNetworkError
```

### Cause

MongoDB container not ready yet.

### Solution

Restart:

```bash
docker compose restart
```

---

# 📌 Check Logs

## MongoDB Logs

```bash
docker logs <mongodb-container-id>
```

---

## Mongo Express Logs

```bash
docker logs <mongo-express-container-id>
```

---

# 📌 Open Shell Inside Container

## MongoDB Container

```bash
docker exec -it <container-id> bash
```

or Alpine images:

```bash
docker exec -it <container-id> sh
```

---

# 📌 List Docker Networks

```bash
docker network ls
```

---

# 📌 Inspect Docker Network

```bash
docker network inspect <network-name>
```

---

# 📌 Persistent Storage (Recommended)

Current setup loses data after container removal.

Better approach:

```yaml
volumes:
  - mongo-data:/data/db

volumes:
  mongo-data:
```

---

# 📌 Improved Production Version

```yaml
version: '3'

services:
  mongodb:
    image: mongo
    container_name: mongodb

    ports:
      - 27017:27017

    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password

    volumes:
      - mongo-data:/data/db

  mongo-express:
    image: mongo-express

    ports:
      - 8081:8081

    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb

    depends_on:
      - mongodb

volumes:
  mongo-data:
```

---

# 📌 Why depends_on?

```yaml
depends_on:
  - mongodb
```

Ensures MongoDB starts before Mongo Express.

---

# 📌 Why volumes?

```yaml
volumes:
  - mongo-data:/data/db
```

Prevents data loss.

Without volume:

❌ Database deleted after container removal

With volume:

✅ Data persists

---

# 📌 Docker Compose Benefits

| Benefit | Explanation |
|---|---|
| Easy setup | Single command |
| Automatic networking | Containers communicate easily |
| Infrastructure as code | Configuration stored in YAML |
| Faster development | Reusable environments |
| Scalable | Add more services easily |

---

# 📌 Useful Commands

---

## Build Containers

```bash
docker compose build
```

---

## Restart Services

```bash
docker compose restart
```

---

## Remove Everything

```bash
docker compose down -v
```

---

## View Real-Time Logs

```bash
docker compose logs -f
```

---

# 🎯 Final Summary

This setup:

✅ Runs MongoDB container  
✅ Runs Mongo Express container  
✅ Creates automatic Docker network  
✅ Allows browser database access  
✅ Uses environment variables securely  
✅ Is beginner friendly and production extendable

---

# 👨‍💻 Author

Docker Compose MongoDB learning project.
