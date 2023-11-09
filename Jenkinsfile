pipeline {
  agent any

  environment {
    CI = 'true'
    PM2_HOME = '/var/lib/jenkins/.pm2' // Set PM2_HOME as an environment variable
    SERVE_PATH = '/var/lib/jenkins/workspace/newreactpipeline' // Set the path to where you want to serve the app
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
          sh 'mkdir -p ${SERVE_PATH}'
          sh 'cp -R build/* ${SERVE_PATH}'
          // Ensure PM2 is installed
          sh 'npm list -g pm2 || npm install -g pm2'
          // Ensure 'serve' is installed
          sh 'npm list -g serve || npm install -g serve'
          // Start or restart the application
          sh 'pm2 start /usr/local/bin/serve --name "react-app" -- -s ${SERVE_PATH} -l 3000'
          // Save the PM2 process list to resurrect processes on reboot
          sh 'pm2 save'
        }
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
    
