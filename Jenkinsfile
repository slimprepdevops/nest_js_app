pipeline {

    agent any

    stages {
        stage("environment preparation"){

            steps {
                sh "git branch -v"
                sh "pwd"
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