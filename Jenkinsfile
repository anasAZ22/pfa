pipeline {
    agent {
        docker {
            image 'node:18-alpine' // Modification : Changer la version de l'image Docker
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/anasAZ22/pfa.git']]]) // Modification : Utiliser le plugin GitSCM et spécifier l'URL du référentiel
            }
        }
        stage('Build') {
            steps {
                sh 'chmod -R 755 .npm' // Modification : Changer le chemin de l'autorisation
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
