pipeline{
    agent  any

    stages{
        stage('clone repo'){
            steps{
                git ('git@github.com:dockersamples/example-voting-app.git')
            
            }
        }
        stage('docker-compos'){
            steps{
                sh 'docker-compose up'
            }
        }
    }
}
