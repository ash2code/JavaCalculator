pipeline {
  agent any
  tools {
    maven 'Maven3' 
  }
  stages {
    stage('git-checkout') {
      steps {
        git branch: 'main', changelog: false, poll: false,
          url: 'https://github.com/ash2code/Java-Hello-World.git'
      }
    }
    stage('code-build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('sonar-analysis') {
      steps {
        withSonarQubeEnv('sonar') { // 'sonar' should match your SonarQube configuration in Jenkins
          sh '''mvn clean verify sonar:sonar \
            -Dsonar.projectKey=Calculator \
            -Dsonar.projectName="Calculator" \
            -Dsonar.host.url=http://3.109.200.189:9000 \
            -Dsonar.login=sqp_985a8e41f28abf1fc4da1889ba6a427747c842ff'''
        }
      }
    }
  }
}
