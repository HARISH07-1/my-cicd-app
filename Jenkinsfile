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



pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'  // Jenkins credential ID for DockerHub
        IMAGE_NAME = 'harish07-1/my-cicd-app:latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/HARISH07-1/my-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker stop my-cicd-container || true'
                    sh 'docker rm my-cicd-container || true'
                    sh 'docker run -d -p 5000:5000 --name my-cicd-container $IMAGE_NAME'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "$DOCKERHUB_CREDENTIALS", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                        sh 'docker push $IMAGE_NAME'
                    }
                }
            }
        }

        // Optional AWS deployment stage can be added here later
    }
}

