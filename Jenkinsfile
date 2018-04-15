pipeline {
    agent any

    parameters {
         string(name: 'deployTostaging', defaultValue: '54.164.57.248', description: 'Staging Server')
         string(name: 'deployToprod', defaultValue: '18.233.171.178', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }
tools {
        maven 'localMaven'
        jdk 'localJDK'
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

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "scp -i /Users/YarrayyaNaidu/tomcat-demo.pem **/target/*.war ec2-user@${params.deployTostaging}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /Users/YarrayyaNaidu/tomcat-demo.pem **/target/*.war ec2-user@${params.deployToprod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}
