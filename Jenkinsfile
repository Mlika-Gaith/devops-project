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
    post{
        always{
            sh 'docker logout'
            sh 'docker rmi $(docker images -q -f dangling=true)'
        }
    }

}