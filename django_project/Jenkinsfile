pipeline {
    agent {
        docker {
            image 'python:3.13.3-slim'
            args '-v $HOME/.cache:/root/.cache'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'python manage.py test'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-django-app:latest .'
            }
        }
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }
    post {
        always {
            sh 'docker-compose down || true'
        }
    }
}