pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {

        stage('Clonar hub de leitura integrado') {
            steps {
                bat 'if exist hub-de-leitura-integrado2 rmdir /s /q hub-de-leitura-integrado2'
                bat 'git clone --depth 1 https://github.com/EBAC-QE/hub-de-leitura-integrado2.git'
            }
        }

        stage('Instalar dependencias do projeto') {
            steps {
                dir('hub-de-leitura-integrado2') {
                    bat 'npm install'
                }
            }
        }

        stage('Subir aplicacao') {
            steps {
                dir('hub-de-leitura-integrado2') {
                    bat 'start /B npm start'
                }
            }
        }

        stage('Esperar app subir') {
            steps {
                bat 'npx wait-on http://localhost:3000'
            }
        }

        stage('Clonar projeto de teste') {
            steps {
                bat 'if exist hub-de-leitura-teste-ui-task rmdir /s /q hub-de-leitura-teste-ui-task'
                bat 'git clone --depth 1 https://github.com/richiellamartillo/hub-de-leitura-teste-ui-task.git'
            }
        }

        stage('Instalar dependencias do teste') {
            steps {
                dir('hub-de-leitura-teste-ui-task') {
                    bat 'npm install'
                }
            }
        }

        stage('Executar testes automatizados') {
            steps {
                dir('hub-de-leitura-teste-ui-task') {
                    bat 'npx cypress run'
                }
            }
        }
    }

post {
    always {
        archiveArtifacts artifacts: 'hub-de-leitura-teste-ui-task/cypress/screenshots/**/*.*', allowEmptyArchive: true
        archiveArtifacts artifacts: 'hub-de-leitura-teste-ui-task/cypress/videos/**/*.*', allowEmptyArchive: true
        bat 'taskkill /F /IM node.exe || exit 0'
    }
}
}