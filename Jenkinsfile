pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            powershell label: '', script: 'pwd'
            powershell label: 'get docker images..', script: 'docker images -a'
            powershell label: 'cd ..', script: 'cd ../ModernCICDPipeline/azure-vote'
            pwsh(script: """
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """)
         }
      }
   }
}
      
        
     
