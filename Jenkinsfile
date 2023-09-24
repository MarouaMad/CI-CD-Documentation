// methode 1 
pipeline {
    
agent any  
tools {   //using plugins
    nodejs 'nodejs'
    dockerTool 'docker'
}
stages{
    stage('Install Docker') {
            steps {
                script {
                    sh 'curl -fsSL https://get.docker.com -o get-docker.sh'
                    sh 'sh get-docker.sh'
                }
            }
        }
        
    
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

    stage("SonarScanner")
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




