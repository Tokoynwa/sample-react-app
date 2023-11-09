pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Checkout the code from the 'main' branch of the GitHub repository
        git(url: 'https://github.com/Tokoynwa/sample-react-app.git', branch: 'main')
      }
    }

    stage('Install Dependencies') {
      steps {
        // Install the project dependencies
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        // Run yousdsr tests here (if any)
        sh 'npm test'
      }
    }

    stage('Build') {
      steps {
        // Build your project
        sh 'npm run build'
      }
    }

    stage('Deploy') {
      steps {
        // Add your deployment steps here
        // For example, to copy to a remote server using scp:
        // sh 'scp -r build/* username@yourserver:/path/to/deployment/directory'
        // Make sure to replace 'username', 'yourserver', and '/path/to/deployment/directory' with your actual data
        echo 'Add your deployment steps here'
      }
    }
  }

  post {
    success {
      // What to do if the pipeline succeeds
      echo 'Build and deployment succeeded!'
    }
    failure {
      // What to do if the pipeline fails
      echo 'Build or deployment failed.'
    }
  }
}
