pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
           
         }
      }
      stage('Docker Build..') {
         steps {
            powershell label: 'cd azure-vote..', script: 'cd azure-vote/'
            powershell label: 'get docker images..', script: 'docker images -a'          
            powershell label: 'docker build..', script: 'docker build -t jenkins-pipeline -f Dockerfile'  
            powershell label: 'get docker images..', script: 'docker images -a'   
         }
      }
   }
}
      
        
     
