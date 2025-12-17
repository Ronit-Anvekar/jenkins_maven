pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-maven-app"
        CONTAINER_NAME = "my-maven-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Ronit-Anvekar/jenkins_maven.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                docker run -d -p 8080:8080 --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
    }

}
