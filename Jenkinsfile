pipeline {
  agent any 

  tools {
    maven 'Maven3'
  }

  stages {
    stage ('check-out') {
      steps {
        git 'https://github.com/ash2code/JavaCalculator.git'
      }
    }
    stage('code-build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('sonar-analysis') {
      steps {
        sh 'mvn clean verify sonar:sonar \
            -Dsonar.projectKey=calculator \
            -Dsonar.projectName="calculator" \
            -Dsonar.host.url=http://44.204.148.6:9000 \
            -Dsonar.login=sqp_0792151799db536d976472233b2498f71d850c0e'
      }
    }
  }
}
        

  
