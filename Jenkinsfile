pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "hola_mundo"
    }

    stages {
        stage('Clonar repositorio') {
            steps {
                git branch: 'main', url: 'https://github.com/SergioCardoso97/JenkinsPipeline'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                echo '🔧 Construyendo imagen con Docker Compose...'
                sh 'docker compose build'
            }
        }

        stage('Desplegar contenedores') {
            steps {
                echo '📦 Desplegando contenedores...'
               sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }

        stage('Verificar contenedores') {
            steps {
                echo '🔍 Contenedores desplegados:'
                sh 'docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"'
            }
        }
    }

    post {
        success {
            echo '✅ App Hola Mundo desplegada correctamente.'
        }
        failure {
            echo '❌ Error durante el pipeline.'
        }
    }
}