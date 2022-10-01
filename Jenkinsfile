pipeline {

    agent any

    stages {
        stage("environment preparation"){

            steps {
                sh "sudo apt install nodejs -y"
                sh "sudo apt install npm -y"
            }

        }

        stage("environment test"){

            steps {
                sh "node --version"
                sh "npm --version"
            }

        }
    }
}