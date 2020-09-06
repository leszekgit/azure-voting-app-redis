pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
            powershell label: 'cd azure-vote..', script: 'cd azure-vote/'
         }
      }
      stage('Docker Build..') {
         steps {

            powershell label: 'get docker images..', script: 'docker images -a'          
          
         }
      }
   }
}
      
        
     
