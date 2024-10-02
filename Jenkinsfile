pipeline{
    agent  any

    stages{
        stage('clone repo'){
            steps{
                git ('git@github.com:dockersamples/example-voting-app.git')
            
            }
        }    
        stage('docker-compose'){
            steps{
                sh 'cd /home/yat/Desktop/final-project/example-voting-app'
                sh 'docker-compose up '
            }
        }
    }
}