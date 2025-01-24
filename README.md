# Notes App Project

This repository contains the code for a **Notes App** built with Django, Dockerized for deployment, and using a MySQL database backend. The project structure is organized for easy development, testing, and deployment.

---

## Project Structure

```
.
├── Dockerfile             # Dockerfile for building the Django application container
├── Procfile              # Configuration file for process management in production
├── README.md             # Project documentation (this file)
├── api/                  # Contains Django application logic for APIs
├── data/                 # Persistent storage volume for the MySQL database
├── db.sqlite3            # Default SQLite database file (local development)
├── docker-compose.yml    # Docker Compose configuration file
├── manage.py             # Django management script
├── mynotes/              # Core Django project folder (settings, URLs, WSGI, etc.)
├── nginx/                # Configuration for Nginx as a reverse proxy for Django
├── notesapp/             # Notes application with models, views, templates, etc.
├── requirements.txt      # Python dependencies for the Django app
├── staticfiles/          # Collected static files for the Django app
```

---

## Folder/Files Overview

### 1. Dockerfile
This file contains the instructions to build a Docker image for the Django app. It defines the base image, dependencies, and commands to run the application.

### 2. Procfile
Used to define the application’s process types and entry points for running the app in production environments (e.g., Heroku or similar).

### 3. README.md
This documentation file explains the project structure, setup instructions, and other key details.

### 4. `api/`
This folder contains the Django application code for APIs. It includes:
- **Views**: API endpoints for handling client requests.
- **Serializers**: Data serialization and validation.
- **URLs**: Routes for the API endpoints.

### 5. `data/`
A directory for MySQL data persistence when running the database container. This ensures that the database data is not lost when the container stops.

### 6. `db.sqlite3`
A default SQLite database file for local development. This can be replaced by the MySQL database configured in the Docker setup.

### 7. docker-compose.yml
This file defines the services required to run the application, including:
- **Django**: The application backend.
- **MySQL**: The database service.
- **Nginx**: The reverse proxy.

It also handles service dependencies (MySQL -> Django -> Nginx).

### 8. manage.py
Django’s command-line utility for managing the project. Use it to run migrations, start the development server, create superusers, etc.

### 9. `mynotes/`
The core Django project folder containing settings, URL configuration, and WSGI/ASGI modules.

### 10. `nginx/`
This folder holds the configuration files for Nginx, which serves as the reverse proxy to forward requests to the Django app and serve static files.

### 11. `notesapp/`
The primary application folder for the Notes App. It includes:
- **Models**: Database schemas.
- **Views**: Business logic for the app.
- **Templates**: HTML files for the user interface.
- **Static Files**: CSS, JavaScript, and images.

### 12. requirements.txt
A list of Python dependencies for the project. These are installed in the Docker image during build time.

### 13. staticfiles/
The directory where Django collects static files when `collectstatic` is run. This is served by Nginx in production.

---

## Setup Instructions

### Prerequisites
- Docker and Docker Compose installed.
- Python 3.x installed (for local development).

### Running the App (Using Docker Compose)
1. Clone the repository:
   ```bash
   git clone <repository_url>
   cd <repository_name>
   ```

2. Build and start the services:
   ```bash
   docker-compose up --build
   ```

3. Access the app at `http://localhost` (or the configured port).
