pipeline {
    agent any
    
    stages {
        stage ('Build Docker image') {
            steps {
                sh 'echo "Executando o comando de Docker build"'
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