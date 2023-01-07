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
                script{
                    waitForQualityGate(abortPipeline: true, credentialsId: 'Jenkins-auth')
                }
            }   

    }
    
}