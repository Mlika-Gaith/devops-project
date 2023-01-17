pipeline{
    agent none
    environment{
        DOCKERHUB_CREDENTIALS=crendentials('DockerHub')
    }
    stages{
        stage('frontend'){
            dir('contacts-frontend'){
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