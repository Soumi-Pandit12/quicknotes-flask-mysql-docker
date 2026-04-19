# 🚀 QuickNotes — Containerized Notes App (Flask + MySQL)

## 📌 Overview

QuickNotes is a lightweight web application designed to store and manage personal notes efficiently.  
It is built using Flask for the backend and MySQL for persistent data storage, and fully containerized using Docker.

The project demonstrates a real-world two-tier architecture where application and database services run in isolated containers.

---

## 🛠 Tech Stack

- **Backend:** Flask (Python)  
- **Database:** MySQL 8  
- **Frontend:** HTML + CSS (custom UI)  
- **Containerization:** Docker & Docker Compose  

---

## 🏗 Architecture

This project follows a **two-tier architecture**:

- Flask application runs in one container  
- MySQL database runs in a separate container  
- Docker Compose orchestrates both services  
- Internal communication via Docker networking  
- Environment variables used for configuration  

---

## ⚙️ Prerequisites

Make sure you have:

- Docker  
- Docker Compose  
- Git  
- Code Editor (optional, e.g., VS Code)  

---

## 📂 Project Structure

```text
quicknotes/
│── app/
│   ├── app.py
│   ├── templates/
│   │   └── index.html
│   ├── static/
│   │   └── style.css
│
│── docker-compose.yml
│── Dockerfile
│── requirements.txt
│── .env
│── .gitignore
│── README.md
```

---

## 🚀 Project Setup

### 1. Clone Repository

```bash
git clone https://github.com/Soumi-Pandit12/quicknotes-flask-mysql-docker
cd quicknotes-flask-mysql-docker
```

---

### 2. Create Environment File

```bash
cp .env.example .env
```

---

### 3. Run Application

```bash
docker-compose up -d --build
```

---

### 4. Access Application

```
http://localhost:5000
```

---

### 5. Stop Application

```bash
docker-compose down
```

---

## ✅ Verification

### 🌐 Check Application
- Open browser → http://localhost:5000  
- Add & delete notes  

### 📦 Check Containers
```bash
docker ps
```

Expected:
- quicknotes_app  
- quicknotes_mysql  

---

### 🗄️ Check Database

```bash
docker exec -it quicknotes_mysql mysql -u root -p
```

```sql
USE quicknotes_db;
SELECT * FROM notes;
```

---

### 📜 Logs

```bash
docker-compose logs -f
```

---

## ⚙️ Run Without Docker Compose

### MySQL Container
```bash
docker run -d \
  --name quicknotes_mysql \
  -e MYSQL_ROOT_PASSWORD=rootpassword \
  -e MYSQL_DATABASE=quicknotes_db \
  -e MYSQL_USER=notesuser \
  -e MYSQL_PASSWORD=notespass \
  -v mysql_data:/var/lib/mysql \
  mysql:8
```

### Build App
```bash
docker build -t quicknotes_app .
```

### Run App
```bash
docker run -d \
  --name quicknotes_app \
  -p 5001:5000 \
  --link quicknotes_mysql:mysql \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=notesuser \
  -e MYSQL_PASSWORD=notespass \
  -e MYSQL_DB=quicknotes_db \
  quicknotes_app
```

---

## 🧠 Key Learnings

- Multi-container Docker setup  
- Container networking  
- Persistent storage with volumes  
- Debugging DB connection issues  


---

# 🚀 CI/CD Pipeline with Jenkins

This project is extended with a fully automated **CI/CD pipeline using Jenkins**.

---

## 🔄 Workflow

```
GitHub → Jenkins → Docker Compose → AWS EC2 → Live App
```

---

## ⚙️ Jenkins Setup

### 1. Launch Jenkins on EC2

```
http://<EC2-IP>:8080
```

---

### 2. Install Dependencies

```bash
sudo apt update
sudo apt install docker.io -y
sudo apt install docker-compose -y
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

---

### 3. Install Plugins

- Pipeline  
- Git  
- Docker Pipeline  

---

### 4. Create Pipeline Job

- Pipeline script from SCM  
- Git repo: your repo  
- Branch: main  
- Script: Jenkinsfile  

---

### 5. Jenkinsfile

```groovy
pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git url: 'https://github.com/Soumi-Pandit12/quicknotes-flask-mysql-docker.git', branch: 'main'
            }
        }

        stage('Stop Containers') {
            steps {
                sh 'docker-compose down || true'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }
    }
}
```

---

### 6. Enable Auto Trigger

GitHub → Settings → Webhooks:

```
http://<EC2-IP>:8080/github-webhook/
```

---

## ⚡ CI/CD Features

- Auto deployment on every push  
- Real-time updates  
- No manual intervention  
- Full automation  

---

## 🧪 CI/CD Test

1. Change code  
2. Push to GitHub  
3. Jenkins triggers automatically  
4. App updates live  

---

## 🧠 CI/CD Learnings

- Jenkins automation  
- Webhook integration  
- Deployment debugging  
- Real DevOps workflow  

---

## 👨‍💻 Author

Soumi Pandit
