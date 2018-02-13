pipeline {
    agent any

    parameters {
         string(name: 'tomcat_staging', defaultValue: '34.207.79.24', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.207.79.24', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
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
                        sh "scp -i /home/ec2-user/Census-Prep.pem **/target/*.war ec2-user@${params.tomcat_staging}:/opt/tomcat-staging/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /home/ec2-user/Census-Prep.pem **/target/*.war ec2-user@${params.tomcat_prod}:/opt/tomcat-prod/webapps"
                    }
                }
            }
        }
    }
}
