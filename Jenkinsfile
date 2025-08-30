pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-django-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Django Tests') {
            steps {
                sh '''
                    docker run --rm --env-file .env $IMAGE_NAME sh -c "
                        pip install -r requirements.txt &&
                        python manage.py test
                    "
                '''
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'docker-compose --env-file .env down || true'
                sh 'docker-compose --env-file .env up -d'
            }
        }
    }

    post {
        always {
            sh 'docker-compose down || true'
        }
    }
}