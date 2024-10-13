pipeline{
    agent  any
    environment {
        MAIL_USER = 'shehabemad3333@gmail.com'
        MAIL_PASS = 'kxea zksz agvz fieo'
    }

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
                sh '''cd /home/yat/Desktop/final-project/example-voting-app
                      docker-compose up -d
                   '''   
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
    post {
        success {
            emailext (
                to: "${mail_user}",
                subject: "Succeeded pipeline: ${currentBuild.fullDisplayName}",
                body: "Well done, Group 2!",
                from: "${env.MAIL_USER}",
                replyTo: "${env.MAIL_USER}"
            )
        }        

        failure {
            emailext (
                to: "${mail_user}",
                subject: "failed pipeline: ${currentBuild.fullDisplayName}",
                body: "try again",
                from: "${env.MAIL_USER}",
                replyTo: "${env.MAIL_USER}"
            )
        }
    }        
}