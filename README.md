# 📝 QuickNotes — Flask + MySQL + Docker

A beginner-friendly, production-inspired **Notes web application** built with **Python Flask**, **MySQL**, and fully containerized using **Docker & Docker Compose**.

> Write it. Store it. Never lose it.

---

## ✨ Features

- ➕ **Add Notes** — Write and save notes instantly
- 📋 **View All Notes** — See all your notes on one clean page, newest first
- 🗑️ **Delete Notes** — Remove any note with a single click
- 🕒 **Timestamps** — Every note shows when it was created
- 🐳 **Fully Dockerized** — Runs anywhere with a single command

---

## 🛠️ Tech Stack

| Layer            | Technology               |
|------------------|--------------------------|
| Backend          | Python 3.9 + Flask       |
| Database         | MySQL 8.0                |
| Frontend         | HTML5 + CSS3 (Vanilla)   |
| Containerization | Docker + Docker Compose  |
| Config           | Environment Variables (.env) |

---

## 📁 Folder Structure

```
QuickNotes/
│
├── app/
│   ├── app.py              # Flask routes and DB logic
│   ├── templates/
│   │   └── index.html      # HTML template (Jinja2)
│   └── static/
│       └── style.css       # Custom CSS styling
│
├── Dockerfile              # Container definition for Flask app
├── docker-compose.yml      # Multi-container orchestration (app + MySQL)
├── requirements.txt        # Python dependencies
├── .env                    # Environment variables (not committed to Git)
├── .gitignore              # Files excluded from version control
└── README.md               # Project documentation (you are here)
```

---

## ⚙️ Setup & Run (Docker)

### Prerequisites
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/QuickNotes.git
cd QuickNotes
```

### 2. Configure Environment Variables

The `.env` file is already provided with default values for local development:

```env
MYSQL_HOST=mysql
MYSQL_USER=notesuser
MYSQL_PASSWORD=notespass
MYSQL_DB=quicknotes_db
```

> ⚠️ Change these values before deploying to any public server.

### 3. Build & Start the Application

```bash
docker-compose up --build
```

This command will:
- Pull the MySQL 8.0 image
- Build the Flask app Docker image
- Start both containers and link them together
- Initialize the database schema automatically

### 4. Open the App

Visit **[http://localhost:5000](http://localhost:5000)** in your browser.

### 5. Stop the Application

```bash
# Stop containers (data is preserved)
docker-compose down

# Stop containers AND delete stored data
docker-compose down -v
```

---

## 🖥️ Screenshots

> _Screenshots will be added after the first deployment._

| Home Page | Add Note | Delete Note |
|-----------|----------|-------------|
| _(screenshot)_ | _(screenshot)_ | _(screenshot)_ |

---

## 🏗️ Architecture Overview

```
Browser (User)
     │
     ▼  HTTP Request (port 5000)
┌──────────────────────────────────┐
│         Flask App (Docker)       │
│  ┌────────────────────────────┐  │
│  │  Routes:                   │  │
│  │   / → View Notes           │  │
│  │   /add → Add Note          │  │
│  │   /delete/<id> → Delete    │  │
│  └────────────┬───────────────┘  │
└───────────────┼──────────────────┘
                │ SQL Queries
                ▼
┌──────────────────────────────────┐
│       MySQL 8.0 (Docker)         │
│  Database: quicknotes_db         │
│  Table: notes                    │
│   - id (INT, PK, AUTO_INCREMENT) │
│   - content (TEXT)               │
│   - created_at (DATETIME)        │
└──────────────────────────────────┘
         │
         ▼
  Named Volume: quicknotes_mysql_data
  (Persists data across restarts)
```

### How It Works

1. **User** submits a note in the browser form
2. **Flask** receives the POST request at `/add`
3. **Flask** connects to **MySQL** (inside the Docker network)
4. The note is inserted into the `notes` table
5. Flask **redirects** back to `/`, which fetches and displays all notes

---

## 🔒 Environment Variables Reference

| Variable          | Description              | Default          |
|-------------------|--------------------------|------------------|
| `MYSQL_HOST`      | MySQL service hostname   | `mysql`          |
| `MYSQL_USER`      | Database username        | `notesuser`      |
| `MYSQL_PASSWORD`  | Database password        | `notespass`      |
| `MYSQL_DB`        | Database name            | `quicknotes_db`  |

---

## 🚀 Future Improvements

- [ ] User authentication (login/signup)
- [ ] Search and filter notes
- [ ] Edit existing notes
- [ ] REST API with JSON responses
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Deploy to AWS / Render / Railway

---

## 👤 Author

**Your Name**
[GitHub](https://github.com/your-username) | [LinkedIn](https://linkedin.com/in/your-username)

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
