pipeline {

    agent any

    stages {
        stage("environment preparation"){

            steps {
                sh "pwd"
                sh "ls"
                sh "${USER}"
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