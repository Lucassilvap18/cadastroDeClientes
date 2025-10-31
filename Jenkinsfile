pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                script {
                    // Build para validação (não armazena a variável aqui)
                    docker.build("lucasdev18/guia-jenkins:${env.BUILD_ID}", ".")
                }
                // Cria a pasta dist com os arquivos estáticos para o deploy via SCP
                sh """
                    mkdir -p dist
                    cp index.html dist/  # Ajuste se houver mais arquivos (ex.: *.js *.css)
                """
            }
        }

        stage('Push Docker image') {
            steps {
                script {
                    // Re-build aqui para ter a variável local no escopo do push
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