pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Instalação das dependencias') {
            steps {
                echo 'Instalando os pacotes node...'
                bat 'npm install'
            }
        }

        stage('Execução dos testes') {
            steps {
                echo 'Executando os testes...'
                bat 'npm test'
            }
        }
    }

    post {
        success {
            echo 'Build e testes executado com sucesso'
        }
        failure {
            echo 'Falha na execução do pipeline'
        }
    }
}