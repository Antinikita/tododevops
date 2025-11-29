pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'tg/tododevops:1.0'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building Spring Boot application...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Push') {
            steps {
                echo 'Pushing Docker image to registry...'
                sh "docker tag ${DOCKER_IMAGE} ${DOCKER_IMAGE}"
                sh "docker push ${DOCKER_IMAGE}"
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
