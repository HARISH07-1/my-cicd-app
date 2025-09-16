# CI/CD Pipeline Project with Jenkins & Docker

## Project Overview
This project demonstrates a complete DevOps pipeline for a simple Flask web application using GitHub, Jenkins, Docker .  
It showcases skills in version control, containerization, automation, and continuous deployment.

**Key Features:**
- Automated code build & deployment using Jenkins.
- Containerized Flask application using Docker.
- Continuous integration pipeline with GitHub webhook trigger.

---

## Tech Stack
| Technology       | Purpose                                      |
|-----------------|----------------------------------------------|
| **Python (Flask)** | Web application framework                  |
| **Docker**       | Containerization of the Flask app           |
| **Jenkins**      | CI/CD pipeline automation                   |
| **GitHub**       | Version control & code repository           |
|          |

---

## Project Structure

my-cicd-app/
│
├── app.py # Flask application
├── requirements.txt # Python dependencies
├── Dockerfile # Docker image instructions
└── Jenkinsfile # CI/CD pipeline instructions


---

## Pipeline Steps
1. **Code Commit:** Developer pushes changes to GitHub (`main` branch).  
2. **Checkout Stage (Jenkins):** Jenkins pulls the latest code.  
3. **Build Docker Image:** Jenkins builds the Docker image.  
4. **Run Docker Container:** Jenkins runs the Flask app in Docker.  
5. **Optional Deploy to EC2:** Docker image is pulled and container restarted on remote EC2.

---

## Jenkinsfile Highlights
```groovy
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps { git branch: 'main', url: 'https://github.com/HARISH07-1/my-cicd-app.git' }
        }
        stage('Build Docker Image') { steps { sh 'docker build -t my-cicd-app:latest .' } }
        stage('Run Docker Container') {
            steps {
                sh 'docker stop my-cicd-container || true'
                sh 'docker rm my-cicd-container || true'
                sh 'docker run -d -p 5000:5000 --name my-cicd-container my-cicd-app:latest'
            }
        }
    }
}


How to Run Locally :
git clone https://github.com/HARISH07-1/my-cicd-app.git
cd my-cicd-app
docker build -t my-cicd-app:latest .
docker run -d -p 5000:5000 --name my-cicd-container my-cicd-app:latest






Skills Demonstrated

DevOps Tools: Jenkins, Docker, GitHub

Automation: CI/CD pipeline creation

Containerization: Packaging and running Flask app in Docker

Version Control: Git workflow

