pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                script {
                    dockerapp = docker.build("lucassilva/guia-jenkins:${env.BUILD_ID}", ".")
                }
            }
        }

        stage('Push Docker image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage('Deploy no Kubernetes') {
            steps {
                echo "Executando o comando kubectl apply"
            }
        }
    }
}

