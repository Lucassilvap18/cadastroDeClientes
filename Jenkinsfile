pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                script {
                    docker.build("lucasdev18/guia-jenkins:${env.BUILD_ID}", ".")
                } 

                sh """
                    mkdir -p dist
                    cp index.html dist/  # Ajuste se houver mais arquivos (ex.: *.js *.css)
                """
            }
        }

        stage('Push Docker image') {
            steps {
                script {
                    def dockerapp = docker.build("lucasdev18/guia-jenkins:${env.BUILD_ID}", ".")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage('Deploy na VM') {
            steps {
                echo "Deploy realizado na VM com Nginx na porta 80"


            }
        }
    }
}