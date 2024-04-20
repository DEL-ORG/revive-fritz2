pipeline {
    agent any

    stages {
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
    
    
    
    
    
    }




}