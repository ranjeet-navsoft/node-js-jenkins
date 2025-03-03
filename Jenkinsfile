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
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Start Application') {
            steps {
                sh 'nohup node app.js > app.log 2>&1 &'  // Run app in background
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
