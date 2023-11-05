// methode 1 
pipeline {
    
agent any  
tools {   //using plugins
    nodejs 'nodejs'
    dockerTool 'docker'
}
stages{
        
    
    stage("git clone"){
        steps{
       git branch:'main', url:'https://github.com/MarouaMad/CI-CD-Documentation.git'
        }
    }
    
      stage("install dependencies"){
        steps{
     
           
           sh 'npm install'
       
        }
    }
    
      stage("build the project"){
        steps{

            sh 'npm run build'
          
       
        }
    }
     stage('Build Docker Image') {
            steps {
                script {
                    def customImageTag = "my-image:v1"  // Specify your desired image tag here
                    sh "docker build -t ${customImageTag} ."
                }
            }
        }

    stage("SonarScanner"){

   agent { 
                docker { 
                    image 'sonarsource/sonar-scanner-cli' 
                    args '-v /var/run/docker.sock:/var/run/docker.sock --network devops_devops'

                } 
            }
            steps{
             sh '''
             curl http://sonarqube:9000 
             
              sonar-scanner \
               -Dsonar.projectKey=test \
               -Dsonar.sources=. \
               -Dsonar.host.url=http://sonarqube:9000 \
               -Dsonar.login=admin \
               -Dsonar.password=sonar
             '''
            }
            
        }
        
    
     stage('run container') {
            steps {
                script {
                     def customImageTag = "my-image:v1" 
                    sh "docker run -d -p9090:80  --name  newcontainerjenkins ${customImageTag} "
                }
            }
        }


 
    
}
}








    //stage("build the image using docker"){
    
  //  steps{
     // script {
         //def customImageTag = "my-image:v1"  // Specify your desired image tag here

 // Build the Docker image from the 'Dockerfile' in the current directory
       //  docker.build(customImageTag, '.')




