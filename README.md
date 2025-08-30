Simple Django Project with Docker and Jenkins CI/CD

This guide provides a basic Django project setup with Docker and a Jenkins pipeline for CI/CD. 
The project includes a simple Django app, a Dockerfile for containerization, 
and a Jenkinsfile for automated testing and deployment.

django_project/
├── manage.py
├── myapp/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations/
│   │   ├── __init__.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── django_project/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── Dockerfile
├── Jenkinsfile
├── requirements.txt
└── docker-compose.yml