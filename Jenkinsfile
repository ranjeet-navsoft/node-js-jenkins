pipeline {
    agent any
    tools {
        nodejs "nodejs_20"  // Ensure Node.js is configured in Jenkins
    }
    environment {
        PORT = '3000'  // Set environment variables if needed
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
    post {
        success {
            echo 'Application deployed successfully!'
        }
        failure {
            echo 'Build failed! Check logs for details.'
        }
    }
}