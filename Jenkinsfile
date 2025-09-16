pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/HARISH07-1/my-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-cicd-app:latest .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker stop my-cicd-container || true'
                sh 'docker rm my-cicd-container || true'
                sh 'docker run -d -p 5000:5000 --name my-cicd-container my-cicd-app:latest'
            }
        }
    }
}

