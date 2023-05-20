pipeline {
    agent { 
        docker { 
            image 'node:18-alpine' 
            args '-p 3000:3000'
            user 'root' // Ajoutez cette ligne pour exécuter les commandes en tant qu'utilisateur root
        } 
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Set Permissions') {
            steps {
                sh 'chown -R 132:142 /.npm' // Supprimez le "sudo"
            }
        }
        
        stage('Build') {
            steps {
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
}
