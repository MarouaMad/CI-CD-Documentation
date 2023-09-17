pipeline {
    
agent any  
tools {   //using plugins
    nodejs 'nodejs'
}
stages{
    stage("git clone"){
        steps{
       git branch:'main', url:'https://github.com/MarouaMad/CI-CD-Documentation.git'
        }
    }
    
      stage("install dependencies"){
        steps{
       nodejs('nodejs'){
           npm 'install'
       }
        }
    }
    
   
      stage("build the project "){
        steps{
         nodejs('nodejs'){
           npm 'run build' 
       }
        }
    }
    
}
        
}