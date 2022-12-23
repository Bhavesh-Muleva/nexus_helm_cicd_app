pipeline{
    
    agent any 
    environment {
        VERSION = "${env.BUILD_ID}"
    }
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Bhavesh-Muleva/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'Sonar-Token') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                }       
            }
         }
        stage('Docker Build & Push to Nexus') {
            steps{
                script{
                    docker build . -t 172.17.0.4:8083/springapp:${VERSION}
                    docker login -u admin -p admin 172.17.0.4:8083
                    docker push 172.17.0.4:8083/springapp:${VERSION}
                }
            }
        }
        
     }
}
