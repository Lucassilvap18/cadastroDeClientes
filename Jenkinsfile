pipeline {
    agent any
    
    stages {
        stage ('Build Docker image') {
            steps {
                script {
                    dockerapp = docker.build("lucassilva/guia-jenkins:${env.BUILD_ID}", '-f Lucassilvap18/cadastroDeClientes/Dockerfile') 
                }
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
