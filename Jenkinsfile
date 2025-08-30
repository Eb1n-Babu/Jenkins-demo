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
                script {
                    if (isUnix()) {
                        sh 'docker build -t $IMAGE_NAME .'
                    } else {
                        bat 'docker build -t %IMAGE_NAME% .'
                    }
                }
            }
        }

        stage('Run Django Tests') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            docker run --rm --env-file .env $IMAGE_NAME sh -c "
                                pip install -r requirements.txt &&
                                python manage.py test
                            "
                        '''
                    } else {
                        // Windows requires PowerShell or CMD syntax; CMD doesn't support multi-line like sh
                        bat '''
                            docker run --rm --env-file .env %IMAGE_NAME% cmd /c "pip install -r requirements.txt && python manage.py test"
                        '''
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker-compose --env-file .env down || true'
                        sh 'docker-compose --env-file .env up -d'
                    } else {
                        bat 'docker-compose --env-file .env down || exit 0'
                        bat 'docker-compose --env-file .env up --

