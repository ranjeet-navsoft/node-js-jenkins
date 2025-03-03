pipeline {
    agent any
    tools {
        nodejs "nodejs_20"
    }
    environment {
        PORT = '3000'
    }
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm // Replace with your actual GitHub repo
            }
        }
         stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }
        stage('Start Application') {
               steps {
                sh 'docker stop my-node-app || true'
                sh 'docker rm my-node-app || true'
                sh 'docker run -d -p 3000:3000 --name my-node-app my-node-app'
            }
        }
    }
    success {
            echo '✅ Application is running in a Docker container!'
            sh 'docker ps | grep my-node-app'
        }
}