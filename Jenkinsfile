pipeline {
    agent any

    stages {
        stage('automation') {
            steps {
                script{
                   echo 'Automating the integration plant model creation using CI pipeline..'
                }
            }
        }
        stage('customize') {
            steps {
                script{
                   echo 'Script customization..'
                }
            }
        }        
    }
  
        post {
    
         always {

                                emailext    attachLog: false,
                                    body: "\nHi Team,\n ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                                    subject: 'Status of Jenkins Build',
                                     to: '${DEFAULT_RECIPIENTS}'
                         
                               cleanWs cleanWhenSuccess: false, notFailBuild: true
                                   
                     
                                }  
    
                            }
 }
