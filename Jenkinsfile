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
        stage('docker login'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {  
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'  
                    }
                }
            }
        }
        stage('push images'){
            steps{
                sh ''' docker tag result_ima 1998shehab/result:01
                       docker push 1998shehab/result:01
                   '''           
            }
        }
    }
    post {
        success {
            mail to: "${mail_user}",
                 subject: "Succeeded pipeline: ${currentBuild.fullDisplayName}",
                 body: "Well done, Group 2!"
        }        

        failure {
            mail to: "${mail_user}",
                 subject: "failed pipeline: ${currentBuild.fullDisplayName}",
                 body: "try again"
        }
    }        
}