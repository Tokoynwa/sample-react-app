pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out source code from SCM
                git clone 'https://github.com/Tokoynwa/sample-react-app.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                // Build the React app
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy to the web server
                // Assuming the web server serves files from /var/www/html
                sh 'cp -R build/* /var/www/html/'
            }
        }
    }
}
