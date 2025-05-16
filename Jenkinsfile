pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins'
        CONTAINER_NAME = 'jenkins-container'
        PORT_MAPPING = '5001:5001'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Vaishnavi2003-ECE/jenkins-test.git'
            }
        }

        stage('Build') {
            steps {
                dir('JenkinTest') {
                    bat 'dotnet build JenkinTest.csproj'
                }
            }
        }

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
}

