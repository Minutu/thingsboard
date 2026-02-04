pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'ls'
                echo 'Ca print pas bro'
            }
        }

        stage('Docker container Test') {
            steps {
                sh "docker run -d --name test-ubuntu -it ubuntu:latest tail -f /dev/null"
            }
        }
    }

    post {
        success {
            echo 'On a pull le repo'
        }
        failure {
            echo 'On n\'a pas pull le repo'
        }
    }
}
