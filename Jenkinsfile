pipeline{
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=credentials('DockerHub')
    }
    stages{
        stage ('docker login'){
            steps{
                bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
            
        }
        stage('installing frontend dependencies'){  
            steps{
                dir("contacts-frontend"){
                    bat 'echo installing depends'
                    bat 'npm install'
                }

            }
        }
        stage ('building frontend for production'){
            steps{
                dir("contacts-frontend"){
                    bat 'echo building frontend'
                    bat 'ng build --prod'
                }
            }
        }
        stage('testing frontend'){
            steps{
                dir ("contacts-frontend"){
                    bat 'echo testing'      
                    bat 'ng test'
                }
            }
            
        }
                   
        
    }
    
}