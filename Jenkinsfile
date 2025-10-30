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
                echo "Executando o comando de Docker push"
                // Exemplo:
                // sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                // sh "docker push lucassilva/guia-jenkins:${env.BUILD_ID}"
            }
        }

        stage('Deploy no Kubernetes') {
            steps {
                echo "Executando o comando kubectl apply"
                // Exemplo:
                // sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}

