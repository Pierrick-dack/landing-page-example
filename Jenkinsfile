pipeline {
    agent {
        label 'Agent-DevOps'
    }

    stages {
        stage('Verification & Cleanup') {
            steps {
                echo 'Vérification de l\'environnement...'
                sh 'docker --version'
                // On nettoie les anciennes images locales pour gagner de la place
                sh 'docker system prune -f'
            }
        }

        stage('Build & Push to DockerHub') {
            steps {
                echo 'Construction de l\'image Docker...'
                // Construction de l'image avec ton tag v1 [cite: 2026-02-25]
                sh 'docker build -t pierrickdevops/landing-page-example:v1 .'
                
                echo 'Publication sur DockerHub...'
                // On pousse l'image vers le cloud [cite: 2026-02-25]
                sh 'docker push pierrickdevops/landing-page-example:v1'
            }
        }

        stage('Deploy to Azure') {
            steps {
                echo 'Déploiement sur la VM Azure...'
                // Connexion SSH pour mettre à jour le conteneur sur Azure [cite: 2026-02-25]
                sh """
                ssh -o StrictHostKeyChecking=no Pierrick@4.251.194.55 "
                    sudo docker pull pierrickdevops/landing-page-example:v1 && \
                    sudo docker stop mon-site || true && \
                    sudo docker rm mon-site || true && \
                    sudo docker run -d -p 80:80 --name mon-site pierrickdevops/landing-page-example:v1
                "
                """
            }
        }
    }
}
