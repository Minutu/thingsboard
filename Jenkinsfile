pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Checkout du répertoire') {
            steps {
                checkout scm
            }
        }
        stage('Compilation et exécution des tests unitaires') {
            steps {
                sh 'mvn clean install --projects common/actor,common/data -am -Dlicense.skip=true'
            }
            // Lecture des resultats des tests qu'on vient de run.
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Construire l'image Docker Thingsboard') {
            steps {
                sh './docker/docker-install-tb.sh --loadDemo'
            }
        }

        //stage('Déployer Thingsboard') {
        //    // Va déployer localement sur Windows
        //    steps {
        //        sh './docker-stop-services.sh || true'
        //        sh './docker-start-services.sh'
        //        sh 'sleep 15'
        //    }
        //}
    }

    post {
        success {
            echo 'Pipeline complétée, Thingsboard déployé et disponible'
        }
        failure {
            echo 'On n\'a pas pull le repo'
        }
    }
}
