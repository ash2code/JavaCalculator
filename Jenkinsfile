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
                        nexusInstanceId: 'nexus-instance', // Provide the ID of the Nexus instance defined in Jenkins
                        protocol: 'http',
                        nexusUrl: 'http://54.173.97.31:8081',
                        groupId: 'com.ravi.cal',
                        version: '1.3',
                        repository: 'calculator',
                        credentialsId: 'nexus-user', // Provide the ID of the credentials configured in Jenkins
                        artifacts: [
                            [
                                artifactId: 'RaviCalculator',
                                classifier: '',
                                file: 'target/RaviCalculator-1.3.jar', // Path to the JAR file relative to the Jenkins workspace
                                type: 'jar'
                            ]
                        ]
                    )
                }
            }
        }
    }
}
