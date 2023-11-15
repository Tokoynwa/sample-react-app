pipeline {
    agent any

    // Uncomment and use this if you have environment variables
    // environment {
    //     NODE_VERSION = '14.17.0'
    // }

    stages {
        stage('Checkout') {
            steps {
                checkout scm: [
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/Tokoynwa/sample-react-app.git']]
                ]
            }
        }
        stage('Install Dependencies') {
            steps {
                // Uncomment and use this if you're using a specific Node.js version with nvm
                // sh 'nvm use $NODE_VERSION'
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
                sh 'cp -R build/* /var/www/html/'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        failure {
            echo 'This will run only if the pipeline fails'
        }
    }
}
