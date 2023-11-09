pipeline {
  agent any

  environment {
    // Define your environment variables if any
    CI = 'true'
  }

  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/Tokoynwa/sample-react-app', branch: 'main')
      }
    }
    
    stage('Install Dependencies') {
      steps {
        // Use the appropriate node version
        sh 'nvm install' // If you have an .nvmrc file with the node version
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        // Run your tests here
        sh 'npm test'
      }
    }

    stage('Build') {
      steps {
        // Build your react app for production
        sh 'npm run build'
      }
    }

    stage('Deploy') {
      steps {
        // Add deployment steps here
        // Example:
        // sh './deploy-script.sh'

        // If you are deploying to a server, you might use scp or rsync:
        // sh 'scp -r build/* user@yourserver:/path/to/your/app'
      }
    }
  }

  post {
    always {
      // Clean up the workspace to not store the node_modules etc.
      cleanWs()
    }
    success {
      // Actions to perform on success
      echo 'Build and deployment succeeded!'
    }
    failure {
      // Actions to perform on failure
      echo 'Build or deployment failed.'
    }
  }
}
