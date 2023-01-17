pipeline{
    agent none
    environment{
        DOCKERHUB_CREDENTIALS=crendentials("DockerHub")
    }
    stages{
        stage("frontend"){
            agent any 
            when{
                // PollSCM triggers a new build if changes are detected 
                // in contacts-frontend
                // ** matches any number of directoires
                // *.* : any filename,any extension
                changeset "**/contacts-frontend/*.*"
                sh "echo change in frontend"
                // execute before agent any
                beforeAgent true
            }
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