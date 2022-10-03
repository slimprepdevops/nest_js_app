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
                script {
                     def remote = [name: 'ubuntu', host: 'ec2-35-92-93-35.us-west-2.compute.amazonaws.com', user: 'ubuntu', identityFile: '$SSH_CRED', allowAnyHosts: true]
                     
                    //  sshCommand remote: remote, command: "df -h"
                     sshCommand remote: remote, command: "df -h"
                     sshCommand remote: remote, command: "curl ifconfig.co"
                 }
                // sh "pwd"
                // sh 'echo "SSH private key is located at $SSH_CRED"'
                
                // sh "ls $SSH_CRED"
                // // sh "ssh -i $SSH_CRED -tt -o StrictHostKeyChecking=no ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com"
                // sh "ssh -i $SSH_CRED -t ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com"
                // sh "echo ${USER}"
                // sh "df -h"
                // sh "curl ifconfig.co"
                
            }

        }
    }
}