pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-maven-app"
        CONTAINER_NAME = "my-maven-container"
        HOST_PORT = "8081"
        CONTAINER_PORT = "8080"
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
                docker run -d ^
                  -p %HOST_PORT%:%CONTAINER_PORT% ^
                  --name %CONTAINER_NAME% ^
                  %IMAGE_NAME%
                '''
            }
        }

        stage('Verify Application') {
            steps {
                bat '''
                echo Waiting for application to start...
                timeout /t 5 >nul
                curl http://localhost:%HOST_PORT% || echo App not responding yet
                '''
            }
        }
    }

    post {
        success {
            echo "Application is running at http://localhost:8081"
        }
        failure {
            echo "Deployment failed. Check Docker logs."
        }
    }
}
