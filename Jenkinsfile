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
                url: 'https://github.com/Narendranadh82/Skill_test.git'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                }
            }
        }

        stage('Run Backend Tests') {
            steps {
                echo 'Skipping backend tests — no tests defined'
            }
        }

        stage('Build Frontend') {
            steps {
                echo 'Skipping Frontend tests — no tests defined'
            }
        }

        stage('Build Docker Images') {
            steps {
                bat 'docker build -t %IMAGE_BACKEND% ./backend'
                bat 'docker build -t %IMAGE_FRONTEND% ./frontend'
            }
        }

        stage('Run Docker Compose') {
            steps {
                bat '%DOCKER_COMPOSE% up -d'
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
