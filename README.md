# Django Notes App Project

This repository contains the code for a **Notes App** built with Django, Dockerized for deployment, and using a MySQL database backend. The project structure is organized for easy development, testing, and deployment, with an integrated CI/CD pipeline using Jenkins.

---

## Project Structure

```
.
├── Dockerfile             # Dockerfile for building the Django application container
├── Jenkinsfile            # Jenkins pipeline configuration file
├── Procfile               # Configuration file for process management in production
├── README.md              # Project documentation (this file)
├── api/                   # Contains Django application logic for APIs
├── data/                  # Persistent storage volume for the MySQL database
├── db.sqlite3             # Default SQLite database file (local development)
├── docker-compose.yml     # Docker Compose configuration file
├── manage.py              # Django management script
├── mynotes/               # Core Django project folder (settings, URLs, WSGI, etc.)
├── nginx/                 # Configuration for Nginx as a reverse proxy for Django
├── notesapp/              # Notes application with models, views, templates, etc.
├── requirements.txt       # Python dependencies for the Django app
├── staticfiles/           # Collected static files for the Django app
```

---

## Folder/Files Overview

### 1. Dockerfile
This file contains the instructions to build a Docker image for the Django app. It defines the base image, dependencies, and commands to run the application.

### 2. Jenkinsfile
Defines the CI/CD pipeline for automating the build, test, and deployment process. The pipeline includes:
- Cloning the repository.
- Building the Docker image.
- Running tests inside the container.
- Pushing the image to a Docker registry.
- Deploying the application using Docker Compose on a remote server.

### 3. Procfile
Used to define the application’s process types and entry points for running the app in production environments (e.g., Heroku or similar).

### 4. README.md
This documentation file explains the project structure, setup instructions, and other key details.

### 5. `api/`
This folder contains the Django application code for APIs. It includes:
- **Views**: API endpoints for handling client requests.
- **Serializers**: Data serialization and validation.
- **URLs**: Routes for the API endpoints.

### 6. `data/`
A directory for MySQL data persistence when running the database container. This ensures that the database data is not lost when the container stops.

### 7. `db.sqlite3`
A default SQLite database file for local development. This can be replaced by the MySQL database configured in the Docker setup.

### 8. docker-compose.yml
This file defines the services required to run the application, including:
- **Django**: The application backend.
- **MySQL**: The database service.
- **Nginx**: The reverse proxy.
- **Jenkins** (if applicable in CI/CD setup).

It also handles service dependencies (MySQL -> Django -> Nginx).

### 9. manage.py
Django’s command-line utility for managing the project. Use it to run migrations, start the development server, create superusers, etc.

### 10. `mynotes/`
The core Django project folder containing settings, URL configuration, and WSGI/ASGI modules.

### 11. `nginx/`
This folder holds the configuration files for Nginx, which serves as the reverse proxy to forward requests to the Django app and serve static files.

### 12. `notesapp/`
The primary application folder for the Notes App. It includes:
- **Models**: Database schemas.
- **Views**: Business logic for the app.
- **Templates**: HTML files for the user interface.
- **Static Files**: CSS, JavaScript, and images.

### 13. requirements.txt
A list of Python dependencies for the project. These are installed in the Docker image during build time.

### 14. staticfiles/
The directory where Django collects static files when `collectstatic` is run. This is served by Nginx in production.

---

## Setup Instructions

### Prerequisites
- Docker and Docker Compose installed.
- Python 3.x installed (for local development).
- Jenkins installed and configured (for CI/CD pipeline).

### Running the App (Using Docker Compose)
1. Clone the repository:
   ```bash
   git clone https://github.com/M-Tayyab06/django-notes-app.git
   cd django-notes-app
   ```

2. Build and start the services:
   ```bash
   docker-compose up --build
   ```

3. Access the app at `http://localhost:8000`.

---

## CI/CD Pipeline with Jenkins

The project includes a **Jenkinsfile** to automate the build, test, and deployment process. Below is an overview of the pipeline stages:

1. **Clone Repository**
   - Fetches the latest code from GitHub.

2. **Build Docker Image**
   - Uses the `Dockerfile` to build the application image.

3. **Run Tests**
   - Executes Django tests inside the container.

4. **Push Docker Image**
   - Uploads the image to a Docker registry (e.g., DockerHub or a private registry).

5. **Deploy Application**
   - SSHs into the deployment server and updates the running containers using Docker Compose.

### Running the Jenkins Pipeline
1. Ensure Jenkins is installed and has the necessary plugins (`Pipeline`, `Docker Pipeline`).
2. Configure credentials for GitHub and Docker registry in Jenkins.
3. Create a new Jenkins pipeline and point it to this repository.
4. Run the pipeline to build, test, and deploy the app automatically.

---

## Contribution
Feel free to submit pull requests or raise issues if you find any bugs or have feature suggestions.

