pipeline {
  agent any
  stages {
    stage('Build') { // You can change 'Build' to whatever stage name is appropriate
      steps {
        git(url: 'https://github.com/Tokoynwa/sample-react-app', branch: 'main')
        // Add other steps here that you want to execute after checking out the code.
      }
    }
    // Add other stages as needed
  }
}
