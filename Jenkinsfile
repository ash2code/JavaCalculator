pipeline {
  agent any

  tools {
    maven 'Maven3'
  }

  stages {
    stage('scm-checkout') {
      steps {
        git branch: 'main', changelog: false, poll: false,
          url: 'https://github.com/ash2code/JavaCalculator.git'
      }
    }
  }
}
