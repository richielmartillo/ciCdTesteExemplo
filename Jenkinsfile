pipeline {
    agent any

    tools {
    nodejs 'nodejs'
    }

    stages {
        stage('Instalação das dependencias') {
            steps {
                bat 'npm install'
            }
        }

                stage('Execução dos testes') {
            steps {
                bat 'npm test'
            }
        }
    }




}