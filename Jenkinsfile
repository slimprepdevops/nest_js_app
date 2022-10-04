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
                REM_USER = "{USER}"
            }

            steps {
                //=============== THIRD APPROACH
                script {
                    sh """
                    #!/bin/bash
                    ssh -i $SSH_CRED -tt -v ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com << EOF
                    curl ifconfig.co/ip
                    df -h
                    echo '\$'USER
                    
                    exit 0
                    << EOF
                    """
                }

                // ============== SECOND APPROACH
                // script {
                //     def remote = [
                //         name: 'ubuntu', 
                //         host: 'ec2-35-92-93-35.us-west-2.compute.amazonaws.com', 
                //         user: 'ubuntu', 
                //         identityFile: "$SSH_CRED", 
                //         identity: "$SSH_CRED", 
                //         password: "$SSH_CRED", 
                //         allowAnyHosts: true,
                //         knownHosts: SSH_CRED
                //     ]
                    
                //     sshCommand remote: remote, command: "df -h"
                //     sshCommand remote: remote, command: "curl ifconfig.co"
                // }

                // ===========FIRST APPROACH 
                // sh "pwd"
                // sh 'echo "SSH private key is located at $SSH_CRED"'
                
                // // sh "ssh -i $SSH_CRED -tt -o StrictHostKeyChecking=no ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com"
                // sh 'ssh -i $SSH_CRED -t ubuntu@ec2-35-92-93-35.us-west-2.compute.amazonaws.com $remoteCommands'
                
            }
        }
    }
}