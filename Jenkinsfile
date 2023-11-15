pipeline {
    agent any

   // environment {
        // Define environment variables if needed
        // NODE_VERSION = '12.x' // Uncomment and set your Node.js version
    // }

    stages {
        stage('Checkout') {
            steps {
                checkout scm: [
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']],  // Explicitly specifying the 'main' branch
                    userRemoteConfigs: [[url: 'https://github.com/Tokoynwa/sample-react-app.git']]
                ]
            }
        }
        stage('Install Dependencies') {
            steps {
                // Use a specific Node.js version if necessary
                // sh 'nvm use $NODE_VERSION' // Uncomment if using nvm and a specific Node.js version
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                // Ensure Jenkins user has the necessary permissions to execute this command
                sh 'cp -R build/* /var/www/html/'
            }
        }
    }
    post {
        always {
            // Steps to perform after the pipeline ends, regardless of result
            // e.g., cleanup, sending notifications
        }
        failure {
            // Steps to perform if the pipeline fails
            // e.g., send a failure notification
        }
    }
}
