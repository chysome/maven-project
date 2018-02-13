pipeline{
    agent any
    stages{
        stage('Init'){
            steps{
                echo "Testing..."
            }
        

            post {
                success {
                    echo 'Now archiving....'
                    archiveartifacts artifacts: '**/target/*.war'
                }
            }
        }
             
    }
}
