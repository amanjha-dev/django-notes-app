# Django Notes App - Dockerized Deployment

A full-stack Dockerized Django Notes Application deployed using Docker Compose with Nginx, Gunicorn, Django, and MySQL.

## Tech Stack

* Python 3.9
* Django
* MySQL 8
* Gunicorn
* Nginx
* Docker
* Docker Compose
* AWS EC2

---

# Project Architecture

```text
Client Browser
       │
       ▼
    Nginx
       │
       ▼
   Gunicorn
       │
       ▼
    Django
       │
       ▼
    MySQL
```

---

# Features

* Dockerized Django application
* Reverse proxy using Nginx
* Production-ready Gunicorn server
* MySQL database integration
* Docker Compose multi-container setup
* Health checks for services
* Automatic migrations on startup
* EC2 deployment ready

---

# Folder Structure

```text
django-notes-app/
│
├── nginx/
│   └── default.conf
│
├── data/
│   └── mysql/
│
├── notesapp/
├── api/
├── manage.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── .gitignore
└── README.md
```

---

# Prerequisites

Make sure you have installed:

* Docker
* Docker Compose
* Git
* Python (optional for local development)

---

# Clone Repository

```bash
git clone https://github.com/amanjha-dev/django-notes-app.git
cd django-notes-app
```

---

# Environment Variables

Create a `.env` file in the project root:

```env
DEBUG=True
SECRET_KEY=your_secret_key
DB_NAME=test_db
DB_USER=root
DB_PASSWORD=root
DB_HOST=db
DB_PORT=3306
```

---

# Dockerfile

The Django application is containerized using Python 3.9.

Key features:

* Installs dependencies
* Installs netcat for DB connection checks
* Uses Gunicorn for production
* Exposes port 8000

---

# Docker Compose Services

## 1. Django App

* Runs migrations automatically
* Waits for MySQL before startup
* Served using Gunicorn

## 2. MySQL Database

* Persistent storage using Docker volumes
* Health checks enabled

## 3. Nginx

* Reverse proxy for Django
* Exposes port 80

---

# Build and Run

Run the following command:

```bash
docker compose up --build
```

Run in detached mode:

```bash
docker compose up -d --build
```

---

# Stop Containers

```bash
docker compose down
```

---

# View Logs

```bash
docker compose logs -f
```

Specific container logs:

```bash
docker logs django_cont
docker logs nginx_cont
docker logs db_cont
```

---

# Useful Docker Commands

## Remove unused Docker resources

```bash
docker system prune -a -f --volumes
```

## Remove build cache

```bash
docker builder prune -a -f
```

## Check running containers

```bash
docker ps
```

---

# Deployment on AWS EC2

## Steps

1. Launch Ubuntu EC2 instance
2. Install Docker and Docker Compose
3. Clone repository
4. Configure security groups
5. Run Docker Compose

---

# Open Required Ports

| Port | Purpose                       |
| ---- | ----------------------------- |
| 22   | SSH                           |
| 80   | HTTP                          |
| 8000 | Django (optional)             |
| 3306 | MySQL (optional/private only) |

---

# Security Notes

* Do not expose MySQL publicly
* Store secrets in environment variables
* Use HTTPS in production
* Replace DEBUG=True with DEBUG=False in production

---

# Common Issues

## MySQL Connection Error

Install netcat inside container:

```Dockerfile
apt-get install -y netcat-openbsd
```

---

## Permission Denied in MySQL Data Folder

Remove MySQL data folder:

```bash
sudo rm -rf data/mysql/db
```

---

## No Space Left on Device

Clean Docker:

```bash
docker system prune -a -f --volumes
```

---

# Future Improvements

* CI/CD using GitHub Actions
* Kubernetes deployment
* HTTPS using Certbot
* Redis caching
* Celery background tasks
* AWS ECS deployment
* Monitoring with Prometheus/Grafana

---

# Author

## Aman Jha

* MERN Stack Developer
* Django & DevOps Learner
* AWS & Docker Enthusiast

GitHub:

[https://github.com/amanjha-dev](https://github.com/amanjha-dev)

---

# Repository

[https://github.com/amanjha-dev/django-notes-app](https://github.com/amanjha-dev/django-notes-app)

---

# License

This project is open-source and available under the MIT License.
