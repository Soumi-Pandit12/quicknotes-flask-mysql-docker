# 🚀 QuickNotes — Containerized Notes App (Flask + MySQL)

## 📌 Overview

QuickNotes is a lightweight web application designed to store and manage personal notes efficiently.
It is built using Flask for the backend and MySQL for persistent data storage, and fully containerized using Docker.

The project demonstrates a real-world two-tier architecture where application and database services run in isolated containers.

---

## 🛠 Tech Stack

* **Backend:** Flask (Python)
* **Database:** MySQL 8
* **Frontend:** HTML + CSS (custom UI)
* **Containerization:** Docker & Docker Compose

---

## 🏗 Architecture

This project follows a **two-tier architecture**:

* The Flask application runs in one container
* The MySQL database runs in a separate container
* Docker Compose orchestrates both services
* Internal communication happens using Docker networking (service name-based connection)
* Environment variables are used for secure configuration

---

⚙️ Prerequisites

Before running this project, make sure you have the following installed on your system:

Docker – required to build and run containers
Docker Compose – used to manage multi-container setup
Git – to clone the repository
Code Editor (optional) – such as VS Code for development and modification

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

## 📂 Project Setup

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

Edit the `.env` file if you want to customize database credentials or configuration.

---

### 3. Run Application

```bash
docker-compose up -d --build
```

---

### 4. Access Application

Open your browser and go to:

```text
http://localhost:5000
```

---

### 5. Stop Application (Optional)

```bash
docker-compose down
```


---

## ✅ Verification

After starting the application, follow these steps to verify everything is working correctly:

---

### 🌐 1. Check Application

Open your browser and go to:

```text
http://localhost:5000
```

* The QuickNotes UI should load successfully
* Try adding a note → it should appear instantly
* Delete a note → it should be removed from the list

---

### 📦 2. Verify Running Containers

Run the following command:

```bash
docker ps
```

You should see two containers running:

* `quicknotes_app`
* `quicknotes_mysql`

---

### 🗄️ 3. Verify Database Data

Access MySQL container:

```bash
docker exec -it quicknotes_mysql mysql -u root -p
```

Then run:

```sql
USE quicknotes_db;
SELECT * FROM notes;
```

* Notes added from UI should appear in the database

---

### 📜 4. Check Logs (Optional)

To view live logs:

```bash
docker-compose logs -f
```

* Ensure there are no connection errors
* Flask app should be running without crashes

---

### 🧠 Expected Result

* Application loads on browser
* Notes can be added and deleted
* Data is stored in MySQL
* Containers run without errors

---


## ⚙️ Run Without Docker Compose

You can also run the application manually using individual Docker commands instead of Docker Compose.

---

### 🗄️ 1. Create MySQL Container

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

---

### 🌐 2. Build Flask Application Image

```bash
docker build -t quicknotes_app .
```

---

### 🚀 3. Run Flask Container

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

### 🌍 4. Access Application

Open your browser:

```text
http://localhost:5000
```

---

### ⚠️ Notes

* Ensure the MySQL container is fully started before running the Flask container
* The `--link` option is used for basic container communication (Docker Compose is recommended for production)
* Data will persist using the Docker volume `mysql_data`



## 🧠 Key Learnings

* Building and containerizing a full-stack application
* Managing multi-container environments with Docker Compose
* Handling environment variables using `.env` files
* Debugging database connection issues in Docker
* Understanding container networking and service communication
* Implementing persistent storage using Docker volumes


---

## 💡 Future Enhancements

* Implement user authentication (login/signup)
* Add edit/update note functionality
* Improve UI responsiveness and styling
* Add REST API support
* Integrate CI/CD pipeline for automated deployment

---

## 👨‍💻 Author

Soumi Pandit
