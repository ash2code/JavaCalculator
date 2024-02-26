pipeline {
  agent any 

  tools {
    maven 'Maven3'
  }

  stages {
    stage('check-out') {
      steps {
        git url: 'https://github.com/ash2code/JavaCalculator.git'
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
            -Dsonar.host.url=http://54.173.97.31:9000 \
            -Dsonar.login=sqp_0792151799db536d976472233b2498f71d850c0e'
      }
    }
    stage('upload-to-nexus') {
    steps {
      script {
        nexusArtifactUploader(
          credentialsId: 'nexus-user',
          groupId: 'com.ravi.cal',
          nexusUrl: '54.173.97.31:8081',
          nexusVersion: 'nexus3',
          protocol: 'http',
          repository: 'calculator',
          version: '1.3',
          file: 'JavaCalculator.jar'
        )
      }
    }
  }
}
