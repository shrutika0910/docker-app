pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred') // set this in Jenkins
        DOCKER_IMAGE = "shrutika91/docker-app"
    }

    pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/shrutika0910/docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t shrutika0910/docker-app .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat '''
                        docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                        docker tag shrutika0910/docker-app %DOCKER_USER%/docker-app:latest
                        docker push %DOCKER_USER%/docker-app:latest
                    '''
                }
            }
        }
    }
}
}
