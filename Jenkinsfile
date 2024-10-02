pipeline{
    agent  any

    stages{
        stage('clone repo'){
            steps{
                git ('git@github.com:dockersamples/example-voting-app.git')
            
            }
        }    
        stage('directory'){
            steps{
                sh 'cd /home/yat/Desktop/final-project/example-voting-app'
            }
        }
        stage('docker-compose'){
            steps{
                sh 'docker-compose up .'
            }
        }
    }
}