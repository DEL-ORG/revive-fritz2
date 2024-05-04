pipeline {
    agent any

    stages {

        stage('Test maven-ui') {
	      agent {
           docker {
             image 'maven:3.8.7-openjdk-18'
           }
         }
           steps {
               sh '''
           cd $WORKSPACE/REVIVE/src/ui/
           mvn  test  -Dmaven.test.skip=true --quiet
               '''
           }
        }

        stage('Test microservice catalog') {
          agent {
            docker {
              image 'golang:1.20.1'
              args '-u 0:0'
            }
           }
            steps {
                sh '''
            cd $WORKSPACE/REVIVE/src/catalog/
            go test
                '''
            }
            
        } 

        stage('Test maven-cart') {
	      agent {
           docker {
             image 'maven:3.8.7-openjdk-18'
           }
         }
           steps {
               sh '''
           cd $WORKSPACE/REVIVE/src/cart/
           mvn  test  -Dmaven.test.skip=true --quiet
               '''
           }
        } 

        stage('Test maven-orders') {
	      agent {
           docker {
             image 'maven:3.8.7-openjdk-18'
           }
         }
           steps {
               sh '''
           cd $WORKSPACE/REVIVE/src/orders/
           mvn  test  -Dmaven.test.skip=true --quiet
               '''
           }
        }

        stage('Test checkout') {
	      agent {
           docker {
             image 'node:14' // Use Node.js 14 image
             args '-u 0:0' // Optional: Run as root user if needed
           }
         }
           steps {
               sh '''
           cd $WORKSPACE/REVIVE/src/checkout/
                //  Run tests for your Node.js application
                sh 'npm test'
               '''
           }
        }

        stage('Build ui') {
            steps {
                sh '''
                    cd $WORKSPACE/REVIVE/src/ui
                    docker build -t bulawesley/revive-ui:${BUILD_NUMBER}.1 .
                '''
            }
        }

        stage('Build catalog') {
            steps {
                sh '''
                    cd $WORKSPACE/REVIVE/src/catalog
                    docker build -t bulawesley/revive-catalog:${BUILD_NUMBER}.1 .
                    docker build -t bulawesley/revive-catalog-db:${BUILD_NUMBER}.1 -f Dockerfile-db .
                '''
            }
        }

        stage('Build cart') {
            steps {
                sh '''
                    cd $WORKSPACE/REVIVE/src/cart
                    docker build -t bulawesley/revive-cart:${BUILD_NUMBER}.1 .
                    docker build -t bulawesley/revive-cart-db:${BUILD_NUMBER}.1 -f Dockerfile-dynamodb .
                '''
            }
        }

        stage('Build orders') {
            steps {
                sh '''
                    cd $WORKSPACE/REVIVE/src/orders
                    docker build -t bulawesley/revive-orders:${BUILD_NUMBER}.1 .
                    docker build -t bulawesley/revive-orders-db:${BUILD_NUMBER}.1 -f Dockerfile-db .
                    docker build -t bulawesley/revive-orders-database-rabbitmq:${BUILD_NUMBER}.1 -f Dockerfile-rabbitmq .
                '''
            }
        }

        stage('Build checkout') {
            steps {
                sh '''
                    cd $WORKSPACE/REVIVE/src/checkout
                    docker build -t bulawesley/revive-checkout:${BUILD_NUMBER}.1 .
                    docker build -t bulawesley/revive-checkout-db:${BUILD_NUMBER}.1 -f Dockerfile-db .
                '''
            }
        }

        stage('Build assets') {
            steps {
                sh '''
                    cd $WORKSPACE/REVIVE/src/assets
                    docker build -t bulawesley/revive-assets:${BUILD_NUMBER}.1 .
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
                "\n Build User : bulawesley" +
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
