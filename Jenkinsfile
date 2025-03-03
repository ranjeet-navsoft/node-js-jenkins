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
            git branch: 'main', 
                    credentialsId: '3cf56ddb-acd5-45de-b5fa-5a16941589eb', 
                    url: 'https://github.com/ranjeet-navsoft/node-js-jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {  // Optional
            steps {
                sh 'npm test'  // Ensure you have tests defined, or skip this stage
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
