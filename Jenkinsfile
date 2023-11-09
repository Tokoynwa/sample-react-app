pipeline {
  agent any

  environment {
    CI = 'true'
  }

  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/Tokoynwa/sample-react-app.git', branch: 'main')
      }
    }

    stage('Install Dependencies') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'npm install'
        }
      }
    }

    stage('Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'npm test'
        }
      }
    }

    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'npm run build'
        }
      }
    }

    stage('Deploy') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          // Ensure PM2 is installed
          sh 'npm list -g pm2 || npm install -g pm2'
          // Ensure 'serve' is installed
          sh 'npm list -g serve || npm install -g serve'
          // Start or restart the application
          sh 'pm2 start serve --name "react-app" -s build -l 3000 --time || pm2 restart "react-app"'
        }
      }
    }
  }

  post {
    always {
      // Clean up the workspace to not store the node_modules etc.
      cleanWs(notFailBuild: true)
    }
    success {
      // What to do if the pipeline succeeds
      echo 'Build and deployment succeeded!'
      // Save the PM2 process list to resurrect processes on reboot
      sh 'pm2 save'
    }
    failure {
      // What to do if the pipeline fails
      echo 'Build or deployment failed.'
    }
  }
}
