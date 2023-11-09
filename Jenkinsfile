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

   stage('Serve') {
      steps {
        sh 'nohup npx serve -s build -l 3000 &'
      }
    }
  }

  post {
    always {
      cleanWs()
    }
    success {
      echo 'Build, deployment, and server startup succeeded!'
    }
    failure {
      echo 'Build, deployment, or server startup failed.'
    }
  }
}
