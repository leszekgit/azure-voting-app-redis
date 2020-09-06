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
            powershell(script: 'docker images -a')
            powershell(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .            
               cd ..
            """)
         }
      }
      stage('Start test app') {
         steps {
            powershell(script: """
               docker-compose up -d
               ./scripts/test_container.ps1
            """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            powershell(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            powershell(script: """
               docker-compose down
            """)
         }
      }

      stage ('Push Container') {
         steps {
            echo "Workspace is $WORKSPACE"
            dir("$WORKSPACE/azure-vote") {
               script {
                  docker.withRegistry('https://index.docker.io/v1/', 'DockerHubCredentials') {
                     def image = docker.build('leszekg8/jenkinsmoderncicd:latest')
                     image.push()
                  }
               }
            }
         }

      }

      stage ('Run Trivy') {
         steps {
            powershell(script: """
              C:\\Windows\\System32\\wsl.exe --
              sudo trivy leszekg8/jenkinsmoderncicd
            """)
         }
      }
   }
}
