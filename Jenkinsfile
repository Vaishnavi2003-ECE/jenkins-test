pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t jenkins -f Dockerfile .'
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                bat 'docker stop jenkins-container || exit 0'
                bat 'docker rm jenkins-container || exit 0'
            }
        }

        stage('Run New Container') {
            steps {
                bat 'docker run -d --name jenkins-container -p 32769:32769 jenkins'
            }
        }
    }
}

