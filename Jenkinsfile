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

    }
    
}