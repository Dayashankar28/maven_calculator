/* groovylint-disable-next-line CompileStatic */
pipeline {
   agent any 

    tools {
        maven 'maven_tool'
    }

    stages {
        stage('BUILD') {
            steps {
                sh '''
                  mvn clean package
               '''
            }
        }

        stage('UNIT TEST') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Integration TEST') {
            steps {
                sh 'mvn clean integration-test'
            }
        }
    stage ('Deploy Tomcat Using jenkins plugin') {
       steps {
         sh 'cd ./target/'
         sh 'pwd'
              script {
                  deploy adapters: [tomcat9(credentialsId: 'tomcatpassword', path: '', 
                  url: 'http://172.20.168.67:8080/')], contextPath: 'calculator', onFailure: false, war: '/var/lib/jenkins/workspace/maven_calculator/target/calculator.war'
              }
       }
    }
    }
}
