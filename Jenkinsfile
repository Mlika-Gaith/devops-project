pipeline{
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=credentials('DockerHub')
    }
    stages{
        stage ("loging to DockerHub"){
            steps{
                //bat "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                powershell -Command "echo $env:DOCKERHUB_CREDENTIALS_PSW | docker login -u $env:DOCKERHUB_CREDENTIALS_USR --password-stdin"
            }
        }

        stage('installing frontend dependencies'){  
            steps{
                dir("contacts-frontend"){
                    bat 'npm install'
                }

            }
        }
        stage ('building frontend for production'){
            steps{
                dir("contacts-frontend"){
                    bat 'ng build --prod'
                }
            }
        }
        stage('testing frontend'){
            steps{
                dir ("contacts-frontend"){      
                    bat 'ng test'
                }
            }
            
        }
        stage ('creating frontend docker image'){
            steps{
                dir("contacts-frontend"){
                    bat 'docker build --tag contacts-frontend:latest .'
                }
            }
        }
        stage('pushing frontend docker image '){
            steps{
                dir("contacts-frontend"){
                    bat "docker push ghaithmlika/contacts-frontend:latest"
                }
            }
        
        }
        stage('Building backend') {
            steps {
                dir('contacts-backend'){
                    bat 'mvn clean install'
                }
                
            }
        }
        stage('Testing backend') {
            steps {
                dir('contacts-backend'){
                    bat 'mvn test'
                }
                
            }
        }
        stage('Creating backend dcker image'){
            steps {
                dir('contacts-backend'){
                    bat 'docker build --tag contacts-backend:latest .'
                }
                
            }
        }
        stage('pushing frontend docker image '){
            steps{
                dir("contacts-backend"){
                    bat "docker push ghaithmlika/contacts-backend:latest"
                }
            }
        
        }
                   
        
    }
    // cleaning
    post{
        always{
            bat 'docker logout'
            // remove dangling images 
            bat 'docker rmi -f ${oldImageID}'
        }
    }
    
}