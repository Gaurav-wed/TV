pipeline {
        agent any

        stages {
            stage('Checkout') {
                steps {
                        checkout scm
                      }}
                stage('Build') {
                   steps {
                          sh '/home/gaurav/Devops/apache-maven-3.9.6/bin/mvn install'
                         }}
                stage('Deployment'){
                   steps {
                sh 'cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.89/webapps'
                        }}
}}

