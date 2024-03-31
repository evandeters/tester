pipeline {
    agent {
        label "Ubuntu 22"
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Clone repo') {
            steps {
                script {
                    checkout scm
                    }
            }
        }

        stage('Build') {
            steps {
                script {
                    app = docker.build("tester")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://905418457085.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:aws-credentials') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
