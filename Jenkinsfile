pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Project Files') {
            steps {
                bat '''
                    dir
                    if not exist "server\\Dockerfile" exit /b 1
                    if not exist "client\\Dockerfile" exit /b 1
                    if not exist "docker-compose.yml" exit /b 1
                    if not exist "README.md" exit /b 1
                '''
            }
        }

        stage('Build Images') {
            steps {
                bat '''
                    docker build -t mern-server ./server
                    docker build -t mern-client ./client
                '''
            }
        }

        stage('Compose Up & Check') {
            steps {
                bat '''
                    docker compose up -d --build
                    docker compose ps
                    docker compose down
                '''
            }
        }
    }
}