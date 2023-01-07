pipeline{

    agent any

    stages{
           
           stage('Git Checkout'){
        
              steps{
                  git branch: 'main', url: 'https://github.com/Raghu-L/Complete-CI-CD-.git'
              }  
            }  

             stage('Unit Testing'){
        
              steps{
                  sh 'mvn test'
              }  
            } 

            stage('Integratin Testing'){
        
              steps{
                  sh 'mvn verify -DskipUnitTests'
              }  
            }   

             stage('Maven Building'){
        
              steps{
                  sh 'mvn clean install'
              }  
            }   

             stage('Static code analysis'){
        
              steps{
                script{ 
                 withSonarQubeEnv(credentialsId: 'Jenkins-auth'){
                 sh 'mvn clean package sonar:sonar'
                 }
                }
              }  
            }

            stage('Quality Gate Status'){
                steps{
                script{
                    waitForQualityGate(abortPipeline: true, credentialsId: 'Jenkins-auth')
                }
                }
            }  

            stage('Upload war file to nexus'){
                steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'springboot', 
                            classifier: '', file: 'target/Uber.jar',
                            type: 'jar'
                        ]
                    ], 
                    credentialsId: 'nexus-auth1', 
                    groupId: 'com.example', 
                    nexusUrl: '100.26.109.64:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'Demoapp-release', 
                    version: '1.0.0'
                }
                }
            }   

    }
    
}