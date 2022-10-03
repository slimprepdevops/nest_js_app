pipeline {

    agent any

    stages {
        stage("environment preparation"){

            steps {
                sh "pwd"
                sh "ls"
                sh "echo ${USER}"
                sh "df -h"
                sh "curl ifconfig.co"
            }

        }

        stage("connect to deploy server"){

            environment { 
                SSH_CRED = credentials('git-test-deploy1') 
            }

            steps {
                sh "pwd"
                sh 'echo "SSH private key is located at $SSH_CRED"'

                
                sh "ls $SSH_CRED"
                sh "ssh -i $SSH_CRED ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com"
                sh "echo ${USER}"
                sh "df -h"
                sh "curl ifconfig.co"
                
            }

        }
    }
}