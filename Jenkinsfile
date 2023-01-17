pipeline{
    agent none
    environment{
        DOCKERHUB_CREDENTIALS=crendentials('DockerHub')
    }
    dir('contacts-frontend'){
    stages{
        stage('frontend'){
            
                steps{
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
            sh 'docker rmi -f ${oldImageID}'
        }
    }

}