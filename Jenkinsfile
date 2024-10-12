pipeline{
    agent  any

    stages{
        stage('clone repo'){
            steps{
                git ('git@github.com:dockersamples/example-voting-app.git')
            
            }
        }    
        stage('docker-images'){
            steps{
                sh '''cd /home/yat/Desktop/final-project/example-voting-app/vote
                      docker build -t vote_image .   
                   '''  
                sh '''cd /home/yat/Desktop/final-project/example-voting-app/worker
                      docker build -t worker_image .
                   ''' 
                sh '''cd /home/yat/Desktop/final-project/example-voting-app/result
                      docker build -t result_image .
                   ''' 
            }
        }
        stage('test images'){
            steps{
                sh 'docker images'
            }
        }
        stage('run docker compose'){
            steps{
                sh 'docker-compose up'
            }
        }
        stage('test app'){
            steps{
                sh '''curl localhost:5000
                      curl localhost:5001
                   '''
            }
        }
    }
}