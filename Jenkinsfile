pipeline {
    agent any

    stages {
        stage('create a dir') {
            steps {
                sh '''
                mkdir fritz
                rm -rf fritz
                '''
            }
        }


        stage('create a file') {
            steps {
                sh '''
                touch text.txt
                rm -rf text.txt
                '''
                
            }
        }

        
    }

    post {
      success {
          slackSend color: '#2EB67D',
          channel: 's6-catchup-notifications', 
          message: "*REVIVE Project Build Status*" +
          "\n Project Name: REVIVE" +
          "\n Job Name: ${env.JOB_NAME}" +
          "\n Build number: ${currentBuild.displayName}" +
          "\n Build Status : *SUCCESS*" +
          "\n Build url : ${env.BUILD_URL}"
      }
      failure {
          slackSend color: '#E01E5A',
          channel: 's6-catchup-notifications',  
          message: "*REVIVE Project Build Status*" +
          "\n Project Name: REVIVE" +
          "\n Job Name: ${env.JOB_NAME}" +
          "\n Build number: ${currentBuild.displayName}" +
          "\n Build Status : *FAILED*" +
          "\n Build User : *fritz*" +
          "\n Action : Please check the console output to fix this job IMMEDIATELY" +
          "\n Build url : ${env.BUILD_URL}"
      }
      unstable {
          slackSend color: '#ECB22E',
          channel: 'REVIVE', 
          message: "*REVIVE Project Build Status*" +
          "\n Project Name: REVIVE" +
          "\n Job Name: ${env.JOB_NAME}" +
          "\n Build number: ${currentBuild.displayName}" +
          "\n Build Status : *UNSTABLE*" +
          "\n Action : Please check the console output to fix this job IMMEDIATELY" +
          "\n Build url : ${env.BUILD_URL}"
      }   
   
}



    
}

