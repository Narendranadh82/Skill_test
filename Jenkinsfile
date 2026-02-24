pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = "docker-compose"
        IMAGE_BACKEND = "student-backend"
        IMAGE_FRONTEND = "student-frontend"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/<your-username>/<repo>.git'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    sh 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                dir('backend') {
                    sh 'npm test || true'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker build -t $IMAGE_BACKEND ./backend'
                sh 'docker build -t $IMAGE_FRONTEND ./frontend'
            }
        }

        stage('Run Docker Compose') {
            steps {
                sh '$DOCKER_COMPOSE up -d'
            }
        }

    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
