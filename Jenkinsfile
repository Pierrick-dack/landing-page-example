pipeline {
    agent {
        label 'Agent-DevOps'
    }

    stages {
        stage ('Verification Agent') {
            steps {
                echo 'Vérification de l\'identité de la machine de travail :'
                sh 'hostname'
                sh 'whoami'
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Pierrick-dack/landing-page-example'
            }
        }
        stage('Build') {
            steps {
                echo 'Simulation du Build en cours...'
                echo 'Le travail est exécuté sur l\'Agent DevOps !'
                sh 'ls -la' 
            }
        }
        stage('Deploy') {
            steps {
                echo 'Déploiement en cours sur le serveur de production...'
                // Simulation d'une copie de fichiers en loca
                sh 'mkdir -p /tmp/production_site'
                sh 'cp index.html /tmp/production_site/'
                echo 'Le site est désormais en ligne !'
            }
        }
    }
}
