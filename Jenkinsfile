pipeline{
    agent none
    environment{
        DOCKERHUB_CREDENTIALS=crendentials("DockerHub")
    }
    stages{
        stage("frontend"){
            steps{
                dir("contacts-frontend"){
                    stages{
                        stage("install dependencies"){
                            sh 'npm install'
                        }
                        stage("build"){
                            sh 'ng build --prod'
                        }
                        stage("test"){
                            sh 'ng test'
                        }
                        stage("build docker image"){
                            sh "docker build -t ghaithmlika/contacts-frontend ."
                        }
                        stage ("docker push front image"){
                            sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                        }
                    }
                }
            }
        }
    }
    // cleaning
    post{
        always{
            sh "docker logout"
            sh "docker rmi -f ${oldImageID}"
        }
    }

}