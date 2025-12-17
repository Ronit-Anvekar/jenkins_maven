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

        stage('Run JAR in Container') {
            steps {
                bat '''
                docker rm -f %CONTAINER_NAME% || echo Container not present
                docker run -d --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }

        stage('View JAR Output') {
            steps {
                bat '''
                echo ===== JAR OUTPUT (Container Logs) =====
                docker logs %CONTAINER_NAME%
                '''
            }
        }
    }
}
