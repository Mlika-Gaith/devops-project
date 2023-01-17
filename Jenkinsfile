pipeline{
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=crendentials('DockerHub')
    }
    stages{
        stage('frontend'){  
            steps{
                dir("contacts-frontend"){
                    echo 'installing depends'
                    sh 'npm install'
                }
                
            }
        }
    }
    

    // cleaning
    post {
        always {
            // remove dangling images 
            sh 'docker rmi -f $(docker images -q -f "dangling=true")'
            // remove volumes created
            sh 'docker volume prune -f'
        }
    }

}