pipeline {
  agent any

  environment {
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
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Deploy') {
      steps {
        // Replace the below example with your actual deployment script or commands
        sh 'echo Deploying application'
        // sh './deploy-script.sh'
        // sh 'scp -r build/* user@yourserver:/path/to/your/app'
      }
    }
  }

  post {
    always {
      cleanWs()
    }
    success {
      echo 'Build and deployment succeeded!'
    }
    failure {
      echo 'Build or deployment failed.'
    }
  }
}
