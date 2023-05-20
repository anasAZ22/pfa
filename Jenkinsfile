pipeline {
    agent {
        docker {
            image 'node:14-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test' // Remplacez la commande par celle appropriée pour exécuter les tests
            }
        }
        stage('Deliver') {
            steps {
                sh 'npm run build' // Remplacez la commande par celle appropriée pour générer les fichiers de livraison
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'npm run deploy' // Remplacez la commande par celle appropriée pour déployer les fichiers de livraison
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
