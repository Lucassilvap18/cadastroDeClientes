pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                script {
                    def dockerapp = docker.build("lucasdev18/guia-jenkins:${env.BUILD_ID}", ".")
                    // Cria a pasta dist com os arquivos estáticos para o deploy via SCP
                    sh """
                        mkdir -p dist
                        cp index.html dist/  # Ajuste se houver mais arquivos (ex.: *.js *.css)
                    """
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

        stage('Deploy na VM') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'deploy-jenkins', keyFileVariable: 'SSH_KEY', usernameVariable: 'SSH_USER')]) {
                    sh """
                        # Copia os arquivos da aplicação para o diretório do Nginx na VM
                        scp -i \$SSH_KEY -o StrictHostKeyChecking=no -r ./dist/ \$SSH_USER@13.220.118.240:/var/www/html/
                        
                        # Reinicia o Nginx na VM para aplicar as mudanças
                        ssh -i \$SSH_KEY -o StrictHostKeyChecking=no \$SSH_USER@13.220.118.240 'sudo systemctl reload nginx'
                    """
                }
                echo "Deploy realizado na VM com Nginx na porta 80"
            }
        }
    }
}