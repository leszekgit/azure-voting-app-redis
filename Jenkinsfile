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
            powershell label: 'get docker images..', script: 'docker images -a'   
            powershell(script: """
             cd azure-vote/
             docker build -t jenkinspipe .
            """)        
           
         }
      }
   }
}
      
        
     
