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
