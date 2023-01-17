pipeline{
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=credentials('DockerHub')
    }
    stages{
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