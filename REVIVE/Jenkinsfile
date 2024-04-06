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
}

