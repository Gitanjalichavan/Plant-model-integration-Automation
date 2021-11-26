pipeline {
    agent any
     options {
        skipDefaultCheckout true
     }
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
                   echo 'Script customization...'
                }
            }
        }
        stage('email-report') {
            steps {
                script{
                    try{
                        def config= '[]'
                        config = readJSON file: "${WORKSPACE}\\mail.json"
                        emailext    attachLog: false,
                                    body: "\nHi Team,\n ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                                    subject: 'Status of Jenkins Build',
                                     to: "${config.email}"
                    }
                    catch(err){
                         echo 'Check the jenkinslog for the error..!'
                         skipRemainingStages = false
                        echo "next stage skip: = ${skipRemainingStages}"
                    }
                }
            }
        }   
//         stage('clean'){
//             steps{
//                       cleanWs cleanWhenSuccess: false, notFailBuild: true 
//             }
//         }
    }

   
  
        post {
    
         failure{

                                emailext    attachLog: false,
                                    body: "\nHi Team,\n ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                                    subject: 'Status of Jenkins Build',
                                     to: '${DEFAULT_RECIPIENTS}'
                               
                               cleanWs cleanWhenSuccess: false, notFailBuild: true
                                   
                     
                                }  
    
                            }
 }
