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
                script {
                    def targetDir = '/home/gaurav/Devops/apache-tomcat-9.0.89/webapps'
                    def environment = params.ENV
                    
                    echo "Deploying to ${environment}"
                    sh "cp target/TV.war ${targetDir}"
                    
                    // Optionally, add environment-specific behavior
                    if (environment == "DEV") {
                        echo "Additional configuration or deployment logic for DEV"
                    } else if (environment == "QA") {
                        echo "Additional configuration or deployment logic for QA"
                    } else if (environment == "UAT") {
                        echo "Additional configuration or deployment logic for UAT"
                    }
                }
            }
        }
        stage('Slack Notification') {
            steps {
                slackSend botUser: true, 
                          channel: '#tv', 
                          color: 'good', 
                          failOnError: true, 
                          message: "Deployment successful for ${params.ENV} environment", 
                          notifyCommitters: true, 
                          teamDomain: 'tv', 
                          tokenCredentialId: '973bcbcb-68f8-4231-8391-0405ddbeab34'
            }
        }
    }
}

