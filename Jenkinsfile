pipeline {
    agent any
    
    stages {
        stage ('Build Docker image') {
            steps {
                script {
                    dockerapp = docker.build("lucassilva/gui-jenkins:${env.BUILD_ID}", '-f src/Dockerfile") 
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
