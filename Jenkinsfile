pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        
            post {
                success {
                    echo 'Now archiving....'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('deploy to Staging'){
            steps {
                build job: ' Deploy-to-staging'
            }
        }
             
    }
}
