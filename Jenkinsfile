pipeline{
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=crendentials('DockerHub')
    }
    stages{
        stage ('docker login'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
            
        }
        stage('installing frontend dependencies'){  
            steps{
                dir("contacts-frontend"){
                    echo 'installing depends'
                    sh 'npm install'
                }

            }
        }
        stage ('building frontend for production'){
            steps{
                dir("contacts-frontend"){
                    sh 'echo building frontend'
                    sh 'ng build --prod'
                }
            }
        }
        stage('testing frontend'){
            steps{
                dir ("contacts-frontend"){
                    sh 'echo testing'      
                    sh 'ng test'
                }
            }
            
        }
                   
        
    }
    
}