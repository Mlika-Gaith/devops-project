pipeline{
    agent none
    environment{
        DOCKERHUB_CREDENTIALS=crendentials("DockerHub")
    }
    stages{
        stage("frontend"){
            dir("contacts-frontend"){
                steps{
                    sh 'echo installing dependencies'
                    sh 'npm install'
                    sh 'echo building for production'
                    sh 'ng build --prod'
                    sh 'echo testing'      
                    sh 'ng test'
                    sh 'echo building docker image' 
                    sh "docker build -t ghaithmlika/contacts-frontend ."
                    sh 'echo pushing frontend image to dockerhub'
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"   
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