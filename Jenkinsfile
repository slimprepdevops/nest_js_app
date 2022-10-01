pipeline {

    agent any

    stages {
        stage("environment preparation"){

            steps {
                sh "apt install nodejs -y"
                sh "apt install npm -y"
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