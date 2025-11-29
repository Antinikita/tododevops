pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'tg/todo-app:1.0'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building Spring Boot application...'
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                bat 'mvn test'
            }
        }

        stage('Push') {
            steps {
                echo 'Pushing Docker image to registry...'
                bat "docker tag %DOCKER_IMAGE% %DOCKER_IMAGE%"
                bat "docker push %DOCKER_IMAGE%"
            }
        }

    }

    post {
        always {
            echo 'Pipeline finished'
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
