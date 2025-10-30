pipeline {
    agent any
    
    stages {
        stage ('Build Docker image') {
            steps {
                sh 'echo "executando build em imagem docker" '
            }
        }

        stage ('Push Docker image') {
            steps {
                sh 'echo "Executando o comando de Docker push"'
            }
        }

        stage ('Deploy no Kubernetes') {
            steps {
                sh 'echo "Executando o comando kubectl apply"'
            }
        }
    }
}
