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
                sh '''
                    ls -la
                    test -f server/Dockerfile
                    test -f client/Dockerfile
                    test -f docker-compose.yml
                    test -f README.md
                '''
            }
        }

        stage('Build Images') {
            steps {
                sh '''
                    docker build -t mern-server ./server
                    docker build -t mern-client ./client
                '''
            }
        }

        stage('Compose Up & Check') {
            steps {
                sh '''
                    docker compose up -d --build
                    docker compose ps
                    docker compose down
                '''
            }
        }
    }
}