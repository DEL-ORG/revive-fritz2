pipeline {
    agent any

    stages {
        stage('create a dir') {
            steps {
                sh '''
                mkdir essai-jks
                rm -rf essai
                '''
            }
        }

        stage('create a file') {
            steps {
                sh '''
                touch test.txt 
                rm-rf text.txt
                '''
            }
        }
    }

    post {
        success {
            slackSend color: '#2EB67D',
            channel: 'essai-jks', 
            message: "REVIVE Project Build Status" +
                "\n Project Name: REVIVE" +
                "\n Job Name: ${env.JOB_NAME}" +
                "\n Build number: ${currentBuild.displayName}" +
                "\n Build Status : SUCCESS" +
                "\n Build url : ${env.BUILD_URL}"
        }
        failure {
            slackSend color: '#E01E5A',
            channel: 'essai-jks',  
            message: "REVIVE Project Build Status" +
                "\n Project Name: REVIVE" +
                "\n Job Name: ${env.JOB_NAME}" +
                "\n Build number: ${currentBuild.displayName}" +
                "\n Build Status : FAILED" +
                "\n Build User : fritz" +
                "\n Action : Please check the console output to fix this job IMMEDIATELY" +
                "\n Build url : ${env.BUILD_URL}"
        }
        unstable {
            slackSend color: '#ECB22E',
            channel: 'REVIVE', 
            message: "REVIVE Project Build Status" +
                "\n Project Name: REVIVE" +
                "\n Job Name: ${env.JOB_NAME}" +
                "\n Build number: ${currentBuild.displayName}" +
                "\n Build Status : UNSTABLE" +
                "\n Action : Please check the console output to fix this job IMMEDIATELY" +
                "\n Build url : ${env.BUILD_URL}"
        }   
    }
}
