pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                set M2_HOME=C:\apache-maven-3.0.4\
                set path=C:\apache-maven-3.0.4\bin:%path%;
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
