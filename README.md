# 🚀 Dockerized Node.js + MongoDB Project

> Production-style beginner DevOps project using Docker, MongoDB, Mongo Express, and Node.js.

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
project/
│
├── screenshots/
├── app/
│   ├── server.js
│   ├── package.json
│   └── index.html
│
├── README.md
└── docker-compose.yml
```

---

# 🚀 Setup Instructions

## 1️⃣ Create Docker Network

```bash
docker network create mynet
```

---

## 2️⃣ Run MongoDB

```bash
docker run -d \
--name mongodb \
--network mynet \
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
mongo
```

---

## 3️⃣ Run Mongo Express

```bash
docker run -d \
--name mongo-express \
--network mynet \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
mongo-express
```

---

## 4️⃣ Start Node.js App

```bash
node server.js
```

---

# 🌐 Application URLs

| Service | URL |
|---------|-----|
| Node.js App | http://localhost:3000 |
| Mongo Express | http://localhost:8081 |

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

Your Name

GitHub: https://github.com/yourusername

---
⭐ If you like this project, give it a star!
