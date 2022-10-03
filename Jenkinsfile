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
                USERNAME = "ubuntu"
            }

            steps {
                //=============== THIRD APPROACH
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'git-test-deploy1', usernameVariable: 'pemfile')]) {
                        def remote = [
                            name: 'ubuntu', 
                            host: 'ec2-35-92-93-35.us-west-2.compute.amazonaws.com', 
                            user: 'ubuntu', 
                            allowAnyHosts: true,
                            // identityFile: PEM_FILE,
                            // identity: PEM_FILE,
                            knownHosts: pemfile,
                        ]
                        
                        sshCommand remote: remote, command: "df -h"
                        sshCommand remote: remote, command: "curl fconfig.co"
                    }
                }



                // ============== SECOND APPROACH
                // script {
                //      def remote = [
                //         name: 'ubuntu', 
                //         host: 'ec2-35-92-93-35.us-west-2.compute.amazonaws.com', 
                //         user: 'ubuntu', 
                //         // identityFile: "$SSH_CRED", 
                //         allowAnyHosts: true,
                //         knownHosts: SSH_CRED
                //     ]
                     
                //     //  sshCommand remote: remote, command: "df -h"
                //      sshCommand remote: remote, command: "df -h"
                //      sshCommand remote: remote, command: "curl ifconfig.co"
                //  }

                // ===========FIRST APPROACH 
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

        stage("alternative connect"){
            steps{
                script {
                    sshagent (credentials: ['git-test-deploy1']) {
                        sh '''
                            ssh -o StrictHostKeyChecking=no -l ubuntu ec2-35-92-93-35.us-west-2.compute.amazonaws.com uname -a
                        '''
                    }
                }
            }
        }
    }
}