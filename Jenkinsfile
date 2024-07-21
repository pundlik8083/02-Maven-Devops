pipeline {
    agent any
    
    
    tools {
        
        maven  "Maven3"
        jdk  "jdk17"
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/pundlik8083/02-Maven-Devops.git'
            }
        }
    
    
    
    
        stage('Maven Build ') {
            steps {
               sh "mvn  clean package"
            }
        }
    
    
    
    
    
    
        stage('Build docker Image') {
            steps {
                sh """
                docker build -t pundlik8083/datastore:v1 .
                
                """
            }
        }
    
    
    
    
    
    
        stage('Scanning Docker Image') {
            steps {
                sh "trivy image pundlik8083/datastore:v1 "
            }
        }
        
        
        
        
         stage('Pushing Image to Dockerhub') {
             
               steps {
                   
                   script{
                   
                   
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                       
                       sh "docker push pundlik8083/datastore:v1 "
    
                        }
                        
                   }        
            
              
             }
        }
        
        
        
         stage('Hello 32') {
            steps {
                echo 'Hello World'
            }
        }
    }
}


