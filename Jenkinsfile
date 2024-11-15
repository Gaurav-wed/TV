pipeline {
    agent any

    parameters {
        string(defaultValue: 'DEV', name: 'ENV')
        choice(choices: ['DEV', 'QA', 'UAT'], name: 'ENV')
    }

    triggers {
        pollSCM('* * * * *')  
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh '/home/gaurav/Devops/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                script {
                    if (env.ENV == 'DEV') {
                        sh 'cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been completed on DEV!"
                    } else if (env.ENV == 'QA') {
                        sh 'cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been completed on QA!"
                    } else if (env.ENV == 'UAT') {
                        sh 'cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been done on UAT!"
                    }
                }
            }
        }
    }
}
