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
        stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-Token'
                    }
                }
         }
        stage('Docker Build & Push to Nexus') {
            steps{
                script{
                    sh '''
                    docker build . -t bhaveshmuleva/springapp:${VERSION}
                    docker login -u bhaveshmuleva -p Muleva@503
                    docker push bhaveshmuleva/springapp:${VERSION}
                    '''
                }
            }
        }
        
     }
}
