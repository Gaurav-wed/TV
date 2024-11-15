pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Poll every minute
    }
    parameters {
        choice(choices: ['DEV', 'QA', 'UAT'], name: 'ENV')
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
                // Deploying a general file (TV.war) to Tomcat
                sh 'cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.89/webapps'
            }
        }
        stage('Environment-Based Deployment') {
            steps {
                sh '''#!/bin/bash
                if [ "${ENV}" == "DEV" ]; then
                    echo "Deployed to DEV"
                    cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.89/webapps
                elif [ "${ENV}" == "QA" ]; then
                    echo "Deployed to QA"
                    cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.89/webapps
                elif [ "${ENV}" == "UAT" ]; then
                    echo "Deployed to UAT"
                    cp target/TV.war /home/gaurav/Devops/apache-tomcat-9.0.89/webapps
                fi'''
            }
        }
    }
     stage('slack') {
            steps {
                  slackSend baseUrl: 'https://hooks.slack.com/services/', channel: 'tv1', color: 'good', failOnError: true, message: 'This is use for slack for notification ', notifyCommitters: true, teamDomain: 'TV', tokenCredentialId: '973bcbcb-68f8-4231-8391-0405ddbeab34'
}
}
}
