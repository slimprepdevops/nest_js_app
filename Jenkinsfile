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
                sh "echo testing"
            }
        }

        stage("connect to deploy server"){

            environment { 
                SSH_CRED = credentials('blank-vm-pem')
            }

            steps {
                
                script {
                    sh """
                    #!/bin/bash
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@ec2-52-25-213-88.us-west-2.compute.amazonaws.com << EOF
                    curl ifconfig.co/ip
                    df -h
                    echo "running apt update"
                    sudo apt update

                    echo "installing nodejs"
                    sudo apt install nodejs -y

                    echo "installing NPM"
                    sudo apt install npm -y

                    echo "installing yarn"
                    sudo npm install -g yarn -y

                    echo "installing pm2"
                    sudo npm install pm2 -g

                    echo "installing project"
                    sudo mkdir app
                    cd app
                    git clone https://github.com/slimprepdevops/nest_js_app.git .
                    npm install -y

                    echo "Building project"
                    yarn build

                    echo "changing directory"
                    cd dist

                    echo "starting project in directory"
                    pm2 start main.js

                    echo "list running apps"
                    pm2 list
                    exit
                    << EOF
                    """
                }
                
            }
        }
    }
}
