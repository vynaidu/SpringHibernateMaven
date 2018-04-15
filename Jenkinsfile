pipeline {
    agent any
    tools {
        maven 'localMaven'
      }
    tools {
        JDK 'localJDK'
      }
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
