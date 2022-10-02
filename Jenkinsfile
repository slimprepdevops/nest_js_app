pipeline {

    agent any

    stages {
        stage("environment preparation"){

            steps {
                sh "pwd"
                sh "ls"
                sh "echo ${USER}"
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