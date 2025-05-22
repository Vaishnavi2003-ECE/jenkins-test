pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins'
        CONTAINER_NAME = 'jenkins-container'
        PORT_MAPPING = '8080:8081'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% -f JenkinTest/Dockerfile JenkinTest"
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                bat """
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                """
            }
        }

        stage('Run New Container') {
            steps {
                bat "docker run -d -p %PORT_MAPPING% --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}

