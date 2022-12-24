pipeline{
    
    agent any 
    environment {
        VERSION = "${env.BUILD_ID}"
    }
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Bhavesh-Muleva/nexus_helm_cicd_app.git'
                }
            }
        }
//         stage('UNIT testing'){
            
//             steps{
                
//                 script{
                    
//                     sh 'mvn test'
//                 }
//             }
//         }
//         stage('Integration testing'){
            
//             steps{
                
//                 script{
                    
//                     sh 'mvn verify -DskipUnitTests'
//                 }
//             }
//         }
//         stage('Maven build'){
            
//             steps{
                
//                 script{
                    
//                     sh 'mvn clean install'
//                 }
//             }
//         }
//         stage('Static code analysis'){
            
//             steps{
                
//                 script{
                    
//                     withSonarQubeEnv(credentialsId: 'Sonar-Token') {
                        
//                         sh 'mvn clean package sonar:sonar'
//                     }
//                 }       
//             }
//          }
//         stage('Quality Gate Status'){
                
//                 steps{
                    
//                     script{
                        
//                         waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-Token'
//                     }
//                 }
//          }
//         stage('Docker Build & Push to Nexus') {
//             steps{
//                 script{
//                     sh '''
//                     docker build . -t bhaveshmuleva/springapp:${VERSION}
//                     docker login -u bhaveshmuleva -p Muleva@503
//                     docker push bhaveshmuleva/springapp:${VERSION}
//                     '''
//                 }
//             }
//         }
	    stage('Identifying misconfigs using datree in helm charts'){
		    steps{
			    script{
				    dir('kubernetes/myapp/') {
					    withEnv(['DATREE_TOKEN=85728c01-9082-4668-9e88-fb941a8b5103']) {
                                                    // some block
						    sh 'helm datree test .'
                                            }
				      
				    }
			    }
		    }
	    }
     }
//      post {
//           always {
//               mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "s1032190332@gmail.com";  
//           }
// 	 }
}
