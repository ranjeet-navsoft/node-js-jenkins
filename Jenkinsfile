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
                // Ensure PM2 is installed globally
                sh 'npm install -g pm2'
                
                // Stop previous instance (if running)
                sh 'pm2 stop node-app || echo "No previous instance running"'
                
                // Start app using PM2 (daemon mode)
                sh 'pm2 start app.js --name node-app --watch --log app.log'
                
                // Save PM2 process list
                sh 'pm2 save'
                
                // Ensure PM2 restarts on reboot
                sh 'pm2 startup'
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
