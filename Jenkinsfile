pipeline {
    agent any

    parameters {
         string(name: 'deploy-to-staging', defaultValue: '54.164.57.248', description: 'Staging Server')
         string(name: 'deploy-to-prod', defaultValue: '18.233.171.178', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
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
                        bat "scp -i /Users/YarrayyaNaidu/tomcat-demo.pem **/target/*.war ec2-user@${params.deploy-to-staging}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /Users/YarrayyaNaidu/tomcat-demo.pem **/target/*.war ec2-user@${params.deploy-to-prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}
