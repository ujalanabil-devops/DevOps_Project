# 🚀 Dockerized Node.js + MongoDB Project

> Production-style beginner DevOps project using Docker, MongoDB, Mongo Express, and Node.js.
> This project demonstrates how a local Node.js application connects securely to MongoDB running inside Docker Container.

---

## 📌 Features

✅ MongoDB Docker Container  
✅ Mongo Express UI  
✅ Custom Docker Network  
✅ Local Node.js App  
✅ MongoDB Connection using Express  
✅ Beginner Friendly DevOps Project

---

# 🏗️ Architecture Diagram

![Architecture](./screenshots/project-architecture.png)

---

# 📸 Project Screenshots

## Docker Containers

![Docker](./screenshots/docker-ps.png)

---

## Mongo Express Dashboard

![Mongo Express](./screenshots/mongo-express.png)

---

## Node.js Server

![Node Server](./screenshots/node-server.png)

---

# ⚙️ Technologies Used

| Technology | Purpose |
|------------|----------|
| Node.js | Backend Runtime |
| Express.js | Web Framework |
| MongoDB | Database |
| Mongo Express | Database UI |
| Docker | Containerization |

---

# 📂 Project Structure

```bash
node-mongo-docker-project/
│
├── screenshots/
├── app/
│   ├── server.js
│   ├── package.json
│   ├── index.html
|   └── images/
|     
│
├── README.md
└── docker-compose.yml
```

---

# 🚀 Setup Instructions

## 1️⃣ Create Docker Network

```bash
docker docker network create mongo-network 

```

```bash
docker network ls
```

---

## 2️⃣ Run MongoDB

```bash
docker pull mongo
```

```bash
docker run -d \
--name mongodb \
--network mongo-network \
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
mongo
```

---

## 3️⃣ Run Mongo Express

```bash
docker pull mongo-express
```

```bash
docker run -d \
--name mongo-express \
--network mongo-network \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express
```

---

## 4️⃣ Start Node.js App

```bash
install npm
```

```bash
node server.js
```

---
# 🔍 Useful Docker Commands

## Show images

```bash
docker images
```

## Show containers

```bash
docker ps (to check running containers only)
docker ps -a (to check stop and running containers)
```

## Stop container

```bash
docker stop mongodb
docker stop mongo-express
```

## Start container

```bash
docker start mongodb
docker start mongo-express
```

## Remove container

```bash
docker rm mongodb
docker rm mongo-express
```

## Remove network

```bash
docker network rm mynet
```

---

# 🌐 Push Project to GitHub

## Initialize Git

```bash
git init
```

## Add files

```bash
git add .
```

## Commit

```bash
git commit -m "Initial Docker MongoDB Node.js Project"
```

## Add GitHub Repository

```bash
git remote add origin YOUR_GITHUB_REPO_URL
```

## Push Code

```bash
git branch -M main
git push -u origin main
```

---

# 📸 Screenshots To Add

Recommended screenshots for GitHub:

- Docker containers running
- Mongo Express dashboard
- Node.js terminal output
- Browser output

---

# 🌐 Application URLs

| Service | URL |
|---------|-----|
| Node.js App | http://localhost:3000 |
| Mongo Express | http://localhost:8081 |

---
# 🎯 Learning Outcomes

After completing this project you will understand:

- Docker networking
- MongoDB containers
- Mongo Express setup
- Node.js MongoDB connection
- Express.js basics
- GitHub project deployment

---
# 📈 Future Improvements

- Docker Compose
- Kubernetes Deployment
- CI/CD Pipeline
- Jenkins Integration
- Nginx Reverse Proxy
- Monitoring with Grafana

---

# 👨‍💻 Author

SYED NABIL AKHTAR

GitHub: https://github.com/ujalanabil-devops

---
⭐ If you like this project, give it a star!
