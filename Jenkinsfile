pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-maven-app"
        CONTAINER_NAME = "my-maven-container"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || echo Container not running
                docker rm %CONTAINER_NAME% || echo Container not present
                docker run -d --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
    }
}


