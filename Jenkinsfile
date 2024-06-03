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

        // stage('UNIT TEST') {
        //     steps {
        //         sh 'mvn clean test'
        //     }
        // }

        // stage('Integration TEST') {
        //     steps {
        //         sh 'mvn clean integration-test'
        //     }
        // }
    stage ('Deploy Tomcat Using jenkins plugin') {
       steps {
              script {
                  deploy adapters: [tomcat9(credentialsId: 'tomcatpassword', path: '', 
                  url: 'http://172.20.168.67:8080/')], 
                  contextPath: '/calculator', war: 'maven_calculator/target/calculator.war'
              }
       }
    }
    }
}
